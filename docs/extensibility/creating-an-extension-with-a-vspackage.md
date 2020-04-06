---
title: VS パッケージを使用して拡張機能を作成する |マイクロソフトドキュメント
ms.date: 3/16/2019
ms.topic: conceptual
ms.assetid: c0cc5e08-4897-44f2-8309-e3478f1f999e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1037ebcc58cc4183e6f02119bc7b46abfc132f52
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739527"
---
# <a name="create-an-extension-with-a-vspackage"></a>VS パッケージを使用して拡張機能を作成します。

このチュートリアルでは、VSIX プロジェクトを作成し、VSPackage プロジェクト項目を追加する方法を示します。 メッセージ ボックスを表示するために、VSPackage を使用して UI シェル サービスを取得します。

## <a name="prerequisites"></a>必須コンポーネント

Visual Studio 2015 以降では、ダウンロード センターから Visual Studio SDK をインストールしません。 これは、Visual Studio のセットアップのオプション機能として含まれています。 VS SDK は後でインストールすることもできます。 詳細については、「 [Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-a-vspackage"></a>VS パッケージの作成

1. という名前の VSIX プロジェクト**を作成します**。 VSIX プロジェクト テンプレートは、"vsix" を検索して **[新しいプロジェクト**] ダイアログで見つけることができます。

2. プロジェクトが開いたら **、"FirstPackage"** という名前の Visual Studio パッケージ項目テンプレートを追加します。 ソリューション**エクスプローラ**で、プロジェクト ノードを右クリックし、[**Add** > **新しい項目**の追加] を選択します。 [**新しい項目の追加]** ダイアログ**で、[Visual C#** > **の機能拡張**] に移動し **、[Visual Studio パッケージ**] を選択します。 ウィンドウの下部にある [**名前]** フィールドで、コマンド ファイル名を*FirstPackage.cs*に変更します。

3. プロジェクトをビルドし、デバッグを開始します。

    Visual Studio の実験用インスタンスが表示されます。 実験インスタンスの詳細については、「[実験インスタンス](../extensibility/the-experimental-instance.md)」を参照してください。

4. 実験用インスタンスで、[**ツール** > **の拡張機能と更新]** ウィンドウを開きます。 ここで**FirstPackage**拡張機能が表示されます。 (Visual Studio の作業用インスタンスで**拡張機能と更新プログラム**を開いた場合は **、FirstPackage**が表示されません。

## <a name="load-the-vspackage"></a>VS パッケージを読み込む

この時点では、読み込みを引き起こす原因となるものがないため、拡張機能は読み込まれません。 拡張機能は、通常、UI を操作する場合 (メニュー コマンドをクリックしてツール ウィンドウを開く)、または VSPackage が特定の UI コンテキストで読み込まれる必要があることを指定することによって読み込むことができます。 VSPackages と UI コンテキストの読み込みの詳細については、「 [VSPackages の読み込み](../extensibility/loading-vspackages.md)」を参照してください。 この手順では、ソリューションが開いているときに VSPackage を読み込む方法を示します。

1. *FirstPackage.cs*ファイルを開きます。 クラスの宣言を探します`FirstPackage`。 既存の属性を次の属性に置き換えます。

    ```csharp
    [PackageRegistration(UseManagedResourcesOnly = true)]
    [InstalledProductRegistration("#110", "#112", "1.0", IconResourceID = 400)] // Info on this package for Help/About
    [ProvideAutoLoad(UIContextGuids80.SolutionExists)]
    [Guid(FirstPackage.PackageGuidString)]
    public sealed class FirstPackage : Package
    ```

2. VSPackage が読み込まれたことを知らせるメッセージを追加しましょう。 これを行うには、VSPackage`Initialize()`がサイト化された後にのみ Visual Studio サービスを取得できるため、この方法を使用します。 (サービスの取得の詳細については、「[方法 : サービスを取得する](../extensibility/how-to-get-a-service.md)」を参照してください)。`Initialize()`の`FirstPackage`メソッドを、サービスを取得し、<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell>インターフェイスを取得し<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell>、そのメソッドを呼<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ShowMessageBox%2A>び出すコードに置き換えます。

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

4. 実験用インスタンスでソリューションを開きます。 **「最初のパッケージ内部初期化()」** というメッセージボックスが表示されます。
