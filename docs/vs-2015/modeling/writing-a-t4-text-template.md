---
title: Writing a T4 Text Template | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- text templates, syntax
- text templates, guide
- text templates, functions that generate text
ms.assetid: 94328da7-953b-4e92-9587-648543d1f732
caps.latest.revision: 45
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: bcd5a4996db4a5e374baabe4f52d5fd1dbac2e5e
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74301124"
---
# <a name="writing-a-t4-text-template"></a>T4 テキスト テンプレートの作成
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

テキスト テンプレートには、そのテンプレートから生成されるテキストが含まれます。 For example, a template that creates a web page will contain "\<html>…" and all the other standard parts of an HTML page. Inserted into the template are *control blocks*, which are fragments of program code. コントロール ブロックはさまざまな値を提供すると共に、テキストの一部を条件付きにしたり、繰り返したりできるようにします。

 この構造によって、テンプレートの作成が簡単になります。生成されるファイルのプロトタイプを最初に作成しておき、結果を変化させるコントロール ブロックは徐々に挿入するという手法を利用できるためです。

 テキスト テンプレートは次の要素から構成されます。

- **Directives** - elements that control how the template is processed.

- **Text blocks** - content that is copied directly to the output.

- **Control blocks** - program code that inserts variable values into the text, and controls conditional or repeated parts of the text.

  To try the examples in this topic, copy them into a template file as described in [Design-Time Code Generation by using T4 Text Templates](../modeling/design-time-code-generation-by-using-t4-text-templates.md). After editing the template file, save it, and then inspect the output **.txt** file.

## <a name="directives"></a>ディレクティブ
 テキスト テンプレート ディレクティブは、変換コードと出力ファイルの生成方法に関する一般的な指示をテキスト テンプレート エンジンに与えます。

 たとえば、次のディレクティブでは、出力ファイルに .txt という拡張子を付けるように指定しています。

```

<#@ output extension=".txt" #>
```

 For more information about directives, see [T4 Text Template Directives](../modeling/t4-text-template-directives.md).

## <a name="text-blocks"></a>テキスト ブロック
 テキスト ブロックのテキストは、出力ファイルに直接挿入されます。 テキスト ブロックに特別な書式指定はありません。 たとえば、次のテキスト テンプレートからは、"Hello" という単語を含むテキスト ファイルが生成されます。

```
<#@ output extension=".txt" #>
Hello
```

## <a name="control-blocks"></a>コントロール ブロック
 コントロール ブロックは、テンプレートの変換に使用されるプログラム コードのセクションです。 既定の言語は C# ですが、次のディレクティブをファイルの先頭に記述すると、[!INCLUDE[vbprvb](../includes/vbprvb-md.md)] を使用できます。

```
<#@ template language="VB" #>
```

 コントロール ブロックでのコードの記述に使用する言語は、生成されるテキストの言語とは関係ありません。

### <a name="standard-control-blocks"></a>標準コントロール ブロック
 標準コントロール ブロックは、出力ファイルの一部を生成するプログラム コードのセクションです。

 テンプレート ファイルには、任意の数のテキスト ブロックと標準コントロール ブロックを混在させることができます。 ただし、コントロール ブロックを他のコントロール ブロックの内部に配置することはできません。 それぞれの標準コントロール ブロックは、`<# ... #>` という記号で区切られます。

 たとえば、次のコントロール ブロックとテキスト ブロックを使用した場合、出力ファイルには "0, 1, 2, 3, 4 Hello!" という行が含まれます。

```

      <#
    for(int i = 0; i < 4; i++)
    {
        Write(i + ", ");
    }
    Write("4");
#> Hello!
```

 明示的な `Write()` ステートメントを使用する代わりに、インタリーブ テキストとインタリーブ コードを使用できます。 The following example prints "Hello!" four times:

```
<#
    for(int i = 0; i < 4; i++)
    {
#>
Hello!
<#
    }
#>
```

 テキスト ブロックは、`Write();` ステートメントを使用できる場所であれば、どこにでも挿入できます。

> [!NOTE]
> When you embed a text block within a compound statement such as a loop or conditional, always use braces {...} to contain the text block.

### <a name="expression-control-blocks"></a>式コントロール ブロック
 式コントロール ブロックでは、式を評価して文字列に変換します。 出力ファイルにはその文字列が挿入されます。

 式コントロール ブロックは `<#= ... #>` という記号で区切られます。

 たとえば、次のコントロール ブロックを使用した場合、出力ファイルには "5" が含まれます。

```
<#= 2 + 3 #>
```

 Notice that the opening symbol has three characters "<#=".

 式には、スコープ内の任意の変数を含めることができます。 たとえば、次のブロックでは、数値を含む複数の行が出力されます。

