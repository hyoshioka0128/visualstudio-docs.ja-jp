---
title: 動的ツールウィンドウを開く |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- tool windows, dynamic
ms.assetid: 21547ba7-6e81-44df-9277-265bf34f877a
caps.latest.revision: 22
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 09b81294abc708cf7616dad03b5dd7333d6a1719
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841964"
---
# <a name="opening-a-dynamic-tool-window"></a>動的なツール ウィンドウを開く
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ツールウィンドウは、通常、メニューのコマンドから、または同等のキーボードショートカットによって開かれます。 ただし、特定の UI コンテキストが適用されるたびに表示されるツールウィンドウが必要になる場合があり、UI コンテキストが適用されなくなると、が終了します。 このようなツールウィンドウは、 *動的* または *自動で表示*されます。  
  
> [!NOTE]
> 定義済みの UI コンテキストの一覧については、「」を参照してください <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT> 。 この場合、  
  
 起動時に動的ツールウィンドウを開き、作成が失敗する可能性がある場合は、インターフェイスを実装 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackageDynamicToolOwnerEx> し、メソッドでエラー条件をテストする必要があり <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackageDynamicToolOwnerEx.QueryShowTool%2A> ます。 起動時に開く必要がある動的なツールウィンドウがあることをシェルが認識できるようにするには、 `SupportsDynamicToolOwner` パッケージ登録に値 (1 に設定) を追加する必要があります。 この値は標準の一部ではない <xref:Microsoft.VisualStudio.Shell.PackageRegistrationAttribute> ため、カスタム属性を作成して追加する必要があります。 カスタム属性の詳細については、「 [カスタム登録属性を使用した拡張機能の登録](../misc/using-a-custom-registration-attribute-to-register-an-extension.md)」を参照してください。  
  
 <xref:Microsoft.VisualStudio.Shell.Package.FindToolWindow%2A>ツールウィンドウを開くには、を使用します。 必要に応じて、ツールウィンドウが作成されます。  
  
> [!NOTE]
> 動的なツールウィンドウは、ユーザーが閉じることができます。 メニューコマンドを作成して、ユーザーがツールウィンドウを再び開くことができるようにするには、ツールウィンドウを開いたのと同じ UI コンテキストでメニューコマンドを有効にし、それ以外の場合は無効にします。  
  
### <a name="to-open-a-dynamic-tool-window"></a>動的ツールウィンドウを開くには  
  
1. **DynamicToolWindow**という名前の VSIX プロジェクトを作成し、 **DynamicWindowPane.cs**という名前のツールウィンドウ項目テンプレートを追加します。 詳細については、「 [ツールウィンドウを使用した拡張機能の作成](../extensibility/creating-an-extension-with-a-tool-window.md)」を参照してください。  
  
2. DynamicWindowPanePackage.cs ファイルで、DynamicWindowPanePackage 宣言を見つけます。 <xref:Microsoft.VisualStudio.Shell.ProvideToolWindowAttribute>ツールウィンドウを登録するには、および T:Microsoft.VisualStudio.Shell.ProvideToolWindowVisibilityAttribute 属性を追加します。  
  
    ```vb  
    [[ProvideToolWindow(typeof(DynamicWindowPane)]  
    [ProvideToolWindowVisibility(typeof(DynamicWindowPane), VSConstants.UICONTEXT.SolutionExists_string)]  
    [PackageRegistration(UseManagedResourcesOnly = true)]  
    [InstalledProductRegistration("#110", "#112", "1.0", IconResourceID = 400)] // Info on this package for Help/About  
    [ProvideMenuResource("Menus.ctmenu", 1)]  
    [ProvideToolWindow(typeof(DynamicToolWindow.DynamicWindowPane))]  
    [Guid(DynamicWindowPanePackageGuids.PackageGuidString)]  
    public sealed class DynamicWindowPanePackage : Package  
    {. . .}  
    ```  
  
     これにより、DynamicWindowPane という名前のツールウィンドウが一時的なウィンドウとして登録されます。このウィンドウは、Visual Studio を閉じてからもう一度開くと保持されません。 DynamicWindowPane は <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionExists_string> 、適用されるたびに開かれ、それ以外の場合は閉じられます。  
  
3. プロジェクトをビルドし、デバッグを開始します。 実験用インスタンスが表示されます。 ツールウィンドウが表示されません。  
  
4. 実験用インスタンスでプロジェクトを開きます。 ツールウィンドウが表示されます。
