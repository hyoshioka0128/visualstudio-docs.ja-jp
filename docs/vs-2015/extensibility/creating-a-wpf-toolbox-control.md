---
title: WPF ツールボックスコントロールの作成 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- toolbox control
- toolbox
- wpf
ms.assetid: 9cc34db9-b0d1-4951-a02f-7537fbbb51ad
caps.latest.revision: 17
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 768d9747635f2106d16f755db6799e356c890838
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68197432"
---
# <a name="creating-a-wpf-toolbox-control"></a>WPF ツールボックス コントロールの作成
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

WPF (Windows Presentation Framework) ツールボックスコントロールテンプレートを使用すると、拡張機能のインストール時に自動的に **ツールボックス** に追加される wpf コントロールを作成できます。 このトピックでは、テンプレートを使用して、他のユーザーに配布できる **ツールボックス** コントロールを作成する方法について説明します。  
  
 Visual Studio 2015 以降では、ダウンロードセンターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップでオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「 [Visual STUDIO SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。  
  
## <a name="creating-a-wpf-toolbox-control"></a>WPF ツールボックス コントロールの作成  
  
#### <a name="create-an-extension-with-a-wpf-toolbox-control"></a>WPF ツールボックスコントロールを使用して拡張機能を作成する  
  
1. という名前の VSIX プロジェクトを作成 `MyToolboxControl` します。 VSIX プロジェクトテンプレートは、[ **新しいプロジェクト** ] ダイアログボックスの [ **Visual C#]/[拡張機能**] で見つけることができます。  
  
2. プロジェクトが開いたら、という名前の **WPF ツールボックスコントロール** 項目テンプレートを追加 `MyToolboxControl` します。 **ソリューションエクスプローラー**で、プロジェクトノードを右クリックし、[追加]、[**新しい項目**] の順に選択します。 [ **新しい項目の追加** ] ダイアログで、[ **Visual C#]/[機能拡張** ] にアクセスし、[ **WPF ツールボックスコントロール**] を選択します。 ウィンドウの下部にある [ **名前** ] フィールドで、コマンドファイル名をに変更し `MyToolboxControl.cs` ます。  
  
     このソリューションには、ユーザーコントロール、 `ProvideToolboxControlAttribute` <xref:Microsoft.VisualStudio.Shell.RegistrationAttribute> コントロールを**ツールボックス**に追加する、および VSIX マニフェストの**VisualStudio ToolboxControl** Asset エントリが含まれるようになりました。  
  
#### <a name="to-create-the-control-ui"></a>コントロール UI を作成するには  
  
1. デザイナーで MyToolboxControl を開きます。  
  
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
 既定では、コントロールは、 **MyToolboxControl**という名前のグループの**MyToolboxControl**として**ツールボックス**に表示されます。 これらの名前は、MyToolboxControl.xaml.cs ファイルで変更できます。  
  
1. コードビューで MyToolboxControl.xaml.cs を開きます。  
  
2. MyToolboxControl クラスを見つけ、その名前を TestControl に変更します。 (これを行う最も簡単な方法は、クラスの名前を変更し、コンテキストメニューから [ **名前の変更** ] を選択して、手順を完了することです。 ( **Rename** コマンドの詳細については、「 [名前の変更リファクタリング (C#)](../csharp-ide/rename-refactoring-csharp.md)」を参照してください)。  
  
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
  
## <a name="building-testing-and-deployment"></a>ビルド、テスト、展開  
 プロジェクトをデバッグするときに、Visual Studio の実験用インスタンスの **ツールボックス** にコントロールがインストールされていることを確認する必要があります。  
  
#### <a name="to-build-and-test-the-control"></a>コントロールをビルドおよびテストするには  
  
1. プロジェクトをリビルドし、デバッグを開始します。  
  
2. Visual Studio の新しいインスタンスで、WPF アプリケーション プロジェクトを作成します。 XAML デザイナーが開いていることを確認します。  
  
3. **[ツールボックス]** で対象のコントロールを見つけて、デザイン画面にドラッグします。  
  
4. WPF アプリケーションのデバッグを開始します。  
  
5. コントロールが表示されることを確認します。  
  
#### <a name="to-deploy-the-control"></a>コントロールを配置するには  
  
1. テストされたプロジェクトをビルドした後、プロジェクトの \bin\debug\ フォルダーに .vsix ファイルを検索できます。  
  
2. .Vsix ファイルをダブルクリックし、インストール手順に従って、ローカルコンピューターにインストールすることができます。 コントロールをアンインストールするには、[ツール]、[ **拡張機能と更新プログラム** ] の順に選択し、コントロールの拡張機能を探して、[ **アンインストール**] をクリックします。  
  
3. .vsix ファイルをネットワークまたは Web サイトにアップロードします。  
  
     ファイルを [Visual Studio Marketplace](https://marketplace.visualstudio.com/) Web サイトにアップロードした場合、他のユーザーは Visual Studio の [ツール]、[ **拡張機能と更新プログラム** ] を使用して、コントロールをオンラインで検索し、インストールすることができます。
