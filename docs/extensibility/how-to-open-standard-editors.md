---
title: '方法 : 標準エディタを開く |マイクロソフトドキュメント'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], opening
- projects [Visual Studio SDK], opening standard editors
ms.assetid: d5ce10f9-047a-4b74-aa1d-295128898b89
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f42cfa64106acc41358568f4c8f6bca2cd1141fd
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80710785"
---
# <a name="how-to-open-standard-editors"></a>方法: 標準エディターを開く
標準エディタを開くと、IDE で指定されたファイルタイプの標準エディタを決定できます。

 メソッドを実装するには、次の<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.OpenItem%2A>手順を実行します。 これにより、標準エディタでプロジェクトファイルが開きます。

## <a name="to-implement-the-openitem-method-with-a-standard-editor"></a>標準エディターを使用して OpenItem メソッドを実装するには

1. ドキュメント<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable>`RDT_EditLock`データ オブジェクト ファイルが既に開かれているかどうかを調べるには、 ( ) を呼び出します。

2. ファイルが既に開いている場合は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.IsDocumentOpen%2A>`IDO_ActivateIfOpen``grfIDO`メソッドを呼び出してファイルを再表示し、パラメーターの値を指定します。

     ファイルが開いていて、ドキュメントが呼び出し元のプロジェクトとは異なるプロジェクトによって所有されている場合、開いているエディターが別のプロジェクトからのものであるという警告がプロジェクトに表示されます。 ファイル ウィンドウが表示されます。

3. 実行中のドキュメント テーブルでドキュメントが開いていない場合、または開いていない場合<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A>は、`OSE_ChooseBestStdEditor`メソッド ( ) を呼び出して、ファイルの標準エディターを開きます。

     このメソッドを呼び出すと、IDE は次のタスクを実行します。

    1. IDE は、レジストリのエディタ/{guidEditorType}/拡張機能サブキーをスキャンして、どのエディターがファイルを開くことができるか、およびこれを行うための最も優先順位が高いかどうかを判断します。

    2. IDE がファイルを開くことができるエディタを決定した後、IDE<xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A>は を呼び出します。 エディターのこのメソッドの実装は、IDE が新しく開いたドキュメントを呼<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.CreateDocumentWindow%2A>び出し、サイトに必要な情報を返します。

    3. 最後に、IDE は、 など<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2>通常の永続性インターフェイスを使用してドキュメントを読み込みます。

    4. IDE が以前に階層または階層項目が使用可能であると判断した場合、IDE<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.GetItemContext%2A>はプロジェクトのメソッドを呼び出して、メソッド<xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider>呼び出しで戻す<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.CreateDocumentWindow%2A>プロジェクトレベルのコンテキストポインターを取得します。

4. エディターに<xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider>プロジェクトからコンテキストを取得させる場合は<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.GetItemContext%2A>、IDE がプロジェクトを呼び出すときに、IDE へのポインターを返します。

     この手順を実行すると、プロジェクトはエディターに追加のサービスを提供できます。

     ドキュメント ビューまたはドキュメント ビュー オブジェクトがウィンドウ フレームに正常に位置指定された場合、オブジェクトは を呼び<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.LoadDocData%2A>出すことによってデータで初期化されます。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider>
- [プロジェクト項目を開いて保存する](../extensibility/internals/opening-and-saving-project-items.md)
- [方法: プロジェクト固有のエディターを開く](../extensibility/how-to-open-project-specific-editors.md)
- [[方法] 開いているドキュメントのエディターを開く](../extensibility/how-to-open-editors-for-open-documents.md)
- [[ファイルを開く] コマンドを使用してファイルを表示する](../extensibility/internals/displaying-files-by-using-the-open-file-command.md)
