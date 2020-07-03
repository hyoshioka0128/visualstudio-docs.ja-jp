---
title: VSPackage | を使用した拡張機能の作成Microsoft Docs
ms.date: 3/16/2019
ms.topic: how-to
ms.assetid: c0cc5e08-4897-44f2-8309-e3478f1f999e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 68ade2f8d334c1f93349e396d910fa300f6b5417
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85903854"
---
# <a name="create-an-extension-with-a-vspackage"></a>VSPackage を使用して拡張機能を作成する

このチュートリアルでは、VSIX プロジェクトを作成し、VSPackage プロジェクト項目を追加する方法について説明します。 VSPackage を使用して、メッセージボックスを表示するために UI シェルサービスを取得します。

## <a name="prerequisites"></a>必須コンポーネント

Visual Studio 2015 以降では、ダウンロードセンターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップでオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「 [Visual STUDIO SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-a-vspackage"></a>VSPackage を作成する

1. **Firstpackage**という名前の VSIX プロジェクトを作成します。 VSIX プロジェクトテンプレートは、"vsix" を検索することで、[**新しいプロジェクト**] ダイアログで見つけることができます。

2. プロジェクトが開いたら、 **Firstpackage**という名前の Visual Studio パッケージ項目テンプレートを追加します。 **ソリューションエクスプローラー**で、プロジェクトノードを右クリックし、[新しい項目の**追加**] を選択し  >  **New Item**ます。 [**新しい項目の追加**] ダイアログで、[ **visual C#** の  >  **機能拡張**] にアクセスし、[ **visual Studio パッケージ**] を選択します。 ウィンドウの下部にある [**名前**] フィールドで、[コマンドファイル名] を*FirstPackage.cs*に変更します。

3. プロジェクトをビルドし、デバッグを開始します。

    Visual Studio の実験用インスタンスが表示されます。 実験用インスタンスの詳細については、[実験用インスタンス](../extensibility/the-experimental-instance.md)を参照してください。

4. 実験用インスタンスで、[**ツール**  >  ] [**拡張機能と更新プログラム**] ウィンドウを開きます。 **Firstpackage**拡張機能がここに表示されます。 (Visual Studio の作業インスタンスで**拡張機能と更新プログラム**を開いた場合、 **firstpackage**は表示されません)。

## <a name="load-the-vspackage"></a>VSPackage を読み込む

この時点では、読み込まれる原因となるものがないため、拡張機能は読み込まれません。 通常、拡張機能を読み込むには、UI を操作する (メニューコマンドをクリックするか、ツールウィンドウを開く) か、または VSPackage が特定の UI コンテキストで読み込むように指定します。 Vspackage と UI コンテキストの読み込みの詳細については、「 [vspackage の読み込み](../extensibility/loading-vspackages.md)」を参照してください。 この手順では、ソリューションが開いているときに VSPackage を読み込む方法について説明します。

1. *FirstPackage.cs*ファイルを開きます。 クラスの宣言を探し `FirstPackage` ます。 既存の属性を次の属性に置き換えます。

    ```csharp
    [PackageRegistration(UseManagedResourcesOnly = true)]
    [InstalledProductRegistration("#110", "#112", "1.0", IconResourceID = 400)] // Info on this package for Help/About
    [ProvideAutoLoad(UIContextGuids80.SolutionExists)]
    [Guid(FirstPackage.PackageGuidString)]
    public sealed class FirstPackage : Package
    ```

2. VSPackage が読み込まれたことを知らせるメッセージを追加してみましょう。 `Initialize()`VSPackage が配置された後にのみ Visual Studio サービスを取得できるため、VSPackage のメソッドを使用します。 (サービスの取得の詳細については、「[方法: サービスを取得する](../extensibility/how-to-get-a-service.md)」を参照してください)。`Initialize()`のメソッドを、 `FirstPackage` サービスを取得するコードに置き換え <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell> 、インターフェイスを取得して、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> メソッドを呼び出し <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ShowMessageBox%2A> ます。

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
