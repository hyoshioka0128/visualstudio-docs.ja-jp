---
title: オプションページを作成する |Microsoft Docs
description: プロパティグリッドを使用してプロパティを確認および設定する簡単なツール/オプションページを作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 3/16/2019
ms.topic: how-to
helpviewer_keywords:
- Tools Options pages [Visual Studio SDK], creating
ms.assetid: 9f4e210c-4b47-4daa-91fa-1c301c4587f9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: eb94554b4ac1af30d8187a8ab75aa83f65dccc72
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105055805"
---
# <a name="create-an-options-page"></a>オプションページを作成する

このチュートリアルでは、プロパティグリッドを使用してプロパティを確認および設定する簡単なツール/オプションページを作成します。

 これらのプロパティをに保存し、設定ファイルから復元するには、次の手順に従い、「 [設定のカテゴリを作成](../extensibility/creating-a-settings-category.md)する」を参照してください。

 MPF には、ツールオプションページ、クラス、およびクラスの作成に役立つ2つのクラスが用意されて <xref:Microsoft.VisualStudio.Shell.Package> <xref:Microsoft.VisualStudio.Shell.DialogPage> います。 クラスをサブクラス化することで、これらのページのコンテナーを提供する VSPackage を作成し `Package` ます。 クラスから派生することによって、各ツールオプションページを作成し `DialogPage` ます。

## <a name="prerequisites"></a>前提条件

 Visual Studio 2015 以降では、ダウンロードセンターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップでオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「 [Visual STUDIO SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-a-tools-options-grid-page"></a>[ツールオプション] グリッドページを作成する

 このセクションでは、簡単なツールオプションのプロパティグリッドを作成します。 このグリッドを使用して、プロパティの値を表示および変更します。

### <a name="to-create-the-vsix-project-and-add-a-vspackage"></a>VSIX プロジェクトを作成して VSPackage を追加するには

1. すべての Visual Studio 拡張機能は、拡張機能アセットを含む VSIX デプロイプロジェクトから開始されます。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]という名前の VSIX プロジェクトを作成 `MyToolsOptionsExtension` します。 VSIX プロジェクトテンプレートは、"vsix" を検索することで、[ **新しいプロジェクト** ] ダイアログで見つけることができます。

