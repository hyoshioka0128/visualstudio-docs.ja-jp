---
title: T4 テキスト テンプレートを使用したデザイン時コード生成
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- text templates, guidelines for code generation
- text templates, data source model
- TextTemplatingFileGenerator custom tool
- Transform All Templates
- text templates, getting started
- Text Template project item
- text templates, generating code for your application
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 06c6244f59482825ed435226f79437da9e2c0df0
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75589631"
---
# <a name="design-time-code-generation-by-using-t4-text-templates"></a>T4 テキスト テンプレートを使用したデザイン時コード生成

デザイン時 T4 テキストテンプレートを使用すると、Visual Studio プロジェクトでプログラムコードやその他のファイルを生成できます。 通常、*モデル*のデータに従って生成されるコードが異なるようにテンプレートを記述します。 モデルは、アプリケーションの要件に関する重要な情報を含むファイルまたはデータベースです。

たとえば、ワークフローをテーブルまたは図として定義したモデルがあるとします。 このモデルから、ワークフローを実行するソフトウェアを生成できます。 ユーザーの要件を変更する場合は、ユーザーと新しいワークフローについて議論することが簡単になります。 ワークフローからコードを再生成すると、コードを手動で更新するよりも信頼性が高まります。

> [!NOTE]
> *モデル*はアプリケーションの特定の側面を説明するデータ ソースです。 モデルはどのような形式でもかまいません。あらゆる種類のファイルまたはデータベースを使用できます。 UML モデルやドメイン固有言語モデルなどの特定の形式である必要はありません。 標準的なモデルの形式は、テーブルまたは XML ファイルです。

コード生成は決して新しい概念ではありません。 Visual Studio ソリューション中の **.resx** 内でリソースを定義するとき、クラスとメソッドがセットになったファイルが自動的に生成されます。 リソースの編集は、クラスやメソッドを直接編集するよりも、リソース ファイルで行った方がはるかに簡単で確実です。 同様に、テキスト テンプレートを使用すると、独自に設計したソースからコードを生成することができます。

テキスト テンプレートには、生成するテキストと、テキストの可変部分を生成するプログラム コードの組み合わせが含まれます。 プログラムコードを使用すると、生成されたテキストの一部を繰り返したり条件付きで省略したりすることができます。 生成されるテキスト自体を、アプリケーションの一部となるプログラム コードにすることもできます。

## <a name="create-a-design-time-t4-text-template"></a>デザイン時 T4 テキストテンプレートを作成する

1. 新しい Visual Studio プロジェクトを作成するか、既存のプロジェクトを開きます。

2. テキストテンプレートファイルをプロジェクトに追加し、拡張子 **.tt**を持つ名前を付けます。

    これを実行するためには、プロジェクトのショートカットメニューの中の **ソリューション エクスプローラー** を選択し、**追加**  >  **新しい項目** を選択します。 **新しい項目の追加**ダイアログ ボックスの中央のウィンドウから**テキスト テンプレート**を選択します。

    ファイルの**カスタム ツール** プロパティは **TextTemplatingFileGenerator** です。

3. ファイルを開きます。 既に次のディレクティブが指定されています。

   ```
   <#@ template hostspecific="false" language="C#" #>
   <#@ output extension=".txt" #>
   ```

    [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] プロジェクトにテンプレートを追加した場合、言語属性は "`VB`" になります。

4. ファイルの最後にテキストを追加します。 例:

   ```
   Hello, world!
   ```

5. ファイルを保存します。

    テンプレートを実行することを確認する**セキュリティ警告**メッセージ ボックスが表示されるかもしれません。 **[OK]** をクリックします。

6. **ソリューション エクスプ ローラー**でテンプレート ファイルのノードを展開すると、 **.txt** 拡張子を持つファイルが表示されます。 このファイルには、テンプレートから生成されたテキストが格納されています。

   > [!NOTE]
   > プロジェクトが Visual Basic プロジェクトの場合は、出力ファイルを確認するために**すべてのファイルを表示する**をクリックする必要があります。

