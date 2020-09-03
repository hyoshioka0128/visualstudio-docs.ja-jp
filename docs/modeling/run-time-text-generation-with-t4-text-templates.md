---
title: T4 テキスト テンプレートを使用した実行時テキスト生成
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- CSharp
- VB
helpviewer_keywords:
- Preprocessed Text Template project item
- TextTemplatingFilePreprocessor custom tool
- text templates, TransformText() method
- text templates, generating files at run time
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 344e15b69bf3e8308c62c6fa1074720b0cd7618d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85520836"
---
# <a name="run-time-text-generation-with-t4-text-templates"></a>T4 テキスト テンプレートを使用した実行時テキスト生成

実行時に、Visual Studio ランタイムテキストテンプレートを使用して、アプリケーションにテキスト文字列を生成できます。 アプリケーションを実行するコンピューターに Visual Studio がインストールされている必要はありません。 ランタイムテンプレートは、コンパイル時にテンプレートによって実行時に実行されるコードが生成されるため、"前処理されたテキストテンプレート" と呼ばれることがあります。

各テンプレートは、生成された文字列とプログラムコードのフラグメントに表示されるテキストを組み合わせたものです。 プログラムフラグメントでは、文字列の変数部分の値を指定すると共に、条件と反復部分も制御します。

たとえば、HTML レポートを作成するアプリケーションでは、次のテンプレートを使用できます。

```html
<#@ template language="C#" #>
<html><body>
<h1>Sales for Previous Month</h2>
<table>
    <# for (int i = 1; i <= 10; i++)
       { #>
         <tr><td>Test name <#= i #> </td>
             <td>Test value <#= i * i #> </td> </tr>
    <# } #>
 </table>
This report is Company Confidential.
</body></html>
```

テンプレートは HTML ページであり、変数部分がプログラムコードに置き換えられていることに注意してください。 このようなページのデザインを開始するには、HTML ページの静的なプロトタイプを作成します。 次に、テーブルやその他の変数部分を、1つの場合によって異なる内容を生成するプログラムコードに置き換えることができます。

アプリケーションでテンプレートを使用すると、出力の最終的な形式を簡単に確認できるようになります。たとえば、長い一連の write ステートメントのようになります。 出力形式を変更することは、より簡単で信頼性が高くなります。

## <a name="creating-a-run-time-text-template-in-any-application"></a>任意のアプリケーションでのランタイムテキストテンプレートの作成

### <a name="to-create-a-run-time-text-template"></a>実行時テキストテンプレートを作成するには

1. ソリューションエクスプローラーのプロジェクトのショートカットメニューで、[ **Add**  >  **新しい項目**の追加] を選択します。

2. [ **新しい項目の追加** ] ダイアログボックスで、[ **ランタイムテキストテンプレート**] を選択します。 (Visual Basic**共通項目**  >  の表示 **[全般**]。)

3. テンプレートファイルの名前を入力します。

    > [!NOTE]
    > テンプレートファイル名は、生成されたコードでクラス名として使用されます。 したがって、スペースや句読点を指定することはできません。

4. **[追加]** をクリックします。

    拡張子が **.tt**の新しいファイルが作成されます。 その **カスタムツール** プロパティは、 **Texttemplatingfilepreprocessor プロセッサ**に設定されています。 次の行が含まれています。

    ```
    <#@ template language="C#" #>
    <#@ assembly name="System.Core" #>
    <#@ import namespace="System.Linq" #>
    <#@ import namespace="System.Text" #>
    <#@ import namespace="System.Collections.Generic" #>
    ```

## <a name="converting-an-existing-file-to-a-run-time-template"></a>既存のファイルを実行時テンプレートに変換する

テンプレートを作成するには、出力の既存の例を変換することをお勧めします。 たとえば、アプリケーションで HTML ファイルを生成する場合は、プレーン HTML ファイルを作成することから始めます。 正しく動作し、その外観が正しいことを確認します。 次に、それを Visual Studio プロジェクトに追加し、テンプレートに変換します。

### <a name="to-convert-an-existing-text-file-to-a-run-time-template"></a>既存のテキストファイルを実行時テンプレートに変換するには

1. ファイルを Visual Studio プロジェクトに含めます。 ソリューションエクスプローラーのプロジェクトのショートカットメニューで、[ **Add**  >  **既存項目**の追加] を選択します。

