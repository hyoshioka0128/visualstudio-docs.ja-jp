---
title: Document Table | を実行していますMicrosoft Docs
description: Visual Studio IDE が実行中のドキュメントテーブルをどのように保持しているかを説明します。これには、すべての開いているドキュメントがメモリに含まれます。
ms.custom: SEO-VS-2020
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
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 863a9b1cdb68218539045c9154fc18d845495222
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99902891"
---
# <a name="running-document-table"></a>ドキュメント テーブルの実行
IDE では、現在開いているすべてのドキュメントの一覧が、実行中のドキュメントテーブル (RDT) と呼ばれる内部構造で保持されます。 この一覧には、これらのドキュメントが現在編集されているかどうかに関係なく、メモリ内のすべての開いているドキュメントが含まれます。 ドキュメントは、プロジェクトまたはメインプロジェクトファイル (.vcxproj ファイルなど) 内のファイルを含む、永続化された任意の項目です。

## <a name="elements-of-the-running-document-table"></a>実行中のドキュメントテーブルの要素
 実行中のドキュメントテーブルには、次のエントリが含まれています。

|要素|説明|
|-------------|-----------------|
|ドキュメントモニカー|ドキュメントデータオブジェクトを一意に識別する文字列。 これは、ファイルを管理するプロジェクトシステムの絶対ファイルパスです (たとえば、C:\MyProject\MyFile)。 この文字列は、データベース内のストアドプロシージャなど、ファイルシステム以外のストアに保存されたプロジェクトにも使用されます。 この場合、プロジェクトシステムは、ドキュメントを格納する方法を決定するために認識して解析できる一意の文字列を指定できます。|
|階層の所有者|ドキュメントを所有する階層オブジェクト。インターフェイスによって表さ <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> れます。|
|項目 ID|階層内の特定の項目の項目識別子。 この値は、このドキュメントを所有する階層内のすべてのドキュメント間で一意ですが、この値は異なる階層間で一意であるとは限りません。|
|ドキュメントデータオブジェクト|少なくとも、これは `IUnknown`<br /><br /> オブジェクト。 IDE では、 `IUnknown` カスタムエディターのドキュメントデータオブジェクトのインターフェイスを超える特定のインターフェイスは必要ありません。 ただし、標準のエディターでは、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2> プロジェクトからのファイルの永続化呼び出しを処理するために、エディターのインターフェイスの実装が必要です。 詳細については、「 [標準ドキュメントの保存](../../extensibility/internals/saving-a-standard-document.md)」を参照してください。|
|フラグ|ドキュメントを保存するかどうかを制御するフラグ (読み取りロックまたは編集ロックを適用するかどうかなど) は、RDT にエントリを追加するときに指定できます。 詳細については、<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS> 列挙型のページをご覧ください。|
|ロック数の編集|編集ロックの数。 編集ロックは、一部のエディターでドキュメントが編集用に開かれていることを示します。 編集ロックの数が0に遷移すると、ドキュメントが変更されている場合は、保存するように求められます。 たとえば、[ **新しいウィンドウ** ] コマンドを使用してエディターでドキュメントを開くたびに、rdt にそのドキュメントの編集ロックが追加されます。 編集ロックを設定するには、ドキュメントに階層または項目 ID が必要です。|
|読み取りロック数|読み取りロックの数。 読み取りロックは、ドキュメントがウィザードなどの何らかのメカニズムによって読み取られていることを示します。 読み取りロックは、ドキュメントを編集できないことを示すために、RDT でドキュメントを保持します。 ドキュメントに階層または項目 ID がない場合でも、読み取りロックを設定できます。 この機能を使用すると、メモリ内のドキュメントを開いて、ドキュメントが階層によって所有されていなくても、RDT に入力できます。 この機能はほとんど使用されません。|
|ロックホルダー|インターフェイスのインスタンス <xref:Microsoft.VisualStudio.Shell.Interop.IVsDocumentLockHolder> 。 ロックホルダーは、エディター以外でドキュメントを開いたり編集したりするためのウィザードなどの機能によって実装されます。 ロックの所有者は、編集ロックを文書に追加して、編集中のドキュメントが閉じられるのを防ぐことができます。 通常、編集ロックは、ドキュメントウィンドウ (つまり、エディター) によってのみ追加されます。|

 RDT 内の各エントリには、一意の階層または項目 ID が関連付けられています。これは、通常、プロジェクト内の1つのノードに対応しています。 編集に使用できるすべてのドキュメントは、通常、階層によって所有されます。 RDT で作成されたエントリは、どの階層が、現在編集中のドキュメントデータオブジェクトを所有しているかをより正確に制御します。 IDE では、RDT の情報を使用して、一度に複数のプロジェクトによってドキュメントが開かれないようにすることができます。

 階層では、データの永続性も制御され、RDT の情報を使用して [ **保存** ] ダイアログボックスと [ **名前を付けて保存** ] ダイアログボックスが更新されます。 ユーザーがドキュメントを変更した後、[**ファイル**] メニューから [**終了**] コマンドを選択すると、[**変更の保存**] ダイアログボックスが表示され、現在変更されているすべてのプロジェクトとプロジェクト項目が表示されます。 これにより、ユーザーは保存するドキュメントを選択できます。 保存するドキュメントの一覧 (変更されたドキュメント) は、RDT から生成されます。 アプリケーションの終了時に [ **変更の保存** ] ダイアログボックスに表示されるはずの項目には、rdt のレコードが含まれている必要があります。 RDT では、保存されるドキュメントと、各ドキュメントの Flags エントリに指定された値を使用して保存操作についてユーザーに確認を求めるかどうかを調整します。 RDT フラグの詳細については、列挙体を参照してください <xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS> 。

