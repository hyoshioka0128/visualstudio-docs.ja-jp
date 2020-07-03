---
title: 基本的なプロジェクトシステムの作成、パート 2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- writing a project system
- project system
- tutorial
ms.assetid: aee48fc6-a15f-4fd5-8420-7f18824de220
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2b9d5ce673e0ee44e888905239c12251241015ab
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85903834"
---
# <a name="create-a-basic-project-system-part-2"></a>基本的なプロジェクトシステムを作成する (第2部)
このシリーズの最初のチュートリアルである「[基本的なプロジェクトシステムを作成する (第1部](../extensibility/creating-a-basic-project-system-part-1.md))」では、基本的なプロジェクトシステムを作成する方法を示します。 このチュートリアルは、Visual Studio テンプレート、プロパティページ、およびその他の機能を追加することによって、基本的なプロジェクトシステム上に構築されています。 このチュートリアルを開始する前に、最初のチュートリアルを完了する必要があります。

このチュートリアルでは、プロジェクトファイル名拡張子*myproj*を持つプロジェクトの種類を作成する方法について説明します。 チュートリアルを完了するには、既存の Visual C# プロジェクトシステムからではチュートリアルを実行するため、独自の言語を作成する必要はありません。

このチュートリアルでは、次のタスクを実行する方法について説明します。

- Visual Studio テンプレートを作成します。

- Visual Studio テンプレートをデプロイします。

- [**新しいプロジェクト**] ダイアログボックスで、[プロジェクトの種類] 子ノードを作成します。

- Visual Studio テンプレートでパラメーターの置換を有効にします。

- プロジェクトのプロパティページを作成します。

> [!NOTE]
> このチュートリアルの手順は、C# プロジェクトに基づいています。 ただし、ファイル名拡張子やコードなどの詳細情報を除き、Visual Basic プロジェクトでも同じ手順を使用できます。

## <a name="create-a-visual-studio-template"></a>Visual Studio テンプレートを作成する
- [基本的なプロジェクトシステムの作成パート1では、](../extensibility/creating-a-basic-project-system-part-1.md)基本的なプロジェクトテンプレートを作成し、プロジェクトシステムに追加する方法を示します。 また、属性を使用してこのテンプレートを Visual Studio に登録する方法についても説明します。これにより <xref:Microsoft.VisualStudio.Shell.ProvideProjectFactoryAttribute> 、 * \\ \\ Templates\Projects\SimpleProject*フォルダーの完全なパスがシステムレジストリに書き込まれます。

基本的なプロジェクトテンプレートの代わりに Visual Studio テンプレート (*.vstemplate*ファイル) を使用すると、[**新しいプロジェクト**] ダイアログボックスでのテンプレートの表示方法と、テンプレートパラメーターの置換方法を制御できます。 *.Vstemplate*ファイルは、プロジェクトシステムテンプレートを使用してプロジェクトを作成するときにソースファイルがどのように含まれるかを記述する XML ファイルです。 プロジェクトシステム自体は、 *.vstemplate*ファイルとソースファイルを *.zip*ファイルに収集し、その *.zip*ファイルを Visual Studio が認識する場所にコピーすることによって作成されます。 このプロセスの詳細については、このチュートリアルの後半で説明します。

1. で、「 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] [基本的なプロジェクトシステムの作成 (パート 1)](../extensibility/creating-a-basic-project-system-part-1.md)」に従って作成した simpleproject ソリューションを開きます。

2. SimpleProjectPackage.cs ファイルで、[ *SimpleProjectPackage.cs* ] 属性を見つけます。 2番目のパラメーター (プロジェクト名) を null に、4番目のパラメーター (プロジェクトのテンプレートフォルダーへのパス) を "で置き換えます。 \\次のように \N ullpath。

    ```
    [ProvideProjectFactory(typeof(SimpleProjectFactory), null,
        "Simple Project Files (*.myproj);*.myproj", "myproj", "myproj",
        ".\\NullPath",
    LanguageVsTemplate = "SimpleProject")]
    ```

