---
title: WPF ツールボックス コントロールを作成する |マイクロソフトドキュメント
ms.date: 3/16/2019
ms.topic: conceptual
helpviewer_keywords:
- toolbox control
- toolbox
- wpf
ms.assetid: 9cc34db9-b0d1-4951-a02f-7537fbbb51ad
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c1400efb0095760bf1cee302dd33dcf6ebb90152
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739570"
---
# <a name="create-a-wpf-toolbox-control"></a>WPF ツールボックス コントロールの作成

WPF (Windows プレゼンテーション フレームワーク) ツールボックス コントロール テンプレートを使用すると、拡張機能のインストール時に**ツールボックス**に自動的に追加される WPF コントロールを作成できます。 このチュートリアルでは、テンプレートを使用して、他のユーザーに配布できる**ツールボックス**コントロールを作成する方法を示します。

Visual Studio 2015 以降では、ダウンロード センターから Visual Studio SDK をインストールしません。 これは、Visual Studio のセットアップのオプション機能として含まれています。 VS SDK は後でインストールすることもできます。 詳細については、「 [Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-the-toolbox-control"></a>ツールボックス コントロールを作成する

### <a name="create-an-extension-with-a-wpf-toolbox-control"></a>WPF ツールボックス コントロールを使用して拡張機能を作成する

1. という名前`MyToolboxControl`の VSIX プロジェクトを作成します。 VSIX プロジェクト テンプレートは、"vsix" を検索して **[新しいプロジェクト**] ダイアログで見つけることができます。

2. プロジェクトが開いたら、 という**WPF Toolbox Control**名前`MyToolboxControl`の WPF ツールボックス コントロール項目テンプレートを追加します。 ソリューション**エクスプローラ**で、プロジェクト ノードを右クリックし、[**Add** > **新しい項目**の追加] を選択します。 [**新しい項目の追加]** ダイアログ**で、[Visual C#** > **の機能拡張**] に移動し **、[WPF ツールボックス コントロール**] を選択します。 ウィンドウの下部にある [**名前]** フィールドで、コマンド ファイル名を*MyToolboxControl.cs*に変更します。

    ソリューションには、ユーザー コントロール、`ProvideToolboxControlAttribute`<xref:Microsoft.VisualStudio.Shell.RegistrationAttribute>**ツールボックス**にコントロールを追加するコントロール、配置用の VSIX マニフェストの**Microsoft.VisualStudio.ToolboxControl**資産エントリが含まれるようになりました。

#### <a name="to-create-the-control-ui"></a>コントロール UI を作成するには

1. デザイナーで*MyToolboxControl.xaml*を開きます。

    デザイナーに、<xref:System.Windows.Controls.Button> コントロールを含む <xref:System.Windows.Controls.Grid> コントロールが表示されます。

2. グリッド レイアウトを配置します。 コントロールを<xref:System.Windows.Controls.Grid>選択すると、グリッドの上端と左端に青色のコントロール バーが表示されます。 バーをクリックすると、グリッドに行と列を追加できます。

3. グリッドに子コントロールを追加します。 子コントロールを配置するには、**ツールボックス**からグリッドのセクションにドラッグするか、XAML で子コントロールと`Grid.Row``Grid.Column`属性を設定します。 次の使用例は、グリッドの上の行に 2 つのラベルを追加し、2 行目にボタンを追加します。

    ```xaml
    <Grid>
        <Label Grid.Row="0" Grid.Column="0" Name="label1" />
        <Label Grid.Row="0" Grid.Column="1" Name="label2" />
        <Button Name="button1" Click="button1_Click" Grid.Row="1" Grid.ColumnSpan="2" />
    </Grid>
    ```

## <a name="renaming-the-control"></a>コントロールの名前を変更する

 既定では、コントロールは**ツールボックス**に**MyToolboxControl**として表示されます。 **MyToolboxControl.MyToolboxControl** これらの名前は *、MyToolboxControl.xaml.cs*ファイルで変更できます。

1. コード ビューで*MyToolboxControl.xaml.cs*を開きます。

2. クラスを`MyToolboxControl`検索し、TestControl に名前を変更します。 (最も速い方法は、クラスの名前を変更し、コンテキスト メニューから **[名前の変更]** を選択して、手順を完了することです。 (**名前の変更**コマンドの詳細については、「[リファクタリングの名前変更 (C#)」](../ide/reference/rename.md)を参照してください。

3. `ProvideToolboxControl`属性に移動し、最初のパラメーターの値を**Test**に変更します。 これは、**ツールボックス**内のコントロールを含むグループの名前です。

    結果のコードは次のようになります。

    ```csharp
    [ProvideToolboxControl("Test", true)]
    public partial class TestControl : UserControl
    {
        public TestControl()
        {
            InitializeComponent();
        }
    }
    ```

## <a name="build-test-and-deployment"></a>ビルド、テスト、および配置

 プロジェクトをデバッグするときに、Visual Studio の実験用インスタンスの**ツールボックス**にインストールされているコントロールを見つける必要があります。

### <a name="to-build-and-test-the-control"></a>コントロールをビルドおよびテストするには

1. プロジェクトをリビルドし、デバッグを開始します。

2. Visual Studio の新しいインスタンスで、WPF アプリケーション プロジェクトを作成します。 XAML デザイナーが開いているかどうかを確認します。

3. **[ツールボックス]** で対象のコントロールを見つけて、デザイン画面にドラッグします。

4. WPF アプリケーションのデバッグを開始します。

5. コントロールが表示されることを確認します。

### <a name="to-deploy-the-control"></a>コントロールを配置するには

1. テストしたプロジェクトをビルドした後、プロジェクトの *\bin\debug\*フォルダーに *.vsix*ファイルを検索できます。

2. *.vsix*ファイルをダブルクリックし、インストール手順に従って、ローカル コンピュータにインストールできます。 コントロールをアンインストールするには、[**ツール** > **の拡張機能と更新プログラム]** に移動し、コントロール拡張を探し、[**アンインストール**] をクリックします。

3. *.vsix*ファイルをネットワークまたは Web サイトにアップロードします。

    ファイルを Visual Studio[マーケットプレース](https://marketplace.visualstudio.com/)Web サイトにアップロードすると、他のユーザーは Visual Studio**のツール** > **拡張機能と更新プログラム**を使用して、コントロールをオンラインで検索してインストールできます。
