---
title: VSPackage | を使用した拡張機能の作成Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: c0cc5e08-4897-44f2-8309-e3478f1f999e
caps.latest.revision: 6
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: ddad7149db75aa662f9427a301c04eaf925146f9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68197428"
---
# <a name="creating-an-extension-with-a-vspackage"></a>VSPackage を使用した拡張機能の作成
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このチュートリアルでは、VSIX プロジェクトを作成し、VSPackage プロジェクト項目を追加する方法について説明します。 VSPackage を使用して、メッセージボックスを表示するために UI シェルサービスを取得します。  
  
## <a name="prerequisites"></a>必須コンポーネント  
 Visual Studio 2015 以降では、ダウンロードセンターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップでオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「 [Visual STUDIO SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。  
  
## <a name="creating-a-vspackage"></a>VSPackage の作成  
  
1. **Firstpackage**という名前の VSIX プロジェクトを作成します。 VSIX プロジェクトテンプレートは、[ **新しいプロジェクト** ] ダイアログボックスの [ **Visual C#]/[拡張機能**] で見つけることができます。  
  
2. プロジェクトが開いたら、 **Firstpackage**という名前の Visual Studio パッケージ項目テンプレートを追加します。 **ソリューションエクスプローラー**で、プロジェクトノードを右クリックし、[追加]、[**新しい項目**] の順に選択します。 [ **新しい項目の追加** ] ダイアログで、[ **Visual C#]/[拡張機能** ] にアクセスし、[ **visual Studio パッケージ**] を選択します。 ウィンドウの下部にある [ **名前** ] フィールドで、[コマンドファイル名] を **FirstPackage.cs**に変更します。  
  
3. プロジェクトをビルドし、デバッグを開始します。  
  
     Visual Studio の実験用インスタンスが表示されます。 実験用インスタンスの詳細については、 [実験用インスタンス](../extensibility/the-experimental-instance.md)を参照してください。  
  
4. 実験用インスタンスで、[ツール]、[ **拡張機能と更新プログラム** ] ウィンドウの順に開きます。 **Firstpackage**拡張機能がここに表示されます。 (Visual Studio の作業インスタンスで **拡張機能と更新プログラム** を開いた場合、 **firstpackage**は表示されません)。  
  
## <a name="loading-the-vspackage"></a>VSPackage を読み込んでいます  
 この時点では、この拡張機能は読み込まれません。これは、読み込みの原因となるものがないためです。 通常、拡張機能を読み込むには、UI を操作する (メニューコマンドをクリックするか、ツールウィンドウを開く) か、または VSPackage が特定の UI コンテキストで読み込むように指定します。 Vspackage と UI コンテキストの読み込みの詳細については、「 [vspackage の読み込み](../extensibility/loading-vspackages.md)」を参照してください。 この手順では、ソリューションが開いているときに VSPackage を読み込む方法について説明します。  
  
1. FirstPackage.cs ファイルを開きます。 FirstPackage クラスの宣言を探します。 既存の属性を次のように置き換えます。  
  
    ```csharp  
    [PackageRegistration(UseManagedResourcesOnly = true)]  
    [InstalledProductRegistration("#110", "#112", "1.0", IconResourceID = 400)] // Info on this package for Help/About  
    [ProvideAutoLoad(UIContextGuids80.SolutionExists)]  
    [Guid(FirstPackageGuids.PackageGuidString)]  
    public sealed class FirstPackage : Package  
    ```  
  
2. VSPackage が読み込まれたことを知らせるメッセージを追加してみましょう。 VSPackage の Initialize () メソッドを使用してこれを行います。これは、VSPackage が配置された後にのみ、Visual Studio サービスを取得できるためです。 (サービスの取得の詳細については、「 [方法: サービスを取得する](../extensibility/how-to-get-a-service.md)」を参照してください)。FirstPackage の Initialize () メソッドを、サービスを取得するコードに置き換え <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell> 、インターフェイスを取得して、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> メソッドを呼び出し <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ShowMessageBox%2A> ます。  
  
    ```csharp  
    protected override void Initialize()  
    {  
        base.Initialize();  
  
        IVsUIShell uiShell = (IVsUIShell)GetService(typeof(SVsUIShell));  
        Guid clsid = Guid.Empty;  
        int result;  
        Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure(uiShell.ShowMessageBox(  
            0,  
            ref clsid,  
            "FirstPackage",  
             string.Format(CultureInfo.CurrentCulture, "Inside {0}.Initialize()", this.GetType().FullName),  
            string.Empty,  
            0,  
            OLEMSGBUTTON.OLEMSGBUTTON_OK,  
            OLEMSGDEFBUTTON.OLEMSGDEFBUTTON_FIRST,  
            OLEMSGICON.OLEMSGICON_INFO,  
            0,  
            out result));  
    }  
    ```  
  
3. プロジェクトをビルドし、デバッグを開始します。 実験用インスタンスが表示されます。  
  
4. 実験用インスタンスでソリューションを開きます。 **最初のパッケージが Initialize () の中**にあるというメッセージボックスが表示されます。
