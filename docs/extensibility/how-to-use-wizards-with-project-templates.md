---
title: '方法 : プロジェクト テンプレートを組み合わせたウィザードを使用する'
ms.date: 3/16/2019
ms.topic: conceptual
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
ms.openlocfilehash: 4d2dc057dfa518bb52c6ba4d30cd0f3e0a822cfd
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80710546"
---
# <a name="how-to-use-wizards-with-project-templates"></a>方法: ウィザードをプロジェクト テンプレートで使用する

Visual Studio には、<xref:Microsoft.VisualStudio.TemplateWizard.IWizard> インターフェイスが用意されています。このインターフェイスを実装すると、ユーザーがテンプレートからプロジェクトを作成する際にカスタム コードを実行できるようになります。

プロジェクト テンプレートのカスタマイズを使用すると、ユーザー入力を収集してテンプレートをカスタマイズしたり、テンプレートにファイルを追加したり、プロジェクトで許可されているその他のアクションを実行できるカスタム UI を表示できます。

インターフェイス<xref:Microsoft.VisualStudio.TemplateWizard.IWizard>メソッドは、プロジェクトの作成中のさまざまな時間に呼び出され、ユーザーが **[新しいプロジェクト**] ダイアログ ボックスで **[OK] を**クリックするとすぐに開始されます。 インターフェイスの各メソッドには、そのメソッドが呼び出される時点を表す名前が付けられます。 たとえば、Visual Studio<xref:Microsoft.VisualStudio.TemplateWizard.IWizard.RunStarted%2A>はプロジェクトの作成を開始するとすぐに呼び出しを行い、ユーザー入力を収集するカスタム コードを記述するのに適しています。

## <a name="create-a-project-template-project-with-a-vsix-project"></a>VSIX プロジェクトを使用してプロジェクト テンプレート プロジェクトを作成する

プロジェクト テンプレート プロジェクトを使用してカスタム テンプレートの作成を開始すると、Visual Studio SDK の一部です。 この手順では、C# プロジェクト テンプレート プロジェクトを使用しますが、Visual Basic プロジェクト テンプレート プロジェクトもあります。 次に、プロジェクト テンプレート プロジェクトを含むソリューションに VSIX プロジェクトを追加します。