```
<#@ output extension=".txt" #>
<#
    for(int i = 0; i < 4; i++)
    {
#>
This is hello number <#= i+1 #>: Hello!
<#
    }
#>
```

### <a name="class-feature-control-blocks"></a>クラス機能コントロール ブロック
 クラス機能コントロール ブロックでは、メインの変換の対象から除外する、プロパティやメソッドなどのコードを定義します。 クラス機能ブロックは、ヘルパー関数でよく使用されます。  Typically, class feature blocks are placed in separate files so that they can be [included](#Include) by more than one text template.

 クラス機能コントロール ブロックは `<#+ ... #>` という記号で区切られます。

 たとえば、次のテンプレート ファイルでは、メソッドを宣言して使用しています。

```
<#@ output extension=".txt" #>
Squares:
<#
    for(int i = 0; i < 4; i++)
    {
#>
    The square of <#= i #> is <#= Square(i+1) #>.
<#
    }
#>
That is the end of the list.
<#+   // Start of class feature block
private int Square(int i)
{
    return i*i;
}
#>
```

 クラス機能は、それを記述するファイルの末尾に配置する必要があります。 ただし、`<#@include#>` を使用すると、`include` ディレクティブの後ろに標準ブロックとテキストが続く場合でも、クラス機能を含むファイルをインクルードすることができます。

 For more information about control blocks, see [Text Template Control Blocks](../modeling/text-template-control-blocks.md).

### <a name="class-feature-blocks-can-contain-text-blocks"></a>クラス機能ブロックにはテキスト ブロックを含めることができる
 テキストを生成するメソッドを記述できます。 (例:

```
List of Squares:
<#
   for(int i = 0; i < 4; i++)
   {  WriteSquareLine(i); }
#>
End of list.
<#+   // Class feature block
private void WriteSquareLine(int i)
{
#>
   The square of <#= i #> is <#= i*i #>.
<#+
}
#>
```

 テキストを生成するメソッドは、複数のテンプレートでインクルードできる独立したファイルに配置すると特に便利です。

## <a name="using-external-definitions"></a>外部定義の使用

### <a name="assemblies"></a>アセンブリ
 テンプレートのコード ブロックでは、最もよく使用される .NET アセンブリ (System.dll など) で定義されている型を使用できます。 さらに、他の .NET アセンブリや独自のアセンブリを参照することもできます。 パス名、つまりアセンブリの厳密な名前を指定できます。

```
<#@ assembly name="System.Xml" #>
```

 絶対パス名を使用するか、パス名で標準マクロ名を使用する必要があります。 (例:

```
<#@ assembly name="$(SolutionDir)library\MyAssembly.dll" #>
```

 For a list of macros, see [Common Macros for Build Commands and Properties](https://msdn.microsoft.com/library/239bd708-2ea9-4687-b264-043f1febf98b).

 The assembly directive has no effect in a [preprocessed text template](../modeling/run-time-text-generation-with-t4-text-templates.md).

 For more information, see [T4 Assembly Directive](../modeling/t4-assembly-directive.md).

### <a name="namespaces"></a>名前空間
 import ディレクティブは、C# での `using` 句または Visual Basic での `imports` 句と同じ働きをします。 これを使用すると、完全修飾名を使用せずにコードで型を参照できます。

```
<#@ import namespace="System.Xml" #>
```

 `assembly` ディレクティブと `import` ディレクティブは、必要に応じていくつでも使用できます。 これらのディレクティブは、テキスト ブロックとコントロール ブロックの前に配置する必要があります。

 For more information, see [T4 Import Directive](../modeling/t4-import-directive.md).

### <a name="Include"></a> Including code and text
 `include` ディレクティブを使用すると、別のテンプレート ファイルのテキストを挿入できます。 たとえば、次のディレクティブでは、`test.txt` のコンテンツが挿入されます。

 `<#@ include file="c:\test.txt" #>`

 インクルードされたコンテンツは、インクルード先のテキスト テンプレートに元から含まれていた場合とほとんど同じように処理されます。 ただし、include ディレクティブの後に通常のテキスト ブロックと標準コントロール ブロックが続く場合でも、クラス機能ブロック (`<#+...#>`) を含むファイルをインクルードすることができます。

 For more information, see [T4 Include Directive](../modeling/t4-include-directive.md).

### <a name="utility-methods"></a>ユーティリティ メソッド
 `Write()` をはじめ、コントロール ブロックでいつでも使用できるメソッドがいくつかあります。 これには、出力のインデントに役立つメソッドや、エラーの報告に役立つメソッドが含まれます。

 独自のユーティリティ メソッドのセットを記述することもできます。

 For more information, see [Text Template Utility Methods](../modeling/text-template-utility-methods.md).

## <a name="transforming-data-and-models"></a>データとモデルの変換
 テキスト テンプレートが最も役に立つのは、モデル、データベース、データ ファイルなどのソースのコンテンツに基づいてマテリアルを生成する場合です。 テンプレートによってデータが抽出され、その書式が再設定されます。 テンプレートのコレクションでは、このようなソースを複数のファイルに変換できます。

 ソース ファイルを読み取る方法はいくつかあります。

 **Read a file in the text template**. これは、テンプレートにデータを取り込む方法としては最も簡単です。

```
<#@ import namespace="System.IO" #>
<# string fileContent = File.ReadAllText(@"C:\myData.txt"); ...
```

 **Load a file as a navigable model**. より効果的な方法は、テキスト テンプレート コードでナビゲートできるモデルとしてデータを読み取ることです。 たとえば、XML ファイルを読み込み、XPath 式でそのファイル内をナビゲートできます。 You could also use [xsd.exe](https://go.microsoft.com/fwlink/?LinkId=178765) to create a set of classes with which you can read the XML data.

 **Edit the model file in a diagram or form.** [!INCLUDE[dsl](../includes/dsl-md.md)] provides tools that let you edit a model as a diagram or Windows form. このため、生成されたアプリケーションのユーザーと、モデルについて効率的に話し合うことができます。 [!INCLUDE[dsl](../includes/dsl-md.md)]では、モデルの構造を反映した、厳密に型指定されたクラスのセットも作成できます。 For more information, see [Generating Code from a Domain-Specific Language](../modeling/generating-code-from-a-domain-specific-language.md).

 **Use a UML model**. UML モデルからコードを生成できます。 これには、使い慣れた表記法を使用して、モデルを図として編集できるという利点があります。 また、図をデザインする必要もありません。 For more information, see [Generate files from a UML model](../modeling/generate-files-from-a-uml-model.md).

### <a name="relative-file-paths-in-design-time-templates"></a>デザイン時テンプレートの相対ファイル パス
 In a [design-time text template](../modeling/design-time-code-generation-by-using-t4-text-templates.md), if you want to reference a file in a location relative to the text template, use `this.Host.ResolvePath()`. また、`hostspecific="true"` ディレクティブで `template` を設定する必要もあります。

```csharp
<#@ template hostspecific="true" language="C#" #>
<#@ output extension=".txt" #>
<#@ import namespace="System.IO" #>
<#
 // Find a path within the same project as the text template:
 string myFile = File.ReadAllText(this.Host.ResolvePath("MyFile.txt"));
#>
Content of MyFile.txt is:
<#= myFile #>

```

 ホストから提供される他のサービスを取得することもできます。 For more information, see [Accessing Visual Studio or other Hosts from a Template](https://msdn.microsoft.com/0556f20c-fef4-41a9-9597-53afab4ab9e4).

### <a name="design-time-text-templates-run-in-a-separate-appdomain"></a>別の AppDomain で実行されるデザイン時テキスト テンプレート
 You should be aware that a [design-time text template](../modeling/design-time-code-generation-by-using-t4-text-templates.md) runs in an AppDomain that is separate from the main application. ほとんどの場合、これは重要ではありませんが、一部の複雑な状況で制限が生じることがあります。 たとえば、別のサービスからテンプレート内またはテンプレート外のデータを渡す場合、そのサービスでシリアル化可能な API を提供する必要があります。

 (This isn’t true of a [run-time text template](../modeling/run-time-text-generation-with-t4-text-templates.md), which provides code that is compiled along with the rest of your code.)

## <a name="editing-templates"></a>テンプレートの編集
 拡張機能マネージャーのオンライン ギャラリーからは、専用のテキスト テンプレート エディターをダウンロードできます。 On the **Tools** menu, click **Extension Manager**. Click **Online Gallery**, and then use the search tool.

## <a name="related-topics"></a>関連トピック

|タスク|トピック|
|----------|-----------|
|テンプレートを作成する。|[T4 テキスト テンプレートの記述に関するガイドライン](../modeling/guidelines-for-writing-t4-text-templates.md)|
|プログラム コードを使用してテキストを生成する。|[Text Template Structure](../modeling/writing-a-t4-text-template.md)|
|[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ソリューション内にファイルを生成する。|[T4 テキスト テンプレートを使用したデザイン時コード生成](../modeling/design-time-code-generation-by-using-t4-text-templates.md)|
|[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] の外部でテキストの生成を行う。|[TextTransform ユーティリティを使用したファイルの生成](../modeling/generating-files-with-the-texttransform-utility.md)|
|ドメイン固有言語の形式でデータを変換する。|[ドメイン固有言語からのコード生成](../modeling/generating-code-from-a-domain-specific-language.md)|
|独自のデータ ソースを変換するためのディレクティブ プロセッサを作成する。|[T4 テキスト変換のカスタマイズ](../modeling/customizing-t4-text-transformation.md)|