3. * \\ Templates\Projects\SimpleProject \\ *フォルダーに、 *simpleproject .VSTEMPLATE*という名前の XML ファイルを追加します。

4. *Simpleproject .vstemplate*の内容を次のコードに置き換えます。

    ```xml
    <VSTemplate Version="2.0.0" Type="Project"
        xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
      <TemplateData>
        <Name>SimpleProject Application</Name>
        <Description>
          A project for creating a SimpleProject application
        </Description>
        <Icon>SimpleProject.ico</Icon>
        <ProjectType>SimpleProject</ProjectType>
      </TemplateData>
      <TemplateContent>
        <Project File="SimpleProject.myproj" ReplaceParameters="true">
          <ProjectItem ReplaceParameters="true" OpenInEditor="true">
            Program.cs
          </ProjectItem>
          <ProjectItem ReplaceParameters="true" OpenInEditor="false">
            AssemblyInfo.cs
          </ProjectItem>
        </Project>
      </TemplateContent>
    </VSTemplate>
    ```

5. [**プロパティ**] ウィンドウで、 * \\ Templates\Projects\SimpleProject \\ *フォルダー内の5つのファイルをすべて選択し、[**ビルド] アクション**を [ **zipproject**] に設定します。

    ![単純なプロジェクトフォルダー](../extensibility/media/simpproj2.png "SimpProj2")

    次のように、[ \<TemplateData> **新しいプロジェクト**] ダイアログボックスで simpleproject プロジェクトの種類の場所と外観を決定します。

- 要素は、 \<Name> プロジェクトテンプレートに Simpleproject アプリケーションという名前を指定します。

- 要素には、 \<Description> プロジェクトテンプレートを選択したときに [**新しいプロジェクト**] ダイアログボックスに表示される説明が含まれています。

- 要素は、 \<Icon> simpleproject プロジェクトの種類と共に表示されるアイコンを指定します。

- \<ProjectType>要素は、[**新しいプロジェクト**] ダイアログボックスでプロジェクトの種類の名前を入力します。 この名前は、指定されたプロジェクト名のパラメーターを置き換えます。

  > [!NOTE]
  > 要素は、 \<ProjectType> `LanguageVsTemplate` SimpleProjectPackage.cs ファイルの属性の引数と一致する必要があり `ProvideProjectFactory` ます。

  このセクションでは、 \<TemplateContent> 新しいプロジェクトの作成時に生成されるこれらのファイルについて説明します。

- *SimpleProject。 myproj*

- *Program.cs*

- *AssemblyInfo.cs*

  3つのファイルすべてが `ReplaceParameters` true に設定されています。これにより、パラメーターの置換が有効になります。 *Program.cs*ファイルは `OpenInEditor` true に設定されています。これにより、プロジェクトの作成時にファイルがコードエディターで開かれます。

  Visual Studio テンプレートスキーマの要素の詳細については、「 [Visual studio テンプレートスキーマ参照](../extensibility/visual-studio-template-schema-reference.md)」を参照してください。

> [!NOTE]
> プロジェクトに複数の Visual Studio テンプレートがある場合、すべてのテンプレートは個別のフォルダーにあります。 そのフォルダー内のすべてのファイルで、**ビルドアクション**が**zipproject**に設定されている必要があります。

## <a name="adding-a-minimal-vsct-file"></a>最小の vsct ファイルの追加
 新規または変更された Visual Studio テンプレートを認識するには、visual Studio をセットアップモードで実行する必要があります。 セットアップモードでは、 *. vsct*ファイルが存在する必要があります。 そのため、プロジェクトに最小の*vsct*ファイルを追加する必要があります。

1. *Simpleproject という名前*の XML ファイルを simpleproject プロジェクトに追加します。

2. *Simpleproject. vsct*ファイルの内容を次のコードに置き換えます。

    ```
    <?xml version="1.0" encoding="utf-8" ?>
    <CommandTable
      xmlns="http://schemas.microsoft.com/VisualStudio/2005-10-18/CommandTable">
    </CommandTable>
    ```