### <a name="regenerate-the-code"></a>コードを再生成する

次のいずれかの場合に、テンプレートが実行され、従属ファイルが生成されます。

- テンプレートを編集し、別の Visual Studio ウィンドウにフォーカスを変更したとき。

- テンプレートを保存します。

- **ビルド**メニューの**すべてのテンプレートの変換**をクリックしたとき。 これにより、Visual Studio ソリューション内のすべてのテンプレートが変換されます。

- **ソリューション エクスプローラー**で、ファイルのショートカット メニューの中の**カスタム ツールの実行**を選択したとき。 この方法は、複数のテンプレートを選択して変換する場合に使用します。

読み取られたデータ ファイルが変更されたときにテンプレートが実行されるように、Visual Studio プロジェクトを設定することもできます。 詳細については、「[コードを自動的に再生成](#Regenerating)」を参照してください。

## <a name="generate-variable-text"></a>変数テキストの生成

テキスト テンプレートから生成されるファイルのコンテンツは、プログラム コードを使用して変化させることができます。

1. `.tt` ファイルの内容を次のように変更します。

   ```csharp
   <#@ template hostspecific="false" language="C#" #>
   <#@ output extension=".txt" #>
   <#int top = 10;

   for (int i = 0; i<=top; i++)
   { #>
      The square of <#= i #> is <#= i*i #>
   <# } #>
   ```

   ```vb
   <#@ template hostspecific="false" language="VB" #>
   <#@ output extension=".txt" #>
   <#Dim top As Integer = 10

   For i As Integer = 0 To top
   #>
       The square of <#= i #> is <#= i*i #>
   <#
   Next
   #>
   ```

2. .tt ファイルを保存し、生成された .txt ファイルを再度確認します。 0 から 10 の数値を 2 乗した値が一覧表示されます。

   複数のステートメントは `<#...#>` で囲まれており、単一の式は `<#=...#>` で囲まれていることに注意してください。 詳細については、「[T4 テキスト テンプレートの作成](../modeling/writing-a-t4-text-template.md)」を参照してください。

   [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] で生成コードを記述する場合は、`template` ディレクティブに `language="VB"` を含める必要があります。 `"C#"` が既定値です。

## <a name="debugging-a-design-time-t4-text-template"></a>デザイン時 T4 テキスト テンプレートをデバッグする

テキスト テンプレートをデバッグするには、以下を実行します。

- `debug="true"` ディレクティブに `template` を挿入します。 例:

   `<#@ template debug="true" hostspecific="false" language="C#" #>`

- 通常のコードと同じように、テンプレートにブレークポイントを設定します。

- ソリューション エクスプ ローラーで、テキスト テンプレート ファイルのショートカット メニューから **T4 テンプレートのデバッグ** を選択します。

   テンプレートが実行され、ブレークポイントで停止します。 通常の方法で、変数を調べコードのステップ実行ができます。

> [!TIP]
> `debug="true"` は、生成されたコードに行番号ディレクティブを挿入することで、生成されたコードをより正確にテキストテンプレートにマップします。 これを省いた場合、ブレークポイントが間違った状態で実行を停止する可能性があります。
>
> ただし、デバッグしていないときでも、template ディレクティブにこれを残しておくことができます。 こうしても実行速度がほんのわずか低下するだけです。

## <a name="generating-code-or-resources-for-your-solution"></a>ソリューションのコードまたはリソースを生成する

生成するプログラム ファイルは、モデルに応じて変化させることができます。 モデルは入力です。たとえば、データベース、構成ファイル、UML モデル、DSL モデルなど、各種のソースがそれに該当します。 通常は、同じモデルから複数のプログラムファイルを生成します。 そのためには、生成するプログラム ファイルごとにテンプレート ファイルを作成し、すべてのテンプレートで同じモデルを読み取るようにします。

### <a name="to-generate-program-code-or-resources"></a>プログラム コードまたはリソースを生成するには

1. 適切な種類のファイル (.cs、.vb、.resx、.xml など) を生成するように output ディレクティブを変更します。

2. 必要なソリューション コードを生成するためのコードを挿入します。 たとえば、クラス内に整数型のフィールド宣言を 3 つ生成するには、次のようにします。

    ```csharp

    <#@ template debug="false" hostspecific="false" language="C#" #>
    <#@ output extension=".cs" #>
    <# var properties = new string [] {"P1", "P2", "P3"}; #>
    // This is generated code:
    class MyGeneratedClass {
    <# // This code runs in the text template:
      foreach (string propertyName in properties)  { #>
      // Generated code:
      private int <#= propertyName #> = 0;
    <# } #>
    }
    ```

    ```vb
    <#@ template debug="false" hostspecific="false" language="VB" #>
    <#@ output extension=".cs" #>
    <# Dim properties = {"P1", "P2", "P3"} #>
    class MyGeneratedClass {
    <#
       For Each propertyName As String In properties
    #>
      private int <#= propertyName #> = 0;
    <#
       Next
    #>
    }

    ```

3. ファイルを保存し、生成されたファイルを調べると、次のコードが含まれていることがわかります。

    ```csharp
    class MyGeneratedClass {
      private int P1 = 0;
      private int P2 = 0;
      private int P3 = 0;
    }
    ```

### <a name="generating-code-and-generated-text"></a>生成コードと生成されたテキスト

プログラム コードを生成する際に最も重要なことは、テンプレート内で実行されるコード生成機構 (コードを生成するためのコード) と、結果として生成されるコード (ソリューションの一部になるコード) とを混同しないことです。 2 つの言語が必ずしも一致している必要はありません。

前の例は、2 つのバージョンで構成されています。 1 つ目のバージョンは C# のコードで生成されます。 2 つ目のバージョンは、Visual Basic のコードで生成されます。 ただし、両方のコードで生成されるテキストは同じであり、C# クラスです。

同様に、[!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] テンプレートは、どのような言語のコードでも生成できます。 生成されるテキストは、プログラム コードが含まれる固有の言語である必要はありません。

### <a name="structuring-text-templates"></a>テキスト テンプレートの構成

ここでは、テンプレート コードを次の 2 つの部分に分けています。

- 構成またはデータ収集の部分。この部分では変数に値を設定しますが、テキスト ブロックは含まれません。 前の例では、`properties` の初期化の部分が該当します。

   この部分はインストア モデルを構築し、通常はモデル ファイルを読み取るため、"モデル" セクションとも呼ばれます。

- テキスト生成部分 (この例では、`foreach(...){...}`)。この部分では変数の値を使用します。

   必ずしもこのように分ける必要はありませんが、このように記述すると、テキストを含む部分の複雑さが軽減され、テンプレートが読みやすくなります。

## <a name="reading-files-or-other-sources"></a>ファイルなど各種ソースを読み取る

モデル ファイルまたはモデル データベースにアクセスするために、テンプレート コードで System.XML などのアセンブリを使用できます。 これらのアセンブリにアクセスするためには、次のようなディレクティブを挿入する必要があります。

```
<#@ assembly name="System.Xml.dll" #>
<#@ import namespace="System.Xml" #>
<#@ import namespace="System.IO" #>
```

`assembly` ディレクティブは、Visual Studio プロジェクトにおける参照セクションと同じ方法で指定したアセンブリをテンプレート コードで利用できるようにします。 System.dll への参照を含める必要はありません。System.dll は自動的に参照されます。 `import` ディレクティブの効果は、完全修飾名を使用せずに型を指定できるようになることです。通常のプログラム ファイルで `using` ディレクティブを使用した場合と同様です。

たとえば、**System.IO** をインポートした後は、次のように記述できます。

```csharp

<# var properties = File.ReadLines("C:\\propertyList.txt");#>
...
<# foreach (string propertyName in properties) { #>
...
```

```vb
<# For Each propertyName As String In
             File.ReadLines("C:\\propertyList.txt")
#>
```

### <a name="opening-a-file-with-a-relative-pathname"></a>相対パス名を指定してファイルを開く

テキスト テンプレートを基準とする場所からファイルを読み込むには、`this.Host.ResolvePath()` を使用します。 this.Host を使用するには、次のように `hostspecific="true"` で `template` を設定する必要があります。

```
<#@ template debug="false" hostspecific="true" language="C#" #>
```

これで、次のようなコードを記述できるようになります。

```csharp
<# string fileName = this.Host.ResolvePath("filename.txt");
  string [] properties = File.ReadLines(filename);
#>
...
<#  foreach (string propertyName in properties { #>
...
```

```vb
<# Dim fileName = Me.Host.ResolvePath("propertyList.txt")
   Dim properties = File.ReadLines(filename)
#>
...
<#   For Each propertyName As String In properties
...
#>
```

`this.Host.TemplateFile` を使用して、現在のテンプレート ファイルの名前を示すこともできます。

`this.Host` (VB の場合は `Me.Host`) の型は、`Microsoft.VisualStudio.TextTemplating.ITextTemplatingEngineHost` です。

### <a name="getting-data-from-visual-studio"></a>Visual Studio からのデータの取得

Visual Studio に用意されているサービスを使用するには、`hostSpecific` 属性を設定し、`EnvDTE` アセンブリを読み込みます。 `GetCOMService()` の拡張メソッドを含む `Microsoft.VisualStudio.TextTemplating`をインポートします。  その後、IServiceProvider.GetCOMService() を使用して、DTE などのサービスにアクセスできます。 例:

```src
<#@ template hostspecific="true" language="C#" #>
<#@ output extension=".txt" #>
<#@ assembly name="EnvDTE" #>
<#@ import namespace="Microsoft.VisualStudio.TextTemplating" #>
<#
  IServiceProvider serviceProvider = (IServiceProvider)this.Host;
  EnvDTE.DTE dte = (EnvDTE.DTE) serviceProvider.GetCOMService(typeof(EnvDTE.DTE));
#>

Number of projects in this VS solution:  <#= dte.Solution.Projects.Count #>
```

> [!TIP]
> テキスト テンプレートは独自のアプリ ドメインで実行され、サービスはマーシャリングによってアクセスされます。 この状況では、GetCOMService() は GetService() よりも信頼性が高くなります。

## <a name="Regenerating"></a> コードの自動再生成

通常、1 つの入力モデルから Visual Studio ソリューションにより複数のファイルが生成されます。 各ファイルはそれぞれ対応するテンプレートから生成されますが、すべてのテンプレートは同じモデルを参照します。

ソース モデルが変更された場合は、ソリューションのすべてのテンプレートを再度実行する必要があります。 これを手動で行うには、 **[ビルド]** メニューの **[すべてのテンプレートの変換]** をクリックします。

Visual Studio モデリング SDK がインストールされている場合は、ビルドを実行するたびにすべてのテンプレートを自動的に変換することができます。 そのためには、プロジェクト ファイル (.csproj または .vbproj) をテキスト エディターで編集し、ファイルの末尾付近の、他の `<import>` ステートメントよりも後に次のコード行を追加します。

> [!NOTE]
> テキストテンプレート変換 SDK と Visual Studio モデリング SDK は、Visual Studio の特定の機能をインストールするときに自動的にインストールされます。 詳細については、[このブログの投稿](https://devblogs.microsoft.com/devops/the-visual-studio-modeling-sdk-is-now-available-with-visual-studio-2017/)を参照してください。

::: moniker range="vs-2017"

```xml
<Import Project="$(MSBuildExtensionsPath)\Microsoft\VisualStudio\v15.0\TextTemplating\Microsoft.TextTemplating.targets" />
<PropertyGroup>
   <TransformOnBuild>true</TransformOnBuild>
   <!-- Other properties can be inserted here -->
</PropertyGroup>
```

::: moniker-end

::: moniker range=">=vs-2019"

```xml
<Import Project="$(MSBuildExtensionsPath)\Microsoft\VisualStudio\v16.0\TextTemplating\Microsoft.TextTemplating.targets" />
<PropertyGroup>
   <TransformOnBuild>true</TransformOnBuild>
   <!-- Other properties can be inserted here -->
</PropertyGroup>
```

::: moniker-end

詳細については、「[ビルド プロセスでのコード生成](../modeling/code-generation-in-a-build-process.md)」を参照してください。

## <a name="error-reporting"></a>エラー レポート

Visual Studio のエラー ウィンドウにエラーと警告メッセージを表示するには、これらのメソッドを使用できます。

```
Error("An error message");
Warning("A warning message");
```

## <a name="Converting"></a>既存のファイルをテンプレートに変換する

テンプレートには、見た目は生成されるファイルとよく似ていて、そこに、プログラム コードが挿入されているという特徴があります。 このことを利用すると、テンプレートを効率的に作成することができます。 まずプロトタイプとして [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] といった通常のファイルを作成し、生成されるファイルを変更するコードを徐々に挿入していきます。

### <a name="to-convert-an-existing-file-to-a-design-time-template"></a>既存のファイルをデザイン時テンプレートに変換するには

1. Visual Studio プロジェクトに、生成する型のファイル (`.cs`、`.vb`、`.resx` ファイルなど) を追加します。

2. この新しいファイルをテストして、ファイルが機能することを確認します。

3. ソリューション エクスプローラーでファイル名拡張子を **.tt** に変更します。

4. **.tt** ファイルの次のプロパティを確認します。

   | | |
   |-|-|
   | **カスタムツール =** | **TextTemplatingFileGenerator** |
   | **ビルドアクション =** | **None** |

5. ファイルの先頭に次の行を挿入します。

   ```
   <#@ template debug="false" hostspecific="false" language="C#" #>
   <#@ output extension=".cs" #>
   ```

    テンプレートのコード生成機構を [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] で記述する場合は、`language` 属性を `"VB"` ではなく、`"C#"` に設定してください。

    `extension` 属性を、生成するファイルの種類のファイル名拡張子 (`.cs`、`.resx`、`.xml` など) に設定します。

6. ファイルを保存します。

    指定された拡張子の従属ファイルが作成されます。 そのプロパティは、ファイルの種類に対応します。 たとえば、.cs ファイルの**ビルド アクション** プロパティは **コンパイル** になります。

    生成されたファイルのコンテンツが、元のファイルと同じであることを確認します。

7. ファイルの可変部分を見極めます。 たとえば、特定の条件を満たした場合にのみ出力する部分や、繰り返し出力する部分、特定の値をどこで変化させるかなどを決めます。 コードを生成するためのコードを挿入します。 ファイルを保存し、従属ファイルが正しく生成されたことを確認します。 この手順を繰り返します。

## <a name="guidelines-for-code-generation"></a>コード生成のガイドライン

[T4 テキスト テンプレートの記述に関するガイドライン](../modeling/guidelines-for-writing-t4-text-templates.md)を参照してください。

## <a name="next-steps"></a>次のステップ:

|次のステップ|トピック|
|-|-|
|補助的な関数、インクルード ファイル、外部データなどを使用したコードを組み合わせて、より高度なテキスト テンプレートを作成し、デバッグする。|[T4 テキスト テンプレートの作成](../modeling/writing-a-t4-text-template.md)|
|実行時にテンプレートからドキュメントを生成する。|[T4 テキスト テンプレートを使用した実行時テキスト生成](../modeling/run-time-text-generation-with-t4-text-templates.md)|
|Visual Studio の外部テキスト生成を実行する。|[TextTransform ユーティリティを使用したファイルの生成](../modeling/generating-files-with-the-texttransform-utility.md)|
|ドメイン固有言語の形式でデータを変換する。|[ドメイン固有言語からのコード生成](../modeling/generating-code-from-a-domain-specific-language.md)|
|独自のデータ ソースを変換するためのディレクティブ プロセッサを作成する。|[T4 テキスト変換のカスタマイズ](../modeling/customizing-t4-text-transformation.md)|

## <a name="see-also"></a>関連項目

- [T4 テキスト テンプレートの記述に関するガイドライン](../modeling/guidelines-for-writing-t4-text-templates.md)