2. ファイルの **カスタムツール** プロパティを **Texttemplatingfilepreprocessor プロセッサ**に設定します。 ソリューションエクスプローラーのファイルのショートカットメニューで、[ **プロパティ**] を選択します。

    > [!NOTE]
    > プロパティが既に設定されている場合は、Texttemplatingfilepreprocessor では**TextTemplatingFileGenerator**なく**texttemplatingfilepreprocessor**であることを確認します。 これは、既に拡張子が .tt のファイルをインクルードした場合に発生する可能性があり **ます**。

3. ファイル名拡張子を **.tt**に変更します。 この手順は省略可能ですが、正しくないエディターでファイルを開くことを避けるのに役立ちます。

4. ファイル名のメイン部分から、スペースまたは句読点を削除します。 たとえば、"My Web Page.tt" は正しくありませんが、"MyWebPage.tt" は正しいです。 ファイル名は、生成されたコードでクラス名として使用されます。

5. ファイルの先頭に次の行を挿入します。 Visual Basic のプロジェクトで作業している場合は、"C#" を "VB" に置き換えます。

    `<#@ template language="C#" #>`

## <a name="the-content-of-the-run-time-template"></a>ランタイムテンプレートの内容

### <a name="template-directive"></a>テンプレートディレクティブ

ファイルを作成したときと同じように、テンプレートの最初の行を保持します。

`<#@ template language="C#" #>`

言語パラメーターは、プロジェクトの言語によって異なります。

### <a name="plain-content"></a>プレーンコンテンツ

アプリケーションで生成するテキストが含まれるように .tt ファイルを編集し **ます** 。 たとえば、次のように入力します。

```html
<html><body>
<h1>Sales for January</h2>
<!-- table to be inserted here -->
This report is Company Confidential.
</body></html>
```

### <a name="embedded-program-code"></a>埋め込みプログラムコード

プログラムコードは、との間に挿入でき `<#` `#>` ます。 たとえば、次のように入力します。

```csharp
<table>
    <# for (int i = 1; i <= 10; i++)
       { #>
         <tr><td>Test name <#= i #> </td>
             <td>Test value <#= i * i #> </td> </tr>
    <# } #>
 </table>
```

```vb
<table>
<#
    For i As Integer = 1 To 10
#>
    <tr><td>Test name <#= i #> </td>
      <td>Test value <#= i*i #> </td></tr>
<#
    Next
#>
</table>
```

との間に式が挿入されることに注意 `<# ... #>` して `<#= ... #>` ください。 詳細については、「 [T4 テキストテンプレートの作成](../modeling/writing-a-t4-text-template.md)」を参照してください。

## <a name="using-the-template"></a>テンプレートの使用

### <a name="the-code-built-from-the-template"></a>テンプレートから作成されたコード

**.Tt**ファイルを保存すると、関連する **.cs**または **.vb**ファイルが生成されます。 このファイルを **ソリューションエクスプローラー**で表示するには、[.tt ファイル] ノードを展開し **ます** 。 Visual Basic プロジェクトで、最初に [**ソリューションエクスプローラー** ] ツールバーの [**すべてのファイルを表示**] を選択します。

この場合、関連するファイルには、というメソッドを含む部分クラスが含まれていることに注意 `TransformText()` してください。 このメソッドは、アプリケーションから呼び出すことができます。

### <a name="generating-text-at-run-time"></a>生成 (実行時にテキストを)

アプリケーションコードでは、次のような呼び出しを使用して、テンプレートのコンテンツを生成できます。

```csharp
MyWebPage page = new MyWebPage();
String pageContent = page.TransformText();
System.IO.File.WriteAllText("outputPage.html", pageContent);
```

```vb
Dim page = New My.Templates.MyWebPage
Dim pageContent = page.TransformText()
System.IO.File.WriteAllText("outputPage.html", pageContent)
```

生成されたクラスを特定の名前空間に配置するには、テキストテンプレートファイルの " **カスタムツールの名前空間** " プロパティを設定します。

### <a name="debugging-runtime-text-templates"></a>ランタイムテキストテンプレートのデバッグ

通常のコードと同じ方法で、ランタイムテキストテンプレートをデバッグおよびテストします。

テキストテンプレートにブレークポイントを設定できます。 Visual Studio からデバッグモードでアプリケーションを起動する場合は、通常の方法でコードをステップ実行し、ウォッチ式を評価できます。

### <a name="passing-parameters-in-the-constructor"></a>コンストラクターでパラメーターを渡す