3. このファイルの**ビルドアクション**を**VSCTCompile**に設定します。 これは、 *.csproj*ファイルでのみ実行でき、[**プロパティ**] ウィンドウでは実行できません。 この時点で、このファイルの**ビルドアクション**が **[なし**] に設定されていることを確認します。

    1. SimpleProject ノードを右クリックし、[ **simpleproject .csproj の編集**] をクリックします。

    2. *.Csproj*ファイルで、 *simpleproject. vsct*項目を見つけます。

        ```
        <None Include="SimpleProject.vsct" />
        ```

    3. ビルドアクションを**VSCTCompile**に変更します。

        ```
        <VSCTCompile Include="SimpleProject.vsct" />
        ```

    4. プロジェクトファイルを開いて、エディターを閉じます。

    5. SimpleProject ノードを保存し、**ソリューションエクスプローラー** [**プロジェクトの再読み込み**] をクリックします。

## <a name="examine-the-visual-studio-template-build-steps"></a>Visual Studio テンプレートのビルド手順を確認する
 VSPackage プロジェクトビルドシステムは、 *.vstemplate*ファイルが変更された場合、または *.vstemplate*ファイルを含むプロジェクトが再構築された場合に、通常はセットアップモードで Visual Studio を実行します。 MSBuild の詳細レベルを [標準] 以上に設定することによって、次の操作を行うことができます。

1. **[ツール]** メニューの **[オプション]** をクリックします。

2. [**プロジェクトおよびソリューション**] ノードを展開し、[**ビルドおよび実行**] を選択します。

3. **MSBuild プロジェクトのビルド出力の詳細**度を**Normal**に設定します。 **[OK]** をクリックします。

4. SimpleProject プロジェクトをリビルドします。

    *.Zip*プロジェクトファイルを作成するためのビルドステップは、次の例のようになります。

```
ZipProjects:
1>  Zipping ProjectTemplates
1>  Zipping <path>\SimpleProject\SimpleProject\obj\Debug\SimpleProject.zip...
1>  Copying file from "<path>\SimpleProject\SimpleProject\obj\Debug\SimpleProject.zip" to "<%LOCALAPPDATA%>\Microsoft\VisualStudio\14.0Exp\ProjectTemplates\\\\SimpleProject.zip".
1>  Copying file from "<path>\SimpleProject\SimpleProject\obj\Debug\SimpleProject.zip" to "bin\Debug\\ProjectTemplates\\\\SimpleProject.zip".
1>  SimpleProject -> <path>\SimpleProject\SimpleProject\bin\Debug\ProjectTemplates\SimpleProject.zip
1>ZipItems:
1>  Zipping ItemTemplates
1>  SimpleProject ->
```

## <a name="deploy-a-visual-studio-template"></a>Visual Studio テンプレートをデプロイする
Visual Studio テンプレートにパス情報が含まれていません。 そのため、テンプレート *.zip*ファイルは、Visual Studio で認識されている場所に配置する必要があります。 通常、ProjectTemplates フォルダーの場所は *<% LOCALAPPDATA% > \microsoft\visualstudio\14.0exp\projecttemplates*です。

プロジェクトファクトリを配置するには、インストールプログラムに管理者特権が必要です。 Visual Studio のインストールノード *..\Microsoft Visual studio 14.0 \ Common7\IDE\ProjectTemplates*にテンプレートがデプロイされます。

## <a name="test-a-visual-studio-template"></a>Visual Studio テンプレートをテストする
プロジェクトファクトリをテストして、Visual Studio テンプレートを使用してプロジェクトの階層を作成するかどうかを確認します。

1. Visual Studio SDK の実験用インスタンスをリセットします。

    [!INCLUDE[win7](../debugger/includes/win7_md.md)]: [**スタート**] メニューで、[ **Microsoft Visual Studio/Microsoft Visual Studio SDK/ツール**] フォルダーを見つけて、[ **Microsoft Visual Studio 実験的なインスタンスをリセットする**] を選択します。

    Windows の新しいバージョン:**スタート**画面で、「 **Microsoft Visual Studio \<version> 実験用インスタンスをリセットする**」と入力します。

