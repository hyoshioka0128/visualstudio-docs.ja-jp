---
title: 動的ツールウィンドウを開く |Microsoft Docs
description: 動的ツールウィンドウについて説明します。これは、UI コンテキストが適用されなくなったときに、特定の UI コンテキストが適用されるたびに開きます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- tool windows, dynamic
ms.assetid: 21547ba7-6e81-44df-9277-265bf34f877a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 357644f67da9a3bbc468d708cf39e44f737dbf0f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105090422"
---
# <a name="open-a-dynamic-tool-window"></a>動的ツールウィンドウを開く
ツールウィンドウは、通常、メニューのコマンドから、または同等のキーボードショートカットによって開かれます。 ただし、特定の UI コンテキストが適用されるたびに表示されるツールウィンドウが必要になる場合があり、UI コンテキストが適用されなくなると、が終了します。 これらの種類のツールウィンドウは、 *動的* または *自動で表示* されます。

> [!NOTE]
> 定義済みの UI コンテキストの一覧については、「」を参照してください <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT> 。

 起動時に動的ツールウィンドウを開き、作成が失敗する可能性がある場合は、インターフェイスを実装 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackageDynamicToolOwnerEx> し、メソッドでエラー条件をテストする必要があり <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackageDynamicToolOwnerEx.QueryShowTool%2A> ます。 起動時に開く必要がある動的なツールウィンドウがあることをシェルが認識できるようにするには、 `SupportsDynamicToolOwner` パッケージ登録に値 (1 に設定) を追加する必要があります。 この値は標準の一部ではない <xref:Microsoft.VisualStudio.Shell.PackageRegistrationAttribute> ため、カスタム属性を作成して追加する必要があります。 カスタム属性の詳細については、「 [カスタム登録属性を使用して拡張機能を登録する](../extensibility/registering-and-unregistering-vspackages.md#using-a-custom-registration-attribute-to-register-an-extension)」を参照してください。

 <xref:Microsoft.VisualStudio.Shell.Package.FindToolWindow%2A>ツールウィンドウを開くには、を使用します。 必要に応じて、ツールウィンドウが作成されます。

> [!NOTE]
> 動的なツールウィンドウは、ユーザーが閉じることができます。 メニューコマンドを作成して、ユーザーがツールウィンドウを再び開くことができるようにするには、ツールウィンドウを開いたのと同じ UI コンテキストでメニューコマンドを有効にし、それ以外の場合は無効にします。

## <a name="to-open-a-dynamic-tool-window"></a>動的ツールウィンドウを開くには

1. **DynamicToolWindow** という名前の VSIX プロジェクトを作成し、 *DynamicWindowPane* という名前のツールウィンドウ項目テンプレートを追加します。 詳細については、「 [ツールウィンドウで拡張機能を作成](../extensibility/creating-an-extension-with-a-tool-window.md)する」を参照してください。

2. *Dynamicwindowpanepackage .cs* ファイルで、dynamicwindowpanepackage 宣言を見つけます。 <xref:Microsoft.VisualStudio.Shell.ProvideToolWindowAttribute> <xref:Microsoft.VisualStudio.Shell.ProvideToolWindowVisibilityAttribute> ツールウィンドウを登録するには、属性と属性を追加します。

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

     上記の属性では、DynamicWindowPane という名前のツールウィンドウを一時的なウィンドウとして登録します。これは、Visual Studio を閉じてからもう一度開くと、永続化されません。 DynamicWindowPane は <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionExists_string> 、適用されるたびに開かれ、それ以外の場合は閉じられます。

3. プロジェクトをビルドし、デバッグを開始します。 実験用インスタンスが表示されます。 ツールウィンドウが表示されません。

4. 実験用インスタンスでプロジェクトを開きます。 ツールウィンドウが表示されます。