通常、テンプレートでは、アプリケーションの他の部分からデータをインポートする必要があります。 これを簡単にするために、テンプレートによって作成されたコードは部分クラスです。 プロジェクト内の別のファイルに、同じクラスの別の部分を作成することができます。 このファイルには、パラメーター、プロパティ、および関数を含むコンストラクターを含めることができます。このコンストラクターには、テンプレートに埋め込まれているコードと、アプリケーションの残りの部分の両方でアクセスできます。

たとえば、 **MyWebPageCode.cs**という別のファイルを作成できます。

```csharp
partial class MyWebPage
{
    private MyData m_data;
    public MyWebPage(MyData data) { this.m_data = data; }}
```

テンプレートファイル **MyWebPage.tt**で、次のように記述できます。

```html
<h2>Sales figures</h2>
<table>
<# foreach (MyDataItem item in m_data.Items)
   // m_data is declared in MyWebPageCode.cs
   { #>
      <tr><td> <#= item.Name #> </td>
          <td> <#= item.Value #> </td></tr>
<# } // end of foreach
#>
</table>
```

アプリケーションでこのテンプレートを使用するには、次のようにします。

```csharp
MyData data = ...;
MyWebPage page = new MyWebPage(data);
String pageContent = page.TransformText();
System.IO.File.WriteAllText("outputPage.html", pageContent);
```

#### <a name="constructor-parameters-in-visual-basic"></a>Visual Basic のコンストラクターパラメーター

Visual Basic では、個別のファイル **Mywebpagecode** に次のものが含まれます。

```vb
Namespace My.Templates
  Partial Public Class MyWebPage
    Private m_data As MyData
    Public Sub New(ByVal data As MyData)
      m_data = data
    End Sub
  End Class
End Namespace
```

テンプレートファイルには次のものが含まれます。

```html
<#@ template language="VB" #>
<html><body>
<h1>Sales for January</h2>
<table>
<#
    For Each item In m_data.Items
#>
    <tr><td>Test name <#= item.Name #> </td>
      <td>Test value <#= item.Value #> </td></tr>
<#
    Next
#>
</table>
This report is Company Confidential.
</body></html>
```

テンプレートは、コンストラクターでパラメーターを渡すことによって呼び出すことができます。

```vb
Dim data = New My.Templates.MyData
    ' Add data values here ....
Dim page = New My.Templates.MyWebPage(data)
Dim pageContent = page.TransformText()
System.IO.File.WriteAllText("outputPage.html", pageContent)
```

#### <a name="passing-data-in-template-properties"></a>テンプレートプロパティでデータを渡す

テンプレートにデータを渡す別の方法として、部分クラス定義でテンプレートクラスにパブリックプロパティを追加する方法があります。 アプリケーションでは、を呼び出す前にプロパティを設定でき `TransformText()` ます。

また、部分定義でテンプレートクラスにフィールドを追加することもできます。 これにより、テンプレートの連続実行の間でデータを渡すことができます。

### <a name="use-partial-classes-for-code"></a>コードに部分クラスを使用する

多くの開発者は、大規模なコード本体をテンプレートに記述することを避けたいと思います。 代わりに、テンプレートファイルと同じ名前を持つ部分クラスでメソッドを定義できます。 これらのメソッドをテンプレートから呼び出します。 このようにして、テンプレートでは、ターゲットの出力文字列がどのように表示されるかがより明確に示されます。 結果の外観に関するディスカッションは、表示されるデータを作成するロジックから分離できます。

### <a name="assemblies-and-references"></a>アセンブリと参照

テンプレートコードで .NET またはその他のアセンブリ ( **System.Xml.dll**など) を参照する場合は、通常の方法でプロジェクトの **参照** に追加します。

ステートメントと同じ方法で名前空間をインポートする場合は、 `using` ディレクティブを使用してこれを行うことができ `import` ます。

```
<#@ import namespace="System.Xml" #>
```

これらのディレクティブは、ディレクティブの直後にあるファイルの先頭に配置する必要があり `<#@template` ます。

### <a name="shared-content"></a>共有コンテンツ

複数のテンプレート間で共有されるテキストがある場合は、それを別のファイルに配置し、表示される各ファイルに含めることができます。

```
<#@include file="CommonHeader.txt" #>
```

含まれているコンテンツには、プログラムコードとプレーンテキストの任意の組み合わせを含めることができ、他のインクルードディレクティブやその他のディレクティブを含めることができます。

Include ディレクティブは、テンプレートファイルまたはインクルードファイルのテキスト内の任意の場所で使用できます。

### <a name="inheritance-between-run-time-text-templates"></a>実行時テキストテンプレート間の継承