2. コマンドプロンプトウィンドウが表示されます。 [任意のキーを**押す**] という単語が表示されたら、 **Enter**キーを押します。 ウィンドウが閉じたら、Visual Studio を開きます。

3. SimpleProject プロジェクトをリビルドし、デバッグを開始します。 実験用インスタンスが表示されます。

4. 実験用インスタンスで、SimpleProject プロジェクトを作成します。 [**新しいプロジェクト**] ダイアログボックスで、[ **simpleproject**] を選択します。

5. SimpleProject の新しいインスタンスが表示できます。

    ![単純なプロジェクトの新しいインスタンス](../extensibility/media/simpproj2_newproj.png "SimpProj2_NewProj")

    ![マイプロジェクトの新しいインスタンス](../extensibility/media/simpproj2_myproj.png "SimpProj2_MyProj")

## <a name="create-a-project-type-child-node"></a>プロジェクトの種類の子ノードを作成する
[**新しいプロジェクト**] ダイアログボックスの [プロジェクトの種類] ノードに子ノードを追加できます。 たとえば、SimpleProject プロジェクトの種類では、コンソールアプリケーション、ウィンドウアプリケーション、web アプリケーションなどの子ノードを持つことができます。

子ノードは、プロジェクトファイルを変更し、要素に子を追加することによって作成され \<OutputSubPath> \<ZipProject> ます。 ビルド中または配置時にテンプレートをコピーすると、すべての子ノードがプロジェクトテンプレートフォルダーのサブフォルダーになります。

このセクションでは、SimpleProject プロジェクトタイプのコンソール子ノードを作成する方法について説明します。

1. * \\ Templates\Projects\SimpleProject \\ *フォルダーの名前を* \\ Templates\Projects\ConsoleApp \\ *に変更します。

2. [**プロパティ**] ウィンドウで、 * \\ Templates\Projects\ConsoleApp \\ *フォルダー内の5つのファイルをすべて選択し、**ビルドアクション**が**zipproject**に設定されていることを確認します。

3. SimpleProject .vstemplate ファイルで、セクションの末尾に \<TemplateData> 、終了タグの直前に次の行を追加します。

    ```
    <NumberOfParentCategoriesToRollUp>1</NumberOfParentCategoriesToRollUp>
    ```

    これにより、コンソールアプリケーションテンプレートがコンソールの子ノードと、子ノードの1レベル上にある SimpleProject 親ノードの両方に表示されるようになります。

4. *Simpleproject .vstemplate*ファイルを保存します。

5. *.Csproj*ファイルで、 \<OutputSubPath> zipproject の各要素にを追加します。 前と同様にプロジェクトをアンロードし、プロジェクトファイルを編集します。

6. 要素を見つけ \<ZipProject> ます。 各要素に対して \<ZipProject> 、 \<OutputSubPath> 要素を追加し、それに値コンソールを指定します。 ZipProject

    ```
    <ZipProject Include="Templates\Projects\ConsoleApp\AssemblyInfo.cs">
      <OutputSubPath>Console</OutputSubPath>
    </ZipProject>
    <ZipProject Include="Templates\Projects\ConsoleApp\Program.cs">
      <OutputSubPath>Console</OutputSubPath>
    </ZipProject>
    <ZipProject Include="Templates\Projects\ConsoleApp\SimpleProject.myproj">
      <OutputSubPath>Console</OutputSubPath>
    </ZipProject>
    <ZipProject Include="Templates\Projects\ConsoleApp\SimpleProject.vstemplate">
      <OutputSubPath>Console</OutputSubPath>
    </ZipProject>
    <ZipProject Include="Templates\Projects\ConsoleApp\SimpleProject.ico">
      <OutputSubPath>Console</OutputSubPath>
    </ZipProject>
    ```

