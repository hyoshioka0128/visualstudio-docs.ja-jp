---
title: ドキュメント テーブルの実行 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- read locks
- running document table (RDT), IVsDocumentLockHolder interface
- running document table (RDT)
- running document table (RDT), edit locks
- document data objects, running document table
ms.assetid: bbec74f3-dd8e-48ad-99c1-2df503c15f5a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9e6aa882921786b1592922372581beae8c4c2443
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705564"
---
# <a name="running-document-table"></a>ドキュメント テーブルの実行
IDE は、現在開いているすべてのドキュメントのリストを、実行中のドキュメントテーブル (RDT) と呼ばれる内部構造で保持します。 このリストには、現在編集中のドキュメントに関係なく、メモリ内のすべての開いているドキュメントが含まれます。 ドキュメントとは、プロジェクト内のファイルやメイン プロジェクト ファイル (たとえば、.vcxproj ファイル) を含め、永続化されたアイテムです。

## <a name="elements-of-the-running-document-table"></a>実行中のドキュメント テーブルの要素
 実行中のドキュメント テーブルには、次のエントリが含まれます。

|要素|説明|
|-------------|-----------------|
|ドキュメント モニカー|ドキュメント データ オブジェクトを一意に識別する文字列。 これは、ファイルを管理するプロジェクト システムの絶対ファイル パスです (たとえば、C:\MyProject\MyFile)。 この文字列は、データベース内のストアド プロシージャなど、ファイル システム以外のストアに保存されたプロジェクトにも使用されます。 この場合、プロジェクト システムは、ドキュメントの格納方法を決定するために、認識できる一意の文字列を作成し、解析できます。|
|階層所有者|<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>インターフェイスによって表されるドキュメントを所有する階層オブジェクト。|
|品目 ID|階層内の特定の項目の項目識別子。 この値は、このドキュメントを所有するすべてのドキュメントで一意ですが、この値が異なる階層間で一意であるとは保証されません。|
|ドキュメント データ オブジェクト|少なくとも、これは`IUnknown`<br /><br /> オブジェクト。 IDE では、カスタムエディタのドキュメントデータオブジェクト`IUnknown`のインタフェース以外の特定のインタフェースは必要ありません。 ただし、標準エディターの場合、プロジェクトからのファイル永続呼び出<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2>しを処理するには、エディターのインターフェイスの実装が必要です。 詳細については、「[標準ドキュメントの保存](../../extensibility/internals/saving-a-standard-document.md)」を参照してください。|
|Flags|ドキュメントを保存するかどうか、読み取りロックと編集ロックのどちらを適用するかを制御するフラグを、エントリが RDT に追加されるときに指定できます。 詳細については、<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS> 列挙型のページをご覧ください。|
|ロック数の編集|編集ロックの数。 編集ロックは、一部の編集者がドキュメントを編集用に開いしていることを示します。 編集ロックのカウントが 0 に遷移すると、変更されている場合は、ドキュメントを保存するように求められます。 たとえば、[**新しいウィンドウ]** コマンドを使用してエディターでドキュメントを開くたびに、RDT でそのドキュメントの編集ロックが追加されます。 編集ロックを設定するには、ドキュメントに階層またはアイテム ID が必要です。|
|読み取りロック数|読み取りロックの数。 読み取りロックは、ドキュメントがウィザードなどのメカニズムを通じて読み取られていることを示します。 読み取りロックは、ドキュメントを編集できないことを示す間、RDT でドキュメントを保持します。 ドキュメントに階層 ID またはアイテム ID がない場合でも、読み取りロックを設定できます。 この機能を使用すると、ドキュメントをメモリ内で開き、階層によって所有されていない、RDT にドキュメントを入力できます。 この機能はほとんど使用されません。|
|ロックホルダー|<xref:Microsoft.VisualStudio.Shell.Interop.IVsDocumentLockHolder>インターフェイスのインスタンス。 ロック・ホルダーは、エディターの外部で文書を開いたり編集したりするウィザードなどの機能によって実装されます。 ロックホルダを使用すると、ドキュメントの編集中にドキュメントが閉じないように、編集ロックをドキュメントに追加できます。 通常、編集ロックはドキュメント ウィンドウ (つまり、エディター) によってのみ追加されます。|

 RDT の各エントリには、一意の階層または項目 ID が関連付けられています。 編集に使用できるすべてのドキュメントは、通常、階層によって所有されます。 RDT で行われたエントリは、編集中のドキュメント データ オブジェクトを現在どの階層に所有しているか、またはより正確にどの階層を管理するかを制御します。 IDE では、RDT の情報を使用して、ドキュメントが複数のプロジェクトで同時に開かれないようにすることができます。

 階層は、データの永続化を制御し、RDT の情報を使用して **[保存**] ダイアログ ボックスと **[名前を付けて保存**] ダイアログ ボックスを更新します。 ユーザーがドキュメントを変更し、[**ファイル]** メニューの **[終了]** コマンドを選択すると、IDE は、現在変更されているプロジェクトとプロジェクト項目をすべて表示する **[変更の保存**] ダイアログ ボックスを表示します。 これにより、保存するドキュメントをユーザーが選択できます。 保存するドキュメントの一覧 (つまり、変更があるドキュメント) は、RDT から生成されます。 アプリケーションを終了したときに **[変更の保存**] ダイアログ ボックスに表示される項目には、RDT にレコードが含まれている必要があります。 RDT は、保存されるドキュメントと、各ドキュメントの Flags エントリで指定された値を使用して保存操作についてユーザーに確認を求めるかどうかを調整します。 RDT フラグの詳細については、列挙を<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS>参照してください。

