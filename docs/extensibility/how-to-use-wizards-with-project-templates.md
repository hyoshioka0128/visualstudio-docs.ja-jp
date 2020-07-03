---
title: '方法 : プロジェクト テンプレートを組み合わせたウィザードを使用する'
ms.date: 3/16/2019
ms.topic: how-to
helpviewer_keywords:
- project templates [Visual Studio], wizards
- Visual Studio templates, wizards
- wizards [Visual Studio], project templates
- templates [Visual Studio], wizards
- IWizard interface
ms.assetid: 47ee26cf-67b7-4ff1-8a9d-ab11a725405c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: e9d36ae9b3a4a4fbbb3c54cc3f3320e9878b6745
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85905514"
---
# <a name="how-to-use-wizards-with-project-templates"></a>方法: プロジェクトテンプレートでウィザードを使用する

Visual Studio には、<xref:Microsoft.VisualStudio.TemplateWizard.IWizard> インターフェイスが用意されています。このインターフェイスを実装すると、ユーザーがテンプレートからプロジェクトを作成する際にカスタム コードを実行できるようになります。

プロジェクトテンプレートのカスタマイズを使用すると、ユーザー入力を収集してテンプレートをカスタマイズしたり、テンプレートにファイルを追加したり、プロジェクトに対して許可されているその他のアクションを追加したりするためのカスタム UI を表示できます。

<xref:Microsoft.VisualStudio.TemplateWizard.IWizard>インターフェイスメソッドは、プロジェクトの作成中にさまざまなタイミングで呼び出され、ユーザーが [**新しいプロジェクト**] ダイアログボックスで **[OK]** をクリックするとすぐに開始されます。 インターフェイスの各メソッドには、そのメソッドが呼び出される時点を表す名前が付けられます。 たとえば、Visual Studio は、 <xref:Microsoft.VisualStudio.TemplateWizard.IWizard.RunStarted%2A> プロジェクトの作成を開始するとすぐにを呼び出し、ユーザー入力を収集するためのカスタムコードを作成するための適切な場所にします。

## <a name="create-a-project-template-project-with-a-vsix-project"></a>VSIX プロジェクトでプロジェクトテンプレートプロジェクトを作成する

Visual Studio SDK の一部であるプロジェクトテンプレートプロジェクトを使用して、カスタムテンプレートの作成を開始します。 この手順では、C# プロジェクトテンプレートプロジェクトを使用しますが、Visual Basic プロジェクトテンプレートプロジェクトもあります。 次に、プロジェクトテンプレートプロジェクトを含むソリューションに VSIX プロジェクトを追加します。

