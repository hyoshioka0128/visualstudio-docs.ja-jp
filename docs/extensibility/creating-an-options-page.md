---
title: オプションページの作成 |マイクロソフトドキュメント
ms.date: 3/16/2019
ms.topic: conceptual
helpviewer_keywords:
- Tools Options pages [Visual Studio SDK], creating
ms.assetid: 9f4e210c-4b47-4daa-91fa-1c301c4587f9
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1607af2a6f68bd5593f9a185188b25b364926fe4
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739518"
---
# <a name="create-an-options-page"></a>オプション ページを作成する

このチュートリアルでは、プロパティ グリッドを使用してプロパティを調べて設定する簡単な [ツール] ページと [オプション] ページを作成します。

 これらのプロパティを設定ファイルに保存して復元するには、次の手順を実行し、「[設定カテゴリを作成する](../extensibility/creating-a-settings-category.md)」を参照してください。

 MPF には、ツール オプション ページ、クラス、およびクラス<xref:Microsoft.VisualStudio.Shell.Package>を作成するのに<xref:Microsoft.VisualStudio.Shell.DialogPage>役立つ 2 つのクラスが用意されています。 クラスをサブクラス化することによって、これらのページのコンテナーを提供する VSPackage`Package`を作成します。 各ツール オプション ページは、クラスから派生`DialogPage`して作成します。

