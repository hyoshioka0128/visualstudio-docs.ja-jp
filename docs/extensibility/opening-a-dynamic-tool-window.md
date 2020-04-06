---
title: ダイナミック ツール ウィンドウを開く |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- tool windows, dynamic
ms.assetid: 21547ba7-6e81-44df-9277-265bf34f877a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ff971f980b0a9b2fb0e22f56fb0ace752829c2c3
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80702259"
---
# <a name="open-a-dynamic-tool-window"></a>動的ツール ウィンドウを開く
ツール ウィンドウは、通常、メニューのコマンドまたは同等のキーボード ショートカットから開きます。 ただし、特定の UI コンテキストが適用されるたびに開き、UI コンテキストが適用されなくなると閉じるツール ウィンドウが必要になる場合があります。 このようなツール ウィンドウは、*動的*または*自動表示*と呼ばれます。

> [!NOTE]
> 定義済み UI コンテキストの一覧については、<xref:Microsoft.VisualStudio.VSConstants.UICONTEXT>を参照してください。

 動的ツール ウィンドウを起動時に開く場合、作成に失敗する可能性がある場合は、インターフェイスを<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackageDynamicToolOwnerEx>実装し、メソッドでエラー条件をテストする<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackageDynamicToolOwnerEx.QueryShowTool%2A>必要があります。 起動時に動的ツール ウィンドウを開く必要があることをシェルが認識するには、パッケージ登録に`SupportsDynamicToolOwner`値 (1 に設定) を追加する必要があります。 この値は標準<xref:Microsoft.VisualStudio.Shell.PackageRegistrationAttribute>の一部ではないため、カスタム属性を作成して追加する必要があります。 カスタム属性の詳細については、「[カスタム登録属性を使用して拡張機能を登録する」を](../extensibility/registering-and-unregistering-vspackages.md#using-a-custom-registration-attribute-to-register-an-extension)参照してください。

 ツール<xref:Microsoft.VisualStudio.Shell.Package.FindToolWindow%2A>ウィンドウを開くために使用します。 必要に応じてツール ウィンドウが作成されます。

> [!NOTE]
> 動的ツール ウィンドウは、ユーザーが閉じることができます。 ユーザーがツール ウィンドウを再び開くことができるようにメニュー コマンドを作成する場合は、メニュー コマンドをツール ウィンドウを開く UI コンテキストで有効にし、それ以外の場合は無効にする必要があります。

## <a name="to-open-a-dynamic-tool-window"></a>動的ツール ウィンドウを開くには

1. **DynamicToolWindow**という名前の VSIX プロジェクトを作成し *、DynamicWindowPane.cs*という名前のツール ウィンドウ項目テンプレートを追加します。 詳細については、「ツール[ウィンドウを使用した拡張機能の作成](../extensibility/creating-an-extension-with-a-tool-window.md)」を参照してください。

2. *DynamicWindowPanePackage.cs*ファイルで、宣言を見つけます。 属性と<xref:Microsoft.VisualStudio.Shell.ProvideToolWindowAttribute><xref:Microsoft.VisualStudio.Shell.ProvideToolWindowVisibilityAttribute>属性を追加して、ツール ウィンドウを登録します。

    ```vb
    [ProvideToolWindow(typeof(DynamicWindowPane)]
    [ProvideToolWindowVisibility(typeof(DynamicWindowPane), VSConstants.UICONTEXT.SolutionExists_string)]
    [PackageRegistration(UseManagedResourcesOnly = true)]
    [InstalledProductRegistration("#110", "#112", "1.0", IconResourceID = 400)] // Info on this package for Help/About
    [ProvideMenuResource("Menus.ctmenu", 1)]
    [ProvideToolWindow(typeof(DynamicToolWindow.DynamicWindowPane))]
    [Guid(DynamicWindowPanePackage.PackageGuidString)]
    public sealed class DynamicWindowPanePackage : Package
    {. . .}
    ```

     上記の属性は、Visual Studio を閉じて再び開いたときに永続化されない一時的なウィンドウとして DynamicWindowPane という名前のツール ウィンドウを登録します。 適用されるたびに<xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionExists_string>開かれ、それ以外の場合は閉じられます。

3. プロジェクトをビルドし、デバッグを開始します。 実験用インスタンスが表示されます。 ツール ウィンドウは表示されません。

4. 実験用インスタンスでプロジェクトを開きます。 ツール ウィンドウが表示されます。
