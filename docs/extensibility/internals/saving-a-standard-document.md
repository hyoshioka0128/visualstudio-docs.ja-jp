---
title: 標準ドキュメントの保存 |Microsoft Docs
description: Visual Studio IDE に追加するプロジェクトの種類の標準ドキュメントに対して発生するプロセスについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], saving standard documents
- projects [Visual Studio SDK], saving standard documents
- persistence, saving standard documents
ms.assetid: d692fedf-b46e-4d60-84bd-578635042235
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: a1864ec689c1068b97775ca1a8bddbd390e7b43a
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105080893"
---
# <a name="saving-a-standard-document"></a>標準ドキュメントの保存
環境は、[保存]、[名前を付けて保存]、および [すべてを保存] コマンドを処理します。 ユーザーが [**ファイル**] メニューの [**保存**]、[名前を付け **て保存**]、または [**すべて** 保存] を選択すると、**すべて保存** が行われるため、次のプロセスが実行されます。

 ![標準エディター](../../extensibility/internals/media/public.gif "パブリック") 標準エディターのすべてのコマンド処理を保存、名前を付けて保存、および保存する

 このプロセスについては、次の手順で詳しく説明します。

1. [名前を付けて **保存** ] および [名前を付け **て保存** ] コマンドを選択すると、環境ではサービスを使用して、 <xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection> アクティブなドキュメントウィンドウと、保存する必要がある項目を決定します。 アクティブなドキュメントウィンドウが判明すると、環境は、実行中のドキュメントテーブル内のドキュメントの階層ポインターと項目識別子 (itemID) を検索します。 詳細については、「 [Document Table の実行](../../extensibility/internals/running-document-table.md)」を参照してください。

    [ **すべて保存** ] コマンドを選択すると、実行中のドキュメントテーブルの情報を使用して、保存するすべての項目の一覧がコンパイルされます。

2. ソリューションは、呼び出しを受け取ると <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> 、選択された一連の項目 (つまり、サービスによって公開される複数の選択項目) を反復処理し <xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection> ます。

3. ソリューションでは、選択項目の各項目に対して、階層ポインターを使用してメソッドを呼び出し、[ <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.IsItemDirty%2A> **保存** ] メニューコマンドを有効にする必要があるかどうかを判断します。 1つ以上の項目がダーティの場合、[ **保存** ] コマンドが有効になります。 階層で標準のエディターが使用されている場合、階層はメソッドを呼び出して、ダーティステータスのクエリをエディターに委任し <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.IsDocDataDirty%2A> ます。

4. 選択された各項目がダーティである場合、ソリューションは階層ポインターを使用して、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.SaveItem%2A> 適切な階層でメソッドを呼び出します。

    階層では、標準のエディターを使用してドキュメントを編集するのが一般的です。 この場合、そのエディターのドキュメントデータオブジェクトはインターフェイスをサポートしている必要があり <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2> ます。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.SaveItem%2A>メソッド呼び出しを受け取った時点で、ドキュメントデータオブジェクトのメソッドを呼び出すことによって、ドキュメントが保存されていることをエディターに通知する必要があり <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.SaveDocData%2A> ます。 エディターでは、インターフェイスに対してを呼び出すことにより、環境で [ **名前を付けて保存** ] ダイアログボックスを処理でき `Query Service` <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell> ます。 これにより、インターフェイスへのポインターが返さ <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> れます。 次に、エディターはメソッドを呼び出し <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SaveDocDataToFile%2A> 、パラメーターを使ってエディターの実装へのポインターを渡す必要があり <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat> `pPersistFile` ます。 その後、環境で保存操作が実行され、エディターの [ **名前を付けて保存** ] ダイアログボックスが表示されます。 次に、を使用してエディターにコールバックし <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat> ます。

5. ユーザーが無題のドキュメント (つまり、以前に保存されていないドキュメント) を保存しようとすると、[名前を付けて保存] コマンドが実際に実行されます。

6. [名前を付けて保存] コマンドを実行すると、[名前を付けて保存] ダイアログボックスが表示され、ユーザーはファイル名を入力するように求められます。

    ファイルの名前が変更されている場合は、(VSFPROPID_MkDocument) を呼び出して、ドキュメントフレームのキャッシュされた情報を更新する必要があり <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.SetProperty%2A> ます。

   [ **名前を付けて保存** ] コマンドを使用してドキュメントの場所を移動し、階層がドキュメントの場所に依存している場合、階層は、開いているドキュメントウィンドウの所有権を別の階層に渡す役割を担います。 たとえば、プロジェクトによって、ファイルがプロジェクトに関連する内部または外部のファイル (その他のファイル) であるかどうかが追跡されている場合に発生します。 ファイルの所有権をその他のファイルプロジェクトに変更するには、次の手順に従います。

## <a name="changing-file-ownership"></a>ファイルの所有権の変更

#### <a name="to-change-file-ownership-to-the-miscellaneous-files-project"></a>ファイルの所有権をその他のファイルプロジェクトに変更するには

1. インターフェイスのクエリサービス <xref:Microsoft.VisualStudio.Shell.Interop.SVsExternalFilesManager> 。

     へのポインター <xref:Microsoft.VisualStudio.Shell.Interop.IVsExternalFilesManager2> が返されます。

2. ドキュメントを <xref:Microsoft.VisualStudio.Shell.Interop.IVsExternalFilesManager2.TransferDocument%2A> `pszMkDocumentNew` `punkWindowFrame` 新しい階層に転送するには、(,) メソッドを呼び出します。 [名前を付けて保存] コマンドを実行する階層では、このメソッドを呼び出します。

## <a name="see-also"></a>こちらもご覧ください
- <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>
- [プロジェクト項目のオープンと保存](../../extensibility/internals/opening-and-saving-project-items.md)
