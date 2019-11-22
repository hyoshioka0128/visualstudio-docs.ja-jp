---
title: Code Generation in a Build Process | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- text templates, build tasks
- text templates, transforming by using msbuild
ms.assetid: 4da43429-2a11-4d7e-b2e0-9e4af7033b5a
caps.latest.revision: 30
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: ae28c59f9c5f19e87b833c90e7dbc6bf3b7497ea
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74297930"
---
# <a name="code-generation-in-a-build-process"></a>ビルド処理でのコード生成
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]
Text transformation can be invoked as part of the build process of a Visual Studio solution. テキスト変換に特化したビルド タスクがあります。 T4 ビルド タスクはデザイン時テキスト テンプレートを実行し、また、実行時 (前処理済み) テキスト テンプレートをコンパイルします。

使用するビルド エンジンに応じて、ビルド タスクができることには違いが生じます。 When you build the solution in Visual Studio, a text template can access the Visual Studio API (EnvDTE) if the [hostspecific="true"](../modeling/t4-template-directive.md) attribute is set. しかし、コマンド ラインからソリューションをビルドするとき、または、Visual Studio 経由でサーバー ビルドを開始するときは、これは当てはまりません。 このような場合、ビルドは MSBuild によって実行され、別の T4 ホストが使用されます。

