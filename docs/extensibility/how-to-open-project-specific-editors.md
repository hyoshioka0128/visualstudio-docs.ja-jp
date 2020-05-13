---
title: '方法 : プロジェクト固有のエディターを開く |マイクロソフトドキュメント'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project types, opening a project-specific editor
- editors [Visual Studio SDK], opening project-specific editors
- projects [Visual Studio SDK], opening folders
ms.assetid: 83e56d39-c97b-4c6b-86d6-3ffbec97e8d1
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 3cb6e360a38d64de4976f83b0167d47dc03fbc87
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80710840"
---
# <a name="how-to-open-project-specific-editors"></a>方法: プロジェクト固有のエディターを開く
プロジェクトによって開かれている項目ファイルが、そのプロジェクトの特定のエディターに本質的にバインドされている場合、プロジェクトはプロジェクト固有のエディターを使用してファイルを開く必要があります。 エディタを選択するための IDE のメカニズムにファイルを委任することはできません。 たとえば、標準のビットマップ エディタを使用する代わりに、このプロジェクト固有のエディター オプションを使用して、プロジェクトに固有のファイル内の情報を認識する特定のビットマップ エディターを指定できます。

 IDE は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.OpenItem%2A>特定のプロジェクトでファイルを開く必要があると判断したときに、このメソッドを呼び出します。 詳細については、「 [[ファイルを開く] コマンドを使用してファイルを表示する](../extensibility/internals/displaying-files-by-using-the-open-file-command.md)」を参照してください。 プロジェクト固有のエディターを使用して`OpenItem`プロジェクトでファイルを開くメソッドを実装するには、次のガイドラインに従います。

## <a name="to-implement-the-openitem-method-with-a-project-specific-editor"></a>プロジェクト固有のエディターを使用して OpenItem メソッドを実装するには

1. <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.FindAndLockDocument%2A>ファイル (ドキュメント`RDT_EditLock`データ オブジェクト) が既に開かれているかどうかを調べるには、メソッド ( ) を呼び出します。

    > [!NOTE]
    > ドキュメント データとドキュメント ビュー オブジェクトの詳細については、「[カスタム エディタでのドキュメント データとドキュメント ビュー](../extensibility/document-data-and-document-view-in-custom-editors.md)」を参照してください。

2. ファイルが既に開いている場合は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.IsDocumentOpen%2A>メソッドを呼び出し、パラメーターに IDO_ActivateIfOpen の値を`grfIDO`指定して、ファイルを再表示します。

     ファイルが開いていて、ドキュメントが呼び出し元のプロジェクト以外のプロジェクトによって所有されている場合、開いているエディターが別のプロジェクトからのものであるという警告がユーザーに表示されます。 ファイル ウィンドウが表示されます。

3. テキスト バッファー (ドキュメント データ オブジェクト) が既に開いている場合に別のビューをアタッチする場合は、そのビューをフックする必要があります。 プロジェクトからビュー (ドキュメント ビュー オブジェクト) をインスタンス化する場合は、次の方法をお勧めします。

    1. インターフェイス`QueryService`へのポインター<xref:Microsoft.VisualStudio.Shell.Interop.SLocalRegistry>を取得するサービスを<xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry2>呼び出します。

    2. ドキュメント<xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry2.CreateInstance%2A>ビュー クラスのインスタンスを作成するメソッドを呼び出します。

4. ドキュメント<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.CreateDocumentWindow%2A>ビュー オブジェクトを指定して、メソッドを呼び出します。

     このメソッドは、ドキュメント ウィンドウ内のドキュメント ビュー オブジェクトをサイト化します。

5. <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat.InitNew%2A>または メソッドに対して適切な呼<xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat.Load%2A>び出しを実行します。

     この時点で、ビューは完全に初期化され、開く準備が整っている必要があります。

6. ビューを<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.Show%2A>表示して開くには、メソッドを呼び出します。

## <a name="see-also"></a>関連項目
- [プロジェクト アイテムを開いて保存する](../extensibility/internals/opening-and-saving-project-items.md)
- [方法: 標準エディターを開く](../extensibility/how-to-open-standard-editors.md)
- [[方法] 開いているドキュメントのエディターを開く](../extensibility/how-to-open-editors-for-open-documents.md)