7. これ \<PropertyGroup> をプロジェクトファイルに追加します。

    ```
    <PropertyGroup>
      <VsTemplateLanguage>SimpleProject</VsTemplateLanguage>
    </PropertyGroup>
    ```

8. プロジェクトファイルを保存し、プロジェクトを再度読み込みます。

## <a name="test-the-project-type-child-node"></a>プロジェクトの種類の子ノードをテストする
変更したプロジェクトファイルをテストして、**コンソール**の子ノードが [**新しいプロジェクト**] ダイアログボックスに表示されているかどうかを確認します。

1. **Microsoft Visual Studio 実験用インスタンスのリセット**ツールを実行します。

2. SimpleProject プロジェクトをリビルドし、デバッグを開始します。 実験用インスタンスが表示されます

3. [**新しいプロジェクト**] ダイアログで、[ **simpleproject** ] ノードをクリックします。 [**テンプレート**] ウィンドウに**コンソールアプリケーション**テンプレートが表示されます。

4. **Simpleproject**ノードを展開します。 **コンソール**の子ノードが表示されます。 **Simpleproject アプリケーション**テンプレートは、[**テンプレート**] ウィンドウに引き続き表示されます。

5. [**キャンセル**] をクリックしてデバッグを停止します。

    ![単純なプロジェクトのロールアップ](../extensibility/media/simpproj2_rollup.png "SimpProj2_Rollup")

    ![単純なプロジェクトコンソールノード](../extensibility/media/simpproj2_subfolder.png "SimpProj2_Subfolder")

## <a name="substitute-project-template-parameters"></a>プロジェクトテンプレートパラメーターの置換
- [基本的なプロジェクトシステムの作成パート1で](../extensibility/creating-a-basic-project-system-part-1.md)は、メソッドを上書きして `ProjectNode.AddFileFromTemplate` 基本的な種類のテンプレートパラメーターの置換を実行する方法を示しました。 このセクションでは、より洗練された Visual Studio テンプレートパラメーターの使用方法について説明します。

[**新しいプロジェクト**] ダイアログボックスで Visual Studio テンプレートを使用してプロジェクトを作成すると、テンプレートパラメーターが文字列に置き換えられ、プロジェクトがカスタマイズされます。 テンプレートパラメーターは、$ 記号 ($time $ など) で始まる特別なトークンです。 次の2つのパラメーターは、テンプレートに基づくプロジェクトでカスタマイズを有効にする場合に特に役立ちます。

- $GUID [1-10] $ は新しい Guid に置き換えられます。 最大10個の一意の Guid (たとえば、$guid $1) を指定できます。

- $safeprojectname $ は、[**新しいプロジェクト**] ダイアログボックスでユーザーによって指定された名前であり、安全でないすべての文字とスペースを削除するように変更されています。

  テンプレート パラメーターの完全な一覧については、「[テンプレート パラメーター](../ide/template-parameters.md)」を参照してください。

### <a name="to-substitute-project-template-parameters"></a>プロジェクトテンプレートパラメーターを置き換えるには

1. *SimpleProjectNode.cs*ファイルで、メソッドを削除し `AddFileFromTemplate` ます。

2. * \\ Templates\Projects\ConsoleApp\SimpleProject.myproj*ファイルで、プロパティを探し、 \<RootNamespace> その値を $safeprojectname $ に変更します。

    ```
    <RootNamespace>$safeprojectname$</RootNamespace>
    ```

3. * \\ Templates\Projects\SimpleProject\Program.cs*ファイルで、ファイルの内容を次のコードに置き換えます。

    ```
    using System;
    using System.Collections.Generic;
    using System.Text;
    using System.Runtime.InteropServices;    // Guid

    namespace $safeprojectname$
    {
        [Guid("$guid1$")]
        public class $safeprojectname$
        {
            static void Main(string[] args)
            {
                Console.WriteLine("Hello VSX!!!");
                Console.ReadKey();
            }
        }
    }
    ```

