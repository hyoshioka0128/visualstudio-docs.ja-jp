---
title: オプションページを作成する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Tools Options pages [Visual Studio SDK], creating
ms.assetid: 9f4e210c-4b47-4daa-91fa-1c301c4587f9
caps.latest.revision: 63
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 7b5897f6c4463cc5a3c7928a722ed5a0a09e42b3
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841992"
---
# <a name="creating-an-options-page"></a>オプション ページの作成
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このチュートリアルでは、プロパティグリッドを使用してプロパティを確認および設定する簡単なツール/オプションページを作成します。  
  
 これらのプロパティをに保存し、設定ファイルから復元するには、次の手順に従い、 [設定カテゴリの作成](../extensibility/creating-a-settings-category.md)に関する説明を参照してください。  
  
 MPF には、ツールオプションページ、クラス、およびクラスの作成に役立つ2つのクラスが用意されて <xref:Microsoft.VisualStudio.Shell.Package> <xref:Microsoft.VisualStudio.Shell.DialogPage> います。 パッケージクラスをサブクラス化することで、これらのページのコンテナーを提供する VSPackage を作成します。 各ツールオプションページは、表示ページクラスから派生することによって作成します。  
  
## <a name="prerequisites"></a>前提条件  
 Visual Studio 2015 以降では、ダウンロードセンターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップでオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「 [Visual STUDIO SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。  
  
## <a name="creating-a-tools-options-grid-page"></a>[ツールオプション] グリッドページの作成  
 このセクションでは、簡単なツールオプションのプロパティグリッドを作成します。 このグリッドを使用して、プロパティの値を表示および変更します。  
  
#### <a name="to-create-the-vsix-project-and-add-a-vspackage"></a>VSIX プロジェクトを作成して VSPackage を追加するには  
  
1. すべての Visual Studio 拡張機能は、拡張機能アセットを含む VSIX デプロイプロジェクトから開始されます。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]という名前の VSIX プロジェクトを作成 `MyToolsOptionsExtension` します。 VSIX プロジェクトテンプレートは、[ **新しいプロジェクト** ] ダイアログボックスの [ **Visual C#]/[拡張機能**] で見つけることができます。  
  
2. という名前の Visual Studio パッケージ項目テンプレートを追加して、VSPackage を追加し `MyToolsOptionsPackage` ます。 **ソリューションエクスプローラー**で、プロジェクトノードを右クリックし、[追加]、[**新しい項目**] の順に選択します。 [ **新しい項目の追加] ダイアログ**で、[ **visual C# 項目/機能拡張** ] にアクセスし、[ **visual Studio パッケージ**] を選択します。 ダイアログの下部にある [ **名前** ] フィールドで、ファイル名をに変更 `MyToolsOptionsPackage.cs` します。 VSPackage を作成する方法の詳細については、「 [VSPackage を使用した拡張機能の作成](../extensibility/creating-an-extension-with-a-vspackage.md)」を参照してください。  
  
#### <a name="to-create-the-tools-options-property-grid"></a>ツールオプションのプロパティグリッドを作成するには  
  
1. コードエディターで MyToolsOptionsPackage ファイルを開きます。  
  
2. 次の using ステートメントを追加します。  
  
    ```csharp  
    using System.ComponentModel;  
    ```  
  
3. OptionPageGrid クラスを宣言し、から派生させ <xref:Microsoft.VisualStudio.Shell.DialogPage> ます。  
  
    ```csharp  
    public class OptionPageGrid : DialogPage  
    {  }  
    ```  
  
4. を VSPackage クラスに適用して、 <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> クラスにオプションのカテゴリとオプションページの名前を割り当てます。 結果は次のようになります。  
  
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
  
     左側のウィンドウに **[マイカテゴリ]** が表示されます。 (オプションのカテゴリはアルファベット順に一覧表示されているため、一覧の半分になります)。[ **マイカテゴリ** ] を開き、[ **マイグリッドページ**] をクリックします。右ペインに [オプション] グリッドが表示されます。 プロパティカテゴリは **My Options**で、プロパティ名は " **My Integer" オプション**です。 ペインの下部に [プロパティの説明] の **[整数] オプション**が表示されます。 値を256の初期値から別の値に変更します。 [ **OK**] をクリックし、[ **グリッドページ**] を再度開きます。 新しい値が保持されていることがわかります。  
  
     オプションページは、Visual Studio のクイック起動からも使用できます。 IDE の右上隅にある [クイック起動] ウィンドウに「 **My category** 」と入力すると、ドロップダウンリストに [my **Category – > my Grid Page** ] と表示されます。  
  
## <a name="creating-a-tools-options-custom-page"></a>ツールオプションのカスタムページの作成  
 このセクションでは、カスタム UI を使用して [ツール] オプションページを作成します。 このページを使用すると、プロパティの値を表示したり、変更したりできます。  
  
1. コードエディターで MyToolsOptionsPackage ファイルを開きます。  
  
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
  
7. **TextBox**コントロールをユーザーコントロールに追加します。  
  
     [ **プロパティ** ] ウィンドウのツールバーで、[ **イベント** ] ボタンをクリックし、[ **Leave** ] イベントをダブルクリックします。 新しいイベントハンドラーが MyUserControl.cs コードに表示されます。  
  
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
  
     フィールドは、 `optionsPage` 親インスタンスへの参照を保持し `OptionPageCustom` ます。 `Initialize`メソッドが `OptionString` **テキストボックス**に表示されます。 イベントハンドラーは、フォーカスが Textbox の外に出たときに、**テキストボックス**の現在の値をに書き込み `OptionString` ます。 **TextBox**  
  
9. パッケージコードファイルで、プロパティのオーバーライドを OptionPageCustom クラスに追加して、 `OptionPageCustom.Window` のインスタンスを作成、初期化、および返すようにし `MyUserControl` ます。 クラスは次のようになります。  
  
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
  
11. 実験用インスタンスで、[ **ツール**]、[オプション] の順にクリックします。  
  
12. [ **マイカテゴリ]** 、[ **マイカスタム] ページ**の順に検索します。  
  
13. **Optionstring**の値を変更します。 [ **OK**] をクリックし、 **カスタムページ**を再度開きます。 新しい値が保持されていることを確認できます。  
  
## <a name="accessing-options"></a>オプションへのアクセス  
 このセクションでは、関連付けられている [ツールオプション] ページをホストする VSPackage からオプションの値を取得します。 同じ手法を使用して、パブリックプロパティの値を取得することもできます。  
  
1. パッケージコードファイルで、 **MyToolsOptionsPackage**クラスに**optioninteger**というパブリックプロパティを追加します。  
  
    ```  
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
  
2. ここで、 **MyToolsOptionsCommand** という名前のカスタムコマンド項目テンプレートを追加して、値を表示します。 [ **新しい項目の追加** ] ダイアログで、[ **Visual C#]/[拡張機能** ] にアクセスし、[ **カスタムコマンド**] を選択します。 ウィンドウの下部にある [ **名前** ] フィールドで、[コマンドファイル名] を **MyToolsOptionsCommand.cs**に変更します。  
  
3. MyToolsOptionsCommand ファイルで、コマンドのメソッドの本体を `ShowMessageBox` 次のように置き換えます。  
  
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
  
## <a name="see-also"></a>参照  
 [オプションとオプション ページ](../extensibility/internals/options-and-options-pages.md)
