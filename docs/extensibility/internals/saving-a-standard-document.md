---
title: 標準ドキュメントを保存する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], saving standard documents
- projects [Visual Studio SDK], saving standard documents
- persistence, saving standard documents
ms.assetid: d692fedf-b46e-4d60-84bd-578635042235
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: e8d50a9e62e69f925564717020a51f88620f5f3b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705550"
---
# <a name="saving-a-standard-document"></a>標準ドキュメントの保存
環境では、[保存]、[名前を付けて保存]、[すべて保存] の各コマンドを処理します。 ユーザーが **[ファイル]** メニューの **[上書き保存**]、[**名前を付けて**保存] 、または **[すべて保存]** を選択するか、またはソリューションを閉じて **[すべて保存]** を実行すると、次の処理が実行されます。

 ![標準エディター](../../extensibility/internals/media/public.gif "パブリック")標準エディタの[保存]、[名前を付けて保存]、[すべて保存]コマンドの処理

 このプロセスの詳細は、次の手順で説明します。

1. **[保存]** コマンドと **[名前を付けて保存]** コマンドを選択すると、環境はサービスを<xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection>使用してアクティブなドキュメント ウィンドウと保存する項目を決定します。 アクティブなドキュメント ウィンドウが判明すると、環境は、実行中のドキュメント テーブルで、ドキュメントの階層ポインターとアイテム識別子 (itemID) を検索します。 詳細については、「[ドキュメント テーブルの実行](../../extensibility/internals/running-document-table.md)」を参照してください。

    **[すべて保存]** コマンドを選択すると、環境は実行中のドキュメント テーブルの情報を使用して、保存するすべてのアイテムのリストをコンパイルします。

2. ソリューションは、呼び出<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>しを受け取ると、選択された項目のセット (つまり、<xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection>サービスによって公開される複数の選択項目) を反復処理します。

3. 選択した各項目で、ソリューションは階層ポインターを使用してメソッドを<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.IsItemDirty%2A>呼び出し、[**保存]** メニュー コマンドを有効にするかどうかを判断します。 1 つまたは複数のアイテムがダーティである場合は、[**保存**] コマンドが有効になります。 階層が標準エディターを使用している場合、メソッドを呼び出すことによって、階層はダーティ ステータスの<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.IsDocDataDirty%2A>クエリをエディターに委任します。

4. 選択した各項目がダーティである場合、ソリューションは階層ポインターを使用して<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.SaveItem%2A>、適切な階層でメソッドを呼び出します。

    階層では、標準のエディタを使用してドキュメントを編集するのが一般的です。 この場合、そのエディターのドキュメント データ オブジェクトがインターフェイスを<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2>サポートしている必要があります。 メソッド呼び<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.SaveItem%2A>出しを受け取ると、プロジェクトはドキュメント データ オブジェクトの<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.SaveDocData%2A>メソッドを呼び出してドキュメントが保存されていることをエディターに通知する必要があります。 エディタは、インターフェイスを呼び出`Query Service`すことによって、環境が [**名前を付けて保存**] ダイアログ ボックスを<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell>処理できるようにします。 インターフェイスへのポインターを<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell>返します。 次に、エディターはメソッド<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SaveDocDataToFile%2A>を呼び出し、パラメーターを使用して<xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat>エディターの実装へのポインター`pPersistFile`を渡す必要があります。 次に、環境が [保存] 操作を実行し、エディターの **[名前を付けて保存**] ダイアログ ボックスを提供します。 環境は、 を使用<xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat>してエディターに呼び出します。

5. ユーザーが無題のドキュメント (以前に保存されていないドキュメント) を保存しようとすると、実際には [名前を付けて保存] コマンドが実行されます。

6. [名前を付けて保存] コマンドの場合は、[名前を付けて保存] ダイアログ ボックスが表示され、ユーザーにファイル名の入力を求めるメッセージが表示されます。

    ファイルの名前が変更された場合、階層は、(VSFPROPID_MkDocumentを呼び出<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.SetProperty%2A>すことによって、ドキュメント フレームのキャッシュされた情報を更新する責任があります。

   [**名前を付けて保存]** コマンドによってドキュメントの場所が移動され、階層がドキュメントの場所に影響を受ける場合、階層は開いているドキュメント ウィンドウの所有権を別の階層に渡します。 たとえば、プロジェクトがプロジェクトに関連する内部ファイルと外部ファイルのどちらであるかをプロジェクトが追跡する場合に発生します。 ファイルの所有権をその他のファイル プロジェクトに変更するには、次の手順を使用します。

## <a name="changing-file-ownership"></a>ファイル所有権の変更

#### <a name="to-change-file-ownership-to-the-miscellaneous-files-project"></a>ファイルの所有権をその他のファイル プロジェクトに変更するには

1. <xref:Microsoft.VisualStudio.Shell.Interop.SVsExternalFilesManager>インターフェイスのクエリ サービス。

     へのポインタ<xref:Microsoft.VisualStudio.Shell.Interop.IVsExternalFilesManager2>が返されます。

2. (`pszMkDocumentNew`, `punkWindowFrame`) メソッドを<xref:Microsoft.VisualStudio.Shell.Interop.IVsExternalFilesManager2.TransferDocument%2A>呼び出して、ドキュメントを新しい階層に転送します。 [名前を付けて保存] コマンドを実行する階層は、このメソッドを呼び出します。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>
- [プロジェクト項目のオープンと保存](../../extensibility/internals/opening-and-saving-project-items.md)