つまり、MSBuild でテキスト テンプレートをビルドすると、プロジェクト ファイル名などに同じようにアクセスできないことになります。 However, you can [pass environment information into text templates and directive processors by using build parameters](#parameters).

## <a name="buildserver"></a> Configure your machines

To enable build tasks on your development computer, install [Modeling SDK for Visual Studio](https://www.microsoft.com/download/details.aspx?id=48148).

If [your build server](https://msdn.microsoft.com/library/788443c3-0547-452e-959c-4805573813a9) runs on a computer on which Visual Studio is not installed, copy the following files to the build computer from your development machine. 最新のバージョン番号を「*」で置き換えます。

- $(ProgramFiles)\MSBuild\Microsoft\VisualStudio\v*.0\TextTemplating

  - Microsoft.VisualStudio.TextTemplating.Sdk.Host.*.0.dll

  - Microsoft.TextTemplating.Build.Tasks.dll

  - Microsoft.TextTemplating.targets

- $(ProgramFiles)\Microsoft Visual Studio *.0\VSSDK\VisualStudioIntegration\Common\Assemblies\v4.0

  - Microsoft.VisualStudio.TextTemplating.*.0.dll

  - Microsoft.VisualStudio.TextTemplating.Interfaces.*.0.dll (複数のファイル)

  - Microsoft.VisualStudio.TextTemplating.VSHost.*.0.dll

- $(ProgramFiles)\Microsoft Visual Studio *.0\Common7\IDE\PublicAssemblies\

  - Microsoft.VisualStudio.TextTemplating.Modeling.*.0.dll

## <a name="to-edit-the-project-file"></a>プロジェクト ファイルを編集するには

MSBuild の機能の一部を構成するには、プロジェクト ファイルを編集する必要があります。

In solution explorer, choose **Unload** from the context menu of your project. これにより XML エディターで .csproj または .vbproj ファイルを編集できるようになります。

When you’ve finished editing, choose **Reload**.

## <a name="import-the-text-transformation-targets"></a>テキスト変換ターゲットのインポート

.vbproj ファイルまたは .csproj ファイルで、次のような行を探します。

`<Import Project="$(MSBuildToolsPath)\Microsoft.CSharp.targets" />`

\- または

`<Import Project="$(MSBuildToolsPath)\Microsoft.VisualBasic.targets" />`

この行の後に、テキスト テンプレートのインポートを挿入します。

```xml
<!-- Optionally make the import portable across VS versions -->
  <PropertyGroup>
    <!-- Get the Visual Studio version – defaults to 10: -->
    <VisualStudioVersion Condition="'$(VisualStudioVersion)' == ''">10.0</VisualStudioVersion>
    <!-- Keep the next element all on one line: -->
    <VSToolsPath Condition="'$(VSToolsPath)' == ''">$(MSBuildExtensionsPath32)\Microsoft\VisualStudio\v$(VisualStudioVersion)</VSToolsPath>
  </PropertyGroup>

<!-- This is the important line: -->
  <Import Project="$(VSToolsPath)\TextTemplating\Microsoft.TextTemplating.targets" />
```

## <a name="transforming-templates-in-a-build"></a>ビルド時のテンプレートの変換

プロジェクト ファイルに挿入して変換タスクを制御できるプロパティがいくつかあります。

- すべてのビルドの開始時に変換タスクを実行します。

    ```xml
    <PropertyGroup>
        <TransformOnBuild>true</TransformOnBuild>
    </PropertyGroup>
    ```

- たとえばチェックアウトされているために、読み取り専用であるファイルを上書きします。

    ```xml
    <PropertyGroup>
        <OverwriteReadOnlyOutputFiles>true</OverwriteReadOnlyOutputFiles>
    </PropertyGroup>
    ```

- 毎回、すべてのテンプレートを変換します。

    ```xml
    <PropertyGroup>
        <TransformOutOfDateOnly>false</TransformOutOfDateOnly>
    </PropertyGroup>
    ```

     既定では、T4 MSBuild タスクは、テンプレート ファイル、または、インクルードされているファイル、または、テンプレートか使用するディレクティブ プロセッサによって前に読み込まれたファイルより出力ファイルが古い場合、出力ファイルを再生成します。 これは、テンプレートと出力ファイルの日付のみを比較する Visual Studio の [すべてのテンプレートの変換] コマンドよりも、はるかに強力な依存関係テストであることに注意してください。

プロジェクトでテキスト変換だけを実行するには、TransformAll タスクを呼び出します。

`msbuild myProject.csproj /t:TransformAll`

特定のテキスト テンプレートを変換するには、次のように実行します。

`msbuild myProject.csproj /t:Transform /p:TransformFile="Template1.tt"`

TransformFile ではワイルドカードを使用できます。

`msbuild dsl.csproj /t:Transform /p:TransformFile="GeneratedCode\**\*.tt"`

## <a name="source-control"></a>ソース管理

ソース管理システムと連携するような専用の機能は組み込まれていません。 ただし、独自の拡張機能を追加して、たとえば生成されたファイルのチェックアウトとチェックインを実行することはできます。既定では、テキスト変換タスクは読み取り専用ファイルを上書きしません。読み取り専用ファイルが見つかると、Visual Studio のエラー一覧にエラーが記録され、タスクは失敗します。

読み取り専用ファイルを上書きするには、次のプロパティを挿入します。

`<OverwriteReadOnlyOutputFiles>true</OverwriteReadOnlyOutputFiles>`

後処理のステップをカスタマイズしない限り、ファイルが上書きされるとエラー一覧に警告が記録されます。

## <a name="customizing-the-build-process"></a>ビルド処理のカスタマイズ

テキスト変換は、ビルド処理で他のタスクよりも前に実行されます。 `$(BeforeTransform)` プロパティと `$(AfterTransform)` プロパティを設定して、変換の前後に呼び出すタスクを定義できます。

```xml
<PropertyGroup>
    <BeforeTransform>CustomPreTransform</BeforeTransform>
    <AfterTransform>CustomPostTransform</AfterTransform>
  </PropertyGroup>
  <Target Name="CustomPreTransform">
    <Message Text="In CustomPreTransform..." Importance="High" />
  </Target>
  <Target Name="CustomPostTransform">
    <Message Text="In CustomPostTransform..." Importance="High" />
  </Target>
```

`AfterTransform` では、ファイルのリストを参照できます。

- GeneratedFiles: 処理中に出力されたファイルのリスト。 既存の読み取り専用ファイルを上書きしたファイルについては、%(GeneratedFiles.ReadOnlyFileOverwritten) が true になります。 これらのファイルは、ソース管理からチェックアウトできます。

- NonGeneratedFiles: 上書きされなかった読み取り専用ファイルのリスト。

  たとえば、GeneratedFiles をチェックアウトするタスクを定義します。

## <a name="outputfilepath-and-outputfilename"></a>OutputFilePath と OutputFileName

これらのプロパティを使用するのは MSBuild だけです。 Visual Studio のコード生成には影響しません。 これらは生成された出力ファイルを別のフォルダーまたはファイルにリダイレクトします。 対象となるフォルダーが既に存在する必要があります。

```xml
<ItemGroup>
  <None Include="MyTemplate.tt">
    <Generator>TextTemplatingFileGenerator</Generator>
    <OutputFilePath>MyFolder</OutputFilePath>
    <LastGenOutput>MyTemplate.cs</LastGenOutput>
  </None>
</ItemGroup>
```

リダイレクト先として便利なフォルダーは `$(IntermediateOutputPath).` です。

出力ファイル名を指定した場合、テンプレートの出力ディレクティブで指定された拡張子より優先されます。

```xml
<ItemGroup>
  <None Include="MyTemplate.tt">
    <Generator>TextTemplatingFileGenerator</Generator>
    <OutputFileName>MyOutputFileName.cs</OutputFileName>
    <LastGenOutput>MyTemplate.cs</LastGenOutput>
  </None>
</ItemGroup>
```

VS 内部で "すべて変換" 機能を使用してテンプレートを変換している場合、または単一ファイル ジェネレーターを実行している場合、OutputFileName または OutputFilePath を指定することはお勧めできません。 変換をどのようにして開始したのかに応じて、ファイル パスが変わります。 これは非常に混乱を招きます。

## <a name="adding-reference-and-include-paths"></a>参照パスとインクルード パスの追加

ホストには、テンプレートで参照されているアセンブリを検索する既定のパス セットがあります。 このパス セットを追加するには、次のように指定します。

```
<ItemGroup>
    <T4ReferencePath Include="$(VsIdePath)PublicAssemblies\" />
    <!-- Add more T4ReferencePath items here -->
</ItemGroup>
```

インクルード ファイルを検索するフォルダーを設定するには、セミコロン区切りのリストを指定します。 通常は、既存のフォルダー リストに追加します。

```
<PropertyGroup>
    <IncludeFolders>
$(IncludeFolders);$(MSBuildProjectDirectory)\Include;AnotherFolder;And\Another</IncludeFolders>
</PropertyGroup>
```

## <a name="parameters"></a> Pass build context data into the templates

プロジェクト ファイルでパラメーター値を設定できます。 For example, you can pass build properties and [environment variables](../msbuild/how-to-use-environment-variables-in-a-build.md):

```xml
<ItemGroup>
  <T4ParameterValues Include="ProjectFolder">
    <Value>$(ProjectDir)</Value>
    <Visible>false</Visible>
  </T4ParameterValues>
</ItemGroup>
```

テキスト テンプレートでは、template ディレクティブで `hostspecific` を設定します。 Use the [parameter](../modeling/t4-parameter-directive.md) directive to get values:

```
<#@template language="c#" hostspecific="true"#>
<#@ parameter type="System.String" name="ProjectFolder" #>
The project folder is: <#= ProjectFolder #>
```

## <a name="msbuild"></a> Using project properties in assembly and include directives

$(SolutionDir) などの Visual Studio のマクロは、MSBuild では動作しません。 その代わりに、プロジェクト プロパティを使用できます。

.csproj ファイルまたは .vbproj ファイルを編集してプロジェクトのプロパティを定義します。 この例では、`myLibFolder` という名前のプロパティを定義します。

```xml
<!-- Define a project property, myLibFolder: -->
<PropertyGroup>
    <myLibFolder>$(MSBuildProjectDirectory)\..\libs</myLibFolder>
</PropertyGroup>

<!-- Tell the MSBuild T4 task to make the property available: -->
<ItemGroup>
    <T4ParameterValues Include="myLibFolder">
      <Value>$(myLibFolder)</Value>
    </T4ParameterValues>
  </ItemGroup>
```

これで、assembly ディレクティブおよび include ディレクティブでプロジェクト プロパティを使用できます。

```
<#@ assembly name="$(myLibFolder)\MyLib.dll" #>
<#@ include file="$(myLibFolder)\MyIncludeFile.t4" #>
```

 これらのディレクティブは、MSBuild ホストおよび Visual Studio ホストの両方で T4parameterValues から値を取得します。

## <a name="q--a"></a>Q & A

**Why would I want to transform templates in the build server? I already transformed templates in Visual Studio before I checked in my code.**

インクルード ファイル、または、テンプレートで読み込まれる別のファイルを更新した場合、Visual Studio ではそのファイルは自動的に変換されません。 ビルドの一部としてテンプレートを変換すると、すべてが最新であることが保証されます。

**What other options are there for transforming text templates?**

- The [TextTransform utility](../modeling/generating-files-with-the-texttransform-utility.md) can be used in command scripts. ほとんどの場合、MSBuild を使用する方が簡単です。

- [VS 拡張機能内でのテキスト変換の呼び出し](../modeling/invoking-text-transformation-in-a-vs-extension.md)

- [Design-time text templates](../modeling/design-time-code-generation-by-using-t4-text-templates.md) are transformed by Visual Studio.

- [Run time text templates](../modeling/run-time-text-generation-with-t4-text-templates.md) are transformed at run time in your application.

## <a name="read-more"></a>関連項目

T4 MSbuild テンプレート、$ (VSToolsPath) \TextTemplating\Microsoft.TextTemplating.targets に優れたガイダンスがあります。

- [T4 テキスト テンプレートの作成](../modeling/writing-a-t4-text-template.md)
- [Visual Studio Visualization and Modeling SDK](https://go.microsoft.com/fwlink/?LinkID=185579)
- [Oleg Sych: Understanding T4:MSBuild Integration](https://github.com/olegsych/T4Toolbox)