4. SimpleProject プロジェクトをリビルドし、デバッグを開始します。 実験用インスタンスが表示されます。

5. 新しい SimpleProject コンソールアプリケーションを作成します。 ([**プロジェクトの種類**] ペインで、[ **simpleproject**] を選択します。 [ **Visual Studio にインストールされたテンプレート**] で、[**コンソールアプリケーション**] を選択します。)

6. 新しく作成したプロジェクトで、 *Program.cs*を開きます。 次のようになります (ファイル内の GUID 値は異なります)。

    ```csharp
    using System;
    using System.Collections.Generic;
    using System.Text;
    using System.Runtime.InteropServices;    // Guid

    namespace Console_Application1
    {
        [Guid("00000000-0000-0000-00000000-00000000)"]
        public class Console_Application1
        {
            static void Main(string[] args)
            {
                Console.WriteLine("Hello VSX!!!");
                Console.ReadKey();
            }
        }
    }
    ```

## <a name="create-a-project-property-page"></a>プロジェクトのプロパティページの作成
ユーザーが自分のテンプレートに基づくプロジェクトのプロパティを表示および変更できるように、プロジェクトの種類のプロパティページを作成できます。 このセクションでは、構成に依存しないプロパティページを作成する方法について説明します。 この基本的なプロパティページでは、プロパティグリッドを使用して、プロパティページクラスで公開するパブリックプロパティを表示します。

基本クラスからプロパティページクラスを派生させ `SettingsPage` ます。 クラスによって提供されるプロパティグリッド `SettingsPage` は、ほとんどのプリミティブデータ型を認識し、それらを表示する方法を認識します。 また、クラスは、 `SettingsPage` プロパティ値をプロジェクトファイルに永続化する方法を認識します。

このセクションで作成するプロパティページでは、次のプロジェクトのプロパティを変更して保存できます。

- AssemblyName

- OutputType

- RootNamespace.

1. *SimpleProjectPackage.cs*ファイルで、次の `ProvideObject` 属性をクラスに追加し `SimpleProjectPackage` ます。

    ```
    [ProvideObject(typeof(GeneralPropertyPage))]
    public sealed class SimpleProjectPackage : ProjectPackage
    ```

    これにより、プロパティページクラスが COM に登録され `GeneralPropertyPage` ます。

2. *SimpleProjectNode.cs*ファイルで、次の2つのオーバーライドされたメソッドをクラスに追加し `SimpleProjectNode` ます。

    ```csharp
    protected override Guid[] GetConfigurationIndependentPropertyPages()
    {
        Guid[] result = new Guid[1];
        result[0] = typeof(GeneralPropertyPage).GUID;
        return result;
    }
    protected override Guid[] GetPriorityProjectDesignerPages()
    {
        Guid[] result = new Guid[1];
        result[0] = typeof(GeneralPropertyPage).GUID;
        return result;
    }
    ```

    これらのメソッドはどちらも、プロパティページ Guid の配列を返します。 全般の Propertypage GUID は配列内の唯一の要素であるため、[**プロパティページ**] ダイアログボックスには1ページしか表示されません。

3. *GeneralPropertyPage.cs*という名前のクラスファイルを simpleproject プロジェクトに追加します。