1. C# プロジェクトテンプレートプロジェクトを作成します (Visual Studio で、[**ファイル**] [新しいプロジェクト] を選択し、[  >  **New**  >  **Project**プロジェクトテンプレート] を検索します)。 **Myprojecttemplate**という名前を指定します。

   > [!NOTE]
   > Visual Studio SDK をインストールするように求められる場合があります。 詳細については、「 [Visual STUDIO SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

2. プロジェクトテンプレートプロジェクトと同じソリューションに新しい VSIX プロジェクトを追加します (**ソリューションエクスプローラー**で、ソリューションノードを選択して右クリックし、[新しいプロジェクトの**追加**] を選択して、  >  **New Project** "VSIX" を検索します)。 **Myprojectwizard という名前を指定します。**

3. VSIX プロジェクトをスタートアッププロジェクトとして設定します。 **ソリューションエクスプローラー**で、[VSIX プロジェクト] ノードを選択し、右クリックし**て [スタートアッププロジェクトに設定**] を選択します。

4. テンプレートプロジェクトを VSIX プロジェクトのアセットとして追加します。 **ソリューションエクスプローラー**の [VSIX プロジェクト] ノードで、 *source.extension.vsixmanifest*ファイルを見つけます。 それをダブルクリックして、マニフェストエディターで開きます。

5. マニフェストエディターで、ウィンドウの左側にある [**アセット**] タブを選択します。

6. [**アセット**] タブで、[**新規**] を選択します。 [**新しい資産の追加**] ウィンドウの [種類] フィールドで、[ **VisualStudio**] を選択します。 [**ソース**] フィールドで、**現在のソリューション内のプロジェクト**を選択します。 [**プロジェクト**] フィールドで、[ **myprojecttemplate**] を選択します。 次に、 **[OK]** をクリックします

7. ソリューションをビルドし、デバッグを開始します。 Visual Studio の 2 番目のインスタンスが表示されます。 (これには数分かかることがあります)。

8. Visual Studio の2番目のインスタンスで、新しいテンプレートを使用して新しいプロジェクトを作成します ([**ファイル**] [  >  **新しい**  >  **プロジェクト**]、"myproject" を検索します)。 新しいプロジェクトが、 **Class1**という名前のクラスと共に表示されます。 これで、カスタムプロジェクトテンプレートが作成されました。 今すぐデバッグを停止します。

## <a name="create-a-custom-template-wizard"></a>カスタムテンプレートの作成ウィザード

この手順では、プロジェクトを作成する前に Windows フォームを開くカスタムウィザードを作成する方法について説明します。 フォームを使用すると、プロジェクトの作成時にソースコードに追加されるカスタムパラメーター値を追加できます。

1. VSIX プロジェクトを設定して、アセンブリを作成できるようにします。

2. **ソリューションエクスプローラー**で、[VSIX プロジェクト] ノードを選択します。 **ソリューションエクスプローラー**の下に、[**プロパティ**] ウィンドウが表示されます。 **表示**されない場合は、[  >  **プロパティウィンドウ**の表示] を選択するか、 **F4**キーを押します。 [**プロパティ**] ウィンドウで、次のフィールドを選択し `true` ます。

   - **VSIX コンテナーにアセンブリを含める**

   - **VSIX コンテナーにデバッグシンボルを含める**

   - **ローカル VSIX 配置にデバッグシンボルを含める**

3. VSIX プロジェクトにアセットとしてアセンブリを追加します。 *Source.extension.vsixmanifest*ファイルを開き、[**アセット**] タブを選択します。[**新しい資産の追加**] ウィンドウの [**種類**] で [ **VisualStudio**] を選択し、[**ソース**] で [現在の**ソリューション] でプロジェクト**を選択し、[**プロジェクト**] で [ **myprojectwizard**] を選択します。

4. 次の参照を VSIX プロジェクトに追加します。 (**ソリューションエクスプローラー**で、[VSIX プロジェクト] ノードの下にある [**参照**] を選択し、右クリックして [**参照の追加**] を選択します)。[**参照の追加**] ダイアログの [**フレームワーク**] タブで、[ **Windows フォーム**アセンブリを見つけて選択します。 また、[**システム**] アセンブリと [**システム**] を選択します。 次に、[**拡張機能**] タブを選択します。 **EnvDTE**アセンブリを見つけて選択します。 また、 **VisualStudio インターフェイス**アセンブリを見つけて選択します。 **[OK]** をクリックします。

5. ウィザード実装のクラスを VSIX プロジェクトに追加します。 (**ソリューションエクスプローラー**で、[VSIX プロジェクト] ノードを右クリックし、[**追加**]、[**新しい項目**]、[**クラス**] の順に選択します)。クラスに**WizardImplementation**という名前を指定します。

6. *WizardImplementationClass.cs*ファイルのコードを次のコードに置き換えます。

   ```csharp
   using System;
   using System.Collections.Generic;
   using Microsoft.VisualStudio.TemplateWizard;
   using System.Windows.Forms;
   using EnvDTE;

   namespace MyProjectWizard
   {
       public class WizardImplementation:IWizard
       {
           private UserInputForm inputForm;
           private string customMessage;

           // This method is called before opening any item that
           // has the OpenInEditor attribute.
           public void BeforeOpeningFile(ProjectItem projectItem)
           {
           }

           public void ProjectFinishedGenerating(Project project)
           {
           }

           // This method is only called for item templates,
           // not for project templates.
           public void ProjectItemFinishedGenerating(ProjectItem
               projectItem)
           {
           }

           // This method is called after the project is created.
           public void RunFinished()
           {
           }

           public void RunStarted(object automationObject,
               Dictionary<string, string> replacementsDictionary,
               WizardRunKind runKind, object[] customParams)
           {
               try
               {
                   // Display a form to the user. The form collects
                   // input for the custom message.
                   inputForm = new UserInputForm();
                   inputForm.ShowDialog();

                   customMessage = UserInputForm.CustomMessage;

                   // Add custom parameters.
                   replacementsDictionary.Add("$custommessage$",
                       customMessage);
               }
               catch (Exception ex)
               {
                   MessageBox.Show(ex.ToString());
               }
           }

           // This method is only called for item templates,
           // not for project templates.
           public bool ShouldAddProjectItem(string filePath)
           {
               return true;
           }
       }
   }
   ```

    このコードで参照される**Userinputform**は、後で実装されます。

    `WizardImplementation` クラスには、<xref:Microsoft.VisualStudio.TemplateWizard.IWizard> のすべてのメンバーに対するメソッドの実装が含まれています。 この例では、<xref:Microsoft.VisualStudio.TemplateWizard.IWizard.RunStarted%2A> メソッドだけがタスクを実行します。 他のすべてのメソッドは、何もしないか、`true` を返します。

    <xref:Microsoft.VisualStudio.TemplateWizard.IWizard.RunStarted%2A> メソッドは、次の 4 つのパラメーターを受け取ります。

   - <xref:System.Object> パラメーター。プロジェクトをカスタマイズできるように、ルートの <xref:EnvDTE._DTE> オブジェクトにキャストできます。

   - <xref:System.Collections.Generic.Dictionary%602> パラメーター。テンプレートで定義済みのすべてのパラメーターのコレクションが含まれます。 テンプレートパラメーターの詳細については、「[テンプレートパラメーター](../ide/template-parameters.md)」を参照してください。

   - <xref:Microsoft.VisualStudio.TemplateWizard.WizardRunKind> パラメーター。使用されているテンプレートの種類に関する情報が含まれます。

   - <xref:System.Object>Visual Studio によってウィザードに渡されるパラメーターのセットを格納している配列。

     この例では、ユーザー入力フォームから <xref:System.Collections.Generic.Dictionary%602> パラメーターにパラメーター値を追加します。 プロジェクト内の `$custommessage$` パラメーターのすべてのインスタンスは、ユーザーが入力したテキストと置き換えられます。

7. 次に、 **Userinputform**を作成します。 *WizardImplementation.cs*ファイルで、クラスの末尾の後に次のコードを追加し `WizardImplementation` ます。

   ```csharp
   public partial class UserInputForm : Form
       {
           private static string customMessage;
           private TextBox textBox1;
           private Button button1;

           public UserInputForm()
           {
               this.Size = new System.Drawing.Size(155, 265);

               button1 = new Button();
               button1.Location = new System.Drawing.Point(90, 25);
               button1.Size = new System.Drawing.Size(50, 25);
               button1.Click += button1_Click;
               this.Controls.Add(button1);

               textBox1 = new TextBox();
               textBox1.Location = new System.Drawing.Point(10, 25);
               textBox1.Size = new System.Drawing.Size(70, 20);
               this.Controls.Add(textBox1);
           }
           public static string CustomMessage
           {
               get
               {
                   return customMessage;
               }
               set
               {
                   customMessage = value;
               }
           }
           private void button1_Click(object sender, EventArgs e)
           {
               customMessage = textBox1.Text;
               this.Close();
           }
       }
   ```

    ユーザー入力フォームには、カスタム パラメーターを入力するための簡単なフォームが用意されています。 このフォームには、`textBox1` という名前のテキスト ボックスおよび `button1` という名前のボタンがあります。 このボタンをクリックすると、テキスト ボックスのテキストが `customMessage` パラメーターに格納されます。

## <a name="connect-the-wizard-to-the-custom-template"></a>ウィザードをカスタムテンプレートに接続する

カスタムプロジェクトテンプレートでカスタムウィザードを使用するには、ウィザードのアセンブリに署名し、いくつかの行をカスタムプロジェクトテンプレートに追加して、新しいプロジェクトが作成されたときにウィザードの実装の場所を把握できるようにする必要があります。

1. アセンブリに署名します。 **ソリューションエクスプローラー**で、VSIX プロジェクトを選択し、右クリックして、[**プロジェクトのプロパティ**] を選択します。

2. プロジェクトの**プロパティ**ウィンドウで、[**署名**] タブを選択します。 [**署名**] タブで、[**アセンブリの署名**] チェックボックスをオンにします。 [**厳密な名前のキーファイルを選択**してください] フィールドで、を選択し **\<New>** ます。 [**厳密な名前キーの作成**] ウィンドウの [**キーファイル名**] フィールドに、「**キー .snk**」と入力します。 **[キーファイルをパスワードで保護**する] フィールドのチェックボックスをオフにします。

3. **ソリューションエクスプローラー**で、VSIX プロジェクトを選択し、[**プロパティ**] ウィンドウを検索します。

4. [**ビルド出力を出力ディレクトリにコピー** ] フィールドを**true**に設定します。 これにより、ソリューションの再構築時にアセンブリを出力ディレクトリにコピーできます。 ファイルにはまだ含まれてい `.vsix` ます。 署名キーを調べるには、アセンブリを確認する必要があります。

5. ソリューションをリビルドします。

6. これで、MyProjectWizard プロジェクトディレクトリ (* \<your disk location> \MyProjectTemplate\MyProjectWizard\key.snk*) でキー .snk ファイルを見つけることができます。 キーの *.snk*ファイルをコピーします。

7. 出力ディレクトリにアクセスし、アセンブリを見つけます (* \<your disk location> \ myprojecttemplate/MyProjectWizard\bin\Debug\MyProjectWizard.dll*)。 キーの *.snk*ファイルをここに貼り付けます。 (これは必ずしも必要ではありませんが、次の手順が簡単になります)。

8. コマンドウィンドウを開き、アセンブリが作成されたディレクトリに移動します。

9. *sn.exe*署名ツールを見つけます。 たとえば、Windows 10 64 ビットオペレーティングシステムでは、一般的なパスは次のようになります。

     *C:\Program Files (x86) \Microsoft SDKs\Windows\v10.0A\bin\NETFX 4.6.1 Tools*

     ツールが見つからない場合は、コマンドウィンドウで**where/r. sn.exe**を実行してみてください。 パスをメモしておきます。

10. *キー .snk*ファイルから公開キーを抽出します。 コマンドウィンドウで、「」と入力します。

     **\<location of sn.exe>\sn.exe-p キーを出力します。**

     ディレクトリ名にスペースが含まれている場合は、 *sn.exe*のパスを引用符で囲むことを忘れないでください。

11. 出力元から公開キートークンを取得します。

     **\<location of sn.exe>\sn.exe-t 出力キー。**

     繰り返しますが、引用符は忘れないでください。 出力には次のような行が表示されます。

     **公開キートークンは\<token>**

     この値を書き留めておきます。

12. カスタムウィザードへの参照をプロジェクトテンプレートの *.vstemplate*ファイルに追加します。 **ソリューションエクスプローラー**で、 *myprojecttemplate .vstemplate*という名前のファイルを見つけて開きます。 セクションの末尾の後 \<TemplateContent> に、次のセクションを追加します。

    ```xml
    <WizardExtension>
        <Assembly>MyProjectWizard, Version=1.0.0.0, Culture=Neutral, PublicKeyToken=token</Assembly>
        <FullClassName>MyProjectWizard.WizardImplementation</FullClassName>
    </WizardExtension>
    ```

     **Myprojectwizard**はアセンブリの名前で、 **token**は前の手順でコピーしたトークンです。

13. プロジェクト内のすべてのファイルを保存し、リビルドします。

## <a name="add-the-custom-parameter-to-the-template"></a>カスタムパラメーターをテンプレートに追加する

この例では、テンプレートとして使用されるプロジェクトに、カスタムウィザードのユーザー入力フォームで指定されたメッセージが表示されます。

1. **ソリューションエクスプローラー**で、 **myprojecttemplate**プロジェクトにアクセスし、 *Class1.cs*を開きます。

2. アプリケーションの `Main` メソッドに次のコード行を追加します。

   ```csharp
   Console.WriteLine("$custommessage$");
   ```

    `$custommessage$` パラメーターは、プロジェクトをテンプレートから作成する際にユーザー入力フォームに入力したテキストで置き換えられます。

テンプレートにエクスポートする前の完全なコードファイルを次に示します。

```csharp
using System;
using System.Collections.Generic;
$if$ ($targetframeworkversion$ >= 3.5)using System.Linq;
$endif$using System.Text;

namespace $safeprojectname$
{
    public class Class1
    {
          static void Main(string[] args)
          {
               Console.WriteLine("$custommessage$");
          }
    }
}
```

## <a name="use-the-custom-wizard"></a>カスタムウィザードを使用する

これで、テンプレートからプロジェクトを作成し、カスタム ウィザードを使用できるようになりました。

1. ソリューションをリビルドし、デバッグを開始します。 Visual Studio の 2 番目のインスタンスが表示されます。

2. 新しい MyProjectTemplate プロジェクトを作成します。 (**ファイル**  > **新規**  > **プロジェクト**)。

3. [**新しいプロジェクト**] ダイアログボックスで、"myproject" を検索してテンプレートを見つけ、名前を入力して、[ **OK**] をクリックします。

     ウィザードのユーザー入力フォームが開きます。

4. カスタム パラメーターの値を入力し、ボタンをクリックします。

     ウィザードのユーザー入力フォームが終了し、プロジェクトがテンプレートから作成されます。

5. **ソリューションエクスプローラー**で、ソースコードファイルを右クリックし、[**コードの表示**] をクリックします。

     `$custommessage$` は、ウィザードのユーザー入力フォームに入力されたテキストで置き換えられています。

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualStudio.TemplateWizard.IWizard>
- [テンプレートのカスタマイズ](../ide/customizing-project-and-item-templates.md)
- [WizardExtension 要素 (Visual Studio テンプレート)](../extensibility/wizardextension-element-visual-studio-templates.md)
- [Visual Studio テンプレートの NuGet パッケージ](/nuget/visual-studio-extensibility/visual-studio-templates)
