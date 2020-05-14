---
title: 基本プロジェクトシステムの作成 パート 2 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
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
ms.openlocfilehash: 7823dc949e78cc6d22514a1ba93476fd5f42d076
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739712"
---
# <a name="create-a-basic-project-system-part-2"></a>基本プロジェクト システムの作成、パート 2
このシリーズの最初のチュートリアル「[基本的なプロジェクト システムを作成する (パート 1)」では、](../extensibility/creating-a-basic-project-system-part-1.md)基本的なプロジェクト システムを作成する方法を示します。 このチュートリアルでは、Visual Studio テンプレート、プロパティ ページ、およびその他の機能を追加することで、基本的なプロジェクト システムに基づいています。 最初のチュートリアルを完了してから、このチュートリアルを開始する必要があります。

このチュートリアルでは、プロジェクト ファイル名拡張子 *.myproj*を持つプロジェクトの種類を作成する方法について説明します。 チュートリアルを完了するには、既存の Visual C# プロジェクト システムから借用するため、独自の言語を作成する必要はありません。

このチュートリアルでは、次のタスクを実行する方法について説明します。

- ビジュアル スタジオ テンプレートを作成します。

- Visual Studio テンプレートを展開します。

- **[新しい**プロジェクト] ダイアログ ボックスで、プロジェクト タイプの子ノードを作成します。

- Visual Studio テンプレートでパラメーターの置換を有効にします。

- プロジェクトのプロパティ ページを作成します。

> [!NOTE]
> このチュートリアルの手順は、C# プロジェクトに基づいています。 ただし、ファイル名拡張子やコードなどの詳細を除き、Visual Basic プロジェクトでも同じ手順を使用できます。

## <a name="create-a-visual-studio-template"></a>ビジュアル スタジオ テンプレートを作成する
- [基本的なプロジェクト システムを作成する、パート 1](../extensibility/creating-a-basic-project-system-part-1.md)では、基本的なプロジェクト テンプレートを作成し、それをプロジェクト システムに追加する方法を示します。 また、システム レジストリの*\\Templates\Projects\SimpleProject\\ * <xref:Microsoft.VisualStudio.Shell.ProvideProjectFactoryAttribute>フォルダーの完全パスを書き込む属性を使用して、このテンプレートを Visual Studio に登録する方法も示します。

基本的なプロジェクト テンプレートの代わりに Visual Studio テンプレート *(.vstemplate*ファイル) を使用すると、[**新しいプロジェクト**] ダイアログ ボックスでテンプレートを表示する方法とテンプレート パラメーターの置換方法を制御できます。 *.vstemplate*ファイルは、プロジェクト システム テンプレートを使用してプロジェクトを作成するときに、ソース ファイルを含める方法を記述する XML ファイルです。 プロジェクト システム自体は *、.vstemplate*ファイルとソース ファイルを *.zip*ファイルに収集してビルドし、.zip ファイル *.zip*を Visual Studio に認識されている場所にコピーして配置します。 このプロセスについては、このチュートリアルで後ほど詳しく説明します。

1. で[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]、[次](../extensibility/creating-a-basic-project-system-part-1.md)の手順を実行して作成した SimpleProject ソリューションを開きます。

2. *SimpleProjectPackage.cs*ファイルで、プロジェクトのファクトリ属性を見つけます。 2 番目のパラメーター (プロジェクト名) を null に置き換え、4 番目のパラメーター (プロジェクト テンプレート フォルダーへのパス) を " .\\\NullPath", 次のように.

    ```
    [ProvideProjectFactory(typeof(SimpleProjectFactory), null,
        "Simple Project Files (*.myproj);*.myproj", "myproj", "myproj",
        ".\\NullPath",
    LanguageVsTemplate = "SimpleProject")]
    ```

3. *SimpleProject.vstemplate*という名前の XML ファイルを*\\テンプレート\プロジェクト\\\シンプル プロジェクト*フォルダーに追加します。

4. *SimpleProject.vstemplate*の内容を次のコードに置き換えます。

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