4. 次のコードを使用して、このファイルの内容を置き換えます。

    ```csharp
    using System;
    using System.Runtime.InteropServices;
    using Microsoft.VisualStudio;
    using Microsoft.VisualStudio.Project;
    using System.ComponentModel;

    namespace SimpleProject
    {
        [ComVisible(true)]
        [Guid("6BC7046B-B110-40d8-9F23-34263D8D2936")]
        public class GeneralPropertyPage : SettingsPage
        {
            private string assemblyName;
            private OutputType outputType;
            private string defaultNamespace;

            public GeneralPropertyPage()
            {
                this.Name = "General";
            }

            [Category("AssemblyName")]
            [DisplayName("AssemblyName")]
            [Description("The output file holding assembly metadata.")]
            public string AssemblyName
            {
                get { return this.assemblyName; }
            }
            [Category("Application")]
            [DisplayName("OutputType")]
            [Description("The type of application to build.")]
            public OutputType OutputType
            {
                get { return this.outputType; }
                set { this.outputType = value; this.IsDirty = true; }
            }
            [Category("Application")]
            [DisplayName("DefaultNamespace")]
            [Description("Specifies the default namespace for added items.")]
            public string DefaultNamespace
            {
                get { return this.defaultNamespace; }
                set { this.defaultNamespace = value; this.IsDirty = true; }
            }

            protected override void BindProperties()
            {
                this.assemblyName = this.ProjectMgr.GetProjectProperty("AssemblyName", true);
                this.defaultNamespace = this.ProjectMgr.GetProjectProperty("RootNamespace", false);

                string outputType = this.ProjectMgr.GetProjectProperty("OutputType", false);
                this.outputType = (OutputType)Enum.Parse(typeof(OutputType), outputType);
            }

            protected override int ApplyChanges()
            {
                this.ProjectMgr.SetProjectProperty("AssemblyName", this.assemblyName);
                this.ProjectMgr.SetProjectProperty("OutputType", this.outputType.ToString());
                this.ProjectMgr.SetProjectProperty("RootNamespace", this.defaultNamespace);
                this.IsDirty = false;

                return VSConstants.S_OK;
            }
        }
    }
    ```

    クラスは、 `GeneralPropertyPage` AssemblyName、OutputType、および RootNamespace という3つのパブリックプロパティを公開します。 AssemblyName には set メソッドがないため、読み取り専用プロパティとして表示されます。 OutputType は列挙定数であるため、ドロップダウンリストとして表示されます。

    `SettingsPage`基本クラスは、 `ProjectMgr` プロパティを永続化するためにを提供します。 メソッドは、を使用して、永続化された `BindProperties` `ProjectMgr` プロパティ値を取得し、対応するプロパティを設定します。 メソッドは、 `ApplyChanges` を使用して `ProjectMgr` プロパティの値を取得し、プロジェクトファイルに永続化します。 プロパティの set メソッドは、 `IsDirty` プロパティを永続化する必要があることを示すために true に設定されます。 永続化は、プロジェクトまたはソリューションを保存するときに行われます。

5. SimpleProject ソリューションをリビルドし、デバッグを開始します。 実験用インスタンスが表示されます。

6. 実験用インスタンスで、新しい SimpleProject アプリケーションを作成します。

7. Visual Studio は、Visual Studio テンプレートを使用してプロジェクトを作成するために、プロジェクトファクトリを呼び出します。 新しい*Program.cs*ファイルがコードエディターで開きます。

8. **ソリューションエクスプローラー**でプロジェクトノードを右クリックし、[**プロパティ**] をクリックします。 **[プロパティ ページ]** ダイアログ ボックスが表示されます。

    ![単純なプロジェクトのプロパティページ](../extensibility/media/simpproj2_proppage.png "SimpProj2_PropPage")

## <a name="test-the-project-property-page"></a>プロジェクトのプロパティページをテストする
これで、プロパティ値を変更および変更できるかどうかをテストできるようになりました。

1. [ **Myconsoleapplication プロパティページ**] ダイアログボックスで、 **Defaultnamespace**を**MyApplication**に変更します。

2. [ **OutputType** ] プロパティを選択し、[**クラスライブラリ**] を選択します。

3. [**適用**] をクリックし、[**OK**] をクリックします。

4. [**プロパティページ**] ダイアログボックスを再び開き、変更が保存されていることを確認します。

5. Visual Studio の実験用インスタンスを終了します。

6. 実験用インスタンスを再度開きます。

7. [**プロパティページ**] ダイアログボックスを再び開き、変更が保存されていることを確認します。

8. Visual Studio の実験用インスタンスを終了します。
    ![実験用インスタンスを閉じる](../extensibility/media/simpproj2_proppage2.png "SimpProj2_PropPage2")
