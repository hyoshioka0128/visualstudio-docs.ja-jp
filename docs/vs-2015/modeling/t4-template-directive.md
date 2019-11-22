---
title: T4 Template Directive | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: 2b0a8e04-6fee-4c6c-b086-e49fc728a3ed
caps.latest.revision: 12
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: d3a17275730cd093f8f9fa433aa28c7f9ca86e80
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74298144"
---
# <a name="t4-template-directive"></a>T4 テンプレート ディレクティブ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

通常、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] の T4 テキスト テンプレートは、テンプレートの処理方法を指定する `template` ディレクティブで始まります。 テキスト テンプレートおよびそれに含まれるファイルには、template ディレクティブを 1 つしか含めることができません。

 For a general overview of writing text templates, see [Writing a T4 Text Template](../modeling/writing-a-t4-text-template.md).

## <a name="using-the-template-directive"></a>template ディレクティブの使用

```
<#@ template [language="VB"] [compilerOptions="options"] [culture="code"] [debug="true"] [hostspecific="true"] [inherits="templateBaseClass"] [visibility="internal"] [linePragmas="false"] #>
```

 `template` ディレクティブには、変換のさまざまな側面を指定できる属性がいくつかあります。 属性はすべて省略可能です。

## <a name="compileroptions-attribute"></a>compilerOptions 属性
 例 : `compilerOptions="optimize+"`

 Valid values: Any valid compiler options. For more information, see [C# Compiler Options Listed by Category](https://msdn.microsoft.com/library/96437ecc-6502-4cd3-b070-e9386a298e83) and [Visual Basic Compiler Options Listed by Category](https://msdn.microsoft.com/library/fbe36f7a-7cfa-4f77-a8d4-2be5958568e3).

 実行時 (前処理された) テンプレートでは無視されます。

 テンプレートが [!INCLUDE[csprcs](../includes/csprcs-md.md)] または [!INCLUDE[vb_current_short](../includes/vb-current-short-md.md)] に変換されている場合にこれらのオプションが適用され、生成されたコードがコンパイルされます。

## <a name="culture-attribute"></a>culture 属性
 例 : `culture="de-CH"`

 Valid values: "", the invariant culture, which is the default.

 xx-XX 形式の文字列で表現されたカルチャ。 たとえば、en-US、ja-JP、de-CH、de-DE などがあります。 詳細については、「<xref:System.Globalization.CultureInfo?displayProperty=fullName>」を参照してください。

 culture 属性では、式ブロックをテキストに変換する際に使用するカルチャを指定します。

## <a name="debug-attribute"></a>debug 属性
 例:

```
debug="true"
```

 Valid values: `true, false`. False が既定値です。

 `debug` 属性が `true` の場合、デバッガーでテンプレート内の中断または例外の発生位置を正確に特定できるようにする情報が中間コード ファイルに出力されるようになります。

 For design-time templates the intermediate code file will be written to your **%TEMP%** directory.

 To run a design-time template in the debugger, save the text template, then open the shortcut menu of the text template in Solution Explorer, and choose **Debug T4 Template**.

## <a name="hostspecific-attribute"></a>hostspecific 属性
 例:

```
hostspecific="true"
```

 Valid values: `true, false, trueFromBase`. False が既定値です。

 この属性の値を `true` に設定した場合、テキスト テンプレートによって生成されたクラスに、`Host` というプロパティが追加されます。 The property is a reference to the host of the transformation engine, and is declared as [ITextTemplatingEngineHost](/previous-versions/visualstudio/visual-studio-2012/bb126505(v=vs.110)). カスタム ホストを定義している場合は、そのカスタム ホストの型にキャストできます。

 このプロパティの型はホストの型に依存するため、特定のホストとのみ連携するテキスト テンプレートを作成している場合以外、利用価値はありません。 It’s applicable to [design-time templates](../modeling/design-time-code-generation-by-using-t4-text-templates.md), but not [run-time templates](../modeling/run-time-text-generation-with-t4-text-templates.md).

 `hostspecific` が `true` で、なおかつ [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] を使用している場合は、`this.Host` を IServiceProvider にキャストして、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] の機能にアクセスすることができます。 また、`Host.ResolvePath(filename)` を使用して、プロジェクトのファイルの絶対パスを取得することもできます。 (例:

```csharp
<#@ template debug="false" hostspecific="true" language="C#" #>
<#@ output extension=".txt" #>
<#@ assembly name="EnvDTE" #>
<#@ import namespace="EnvDTE" #>
<#@ import namespace="System.IO" #>
<# // Get the Visual Studio API as a service:
 DTE dte = ((IServiceProvider)this.Host).GetCOMService(typeof(DTE)) as DTE;
#>
Number of projects in this solution: <#=  dte.Solution.Projects.Count #>

<#
 // Find a path within the current project:
 string myFile = File.ReadAllText(this.Host.ResolvePath("MyFile.txt"));
#>
Content of myFile is:
<#= myFile #>

```

 `inherits` 属性と `hostspecific` 属性を一緒に使用する場合は、派生クラスで host="trueFromBase"、基底クラスで host="true" を指定します。 これで、生成されるコードで `Host` プロパティの定義が重複することを回避できます。

## <a name="language-attribute"></a>language 属性
 例 : `language="VB"`

 Valid values: `C#` (default)

 `VB`

 The language attribute specifies the language ([!INCLUDE[vbprvb](../includes/vbprvb-md.md)] or [!INCLUDE[csprcs](../includes/csprcs-md.md)]) to use for the source code in statement and expression blocks. 出力の生成元である中間コード ファイルでこの言語が使用されます。 この言語はテンプレートで生成される言語とは無関係であり、どのような種類のテキストであってもかまいません。

 (例:

```vb
<#@ template language="VB" #>
<#@ output extension=".txt" #>
Squares of numbers:
<#
  Dim number As Integer
  For number = 1 To 4
#>
  Square of <#= number #> is <#= number * number #>
<#
  Next number
#>

```

## <a name="inherits-attribute"></a>inherits 属性
 テンプレートのプログラム コードを別のクラスから継承できることを指定できます。クラスは、テキスト テンプレートから生成することもできます。

### <a name="inheritance-in-a-run-time-preprocessed-text-template"></a>実行時 (前処理された) テキスト テンプレートでの継承
 実行時テキスト テンプレート間で継承を使用して、複数の派生バリアントを含む基本テンプレートを作成できます。 Run-time templates are those that have the **Custom Tool** property set to **TextTemplatingFilePreprocessor**. 実行時テンプレートでは、そのテンプレートに定義されているテキストを作成するために、アプリケーションで呼び出すことができるコードが生成されます。 For more information, see [Run-Time Text Generation with T4 Text Templates](../modeling/run-time-text-generation-with-t4-text-templates.md).

 `inherits` 属性を指定しない場合は、テキスト テンプレートから基底クラスと派生クラスが生成されます。 `inherits` 属性を指定すると、派生クラスだけが生成されます。 基底クラスは手動で作成できますが、派生クラスで使用するメソッドを提供する必要があります。

 通常は、前処理された別のテンプレートを基底クラスとして指定します。 基本テンプレートでは、派生テンプレートのテキストとインタリーブできる共通のテキスト ブロックを提供します。 クラス機能ブロック (`<#+ ... #>`) を使用して、テキスト フラグメントを含むメソッドを定義できます。 たとえば、基本テンプレートに出力テキストのフレームワークを配置し、派生テンプレートでオーバーライドできる仮想メソッドを提供することができます。

 実行時 (前処理された) テキスト テンプレートの BaseTemplate.tt:

```scr
This is the common header.
<#
  SpecificFragment1();
#>
A common central text.
<#
  SpecificFragment2();
#>
This is the common footer.
<#+
  // Declare abstract methods
  protected virtual void SpecificFragment1() { }
  protected virtual void SpecificFragment2() { }
#>

```

 実行時 (前処理された) テキスト テンプレートの DerivedTemplate1.tt:

```csharp
<#@ template language="C#" inherits="BaseTemplate" #>
<#
  // Run the base template:
  base.TransformText();
#>
<#+
// Provide fragments specific to this derived template:
protected override void SpecificFragment1()
{
#>
   Fragment 1 for DerivedTemplate1
<#+
}
protected override void SpecificFragment2()
{
#>
   Fragment 2 for DerivedTemplate1
<#+
}
#>

```

 DerivedTemplate1 を呼び出すアプリケーション コード:

```csharp
Console.WriteLine(new DerivedTemplate().TransformText());
```

 結果の出力:

```
This is the common header.
   Fragment 1 for DerivedTemplate1
A common central text.
   Fragment 2 for DerivedTemplate1
This is the common footer.
```

 さまざまなプロジェクトの基底クラスと派生クラスを作成できます。 派生プロジェクトの参照に基本プロジェクトまたは基本アセンブリを追加することを忘れないでください。

 手動で作成した通常のクラスを基底クラスとして使用することもできます。 基底クラスでは、派生クラスで使用するメソッドを提供する必要があります。

> [!WARNING]
> `inherits` 属性と `hostspecific` 属性を一緒に使用する場合は、派生クラスで hostspecific="trueFromBase"、基底クラスで host="true" を指定します。 これで、生成されるコードで `Host` プロパティの定義が重複することを回避できます。

### <a name="inheritance-in-a-design-time-text-template"></a>デザイン時テキスト テンプレートでの継承
 A design-time text template is a file for which **Custom Tool** is set to **TextTemplatingFileGenerator**. このテンプレートでは、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] プロジェクトの一部となるコードまたはテキストの出力ファイルが生成されます。 出力ファイルを生成するために、テンプレートは、まず中間プログラム コード ファイルに変換されます。通常、このファイルは表示されません。 `inherits` 属性では、この中間コードの基底クラスを指定します。

 デザイン時テキスト テンプレートの場合、<xref:Microsoft.VisualStudio.TextTemplating.TextTransformation?displayProperty=fullName> から派生した基底クラスを指定できます。 `<#@assembly#>` ディレクティブを使用して、基底クラスを含むアセンブリまたはプロジェクトを読み込みます。

 For more information, see ["Inheritance in Text Templates" in Gareth Jones’ Blog](https://go.microsoft.com/fwlink/?LinkId=208373).

## <a name="linepragmas-attribute"></a>LinePragmas 属性
 例 : `linePragmas="false"`

 Valid values: `true` (default)

 `false`

 この属性を false に設定すると、生成されたコード内で行番号を識別するタグが削除されます。 つまり、コンパイラは生成されたコードの行番号を使用してエラーを報告します。このため、デバッグ時の選択肢が増えて、テキスト テンプレートをデバッグするか、それとも生成されたコードをデバッグするかを選択できます。

 この属性は、プラグマの絶対ファイル名によってソース コード管理下で無駄なマージが発生している場合にも役立ちます。

## <a name="visibility-attribute"></a>Visibility 属性
 例 : `visibility="internal"`

 Valid values: `public` (default)

 `internal`

 実行時テキスト テンプレートでは、これは生成されたクラスの可視性属性を設定します。 既定では、クラスはコードのパブリック API の一部ですが、`visibility="internal"` を設定すると、自分のコードだけがそのテキスト生成クラスを使用するようにできます。