## <a name="edit-locks-and-read-locks"></a>ロックの編集とロックの読み取り
 編集ロックと読み取りロックは RDT に存在します。 ドキュメント ウィンドウは、編集ロックをインクリメントおよびデクリメントします。 したがって、ユーザーが新しいドキュメント ウィンドウを開くと、編集ロック数は 1 ずつ増加します。 編集ロックの数がゼロになると、階層は、関連付けられたドキュメントのデータを永続化または保存するように通知されます。 階層は、ファイルとして、またはリポジトリ内のアイテムとして保持するなど、どのような方法でもデータを保持できます。 インターフェイスのメソッドを<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.LockDocument%2A><xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable>使用して、編集ロックと読み取りロックを追加し<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.UnlockDocument%2A>、これらのロックを削除するメソッドを使用できます。

 通常、エディターのドキュメント ウィンドウがインスタンス化されると、ウィンドウ フレームは自動的に RDT 内のドキュメントの編集ロックを追加します。 ただし、標準のドキュメント ウィンドウを使用しない (つまり、<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame>インターフェイスを実装しない) ドキュメントのカスタム ビューを作成する場合は、独自の編集ロックを設定する必要があります。 たとえば、ウィザードでは、ドキュメントはエディターで開かれずに編集されます。 ウィザードおよび同様のエンティティによってドキュメント ロックを開くには、これらのエンティティがインターフェイスを実装する<xref:Microsoft.VisualStudio.Shell.Interop.IVsDocumentLockHolder>必要があります。 ドキュメント ロック ホルダを登録するには<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.RegisterDocumentLockHolder%2A>、メソッドを呼び出<xref:Microsoft.VisualStudio.Shell.Interop.IVsDocumentLockHolder>して実装を渡します。 これにより、ドキュメント ロック ホルダーが RDT に追加されます。 ドキュメント ロック ホルダを実装する別のシナリオとして、特殊なツール ウィンドウでドキュメントを開く場合があります。 この場合、ツール ウィンドウでドキュメントを閉じることができません。 ただし、RDT にドキュメント ロック ホルダーとして登録すると、IDE は、メソッドの実装<xref:Microsoft.VisualStudio.Shell.Interop.IVsDocumentLockHolder.CloseDocumentHolder%2A>を呼び出して、ドキュメントの終了を要求できます。

## <a name="other-uses-of-the-running-document-table"></a>実行中のドキュメント テーブルのその他の用途
 IDE の他のエンティティは、ドキュメントに関する情報を取得するために RDT を使用します。 たとえば、ソース管理マネージャーは、ファイルの最新バージョンを取得した後、システムにドキュメントをエディターに再読み込みするように指示するために RDT を使用します。 これを行うには、ソース管理マネージャーは、開いているファイルがあるかどうかを確認するために、RDT 内のファイルを検索します。 その場合、ソース管理マネージャーはまず、階層が<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.ReloadItem%2A>メソッドを実装しているかどうかを確認します。 プロジェクトがメソッドを<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.ReloadItem%2A>実装しない場合、ソース管理マネージャーは、ドキュメント データ オブジェクトに対<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.ReloadDocData%2A>するメソッドの実装を直接チェックします。

 IDE は、ユーザーがドキュメントを要求した場合に、開いているドキュメントを再表示 (前面) に再表示するために RDT を使用します。 詳細については、「[ファイルを開くコマンドを使用してファイルを表示する](../../extensibility/internals/displaying-files-by-using-the-open-file-command.md)」を参照してください。 RDT でファイルが開いているかどうかを確認するには、次のいずれかの操作を行います。

- アイテムが開いているかどうかを調べるドキュメント モニカー (つまり、完全なドキュメント パス) を照会します。

- 階層または項目 ID を使用して、プロジェクト システムに完全なドキュメント パスを要求し、RDT で項目を検索します。

## <a name="see-also"></a>関連項目
- [RDT_ReadLock の使用法](../../extensibility/internals/rdt-readlock-usage.md)
- [ドキュメント テーブルの保存と実行](../../extensibility/internals/persistence-and-the-running-document-table.md)