基本クラステンプレートを記述することによって、実行時テンプレート間でコンテンツを共有できます。これは抽象クラスです。 `inherits` `<@#template#>` 別のランタイムテンプレートクラスを参照するには、ディレクティブのパラメーターを使用します。

#### <a name="inheritance-pattern-fragments-in-base-methods"></a>継承パターン: 基本メソッドのフラグメント

次の例で使用しているパターンでは、次の点に注意してください。

- 基底クラスは、 `SharedFragments` クラス機能ブロック内のメソッドを定義し `<#+ ... #>` ます。

- 基底クラスには自由テキストは含まれません。 代わりに、すべてのテキストブロックはクラスの機能メソッド内で発生します。

- 派生クラスは、で定義されているメソッドを呼び出し `SharedFragments` ます。

- アプリケーションは `TextTransform()` 派生クラスのメソッドを呼び出しますが、基底クラスを変換しません `SharedFragments` 。

- 基本クラスと派生クラスは、どちらもランタイムテキストテンプレートです。つまり、 **カスタムツール** プロパティは **Texttemplatingfilepreprocessor プロセッサ**に設定されます。

**SharedFragments.tt:**

```
<#@ template language="C#" #>
<#+
protected void SharedText(int n)
{
#>
   Shared Text <#= n #>
<#+
}
// Insert more methods here if required.
#>
```

**MyTextTemplate1.tt:**

```
<#@ template language="C#" inherits="SharedFragments" #>
begin 1
   <# SharedText(2); #>
end 1
```

**MyProgram.cs:**

```csharp
...
MyTextTemplate1 t1  = new MyTextTemplate1();
string result = t1.TransformText();
Console.WriteLine(result);
```

**結果の出力は次のようになります。**

```
begin 1
    Shared Text 2
end 1
```

#### <a name="inheritance-pattern-text-in-base-body"></a>継承パターン: ベース本文のテキスト

この別の方法でテンプレートの継承を使用する場合、テキストの大部分は基本テンプレートで定義されます。 派生テンプレートでは、基本コンテンツに適したデータとテキストフラグメントが提供されます。

**AbstractBaseTemplate1.tt:**

```
<#@ template language="C#" #>

Here is the description for this derived template:
  <#= this.Description #>

Here is the fragment specific to this derived template:
<#
  this.PushIndent("  ");
  SpecificFragment(42);
  this.PopIndent();
#>
End of common template.
<#+
  // State set by derived class before calling TextTransform:
  protected string Description = "";
  // 'abstract' method to be defined in derived classes:
  protected virtual void SpecificFragment(int n) { }
#>
```

**DerivedTemplate1.tt:**

```
<#@ template language="C#" inherits="AbstractBaseTemplate1" #>
<#
  // Set the base template properties:
  base.Description = "Description for this derived class";

  // Run the base template:
  base.TransformText();

#>
End material for DerivedTemplate1.

<#+
// Provide a fragment specific to this derived template:

protected override void SpecificFragment(int n)
{
#>
   Specific to DerivedTemplate1 : <#= n #>
<#+
}
#>
```

**アプリケーションコード:**

```csharp
...
DerivedTemplate1 t1 = new DerivedTemplate1();
string result = t1.TransformText();
Console.WriteLine(result);
```

**結果の出力:**

```
Here is the description for this derived template:
  Description for this derived class

Here is the fragment specific to this derived template:
     Specific to DerivedTemplate1 : 42
End of common template.
End material for DerivedTemplate1.
```

## <a name="related-topics"></a>関連トピック

デザイン時テンプレート: テンプレートを使用して、アプリケーションの一部となるコードを生成する場合は、「 [T4 テキストテンプレートを使用したデザイン時のコード生成](../modeling/design-time-code-generation-by-using-t4-text-templates.md)」を参照してください。

ランタイムテンプレートは、コンパイル時にテンプレートとその内容が決定されるすべてのアプリケーションで使用できます。 ただし、実行時に変更されるテンプレートからテキストを生成する Visual Studio 拡張機能を作成する場合は、「 [VS 拡張機能でのテキスト変換の呼び出し](../modeling/invoking-text-transformation-in-a-vs-extension.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [コード生成と T4 テキストテンプレート](../modeling/code-generation-and-t4-text-templates.md)
- [T4 テキスト テンプレートの作成](../modeling/writing-a-t4-text-template.md)
- [T4 ツールボックス](http://olegsych.com/T4Toolbox/)
