---
title: T4 インクルード ディレクティブ
ms.date: 11/04/2016
ms.topic: reference
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a1ee58c29be3c4dfb5e2148c54464a7a511d1839
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75591854"
---
# <a name="t4-include-directive"></a>T4 インクルード ディレクティブ

`<#@include#>`ディレクティブにより、Visual Studio でのテキスト テンプレートにおいて、別のファイルからテキストをインクルードすることができます。 `include` ディレクティブは、テキスト テンプレートに含まれる最初のクラス機能ブロック (`<#+ ... #>`) の前の任意の場所に配置できます。 インクルード ファイルに、`include` ディレクティブや他のディレクティブを含めることもできます。 これにより、テンプレート間でテンプレート コードや定型句を共有できるようになります。

## <a name="using-include-directives"></a>include ディレクティブの使用

```
<#@ include file="filePath" [once="true"] #>
```

- `filePath` は、絶対パスでも、現在のテンプレートファイルからの相対パスでもかまいません。

   さらに、特定の Visual Studio 拡張機能は、インクルード ファイルを検索する独自のディレクトリを指定することがあります。 たとえば、Visualization and Modeling SDK (DSL) ツールをインストールしたら、次のフォルダーがインクルード一覧に追加されます:`Program Files\Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft\DSL SDK\DSL Designer\11.0\TextTemplates`

   追加されるこれらのインクルード フォルダーは、インクルード ファイルの拡張子によって異なります。 たとえば、DSL ツールのインクルード フォルダーは、インクルード ファイルの拡張子が `.tt` の場合にのみ追加されます。

- `filePath` には、"%" で区切られた環境変数を含めることもできます。 例:

  ```
  <#@ include file="%HOMEPATH%\MyIncludeFile.t4" #>
  ```

- インクルード ファイルの名前に、拡張子 `".tt"` を使用する必要はありません。

   必要に応じて、インクルード ファイルには、`".t4"` など別の拡張子を使用できます。 これは、`.tt`ファイルをプロジェクトに追加すると、Visual Studio が自動的に、**カスタム ツール**プロパティを`TextTemplatingFileGenerator`に設定するためです。 通常、インクルード ファイルを個別に変換することは望ましくありません。

   一方、ファイルの拡張子によって、インクルード ファイルの検索先となる追加フォルダーが決まる場合があることに注意してください。 これは、インクルード ファイルに他のファイルが含まれている場合に重要となります。

- インクルードされたコンテンツは、インクルード先のテキスト テンプレートに元から含まれていた場合とほとんど同じように処理されます。 ただし、`<#+...#>` ディレクティブの後に通常のテキスト ブロックと標準コントロール ブロックが続く場合でも、クラス機能ブロック (`include`) を含むファイルをインクルードすることができます。

- 1 つ以上のインクルード ファイルが呼び出された場合でも、テンプレートが 1 回だけインクルードされることを確実にするためには、`once="true"`を使用します。

   この機能により、その他のいくつかのスニペットが既に含まれていることを気にせずに、再利用可能な T4 スニペットのライブラリを構築することが容易になります。  たとえば、テンプレートを処理し C# コードの生成を処理する非常に短いスニペットのライブラリがあるとします。  これらは、例外を生成するなどのタスク固有なユーティリティによって使用され、複数のアプリケーション固有の任意のテンプレートから使用されます。 依存関係グラフを描画すると、何回もインクルードされるスニペットがあることがわかります。 ただし、`once` パラメーターが指定されると、以降はインクルードが無効になります。

  **MyTextTemplate.tt:**

```
<#@ output extension=".txt" #>
Output message 1 (from top template).
<#@ include file="TextFile1.t4"#>
Output message 5 (from top template).
<#
   GenerateMessage(6); // defined in TextFile1.t4
   AnotherGenerateMessage(7); // defined in TextFile2.t4
#>
```

 **TextFile1.t4:**

```
   Output Message 2 (from included file).
<#@ include file="TextFile2.t4" #>
   Output Message 4 (from included file).
<#+ // Start of class feature control block.
void GenerateMessage(int n)
{
#>
   Output Message <#= n #> (from GenerateMessage method).
<#+
}
#>
```

 **TextFile2.t4:**

```
        Output Message 3 (from included file 2).
<#+ // Start of class feature control block.
void AnotherGenerateMessage(int n)
{
#>
       Output Message <#= n #> (from AnotherGenerateMessage method).
<#+
}
#>
```

 **生成されたファイル：MyTextTemplate.txt**

```
Output message 1 (from top template).
   Output Message 2 (from included file).
        Output Message 3 (from included file 2).

   Output Message 4 (from included file).

Output message 5 (from top template).
   Output Message 6 (from GenerateMessage method).
       Output Message 7 (from AnotherGenerateMessage method).
```

## <a name="msbuild"></a>MSBuild および Visual Studio でのプロジェクト プロパティの使用
 include ディレクティブで $ (solutiondir) などの Visual Studio マクロを使用できますが、MSBuild では動作しません。 ビルド コンピューターでテンプレートを変換する場合、代わりにプロジェクトのプロパティを使用する必要があります。

 .csproj ファイルまたは .vbproj ファイルを編集してプロジェクトのプロパティを定義します。 この例では、`myIncludeFolder` という名前のプロパティを定義します。

```xml
<!-- Define a project property, myIncludeFolder: -->
<PropertyGroup>
    <myIncludeFolder>$(MSBuildProjectDirectory)\..\libs</myIncludeFolder>
</PropertyGroup>

<!-- Tell the MSBuild T4 task to make the property available: -->
<ItemGroup>
    <T4ParameterValues Include="myIncludeFolder">
      <Value>$(myIncludeFolder)</Value>
    </T4ParameterValues>
  </ItemGroup>
```

 これで、Visual Studio および MSBuild の両方で正しく変換できるテキスト テンプレートでプロジェクトのプロパティを使用できます。

```
<#@ include file="$(myIncludeFolder)\defs.tt" #>
```