## <a name="edit-locks-and-read-locks"></a>ロックと読み取りロックの編集
 Edit locks と read locks は RDT に存在します。 ドキュメントウィンドウは、編集ロックを増減します。 このため、ユーザーが新しいドキュメントウィンドウを開くと、編集ロックカウントは1ずつ増加します。 編集ロックの数が0になると、階層は、関連付けられているドキュメントのデータを永続化または保存するように通知されます。 階層では、ファイルとして永続化したり、リポジトリ内の項目として保持するなど、任意の方法でデータを永続化することができます。 インターフェイスでメソッドを使用して、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.LockDocument%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable> 編集ロックと読み取りロックを追加したり、メソッドを使用してこれらのロックを解除したりでき <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.UnlockDocument%2A> ます。

 通常、エディターのドキュメントウィンドウがインスタンス化されると、ウィンドウフレームによって、RDT 内のドキュメントの編集ロックが自動的に追加されます。 ただし、標準のドキュメントウィンドウを使用しない (つまり、インターフェイスを実装しない) ドキュメントのカスタムビューを作成する場合は、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame> 独自の編集ロックを設定する必要があります。 たとえば、ウィザードでは、エディターで開かずにドキュメントが編集されます。 ウィザードと同様のエンティティによってドキュメントロックが開かれるようにするには、これらのエンティティがインターフェイスを実装する必要があり <xref:Microsoft.VisualStudio.Shell.Interop.IVsDocumentLockHolder> ます。 ドキュメントのロックホルダーを登録するには、メソッドを呼び出し、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.RegisterDocumentLockHolder%2A> 実装を渡し <xref:Microsoft.VisualStudio.Shell.Interop.IVsDocumentLockHolder> ます。 これにより、ドキュメントのロックホルダーが RDT に追加されます。 ドキュメントロックホルダーを実装するもう1つのシナリオは、特別なツールウィンドウでドキュメントを開く場合です。 このインスタンスでは、ツールウィンドウでドキュメントを閉じることはできません。 ただし、RDT でドキュメントのロックの所有者として登録することにより、IDE はメソッドの実装を呼び出して、ドキュメントを閉じるように求めることができ <xref:Microsoft.VisualStudio.Shell.Interop.IVsDocumentLockHolder.CloseDocumentHolder%2A> ます。

## <a name="other-uses-of-the-running-document-table"></a>実行中のドキュメントテーブルのその他の使用
 IDE 内の他のエンティティは、RDT を使用してドキュメントに関する情報を取得します。 たとえば、ソース管理マネージャーは RDT を使用して、ファイルの最新バージョンを取得した後に、エディターでドキュメントを再読み込みするようにシステムに指示します。 これを行うには、ソース管理マネージャーが RDT 内のファイルを検索して、いずれかが開いているかどうかを確認します。 指定されている場合、ソース管理マネージャーはまず、階層がメソッドを実装していることを確認し <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.ReloadItem%2A> ます。 プロジェクトがメソッドを実装していない場合 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.ReloadItem%2A> 、ソース管理マネージャーは、ドキュメントデータオブジェクトに対してメソッドの実装を直接確認し <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.ReloadDocData%2A> ます。

 また、ユーザーがドキュメントを要求した場合、IDE は RDT を使用して開いているドキュメントを resurface (前面に移動) します。 詳細については、「[ [ファイルを開く] コマンドを使用したファイルの表示](../../extensibility/internals/displaying-files-by-using-the-open-file-command.md)」を参照してください。 ファイルが RDT で開かれているかどうかを確認するには、次のいずれかの操作を行います。

- ドキュメントモニカー (つまり、完全なドキュメントパス) を照会して、アイテムが開いているかどうかを確認します。

- 階層または項目 ID を使用して、プロジェクトシステムに完全なドキュメントパスを要求してから、RDT で項目を確認します。

## <a name="see-also"></a>関連項目
- [RDT_ReadLock の使用法](../../extensibility/internals/rdt-readlock-usage.md)
- [ドキュメント テーブルの保存と実行](../../extensibility/internals/persistence-and-the-running-document-table.md)
