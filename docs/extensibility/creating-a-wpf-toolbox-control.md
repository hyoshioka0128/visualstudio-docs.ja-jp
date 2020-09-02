---
title: WPF ツールボックスコントロールの作成 |Microsoft Docs
ms.date: 3/16/2019
ms.topic: how-to
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
ms.openlocfilehash: a6aa6051648e495e21f7954a737f7b572ce6a6f2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85903941"
---
# <a name="create-a-wpf-toolbox-control"></a>WPF ツールボックスコントロールの作成

WPF (Windows Presentation Framework) ツールボックスコントロールテンプレートを使用すると、拡張機能のインストール時に自動的に **ツールボックス** に追加される wpf コントロールを作成できます。 このチュートリアルでは、テンプレートを使用して、他のユーザーに配布できる **ツールボックス** コントロールを作成する方法について説明します。

Visual Studio 2015 以降では、ダウンロードセンターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップでオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「 [Visual STUDIO SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-the-toolbox-control"></a>ツールボックスコントロールを作成する

### <a name="create-an-extension-with-a-wpf-toolbox-control"></a>WPF ツールボックスコントロールを使用して拡張機能を作成する

1. という名前の VSIX プロジェクトを作成 `MyToolboxControl` します。 VSIX プロジェクトテンプレートは、"vsix" を検索することで、[ **新しいプロジェクト** ] ダイアログで見つけることができます。

2. プロジェクトが開いたら、という名前の **WPF ツールボックスコントロール** 項目テンプレートを追加 `MyToolboxControl` します。 **ソリューションエクスプローラー**で、プロジェクトノードを右クリックし、[新しい項目の**追加**] を選択し  >  **New Item**ます。 [**新しい項目の追加**] ダイアログで、[ **Visual C#** の機能拡張] にアクセスし、  >  **Extensibility** [ **WPF ツールボックスコントロール**] を選択します。 ウィンドウの下部にある [ **名前** ] フィールドで、[コマンドファイル名] を *MyToolboxControl.cs*に変更します。

    このソリューションには、ユーザーコントロール、 `ProvideToolboxControlAttribute` <xref:Microsoft.VisualStudio.Shell.RegistrationAttribute> コントロールを **ツールボックス**に追加する、および VSIX マニフェストの **VisualStudio ToolboxControl** Asset エントリが含まれるようになりました。

#### <a name="to-create-the-control-ui"></a>コントロール UI を作成するには

1. デザイナーで *MyToolboxControl* を開きます。

    デザイナーに、<xref:System.Windows.Controls.Button> コントロールを含む <xref:System.Windows.Controls.Grid> コントロールが表示されます。

2. グリッドレイアウトを配置します。 コントロールを選択すると <xref:System.Windows.Controls.Grid> 、グリッドの上端と左端に青いコントロールバーが表示されます。 グリッドに行と列を追加するには、バーをクリックします。

3. グリッドに子コントロールを追加します。 子コントロールは、 **ツールボックス** からグリッドのセクションにドラッグするか、 `Grid.Row` XAML で属性と属性を設定することによって配置でき `Grid.Column` ます。 次の例では、グリッドの一番上の行に2つのラベルを追加し、2番目の行にボタンを追加します。

    ```xaml
    <Grid>
        <Label Grid.Row="0" Grid.Column="0" Name="label1" />
        <Label Grid.Row="0" Grid.Column="1" Name="label2" />
        <Button Name="button1" Click="button1_Click" Grid.Row="1" Grid.ColumnSpan="2" />
    </Grid>
    ```

## <a name="renaming-the-control"></a>コントロールの名前を変更する

 既定では、コントロールは、 **MyToolboxControl**という名前のグループの**MyToolboxControl**として**ツールボックス**に表示されます。 これらの名前は、 *MyToolboxControl.xaml.cs* ファイルで変更できます。

1. コードビューで *MyToolboxControl.xaml.cs* を開きます。

2. クラスを見つけ `MyToolboxControl` て、その名前を TestControl に変更します。 (これを行う最も簡単な方法は、クラスの名前を変更し、コンテキストメニューから [ **名前の変更** ] を選択して、手順を完了することです。 ( **Rename** コマンドの詳細については、「 [名前の変更リファクタリング (C#)](../ide/reference/rename.md)」を参照してください)。

3. 属性に移動し、 `ProvideToolboxControl` 最初のパラメーターの値を **Test**に変更します。 これは、 **ツールボックス**にコントロールを格納するグループの名前です。

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

 プロジェクトをデバッグするときに、Visual Studio の実験用インスタンスの **ツールボックス** にコントロールがインストールされていることを確認する必要があります。

### <a name="to-build-and-test-the-control"></a>コントロールをビルドおよびテストするには

1. プロジェクトをリビルドし、デバッグを開始します。

2. Visual Studio の新しいインスタンスで、WPF アプリケーション プロジェクトを作成します。 XAML デザイナーが開いていることを確認します。

3. **[ツールボックス]** で対象のコントロールを見つけて、デザイン画面にドラッグします。

4. WPF アプリケーションのデバッグを開始します。

5. コントロールが表示されることを確認します。

### <a name="to-deploy-the-control"></a>コントロールを配置するには

1. テストされたプロジェクトをビルドした後、プロジェクトの * \bin\debug フォルダーで *.vsix*ファイルを見つけることができます。 \*

2. *.Vsix*ファイルをダブルクリックし、インストール手順に従って、ローカルコンピューターにインストールすることができます。 コントロールをアンインストールするには、[**ツール**] [  >  **拡張機能と更新プログラム**] にアクセスし、コントロールの拡張機能を探して、[**アンインストール**] をクリックします。

3. *.Vsix*ファイルをネットワークまたは Web サイトにアップロードします。

    ファイルを[Visual Studio Marketplace](https://marketplace.visualstudio.com/) Web サイトにアップロードした場合、他のユーザーは**Tools**  >  Visual Studio のツールの**拡張機能と更新プログラム**を使用して、コントロールをオンラインで検索し、インストールすることができます。