1. C# プロジェクト テンプレート プロジェクトを作成します (Visual Studio で[**ファイル] を選択して** > **[新しい** > **プロジェクト**] を選択し、"プロジェクト テンプレート" を検索します)。 名前**を付**けます。

   > [!NOTE]
   > Visual Studio SDK のインストールを求められる場合があります。 詳細については、「 [Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

2. プロジェクト テンプレート プロジェクトと同じソリューションに新しい VSIX プロジェクトを追加します (**ソリューション エクスプローラー**でソリューション ノードを選択し、右クリックして[**新しいプロジェクト**の**追加** > ]を選択し、"vsix" を検索します)。 **名前を付けます。**

3. VSIX プロジェクトをスタートアップ プロジェクトとして設定します。 **ソリューション エクスプローラー**で、VSIX プロジェクト ノードを選択し、右クリックして [**スタートアップ プロジェクトに設定**] をクリックします。

4. VSIX プロジェクトのアセットとしてテンプレート プロジェクトを追加します。 **ソリューション エクスプローラー**の VSIX プロジェクト ノードで、*ソース.extension.vsixmanifest*ファイルを見つけます。 ダブルクリックして、マニフェスト エディターで開きます。

5. マニフェスト エディターで、ウィンドウの左側にある **[Assets]** タブを選択します。

6. [**資産**] タブで、[**新規**] を選択します。 [**新しい資産の追加**] ウィンドウの [種類] フィールドで、[**テンプレート**] を選択します。 [**ソース**] フィールド**で、[現在のソリューションのプロジェクト**] を選択します。 [**プロジェクト**] フィールドで、[**マイプロジェクトテンプレート**] を選択します。 次に、 **[OK]** をクリックします

7. ソリューションをビルドし、デバッグを開始します。 Visual Studio の 2 番目のインスタンスが表示されます。 (これには数分かかることがあります)。

8. Visual Studio の 2 番目のインスタンスで、新しいテンプレートを使用して新しいプロジェクトを作成します (**ファイル** > **の新しい** > プロジェクト 、"myproject" を検索)。**Project** 新しいプロジェクトは**Class1**という名前のクラスで表示されます。 これで、カスタム プロジェクト テンプレートが作成されました。 今すぐデバッグを停止します。

## <a name="create-a-custom-template-wizard"></a>カスタム テンプレート ウィザードを作成する

この手順では、プロジェクトを作成する前に Windows フォームを開くカスタム ウィザードを作成する方法を示します。 フォームを使用すると、ユーザーはプロジェクトの作成時にソース コードに追加されるカスタム パラメーター値を追加できます。

1. アセンブリを作成できるように VSIX プロジェクトを設定します。

2. **ソリューション エクスプローラー**で、VSIX プロジェクト ノードを選択します。 **[ソリューション エクスプローラー**] の下に **[プロパティ]** ウィンドウが表示されます。 表示しない場合は、[**プロパティ ウィンドウ****の表示** > ] を選択するか **、F4**キーを押します。 **[プロパティ]** ウィンドウで、次のフィールド`true`を選択します。

   - **VSIX コンテナーにアセンブリを含める**

   - **VSIX コンテナーにデバッグ シンボルを含める**

   - **ローカル VSIX 配置にデバッグ シンボルを含める**

3. VSIX プロジェクトにアセットとしてアセンブリを追加します。 *source.extension.vsixmanifest*ファイルを開き、[**資産**] タブを選択します。[**新しい資産の追加**] ウィンドウの **[種類**] で **[Microsoft.VisualStudio.Assembly]** を選択し、[**ソース**] で **[現在のソリューションのプロジェクト**] を選択し、[**プロジェクト**] で **[MyProjectWizard]** を選択します。

4. VSIX プロジェクトに次の参照を追加します。 (**ソリューション エクスプローラー**の VSIX プロジェクト ノードで、[**参照**] を選択し、右クリックして [参照の**追加**] を選択します。[**参照の追加**] ダイアログの [**フレームワーク**] タブで **、System.Windows フォーム**アセンブリを見つけて選択します。 また、**システム**アセンブリと**システム図面アセンブリを**検索して選択します。 次に、[**拡張機能**]**タブを選択**します。 また **、アセンブリ**を見つけて選択します。 **[OK]** をクリックします。

5. ウィザード実装のクラスを VSIX プロジェクトに追加します。 (**ソリューション エクスプローラー**で、VSIX プロジェクト ノードを右クリックし、[**追加**]、[**新しい項目**]、[**クラス**] の順にクリックします)。クラスに名前**を付けます ウィザード実装**.

6. *WizardImplementationClass.cs*ファイル内のコードを次のコードに置き換えます。

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

    このコードで参照される**ユーザー入力フォーム**は、後で実装されます。

    `WizardImplementation` クラスには、<xref:Microsoft.VisualStudio.TemplateWizard.IWizard> のすべてのメンバーに対するメソッドの実装が含まれています。 この例では、<xref:Microsoft.VisualStudio.TemplateWizard.IWizard.RunStarted%2A> メソッドだけがタスクを実行します。 他のすべてのメソッドは、何もしないか、`true` を返します。

    <xref:Microsoft.VisualStudio.TemplateWizard.IWizard.RunStarted%2A> メソッドは、次の 4 つのパラメーターを受け取ります。

   - <xref:System.Object> パラメーター。プロジェクトをカスタマイズできるように、ルートの <xref:EnvDTE._DTE> オブジェクトにキャストできます。

   - <xref:System.Collections.Generic.Dictionary%602> パラメーター。テンプレートで定義済みのすべてのパラメーターのコレクションが含まれます。 テンプレート パラメーターの詳細については、「テンプレート[パラメーター](../ide/template-parameters.md)」を参照してください。

   - <xref:Microsoft.VisualStudio.TemplateWizard.WizardRunKind> パラメーター。使用されているテンプレートの種類に関する情報が含まれます。

   - Visual <xref:System.Object> Studio によってウィザードに渡されるパラメーターのセットを格納する配列。

     この例では、ユーザー入力フォームから <xref:System.Collections.Generic.Dictionary%602> パラメーターにパラメーター値を追加します。 プロジェクト内の `$custommessage$` パラメーターのすべてのインスタンスは、ユーザーが入力したテキストと置き換えられます。

7. ここで **、ユーザー入力フォーム**を作成します。 *WizardImplementation.cs*ファイルで、クラスの末尾の後に次のコード`WizardImplementation`を追加します。

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

## <a name="connect-the-wizard-to-the-custom-template"></a>ウィザードをカスタム テンプレートに接続する

カスタム プロジェクト テンプレートでカスタム ウィザードを使用するには、ウィザード アセンブリに署名し、カスタム プロジェクト テンプレートにいくつかの行を追加して、新しいプロジェクトの作成時にウィザードの実装を検索する場所を知らせる必要があります。

1. アセンブリに署名します。 ソリューション**エクスプローラ**で VSIX プロジェクトを選択し、右クリックして [**プロジェクトのプロパティ]** を選択します。

2. [**プロジェクトのプロパティ]** ウィンドウで **、[署名**] タブの [**署名**] タブを選択し、[**アセンブリに署名**する] をオンにします。 [**厳密な名前のキー ファイルを選択**してください] フィールドで、[**\<新規>]** を選択します。 [**厳密な名前キーの作成**] ウィンドウの [**キー ファイル名**] フィールドに**key.snk**と入力します。 [キー**ファイルをパスワードで保護する**] フィールドをオフにします。

3. ソリューション**エクスプローラー**で VSIX プロジェクトを選択し、[**プロパティ]** ウィンドウを見つけます。

4. [**ビルド出力を出力ディレクトリにコピー]** フィールドを**true**に設定します。 これにより、ソリューションの再構築時に、アセンブリを出力ディレクトリにコピーできます。 ファイルにまだ含`.vsix`まれています。 署名キーを見つけるためにアセンブリを確認する必要があります。

5. ソリューションをリビルドします。

6. これで、MyProjectWizard プロジェクト ディレクトリ (*\<ディスクの場所>\MyProjectTemplate\MyProjectWizard\key.snk) で key.snk*ファイルを見つけることができます。 *key.snk*ファイルをコピーします。

7. 出力ディレクトリに移動し、アセンブリ (*\<ディスクの場所>\MyProjectTemplate/MyProjectWizard\bin\デバッグ\MyProjectWizard.dll)* を見つけます。 ここに*key.snk*ファイルを貼り付けます。 (これは絶対に必要ではありませんが、次の手順が簡単になります)。

8. コマンド ウィンドウを開き、アセンブリが作成されているディレクトリに移動します。

9. *sn.exe*署名ツールを見つけます。 たとえば、Windows 10 64 ビット オペレーティング システムでは、一般的なパスは次のようになります。

     *C:\プログラム ファイル (x86)\マイクロソフト SDK\Windows\v10.0A\bin\NETFX 4.6.1 ツール*

     ツールが見つからない場合は、コマンド ウィンドウで **/R .sn.exe**を実行してみてください。 パスをメモします。

10. *key.snk*ファイルから公開キーを抽出します。 コマンド ウィンドウで、次のように入力します。

     **\<sn.exe>\sn.exe -p key.snk アウトファイル.キーの場所。**

     ディレクトリ名にスペースがある場合は *、sn.exe*のパスを引用符で囲むことを忘れないでください。

11. 公開鍵トークンをアウトファイルから取得します。

     **\<の場所>\sn.exe -t アウトファイル.key です。**

     繰り返しますが、引用符を忘れないでください。 次のような出力に行が表示されます。

     **公開鍵トークンは\<トークン・トークン>**

     この値をメモしておきます。

12. カスタム ウィザードへの参照をプロジェクト テンプレートの *.vstemplate*ファイルに追加します。 ソリューション**エクスプローラー**で *、MyProjectTemplate.vstemplate*という名前のファイルを見つけて開きます。 \<テンプレートコンテンツ> セクションの終了後、次のセクションを追加します。

    ```xml
    <WizardExtension>
        <Assembly>MyProjectWizard, Version=1.0.0.0, Culture=Neutral, PublicKeyToken=token</Assembly>
        <FullClassName>MyProjectWizard.WizardImplementation</FullClassName>
    </WizardExtension>
    ```

     ここで **、MyProjectWizard**はアセンブリの名前で、**トークン**は前の手順でコピーしたトークンです。

13. プロジェクト内のすべてのファイルを保存して、再構築します。

## <a name="add-the-custom-parameter-to-the-template"></a>テンプレートにカスタム パラメータを追加する

この例では、テンプレートとして使用されるプロジェクトは、カスタム ウィザードのユーザー入力フォームで指定されたメッセージを表示します。

1. ソリューション**エクスプローラー**で **、 MyProjectTemplate**プロジェクトに移動し、 *Class1.cs*を開きます。

2. アプリケーションの `Main` メソッドに次のコード行を追加します。

   ```csharp
   Console.WriteLine("$custommessage$");
   ```

    `$custommessage$` パラメーターは、プロジェクトをテンプレートから作成する際にユーザー入力フォームに入力したテキストで置き換えられます。

テンプレートにエクスポートされる前の完全なコード ファイルを次に示します。

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

## <a name="use-the-custom-wizard"></a>カスタム ウィザードを使用する

これで、テンプレートからプロジェクトを作成し、カスタム ウィザードを使用できるようになりました。

1. ソリューションをリビルドし、デバッグを開始します。 Visual Studio の 2 番目のインスタンスが表示されます。

2. 新しいプロジェクト テンプレート プロジェクトを作成します。 (**ファイル** > **の新しい** > **プロジェクト**)

3. [**新しいプロジェクト**] ダイアログ ボックスで、"myproject" を検索してテンプレートを検索し、名前を入力**して [OK]** をクリックします。

     ウィザードのユーザー入力フォームが開きます。

4. カスタム パラメーターの値を入力し、ボタンをクリックします。

     ウィザードのユーザー入力フォームが終了し、プロジェクトがテンプレートから作成されます。

5. **ソリューション エクスプローラ**で、ソース コード ファイルを右クリックし、[**コードの表示**] をクリックします。

     `$custommessage$` は、ウィザードのユーザー入力フォームに入力されたテキストで置き換えられています。

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualStudio.TemplateWizard.IWizard>
- [テンプレートをカスタマイズする](../ide/customizing-project-and-item-templates.md)
- [拡張要素のウィザード](../extensibility/wizardextension-element-visual-studio-templates.md)
- [Visual Studio テンプレートの NuGet パッケージ](/nuget/visual-studio-extensibility/visual-studio-templates)