5. [**プロパティ]** ウィンドウで、[*\\テンプレート\プロジェクト\SimpleProject]\\*フォルダの 5 つのファイルをすべて選択し、[ビルド**アクション**] を **[ZipProject]** に設定します。

    ![単純なプロジェクト フォルダ](../extensibility/media/simpproj2.png "シンププロジ2")

    [\<テンプレート データ> セクションでは、[**新しいプロジェクト**] ダイアログ ボックスで SimpleProject プロジェクトの種類の場所と外観を次のように指定します。

- 名前\<>要素は、プロジェクト テンプレートを SimpleProject アプリケーションに指定します。

- 説明\<>要素には、プロジェクト テンプレートを選択したときに [**新しいプロジェクト**] ダイアログ ボックスに表示される説明が含まれています。

- アイコン\<>要素は、SimpleProject プロジェクトの種類と共に表示されるアイコンを指定します。

- 要素\<要素は、プロジェクトの種類を **[新しいプロジェクト**]ダイアログ ボックスで>します。 この名前は、属性のプロジェクト名パラメーターに置き換えられます。

  > [!NOTE]
  > プロジェクト\<の種類>要素は、SimpleProjectPackage.cs`LanguageVsTemplate`ファイル内`ProvideProjectFactory`の属性の引数と一致する必要があります。

  TemplateContent \<>セクションでは、新しいプロジェクトの作成時に生成されるこれらのファイルについて説明します。

- *シンプルプロジェクト.ミプロジ*

- *Program.cs*

- *AssemblyInfo.cs*

  3 つのファイル`ReplaceParameters`はすべて true に設定されており、パラメーター置換が可能です。 *Program.cs*ファイルが`OpenInEditor`true に設定され、プロジェクトの作成時にコード エディターでファイルが開かれます。

  Visual Studio テンプレート スキーマの要素の詳細については[、「Visual Studio テンプレート スキーマ リファレンス](../extensibility/visual-studio-template-schema-reference.md)」を参照してください。

> [!NOTE]
> プロジェクトに複数の Visual Studio テンプレートがある場合、すべてのテンプレートは別のフォルダーに格納されます。 そのフォルダ内のすべてのファイルは、**ビルド アクション**を**ZipProject**に設定する必要があります。

## <a name="adding-a-minimal-vsct-file"></a>最小の .vsct ファイルを追加する
 新しいまたは変更された Visual Studio テンプレートを認識するには、セットアップ モードで Visual Studio を実行する必要があります。 セットアップ モードでは *、.vsct*ファイルが存在している必要があります。 したがって、プロジェクトに最小の *.vsct*ファイルを追加する必要があります。

1. という名前の XML ファイル*を SimpleProject*プロジェクトに追加します。

2. 次のコードで *、SimpleProject.vsct*ファイルの内容を置き換えます。

    ```
    <?xml version="1.0" encoding="utf-8" ?>
    <CommandTable
      xmlns="http://schemas.microsoft.com/VisualStudio/2005-10-18/CommandTable">
    </CommandTable>
    ```

3. このファイルの**ビルド アクション**を**VSCTCompile**に設定します。 これは *、.csproj*ファイルでのみ行うことができます。 **Properties** この時点で、このファイルの**ビルド アクション**が **[なし]** に設定されていることを確認します。

    1. [SimpleProject] ノードを右クリックし **、[SimpleProject.csproj の編集]** をクリックします。

    2. *csproj*ファイルで *、SimpleProject.vsct*項目を見つけます。

        ```
        <None Include="SimpleProject.vsct" />
        ```

    3. ビルド アクションを**VSCTCompile**に変更します。

        ```
        <VSCTCompile Include="SimpleProject.vsct" />
        ```

    4. プロジェクト ファイルを開き、エディターを閉じます。

    5. SimpleProject ノードを保存し、ソリューション**エクスプローラ**で [**プロジェクトの再読み込み**] をクリックします。

## <a name="examine-the-visual-studio-template-build-steps"></a>Visual Studio テンプレートのビルド手順を確認する
 VSPackage プロジェクト ビルド システムは、通常 *、.vstemplate*ファイルが変更されたとき、または *.vstemplate*ファイルを含むプロジェクトが再構築されたときに、Visual Studio をセットアップ モードで実行します。 MSBuild の詳細レベルを [標準] 以上に設定すると、次の手順に従うことができます。

1. **[ツール]** メニューの **[オプション]** をクリックします。

2. [**プロジェクトとソリューション]** ノードを展開し、[**ビルドして実行**] を選択します。

3. **MSBuild プロジェクト ビルド出力の詳細を** **[標準**] に設定します。 **[OK]** をクリックします。

4. プロジェクトを再構築します。

    *.zip*プロジェクト ファイルを作成するビルド 手順は、次の例のようになります。

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

## <a name="deploy-a-visual-studio-template"></a>Visual Studio テンプレートを展開する
Visual Studio テンプレートにはパス情報が含まれていません。 したがって、テンプレート *.zip*ファイルは、Visual Studio に認識されている場所に配置する必要があります。 プロジェクト テンプレート フォルダーの場所は*通常<%LOCALAPPDATA%>\マイクロソフト\VisualStudio\14.0Exp\プロジェクト テンプレートです*。

プロジェクト ファクトリを配置するには、インストール プログラムに管理者権限が必要です。 Visual Studio のインストール ノードの下にテンプレートを*展開します。*

## <a name="test-a-visual-studio-template"></a>Visual Studio テンプレートをテストする
プロジェクト ファクトリをテストして、Visual Studio テンプレートを使用してプロジェクト階層を作成するかどうかを確認します。

1. Visual Studio SDK の実験用インスタンスをリセットします。

    オン[!INCLUDE[win7](../debugger/includes/win7_md.md)]にします: [**スタート]** メニューで **、[Microsoft Visual Studio/Microsoft Visual Studio SDK/ツール]** フォルダーを見つけて **、[Microsoft Visual Studio 実験用インスタンスをリセット**する] を選択します。

    Windows の新しいバージョンでは、**スタート**画面で、「 **Microsoft Visual \<Studio のバージョンを試験的なインスタンス>リセット**する 」と入力します。

2. コマンド プロンプト ウィンドウが表示されます。 "任意のキーを**押して続行**します" という言葉が表示されたら **、Enter キーをクリック**します。 ウィンドウが閉じた後、Visual Studio を開きます。

3. SimpleProject プロジェクトをリビルドし、デバッグを開始します。 実験用インスタンスが表示されます。

4. 実験用インスタンスで、SimpleProject プロジェクトを作成します。 [**新しいプロジェクト**] ダイアログ ボックスで、[**シンプル プロジェクト**] を選択します。

5. SimpleProject の新しいインスタンスが表示されます。

    ![単純なプロジェクトの新しいインスタンス](../extensibility/media/simpproj2_newproj.png "SimpProj2_NewProj")

    ![マイ プロジェクトの新しいインスタンス](../extensibility/media/simpproj2_myproj.png "SimpProj2_MyProj")

## <a name="create-a-project-type-child-node"></a>プロジェクト タイプの子ノードを作成する
[**新しい**プロジェクト] ダイアログ ボックスで、プロジェクトの種類のノードに子ノードを追加できます。 たとえば、SimpleProject プロジェクトの種類の場合、コンソール アプリケーション、ウィンドウ アプリケーション、Web アプリケーションなどの子ノードを使用できます。

子ノードは、プロジェクト ファイルを変更し、ZipProject>要素に OutputSubPath>子を\<\<追加することによって作成されます。 ビルドまたは配置中にテンプレートをコピーすると、すべての子ノードがプロジェクト テンプレート フォルダーのサブフォルダーになります。

このセクションでは、SimpleProject プロジェクトの種類のコンソール子ノードを作成する方法について説明します。

1. *\\テンプレート\プロジェクト\シンプル プロジェクト\\*フォルダーの名前を*\\テンプレート\プロジェクト\\\コンソール アプリ*に変更します。

2. [**プロパティ]** ウィンドウで、[*\\テンプレート\プロジェクト\コンソール アプリ\\*] フォルダの 5 つのファイルをすべて選択し、[ビルド**アクション**] が **[ZipProject]** に設定されていることを確認します。

3. SimpleProject.vstemplate ファイルで、終了タグの直前の\<[テンプレート データ>] セクションの最後に次の行を追加します。

    ```
    <NumberOfParentCategoriesToRollUp>1</NumberOfParentCategoriesToRollUp>
    ```

    これにより、コンソール アプリケーション テンプレートは、コンソール子ノードと、子ノードの 1 つ上の SimpleProject 親ノードの両方に表示されます。

4. *ファイル*を保存します。

5. *csproj*ファイルで、各\<ZipProject 要素に出力サブパス>を追加します。 プロジェクトを以前のようにアンロードし、プロジェクト ファイルを編集します。

6. 要素を\<見つける、zip プロジェクト>。 各\<ZipProject>要素に、\<出力サブパス>要素を追加し、値コンソールを指定します。 ジッププロジェクト

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

7. 次の\<プロパティ グループ>をプロジェクト ファイルに追加します。

    ```
    <PropertyGroup>
      <VsTemplateLanguage>SimpleProject</VsTemplateLanguage>
    </PropertyGroup>
    ```

8. プロジェクト ファイルを保存し、プロジェクトを再読み込みします。

## <a name="test-the-project-type-child-node"></a>プロジェクトタイプの子ノードをテストする
変更したプロジェクト ファイルをテストして、[**新しいプロジェクト**] ダイアログ ボックスに **[コンソール**] 子ノードが表示されるかどうかを確認します。

1. マイクロソフトの**Visual Studio の実験用インスタンスのリセットツールを実行します**。

2. SimpleProject プロジェクトをリビルドし、デバッグを開始します。 実験用インスタンスが表示されます。

3. [**新しいプロジェクト**]ダイアログで、[**シンプル プロジェクト**]ノードをクリックします。 **コンソール アプリケーション**テンプレートが **[テンプレート]** ウィンドウに表示されます。

4. **[プロジェクト**] ノードを展開します。 **コンソールの**子ノードが表示されます。 **SimpleProject アプリケーション**テンプレートは、[**テンプレート]** ウィンドウに表示されます。

5. [**キャンセル] を**クリックしてデバッグを中止します。

    ![単純なプロジェクトのロールアップ](../extensibility/media/simpproj2_rollup.png "SimpProj2_Rollup")

    ![単純なプロジェクト コンソール ノード](../extensibility/media/simpproj2_subfolder.png "SimpProj2_Subfolder")

## <a name="substitute-project-template-parameters"></a>代替プロジェクト テンプレート パラメーター
- [基本的なプロジェクト システムを作成するパート 1 では、](../extensibility/creating-a-basic-project-system-part-1.md)基本的な種類の`ProjectNode.AddFileFromTemplate`テンプレート パラメータ置換を行うメソッドを上書きする方法を示しました。 このセクションでは、より高度な Visual Studio テンプレート パラメーターの使用方法について説明します。

[**新しいプロジェクト**] ダイアログ ボックスで Visual Studio テンプレートを使用してプロジェクトを作成すると、テンプレート パラメーターが文字列に置き換えられ、プロジェクトをカスタマイズできます。 テンプレート パラメーターは、ドル記号で始まり、ドル記号で終わる特殊なトークンです ($time$ など)。 テンプレートに基づくプロジェクトでカスタマイズを有効にする場合は、次の 2 つのパラメータが特に役立ちます。

- $GUID[1-10]$は新しい Guid に置き換えられます。 10 個までの一意の GUID を指定できます (たとえば、$guid1$)。

- $safeprojectname$ は、ユーザーが [**新しいプロジェクト**] ダイアログ ボックスで指定した名前で、安全でない文字とスペースをすべて削除するように変更されています。

  テンプレート パラメーターの完全な一覧については、「[テンプレート パラメーター](../ide/template-parameters.md)」を参照してください。

### <a name="to-substitute-project-template-parameters"></a>プロジェクト テンプレート パラメーターを置き換える

1. *SimpleProjectNode.cs*ファイルで、メソッドを`AddFileFromTemplate`削除します。

2. *テンプレート\プロジェクト\コンソールアプリ\シンプルプロジェクト.myprojファイルで、ルート名前空間>プロパティを見つけて、その値を$safeprojectname$に変更します。 \\* \<

    ```
    <RootNamespace>$safeprojectname$</RootNamespace>
    ```

3. テンプレート\プロジェクト\SimpleProject\Program.cs ファイルで、ファイルの内容を次のコードに置き換えます。 * \\*

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

5. 新しい簡易プロジェクト コンソール アプリケーションを作成します。 (プロジェクトの**種類**ペインで **、SimpleProject**を選択します。 [Visual **Studio のインストール済みテンプレート**] で、[**コンソール アプリケーション**] を選択します。

6. 新しく作成したプロジェクトで、 *Program.cs*を開きます。 次のようになります (ファイル内の GUID 値が異なります)。

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

## <a name="create-a-project-property-page"></a>プロジェクト プロパティ ページを作成する
ユーザーがテンプレートに基づくプロジェクトのプロパティを表示および変更できるように、プロジェクトの種類のプロパティ ページを作成できます。 このセクションでは、構成に依存しないプロパティ ページを作成する方法について説明します。 この基本的なプロパティ ページでは、プロパティ グリッドを使用して、プロパティ ページ クラスで公開するパブリック プロパティを表示します。

基本クラスからプロパティ ページ`SettingsPage`クラスを派生させます。 クラスによって提供される`SettingsPage`プロパティ グリッドは、ほとんどのプリミティブ データ型を認識し、それらを表示する方法を認識しています。 また、`SettingsPage`クラスは、プロジェクト ファイルにプロパティ値を永続化する方法を認識しています。

このセクションで作成するプロパティ ページでは、次のプロジェクト プロパティを変更して保存できます。

- AssemblyName

- [OutputType]

- 名前空間。

1. *SimpleProjectPackage.cs*ファイルで、次`ProvideObject`の属性をクラス`SimpleProjectPackage`に追加します。

    ```
    [ProvideObject(typeof(GeneralPropertyPage))]
    public sealed class SimpleProjectPackage : ProjectPackage
    ```

    これにより、プロパティ ページ クラス`GeneralPropertyPage`が COM に登録されます。

2. *SimpleProjectNode.cs*ファイルで、オーバーライドされた次の 2 つの`SimpleProjectNode`メソッドをクラスに追加します。

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

    どちらのメソッドも、プロパティ ページ GUID の配列を返します。 この配列の中で唯一の要素は、プロパティ**ページ**のダイアログ ボックスには 1 ページしか表示されません。

3. GeneralPropertyPage.cs*という名前*のクラス ファイルを SimpleProject プロジェクトに追加します。

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

    この`GeneralPropertyPage`クラスは、3 つのパブリック プロパティを公開します。 AssemblyName にはメソッドが設定されていないため、読み取り専用プロパティとして表示されます。 OutputType は列挙定数なので、ドロップダウン リストとして表示されます。

    基本`SettingsPage`クラスは、`ProjectMgr`プロパティを永続化するために提供します。 この`BindProperties`メソッドは`ProjectMgr`、永続化されたプロパティ値を取得し、対応するプロパティを設定するために使用します。 この`ApplyChanges`メソッドは`ProjectMgr`、プロパティの値を取得し、それらをプロジェクト ファイルに永続化するために使用します。 プロパティ セット メソッド`IsDirty`は true に設定され、プロパティを永続化する必要があることを示します。 永続化は、プロジェクトまたはソリューションを保存するときに発生します。

5. SimpleProject ソリューションをリビルドし、デバッグを開始します。 実験用インスタンスが表示されます。

6. 実験用インスタンスで、新しい SimpleProject アプリケーションを作成します。

7. Visual Studio は、プロジェクト ファクトリを呼び出して、Visual Studio テンプレートを使用してプロジェクトを作成します。 新しい*Program.cs*ファイルがコード エディターで開かれます。

8. **ソリューション エクスプローラ**でプロジェクト ノードを右クリックし、[**プロパティ**] をクリックします。 **[プロパティ ページ]** ダイアログ ボックスが表示されます。

    ![[単純プロジェクト] プロパティ ページ](../extensibility/media/simpproj2_proppage.png "SimpProj2_PropPage")

## <a name="test-the-project-property-page"></a>プロジェクトのプロパティ ページをテストする
これで、プロパティ値を変更および変更できるかどうかをテストできます。

1. **[MyConsole アプリケーション プロパティ ページ**] ダイアログ ボックスで、[既定の**名前空間**] を **[MyApplication]** に変更します。

2. [**出力] プロパティ**を選択し、[**クラス ライブラリ**] を選択します。

3. [**適用**] をクリックし、[**OK**] をクリックします。

4. [プロパティ**ページ**] ダイアログ ボックスを再度開き、変更が保持されていることを確認します。

5. Visual Studio の実験用インスタンスを終了します。

6. 実験用インスタンスを再度開きます。

7. [プロパティ**ページ**] ダイアログ ボックスを再度開き、変更が保持されていることを確認します。

8. Visual Studio の実験用インスタンスを終了します。
    ![実験用インスタンスを閉じる](../extensibility/media/simpproj2_proppage2.png "SimpProj2_PropPage2")