2. という名前の Visual Studio パッケージ項目テンプレートを追加して、VSPackage を追加し `MyToolsOptionsPackage` ます。 **ソリューションエクスプローラー** で、プロジェクトノードを右クリックし、[新しい項目の **追加**] を選択し  >  ます。 [**新しい項目の追加] ダイアログ** で、[ **visual C# 項目** の  >  **機能拡張**] にアクセスし、[ **visual Studio パッケージ**] を選択します。 ダイアログの下部にある [ **名前** ] フィールドで、ファイル名をに変更 `MyToolsOptionsPackage.cs` します。 VSPackage を作成する方法の詳細については、「 [VSPackage を使用した拡張機能の作成](../extensibility/creating-an-extension-with-a-vspackage.md)」を参照してください。

### <a name="to-create-the-tools-options-property-grid"></a>ツールオプションのプロパティグリッドを作成するには

1. コードエディターで *MyToolsOptionsPackage* ファイルを開きます。

2. 次の using ステートメントを追加します。

   ```csharp
   using System.ComponentModel;
   ```

3. クラスを宣言 `OptionPageGrid` し、から派生させ <xref:Microsoft.VisualStudio.Shell.DialogPage> ます。

   ```csharp
   public class OptionPageGrid : DialogPage
   {  }
   ```

4. クラスにを適用して、 <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> `VSPackage` オプションのカテゴリとオプションページ名をオプションページグリッドに割り当てます。 結果は次のようになります。

    ```csharp
    [PackageRegistration(UseManagedResourcesOnly = true)]
    [InstalledProductRegistration("#110", "#112", "1.0", IconResourceID = 400)]
    [ProvideMenuResource("Menus.ctmenu", 1)]
    [Guid(GuidList.guidMyToolsOptionsPkgString)]
    [ProvideOptionPage(typeof(OptionPageGrid),
        "My Category", "My Grid Page", 0, 0, true)]
    public sealed class MyToolsOptionsPackage : Package
    ```

5. `OptionInteger`クラスにプロパティを追加 `OptionPageGrid` します。

    - プロパティ <xref:System.ComponentModel.CategoryAttribute?displayProperty=fullName> グリッドカテゴリのプロパティに割り当てるを適用します。

    - を適用し <xref:System.ComponentModel.DisplayNameAttribute?displayProperty=fullName> て、プロパティに名前を割り当てます。

    - を適用し <xref:System.ComponentModel.DescriptionAttribute?displayProperty=fullName> て、プロパティに説明を割り当てます。

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
    > の既定の実装で <xref:Microsoft.VisualStudio.Shell.DialogPage> は、適切なコンバーターを持つプロパティ、または適切なコンバーターを持つプロパティに拡張できる構造体または配列であるプロパティがサポートされています。 コンバーターの一覧については、「名前空間」を参照してください <xref:System.ComponentModel> 。

6. プロジェクトをビルドし、デバッグを開始します。

7. Visual Studio の実験用インスタンスで、[ **ツール** ] メニューの [ **オプション**] をクリックします。

     左側のウィンドウに **[マイカテゴリ]** が表示されます。 (オプションのカテゴリはアルファベット順に一覧表示されているため、一覧の半分になります)。[ **マイカテゴリ** ] を開き、[ **マイグリッドページ**] をクリックします。 右ペインに [オプション] グリッドが表示されます。 プロパティカテゴリは **My Options** で、プロパティ名は " **My Integer" オプション** です。 ペインの下部に [プロパティの説明] の **[整数] オプション** が表示されます。 値を256の初期値から別の値に変更します。 [ **OK**] をクリックし、[ **グリッドページ**] を再度開きます。 新しい値が保持されていることがわかります。

     [オプション] ページは、Visual Studio の検索ボックスからも使用できます。 IDE の上部付近にある検索ボックスに「 **My category** 」と入力すると、[ **カテゴリ-> マイグリッド] ページ** が結果に表示されます。

## <a name="create-a-tools-options-custom-page"></a>ツールオプションのカスタムページを作成する

 このセクションでは、カスタム UI を使用して [ツール] オプションページを作成します。 このページを使用すると、プロパティの値を表示したり、変更したりできます。

1. コードエディターで *MyToolsOptionsPackage* ファイルを開きます。

2. 次の using ステートメントを追加します。

    ```csharp
    using System.Windows.Forms;
    ```

3. クラス `OptionPageCustom` の直前に、クラスを追加し `OptionPageGrid` ます。 から新しいクラスを派生させ `DialogPage` ます。

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

4. GUID 属性を追加します。 OptionString プロパティを追加します。

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

5. VSPackage クラスに2つ目のを適用 <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> します。 この属性は、クラスにオプションのカテゴリとオプションページの名前を割り当てます。

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

6. MyUserControl という名前の新しい **ユーザーコントロール** をプロジェクトに追加します。

7. **TextBox** コントロールをユーザーコントロールに追加します。

     [ **プロパティ** ] ウィンドウのツールバーで、[ **イベント** ] ボタンをクリックし、[ **Leave** ] イベントをダブルクリックします。 新しいイベントハンドラーが *MyUserControl* コードに表示されます。

8. パブリックフィールドと `OptionsPage` `Initialize` メソッドをコントロールクラスに追加し、イベントハンドラーを更新して、オプションの値をテキストボックスの内容に設定します。

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

     フィールドは、 `optionsPage` 親インスタンスへの参照を保持し `OptionPageCustom` ます。 `Initialize`メソッドが `OptionString` **テキストボックス** に表示されます。 イベントハンドラーは、フォーカスが Textbox の外に出たときに、**テキストボックス** の現在の値をに書き込み `OptionString` ます。 

9. パッケージコードファイルで、プロパティのオーバーライドをクラスに追加して、 `OptionPageCustom.Window` `OptionPageCustom` のインスタンスを作成、初期化、および返すようにし `MyUserControl` ます。 クラスは次のようになります。

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

11. 実験用インスタンスで、[**ツール**] [オプション] の順にクリックし  >  ます。

12. [ **マイカテゴリ]** 、[ **マイカスタム] ページ** の順に検索します。

13. **Optionstring** の値を変更します。 [ **OK**] をクリックし、 **カスタムページ** を再度開きます。 新しい値が保持されていることを確認できます。

## <a name="access-options"></a>アクセスオプション

 このセクションでは、関連付けられている [ツールオプション] ページをホストする VSPackage からオプションの値を取得します。 同じ手法を使用して、パブリックプロパティの値を取得することもできます。

1. パッケージコードファイルで、 **MyToolsOptionsPackage** クラスに **optioninteger** というパブリックプロパティを追加します。

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

     このコード <xref:Microsoft.VisualStudio.Shell.Package.GetDialogPage%2A> は、を呼び出してインスタンスを作成または取得 `OptionPageGrid` します。 `OptionPageGrid` を呼び出して <xref:Microsoft.VisualStudio.Shell.DialogPage.LoadSettingsFromStorage%2A> 、パブリックプロパティであるオプションを読み込みます。

2. ここで、 **MyToolsOptionsCommand** という名前のカスタムコマンド項目テンプレートを追加して、値を表示します。 [**新しい項目の追加**] ダイアログで、[ **Visual C#** の  >  **機能拡張**] にアクセスし、[**カスタムコマンド**] を選択します。 ウィンドウの下部にある [ **名前** ] フィールドで、[コマンドファイル名] を *MyToolsOptionsCommand* に変更します。

3. *MyToolsOptionsCommand* ファイルで、コマンドのメソッドの本体を `ShowMessageBox` 次のように置き換えます。

    ```csharp
    private void ShowMessageBox(object sender, EventArgs e)
    {
        MyToolsOptionsPackage myToolsOptionsPackage = this.package as MyToolsOptionsPackage;
        System.Windows.Forms.MessageBox.Show(string.Format(CultureInfo.CurrentCulture, "OptionInteger: {0}", myToolsOptionsPackage.OptionInteger));
    }

    ```

4. プロジェクトをビルドし、デバッグを開始します。

5. 実験用インスタンスで、[ **ツール** ] メニューの [ **MyToolsOptionsCommand の呼び出し**] をクリックします。

     メッセージボックスに、の現在の値が表示され `OptionInteger` ます。

## <a name="see-also"></a>こちらもご覧ください

- [[オプション] ページと [オプション] ページ](../extensibility/internals/options-and-options-pages.md)