## <a name="prerequisites"></a>必須コンポーネント

 Visual Studio 2015 以降では、ダウンロード センターから Visual Studio SDK をインストールしません。 これは、Visual Studio のセットアップのオプション機能として含まれています。 VS SDK は後でインストールすることもできます。 詳細については、「 [Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-a-tools-options-grid-page"></a>ツール オプション グリッド ページの作成

 このセクションでは、単純な [ツール オプション] プロパティ グリッドを作成します。 このグリッドを使用して、プロパティの値を表示および変更します。

### <a name="to-create-the-vsix-project-and-add-a-vspackage"></a>VSIX プロジェクトを作成し、VS パッケージを追加するには

1. すべての Visual Studio 拡張機能は、拡張機能の資産を含む VSIX 配置プロジェクトで開始します。 という名前[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]`MyToolsOptionsExtension`の VSIX プロジェクトを作成します。 VSIX プロジェクト テンプレートは、"vsix" を検索して **[新しいプロジェクト**] ダイアログで見つけることができます。

2. という名前`MyToolsOptionsPackage`の Visual Studio パッケージ項目テンプレートを追加して VSPackage を追加します。 ソリューション**エクスプローラ**で、プロジェクト ノードを右クリックし、[**Add** > **新しい項目**の追加] を選択します。 [**新しい項目の追加**] ダイアログ で **、[Visual C# アイテム** > **の機能拡張**] に移動し **、[Visual Studio パッケージ**] を選択します。 ダイアログの下部にある [**名前]** フィールドで、ファイル名を`MyToolsOptionsPackage.cs`に変更します。 VSPackage を作成する方法の詳細については、「 [VSPackage を使用して拡張機能を作成する](../extensibility/creating-an-extension-with-a-vspackage.md)」を参照してください。

### <a name="to-create-the-tools-options-property-grid"></a>[ツール オプション] プロパティ グリッドを作成するには

1. コード エディターで*MyTools オプションパッケージ*ファイルを開きます。

2. 次の using ステートメントを追加します。

   ```csharp
   using System.ComponentModel;
   ```

3. クラスを`OptionPageGrid`宣言し、 から<xref:Microsoft.VisualStudio.Shell.DialogPage>派生します。

   ```csharp
   public class OptionPageGrid : DialogPage
   {  }
   ```

4. クラスに<xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute>a`VSPackage`を適用して、オプション カテゴリとオプション ページ名をクラスに割り当てます。 結果は次のようになります。

    ```csharp
    [PackageRegistration(UseManagedResourcesOnly = true)]
    [InstalledProductRegistration("#110", "#112", "1.0", IconResourceID = 400)]
    [ProvideMenuResource("Menus.ctmenu", 1)]
    [Guid(GuidList.guidMyToolsOptionsPkgString)]
    [ProvideOptionPage(typeof(OptionPageGrid),
        "My Category", "My Grid Page", 0, 0, true)]
    public sealed class MyToolsOptionsPackage : Package
    ```

5. クラスに`OptionInteger`プロパティを追加`OptionPageGrid`します。

    - プロパティに<xref:System.ComponentModel.CategoryAttribute?displayProperty=fullName>プロパティ グリッド カテゴリを割り当てるには、 を適用します。

    - プロパティに<xref:System.ComponentModel.DisplayNameAttribute?displayProperty=fullName>名前を割り当てるには、 を適用します。

    - プロパティに<xref:System.ComponentModel.DescriptionAttribute?displayProperty=fullName>説明を割り当てるには、 を適用します。

    ```csharp
    public class OptionPageGrid : DialogPage
    {
        private int optionInt = 256;

        [Category("My Category")]
        [DisplayName("My Integer Option")]
        [Description("My integer option")]
        public int OptionInteger
        {
            get { return optionInt; }
            set { optionInt = value; }
        }
    }
    ```

    > [!NOTE]
    > 既定の<xref:Microsoft.VisualStudio.Shell.DialogPage>実装では、適切なコンバーターを持つプロパティ、または適切なコンバーターを持つプロパティに展開できる構造体または配列をサポートするプロパティがサポートされます。 コンバータの一覧については、名前空間を<xref:System.ComponentModel>参照してください。

6. プロジェクトをビルドし、デバッグを開始します。

7. Visual Studio の実験用インスタンスで、[**ツール**] メニューの [**オプション**] をクリックします。

     左側のウィンドウに [マイ**カテゴリ]** が表示されます。 (オプションのカテゴリはアルファベット順にリストされているので、リストの半分ほど下に表示されます)。**[マイ カテゴリ] を**開き、[**マイ グリッド ページ**] をクリックします。 右側のペインにオプション グリッドが表示されます。 プロパティ カテゴリは **[マイ オプション]** で、プロパティ名は **[My Integer Option]** です。 プロパティの説明の **[自分の整数] オプション**がウィンドウの下部に表示されます。 初期値の 256 から別のものに値を変更します。 **[OK] を**クリックし、[**マイ グリッド ページ]** を再度開きます。 新しい値が保持されていることがわかります。

     オプション ページは、Visual Studio の検索ボックスからも使用できます。 IDE の上部近くの検索ボックスに **「マイ カテゴリ**」と入力すると、結果に **[マイ カテゴリ - >マイ グリッド ページ**が表示されます。

## <a name="create-a-tools-options-custom-page"></a>ツール オプションのカスタム ページを作成する

 このセクションでは、カスタム UI を使用して [ツール オプション] ページを作成します。 このページを使用して、プロパティの値を表示および変更します。

1. コード エディターで*MyTools オプションパッケージ*ファイルを開きます。

2. 次の using ステートメントを追加します。

    ```csharp
    using System.Windows.Forms;
    ```

3. クラスの`OptionPageCustom`直前にクラスを追加`OptionPageGrid`します。 から新しいクラスを`DialogPage`派生します。

    ```csharp
    public class OptionPageCustom : DialogPage
    {
        private string optionValue = "alpha";

        public string OptionString
        {
            get { return optionValue; }
            set { optionValue = value; }
        }
    }
    ```

4. GUID 属性を追加します。 プロパティを追加します。

    ```csharp
    [Guid("00000000-0000-0000-0000-000000000000")]
    public class OptionPageCustom : DialogPage
    {
        private string optionValue = "alpha";

        public string OptionString
        {
            get { return optionValue; }
            set { optionValue = value; }
        }
    }
    ```

5. VSPackage<xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute>クラスに 2 番目を適用します。 この属性は、クラスにオプションカテゴリとオプションページ名を割り当てます。

    ```csharp
    [PackageRegistration(UseManagedResourcesOnly = true)]
    [InstalledProductRegistration("#110", "#112", "1.0", IconResourceID = 400)]
    [ProvideMenuResource("Menus.ctmenu", 1)]
    [Guid(GuidList.guidMyToolsOptionsPkgString)]
    [ProvideOptionPage(typeof(OptionPageGrid),
        "My Category", "My Grid Page", 0, 0, true)]
    [ProvideOptionPage(typeof(OptionPageCustom),
        "My Category", "My Custom Page", 0, 0, true)]
    public sealed class MyToolsOptionsPackage : Package
    ```

6. プロジェクトに MyUserControl という名前の新しい**ユーザー コントロール**を追加します。

7. ユーザー コントロールに**TextBox**コントロールを追加します。

     [**プロパティ]** ウィンドウのツール バーで、[**イベント**] ボタンをクリックし **、Leave**イベントをダブルクリックします。 新しいイベント ハンドラーが*MyUserControl.cs*コードに表示されます。

8. パブリック`OptionsPage`フィールドとメソッドを`Initialize`コントロール クラスに追加し、オプション値をテキスト ボックスの内容に設定するようにイベント ハンドラーを更新します。

    ```csharp
    public partial class MyUserControl : UserControl
    {
        public MyUserControl()
        {
            InitializeComponent();
        }

        internal OptionPageCustom optionsPage;

        public void Initialize()
        {
            textBox1.Text = optionsPage.OptionString;
        }

        private void textBox1_Leave(object sender, EventArgs e)
        {
            optionsPage.OptionString = textBox1.Text;
        }
    }
    ```

     フィールド`optionsPage`には、親`OptionPageCustom`インスタンスへの参照が格納されます。 メソッド`Initialize`は、`OptionString`テキスト**ボックス**に表示されます。 イベント ハンドラーは、フォーカスが TextBox から離`OptionString`れるとき **、TextBox**の現在の値を書き込**みます**。

9. パッケージ コード ファイルで、`OptionPageCustom.Window``OptionPageCustom`プロパティのオーバーライドをクラスに追加して、`MyUserControl`のインスタンスを作成、初期化、および返します。 クラスは次のようになります。

    ```csharp
    [Guid("00000000-0000-0000-0000-000000000000")]
    public class OptionPageCustom : DialogPage
    {
        private string optionValue = "alpha";

        public string OptionString
        {
            get { return optionValue; }
            set { optionValue = value; }
        }

        protected override IWin32Window Window
        {
            get
            {
                MyUserControl page = new MyUserControl();
                page.optionsPage = this;
                page.Initialize();
                return page;
            }
        }
    }
    ```

10. プロジェクトをビルドして実行します。

11. 実験用インスタンスで、[**ツール** > **オプション**] をクリックします。

12. **[マイ カテゴリ]** を見つけて、[**マイ カスタム ページ]** をクリックします。

13. の値を変更**します**。 **[OK] を**クリックし、[**マイ カスタム ページ] を**再度開きます。 新しい値が永続化されていることがわかります。

## <a name="access-options"></a>アクセスオプション

 このセクションでは、関連付けられているツール オプション ページをホストする VSPackage からオプションの値を取得します。 同じ手法を使用して、任意のパブリック プロパティの値を取得できます。

1. パッケージ コード ファイルで、**オプション整数**というパブリック プロパティを**MyToolsOptions パッケージ クラス**に追加します。

    ```csharp
    public int OptionInteger
    {
        get
        {
            OptionPageGrid page = (OptionPageGrid)GetDialogPage(typeof(OptionPageGrid));
            return page.OptionInteger;
        }
    }

    ```

     このコードは<xref:Microsoft.VisualStudio.Shell.Package.GetDialogPage%2A>、インスタンスを作成または`OptionPageGrid`取得するために呼び出します。 `OptionPageGrid`その<xref:Microsoft.VisualStudio.Shell.DialogPage.LoadSettingsFromStorage%2A>オプションを読み込むための呼び出しは、パブリック プロパティです。

2. 次に **、MyToolsOptionsCommand**という名前のカスタム コマンド項目テンプレートを追加して、値を表示します。 [**新しい項目の追加]** ダイアログで **、[Visual C#** > **の機能拡張**] に移動し、[**カスタム コマンド**] を選択します。 ウィンドウの下部にある [**名前]** フィールドで、コマンド ファイル名を*MyToolsOptionsCommand.cs*に変更します。

3. *MyToolsOptionsCommand*ファイルで、コマンドの`ShowMessageBox`メソッドの本体を次のように置き換えます。

    ```csharp
    private void ShowMessageBox(object sender, EventArgs e)
    {
        MyToolsOptionsPackage myToolsOptionsPackage = this.package as MyToolsOptionsPackage;
        System.Windows.Forms.MessageBox.Show(string.Format(CultureInfo.CurrentCulture, "OptionInteger: {0}", myToolsOptionsPackage.OptionInteger));
    }

    ```

4. プロジェクトをビルドし、デバッグを開始します。

5. 実験用のインスタンスで、[**ツール**] メニューの [**ツール] オプション コマンドの呼び出し**をクリックします。

     メッセージ ボックスに、 の現在`OptionInteger`の値が表示されます。

## <a name="see-also"></a>関連項目

- [オプションとオプションページ](../extensibility/internals/options-and-options-pages.md)
