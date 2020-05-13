---
title: コード スニペット スキーマ リファレンス
ms.date: 03/31/2020
ms.topic: reference
helpviewer_keywords:
- schema reference [Visual Studio]
- snippets [Visual Studio], schema reference
- code snippets [Visual Studio], schema reference
- IntelliSense Code Snippets, XML Schema
ms.assetid: 58a60621-725f-4763-93b7-62ea5424ef88
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 867aac31f1515136e3aa9f0a6f171ec425d90cf7
ms.sourcegitcommit: ce3d0728ec1063ab548dac71c8eaf26d20450acc
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/01/2020
ms.locfileid: "80472795"
---
# <a name="code-snippets-schema-reference"></a>コード スニペット スキーマ リファレンス

IntelliSense コード スニペットとは、Visual Studio でのアプリケーション開発時に、簡単に挿入できるようにあらかじめ作成されたコードです。 同じようなコードを繰り返し入力したり、サンプルを検索したりする時間を短縮するコード スニペットを用意しておくことで、生産性を高めることができます。 IntelliSense コード スニペット XML スキーマを使用すると、独自のコード スニペットを作成し、それらを Visual Studio に標準で付属しているコード スニペットに追加できます。

## <a name="assembly-element"></a>Assembly 要素

コード スニペットによって参照されるアセンプリの名前を指定します。

**Assembly** 要素のテキスト値は、アセンブリの表示名 (`System.dll` など) で指定することも、厳密な名前 (`System,Version=1.0.0.1,Culture=neutral,PublicKeyToken=9b35aa323c18d4fb1` など) で指定することもできます。

```xml
<Assembly>
    AssemblyName
</Assembly>
```

|親要素|説明|
| - |-----------------|
|[Reference 要素](../ide/code-snippets-schema-reference.md#reference-element)|コード スニペットで参照する必要のあるアセンブリについての情報が格納されます。|

テキスト値が必要です。 このテキストで、コード スニペットが参照するアセンブリを指定します。

## <a name="author-element"></a>Author 要素

スニペット作成者の名前を指定します。 **コード スニペット マネージャー**には、コード スニペットの `Author` 要素に格納された名前が表示されます。

```xml
<Author>
   Code Snippet Author
</Author>
```

|親要素|説明|
| - |-----------------|
|[Header 要素](../ide/code-snippets-schema-reference.md#header-element)|コード スニペットに関する全般的な情報が格納されます。|

テキスト値が必要です。 このテキストでコード スニペットの作成者を指定します。

## <a name="code-element"></a>コード要素

短いコード ブロックのコンテナーを提供します。

### <a name="keywords"></a>キーワード

`Code` 要素のテキストでは、`$end$` および `$selected$` という 2 つの予約語を使用できます。 `$end$` は、コード スニペットの挿入後のカーソル位置を指定します。 `$selected$` は、ドキュメントで選択されているテキストを表し、スニペットが呼び出されたときに置き換えられます。 たとえば、次のコードを含むスニペットがあるとします。

```
$selected$ is a great color.
```

ユーザーがテンプレートを呼び出したときに、単語 "Blue" を選択した場合、結果は次のようになります。

```
Blue is a great color.
```

`$end$` と `$selected$` は、どちらもコード スニペット内で複数回使用することはできません。 複数回使用した場合、2 つ目のインスタンスだけが認識されます。 次のコードを含むスニペットがあるとします。

```
$selected$ is a great color. I love $selected$.
```

単語 "Blue" を選択した場合、結果は次のようになります。

```
 is a great color. I love Blue.
```

`$selected$` と `is` の間にスペースがあるため、先頭にスペースが表示されます。

その他の `$` キーワードはすべて、`<Literal>` タグおよび `<Object>` タグで動的に定義されます。

Code 要素の構造を以下に示します。

```xml
<Code Language="Language"
    Kind="method body/method decl/type decl/page/file/any"
    Delimiter="Delimiter">
    Code to insert
</Code>
```

テキスト値が必要です。 このテキストで、コード スニペットをコード ファイルに挿入した場合に使用できるコードを、リテラルおよびオブジェクトと共に指定します。

### <a name="attributes"></a>属性

Code 要素に使用できる属性には次の 3 つがあります。

- **Language** - _必須_ の属性。コード スニペットの言語を指定します。 値は次のいずれかになります。

   |[値]|説明|
   |-----|-----------|
   |`VB`|Visual Studio のコード スニペットであることを示します。|
   |`CSharp`|C# のコード スニペットであることを示します。|
   |`CPP`|C++ のコード スニペットであることを示します。|
   |`XML`|XML のコード スニペットであることを示します。|
   |`JavaScript`|JavaScript のコード スニペットであることを示します。|
   |`TypeScript`|TypeScript のコード スニペットであることを示します。|
   |`SQL`|SQL のコード スニペットであることを示します。|
   |`HTML`|HTML のコード スニペットであることを示します。|

- **Kind** - スニペットに含まれるコードの種類を指定する_省略可能な_属性。 値は次のいずれかになります。

   |[値]|説明|
   |-----|-----------|
   |`method body`|コード スニペットがメソッドの本体であり、メソッド宣言の内部に挿入する必要があることを示します。|
   |`method decl`|コード スニペットがメソッドであり、クラスまたはモジュールの内部に挿入する必要があることを示します。|
   |`type decl`|コード スニペットが型であり、クラス、モジュール、または名前空間の内部に挿入する必要があることを示します。|
   |`file`|スニペットが完全なコード ファイルであることを示します。 これらのコード スニペットは、単体でコード ファイルに挿入することも、名前空間内に挿入することもできます。|
   |`any`|スニペットをどこにでも挿入できることを示します。 このタグは、コメントなど、コンテキストに依存しないコード スニペットに使用します。|

- **Delimiter** - _省略可能_ な属性。コード内のリテラルおよびオブジェクトを説明するために使用される区切り文字を指定します。 既定では、区切り記号は `$` です。

### <a name="parent-element"></a>親要素

|親要素|説明|
| - |-----------------|
|[Snippet 要素](../ide/code-snippets-schema-reference.md#snippet-element)|コード スニペットの参照、インポート、宣言、およびコードが格納されます。|

## <a name="codesnippet-element"></a>CodeSnippet 要素

Visual Studio Code ファイルに挿入できる見出しと複数の IntelliSense コード スニペットを指定します。

```xml
<CodeSnippet Format="x.x.x">
    <Header>... </Header>
    <Snippet>... </Snippet>
</CodeSnippet>
```

|属性|説明|
|---------------|-----------------|
|`Format`|必須の属性です。 コード スニペットのスキーマ バージョンを指定します。 Format 属性は、x.x.x (x はそれぞれバージョン番号の数値) の構文の文字列で指定されなければなりません。 Visual Studio では、理解できない `Format` 属性を含むコード スニペットを無視します。|

|子要素|説明|
|-------------------|-----------------|
|[Header 要素](../ide/code-snippets-schema-reference.md#header-element)|必須の要素です。 コード スニペットに関する全般的な情報が格納されます。 コード スニペットで使用できる `Header` 要素は 1 つだけです。|
|[Snippet 要素](../ide/code-snippets-schema-reference.md#snippet-element)|必須の要素です。 Visual Studio によって挿入されるコードが格納されます。 コード スニペットで使用できる `Snippet` 要素は 1 つだけです。|

|親要素|説明|
| - |-----------------|
|[CodeSnippets 要素](../ide/code-snippets-schema-reference.md#codesnippets-element)|コード スニペットの XML スキーマのルート要素です。|

## <a name="codesnippets-element"></a>CodeSnippets 要素

複数の [CodeSnippet](../ide/code-snippets-schema-reference.md#codesnippet-element) 要素をグループ化します。 `CodeSnippets` 要素は、コード スニペットの XML スキーマにおけるルート要素です。

```xml
<CodeSnippets>
    <CodeSnippet>... </CodeSnippet>
</CodeSnippets>
```

|子要素|説明|
|-------------------|-----------------|
|[CodeSnippet 要素](../ide/code-snippets-schema-reference.md#codesnippet-element)|省略可能な要素です。 すべてのコード スニペット データを下位に持つ親要素です。 `CodeSnippet` 要素に 0 個以上の `CodeSnippets` 要素があります。|

## <a name="declarations-element"></a>Declarations 要素

編集できるコード スニペットの部分を構成するリテラルとオブジェクトを指定します。

```xml
<Declarations>
    <Literal>... </Literal>
    <Object>... </Object>
</Declarations>
```

|子要素|説明|
|-------------------|-----------------|
|[Literal 要素](../ide/code-snippets-schema-reference.md#literal-element)|省略可能な要素です。 編集できるコード スニペットのリテラルを定義します。 `Literal` 要素に 0 個以上の `Declarations` 要素があります。|
|[Object 要素](../ide/code-snippets-schema-reference.md#object-element)|省略可能な要素です。 編集できるコード スニペットのオブジェクトを定義します。 `Object` 要素に 0 個以上の `Declarations` 要素があります。|

|親要素|説明|
| - |-----------------|
|[Snippet 要素](../ide/code-snippets-schema-reference.md#snippet-element)|コード スニペットの参照、インポート、宣言、およびコードが格納されます。|

## <a name="default-element"></a>Default 要素

IntelliSense コード スニペットのリテラルまたはオブジェクトの既定値を指定します。

```xml
<Default>
    Default value
</Default>
```

|親要素|説明|
| - |-----------------|
|[Literal 要素](../ide/code-snippets-schema-reference.md#literal-element)|編集が可能なコード スニペットのリテラル フィールドを定義します。|
|[Object 要素](../ide/code-snippets-schema-reference.md#object-element)|編集が可能なコード スニペットのオブジェクト フィールドを定義します。|

テキスト値が必要です。 このテキストは、編集できるコード スニペットのフィールドに入れるリテラルまたはオブジェクトの既定値を指定します。

## <a name="description-element"></a>Description 要素

IntelliSense コード スニペットの内容に関する説明文を指定します。

```xml
<Description>
    Code Snippet Description
</Description>
```

|親要素|説明|
| - |-----------------|
|[Header 要素](../ide/code-snippets-schema-reference.md#header-element)|コード スニペットに関する全般的な情報が格納されます。|

テキスト値が必要です。 このテキストで、コード スニペットについて説明します。

## <a name="function-element"></a>Function 要素

Visual Studio でリテラルまたはオブジェクトがフォーカスを取得するときに実行される関数を指定します。

> [!NOTE]
> 一部の言語は `function` 要素をサポートしていません。 どの機能を使用できるかについては、言語固有のドキュメントを参照してください。

```xml
<Function>
    FunctionName
</Function>
```

|親要素|説明|
| - |-----------------|
|[Literal 要素](../ide/code-snippets-schema-reference.md#literal-element)|編集が可能なコード スニペットのリテラル フィールドを定義します。|
|[Object 要素](../ide/code-snippets-schema-reference.md#object-element)|編集が可能なコード スニペットのオブジェクト フィールドを定義します。|

テキスト値が必要です。 このテキストで、Visual Studio でリテラルまたはオブジェクト フィールドがフォーカスを取得するときに実行される関数を指定します。

## <a name="header-element"></a>Header 要素

IntelliSense コード スニペットの一般情報を指定します。

```xml
<Header>
    <Title>... </Title>
    <Author>... </Author>
    <Description>... </Description>
    <HelpUrl>... </HelpUrl>
    <SnippetTypes>... </SnippetTypes>
    <Keywords>... </Keywords>
    <Shortcut>... </Shortcut>
</Header>
```

|子要素|説明|
|-------------------|-----------------|
|[Author 要素](../ide/code-snippets-schema-reference.md#author-element)|省略可能な要素です。 コード スニペットを作成した個人または会社の名前です。 `Author` 要素には 0 個または 1 個の `Header` 要素があります。|
|[Description 要素](../ide/code-snippets-schema-reference.md#description-element)|省略可能な要素です。 コード スニペットの説明です。 `Description` 要素には 0 個または 1 個の `Header` 要素があります。|
|[HelpUrl 要素](../ide/code-snippets-schema-reference.md#helpurl-element)|省略可能な要素です。 コード スニペットに関する詳細な情報が記載された URL です。 Header 要素には 0 個または 1 個の `HelpURL` 要素があります。 **注:** Visual Studio では `HelpUrl` 要素を使用しません。 この要素は IntelliSense コード スニペット XML スキーマの一部であり、この要素を含むコード スニペットはすべて問題なく検証されますが、要素の値が使われることはありません。|
|[Keywords 要素](../ide/code-snippets-schema-reference.md#keywords-element)|省略可能な要素です。 複数の `Keyword` 要素をグループ化します。 `Keywords` 要素には 0 個または 1 個の `Header` 要素があります。|
|[Shortcut 要素](../ide/code-snippets-schema-reference.md#shortcut-element)|省略可能な要素です。 スニペットの挿入に使用するショートカット テキストを指定します。 `Shortcut` 要素には 0 個または 1 個の `Header` 要素があります。|
|[SnippetTypes 要素](../ide/code-snippets-schema-reference.md#snippettypes-element)|省略可能な要素です。 複数の `SnippetType` 要素をグループ化します。 `SnippetTypes` 要素には 0 個または 1 個の `Header` 要素があります。 `SnippetTypes` 要素が存在しない場合、コード スニペットは常に有効となります。|
|[Title 要素](../ide/code-snippets-schema-reference.md#title-element)|必須の要素です。 コード スニペットの表示名です。 `Title` 要素で使用できる `Header` 要素は 1 つだけです。|

|親要素|説明|
| - |-----------------|
|[CodeSnippet 要素](../ide/code-snippets-schema-reference.md#codesnippet-element)|すべてのコード スニペット データを下位に持つ親要素です。|

## <a name="helpurl-element"></a>HelpUrl 要素

コード スニペットに関する詳細な情報の入手先 URL を指定します。

> [!NOTE]
> Visual Studio では `HelpUrl` 要素を使用しません。 この要素は IntelliSense コード スニペット XML スキーマの一部であり、この要素を含むコード スニペットはすべて問題なく検証されますが、要素の値が使われることはありません。

```xml
<HelpUrl>
    www.microsoft.com
</HelpUrl>
```

|親要素|説明|
| - |-----------------|
|[Header 要素](../ide/code-snippets-schema-reference.md#header-element)|コード スニペットに関する全般的な情報が格納されます。|

テキスト値は省略可能です。 このテキストで、コード スニペットに関する詳細情報の入手先 URL を指定します。

## <a name="id-element"></a>ID 要素

`Literal` 要素または `Object` 要素の一意の識別子を指定します。 同じコード スニペットの 2 つのリテラルまたはオブジェクトがその `ID` 要素に同じテキスト値を持つことはできません。 リテラルとオブジェクトに、end という値の `ID` 要素を含めることはできません。 `$end$` という値は、コード スニペットの挿入後のカーソル位置をマーキングする目的で予約されています。

```xml
<ID>
    Unique Identifier
</ID>
```

|親要素|説明|
| - |-----------------|
|[Literal 要素](../ide/code-snippets-schema-reference.md#literal-element)|編集が可能なコード スニペットのリテラル フィールドを定義します。|
|[Object 要素](../ide/code-snippets-schema-reference.md#object-element)|編集が可能なコード スニペットのオブジェクト フィールドを定義します。|

テキスト値が必要です。 このテキストで、オブジェクトまたはリテラルの一意の識別子を指定します。

## <a name="import-element"></a>Import 要素

IntelliSense コード スニペットによって使用されるインポートされた名前空間を指定します。

```xml
<Import>
    <Namespace>... </Namespace>
</Import>
```

|子要素|説明|
|-------------------|-----------------|
|[名前空間要素](../ide/code-snippets-schema-reference.md#namespace-element)|必須の要素です。 コード スニペットで使用される名前空間を指定します。 `Namespace` 要素で使用できる `Import` 要素は 1 つだけです。|

|親要素|説明|
| - |-----------------|
|[Imports 要素](../ide/code-snippets-schema-reference.md#imports-element)|**Import** 要素のグループ化要素です。|

## <a name="imports-element"></a>Imports 要素

複数の `Import` 要素をグループ化します。

```xml
<Imports>
    <Import>... </Import>
</Imports>
```

|子要素|説明|
|-------------------|-----------------|
|[Import 要素](../ide/code-snippets-schema-reference.md#import-element)|省略可能な要素です。 コード スニペットでインポートする必要のある名前空間が格納されます。 `Imports` 要素には 0 個以上の **Import** 要素があります。|

|親要素|説明|
| - |-----------------|
|[Snippet 要素](../ide/code-snippets-schema-reference.md#snippet-element)|コード スニペットの参照、インポート、宣言、およびコードが格納されます。|

## <a name="keyword-element"></a>Keyword 要素

コード スニペットのカスタム キーワードを指定します。 コード スニペットのキーワードは Visual Studio によって使用され、検索や分類のためのカスタム キーワードを追加する手段をオンライン コンテンツ プロバイダーに提供します。

```xml
<Keyword>
    Code Snippet Keyword
</Keyword>
```

|親要素|説明|
| - |-----------------|
|[Keywords 要素](../ide/code-snippets-schema-reference.md#keywords-element)|複数の `Keyword` 要素をグループ化します。|

テキスト値が必要です。 コード スニペットのキーワードを指定します。

## <a name="keywords-element"></a>Keywords 要素

複数の `Keyword` 要素をグループ化します。 コード スニペットのキーワードは Visual Studio によって使用され、検索や分類のためのカスタム キーワードを追加する手段をオンライン コンテンツ プロバイダーに提供します。

```xml
<Keywords>
    <Keyword>... </Keyword>
    <Keyword>... </Keyword>
</Keywords>
```

|子要素|説明|
|-------------------|-----------------|
|[Keyword 要素](../ide/code-snippets-schema-reference.md#keyword-element)|省略可能な要素です。 コード スニペットの複数のキーワードが格納されます。 `Keyword` 要素に 0 個以上の `Keywords` 要素があります。|

|親要素|説明|
| - |-----------------|
|[Header 要素](../ide/code-snippets-schema-reference.md#header-element)|コード スニペットに関する全般的な情報が格納されます。|

## <a name="literal-element"></a>Literal 要素

編集できるコード スニペットのリテラルを定義します。 `Literal` 要素は、コード スニペットの中で置き換えて使用できる部分を識別する目的で使用されます。 たとえば、リテラル文字列、数値、および変数名はリテラルとして宣言されなければなりません。

リテラルおよびオブジェクトに、selected または end という値の **ID** 要素を含めることはできません。 値 `$selected$` は、ドキュメントで選択されているテキストを表し、スニペットが呼び出されたときに置き換えられます。 `$end$` は、コード スニペットの挿入後のカーソル位置を指定します。

```xml
<Literal Editable="true/false">
   <ID>... </ID>
   <ToolTip>... </ToolTip>
   <Default>... </Default>
   <Function>... </Function>
</Literal>
```

|属性|説明|
|---------------|-----------------|
|`Editable`|省略可能な `Boolean` 属性です。 コード スニペットが挿入された後にリテラルを編集可能にするかどうかを指定します。 この属性の既定値は `true` です。|

|子要素|説明|
|-------------------|-----------------|
|[Default 要素](../ide/code-snippets-schema-reference.md#default-element)|必須の要素です。 コード スニペットを挿入した場合に、既定で使用されるリテラルの値を指定します。 `Default` 要素で使用できる `Literal` 要素は 1 つだけです。|
|[Function 要素](../ide/code-snippets-schema-reference.md#function-element)|省略可能な要素です。 リテラルが Visual Studio でフォーカスを受け取ったときに実行される関数を指定します。 `Function` 要素には 0 個または 1 個の `Literal` 要素があります。|
|[ID 要素](../ide/code-snippets-schema-reference.md#id-element)|必須の要素です。 リテラルの一意の識別子を指定します。 `ID` 要素で使用できる `Literal` 要素は 1 つだけです。|
|[ToolTip 要素](../ide/code-snippets-schema-reference.md#tooltip-element)|省略可能な要素です。 リテラルに予想される値と使用法に関する説明文です。 `Literal` 要素には 0 個または 1 個の **Tooltip** 要素があります。|

|親要素|説明|
| - |-----------------|
|[Declarations 要素](../ide/code-snippets-schema-reference.md#declarations-element)|編集が可能なコード スニペットのリテラルおよびオブジェクトを保持します。|

## <a name="namespace-element"></a>Namespace 要素

コード スニペットをコンパイルおよび実行するためにインポートする必要のある名前空間を指定します。 `Namespace` 要素で指定された名前空間が存在しない場合、コードの先頭の `using` ディレクティブまたは `Imports` ステートメントに自動的に追加されます。

```xml
<Namespace>
    Namespace
</Namespace>
```

|親要素|説明|
| - |-----------------|
|[Import 要素](../ide/code-snippets-schema-reference.md#import-element)|指定された名前空間をインポートします。|

テキスト値が必要です。 このテキストで、コード スニペットを使用するためにインポートする必要のある名前空間を指定します。

## <a name="object-element"></a>Object 要素

編集できるコード スニペットのオブジェクトを定義します。 `Object` 要素は、コード スニペット自体には定義されておらず、外部で定義する必要のある項目を指定するときに使用します。 たとえば、Windows フォーム コントロール、ASP.NET コントロール、オブジェクトのインスタンス、型のインスタンスなどをオブジェクトとして宣言します。 オブジェクトの宣言では、`Type` 要素で型を指定する必要があります。

```xml
<Object Editable="true/false">
    <ID>... </ID>
    <Type>... </Type>
    <ToolTip>... </ToolTip>
    <Default>... </Default>
    <Function>... </Function>
</Object>
```

|属性|説明|
|---------------|-----------------|
|`Editable`|省略可能な `Boolean` 属性です。 コード スニペットが挿入された後にリテラルを編集可能にするかどうかを指定します。 この属性の既定値は `true` です。|

|子要素|説明|
|-------------------|-----------------|
|[Default 要素](../ide/code-snippets-schema-reference.md#default-element)|必須の要素です。 コード スニペットを挿入した場合に、既定で使用されるリテラルの値を指定します。 `Default` 要素で使用できる `Literal` 要素は 1 つだけです。|
|[Function 要素](../ide/code-snippets-schema-reference.md#function-element)|省略可能な要素です。 リテラルが Visual Studio でフォーカスを受け取ったときに実行される関数を指定します。 `Function` 要素には 0 個または 1 個の `Literal` 要素があります。|
|[ID 要素](../ide/code-snippets-schema-reference.md#id-element)|必須の要素です。 リテラルの一意の識別子を指定します。 `ID` 要素で使用できる `Literal` 要素は 1 つだけです。|
|[ToolTip 要素](../ide/code-snippets-schema-reference.md#tooltip-element)|省略可能な要素です。 リテラルに予想される値と使用法に関する説明文です。 `Literal` 要素には 0 個または 1 個の **Tooltip** 要素があります。|
|[Type 要素](../ide/code-snippets-schema-reference.md#type-element)|必須の要素です。 オブジェクトの種類を指定します。 `Type` 要素で使用できる `Object` 要素は 1 つだけです。|

|親要素|説明|
| - |-----------------|
|[Declarations 要素](../ide/code-snippets-schema-reference.md#declarations-element)|編集が可能なコード スニペットのリテラルおよびオブジェクトを保持します。|

## <a name="reference-element"></a>Reference 要素

コード スニペットで参照する必要のあるアセンブリについての情報を指定します。

```xml
<Reference>
    <Assembly>... </Assembly>
    <Url>... </Url>
</Reference>
```

|子要素|説明|
|-------------------|-----------------|
|[Assembly 要素](../ide/code-snippets-schema-reference.md#assembly-element)|必須の要素です。 コード スニペットによって参照されるアセンプリの名前が格納されます。 `Assembly` 要素で使用できる `Reference` 要素は 1 つだけです。|
|[Url 要素](../ide/code-snippets-schema-reference.md#url-element)|省略可能な要素です。 参照アセンブリに関する詳細な情報の入手先 URL が格納されます。 `Url` 要素には 0 個または 1 個の `Reference` 要素があります。|

|親要素|説明|
| - |-----------------|
|[References 要素](../ide/code-snippets-schema-reference.md#references-element)|`Reference` 要素のグループ化要素です。|

## <a name="references-element"></a>References 要素

複数の `Reference` 要素をグループ化します。

```xml
<References>
    <Reference>... </Reference>
</References>
```

|子要素|説明|
|-------------------|-----------------|
|[Reference 要素](../ide/code-snippets-schema-reference.md#reference-element)|省略可能な要素です。 コード スニペットで参照する必要のあるアセンブリについての情報が格納されます。 `Reference` 要素に 0 個以上の `References` 要素があります。|

|親要素|説明|
| - |-----------------|
|[Snippet 要素](../ide/code-snippets-schema-reference.md#snippet-element)|コード スニペットの参照、インポート、宣言、およびコードが格納されます。|

## <a name="shortcut-element"></a>Shortcut 要素

スニペットの挿入に使用するショートカット テキストを指定します。 `Shortcut` 要素のテキスト値には、英数字、アンダースコア ( _ ) のみを含めることができます。

> [!CAUTION]
> アンダースコア ( _ ) の文字は C++ スニペットのショートカットではサポートされていません。

```xml
<Shortcut>
    Shortcut Text
</Shortcut>
```

|親要素|説明|
| - |-----------------|
|[Header 要素](../ide/code-snippets-schema-reference.md#header-element)|コード スニペットに関する全般的な情報が格納されます。|

テキスト値は省略可能です。 このテキストは、コード スニペットを挿入するためのショートカットとして使用されます。

## <a name="snippet-element"></a>Snippet 要素

参照、インポート、宣言およびコード スニペット用のコードを指定します。

```xml
<Snippet>
    <References>... </References>
    <Imports>... </Imports>
    <Declarations>... </Declarations>
    <Code>... </Code>
</Snippet>
```

|子要素|説明|
|-------------------|-----------------|
|[Code 要素](../ide/code-snippets-schema-reference.md#code-element)|必須の要素です。 ドキュメント ファイルに挿入するコードを指定します。 `Code` 要素で使用できる `Snippet` 要素は 1 つだけです。|
|[Declarations 要素](../ide/code-snippets-schema-reference.md#declarations-element)|省略可能な要素です。 編集できるコード スニペットの部分を構成するリテラルとオブジェクトを指定します。 `Declarations` 要素には 0 個または 1 個の `Snippet` 要素があります。|
|[Imports 要素](../ide/code-snippets-schema-reference.md#imports-element)|省略可能な要素です。 複数の `Import` 要素をグループ化します。 `Imports` 要素には 0 個または 1 個の `Snippet` 要素があります。|
|[References 要素](../ide/code-snippets-schema-reference.md#references-element)|省略可能な要素です。 複数の `Reference` 要素をグループ化します。 `References` 要素には 0 個または 1 個の `Snippet` 要素があります。|

|親要素|説明|
| - |-----------------|
|[CodeSnippet 要素](../ide/code-snippets-schema-reference.md#codesnippet-element)|Visual Studio Code ファイルに挿入できる見出しと複数の IntelliSense コード スニペットを指定します。|

## <a name="snippettype-element"></a>SnippetType 要素

Visual Studio がコード スニペットをどのように挿入するかを指定します。

```xml
<SnippetType>
    SurroundsWith/Expansion
</SnippetType>
```

|親要素|説明|
| - |-----------------|
|[SnippetTypes 要素](../ide/code-snippets-schema-reference.md#snippettypes-element)|複数の `SnippetType` 要素をグループ化します。|

テキスト値は、次のいずれかの値である必要があります。

- `SurroundsWith`: 選択したコードの周りにコード スニペットを配置します。

- `Expansion` : カーソル位置にコード スニペットを挿入します。

- `Refactoring`: C# のリファクタリング中にコード スニペットを使用するよう指定します。 `Refactoring` は、カスタムのコード スニペットには使用できません。

## <a name="snippettypes-element"></a>SnippetTypes 要素

複数の `SnippetType` 要素をグループ化します。 `SnippetTypes` 要素が存在しない場合、コード スニペットはコード内のどこにでも挿入できます。

```xml
<SnippetTypes>
    <SnippetType>... </SnippetType>
    <SnippetType>... </SnippetType>
</SnippetTypes>
```

|子要素|説明|
|-------------------|-----------------|
|[SnippetType 要素](../ide/code-snippets-schema-reference.md#snippettype-element)|省略可能な要素です。 Visual Studio がコード スニペットをコードに挿入するときの動作を指定します。 `SnippetType` 要素に 0 個以上の `SnippetTypes` 要素があります。|

|親要素|説明|
| - |-----------------|
|[Header 要素](../ide/code-snippets-schema-reference.md#header-element)|コード スニペットに関する全般的な情報を指定します。|

## <a name="title-element"></a>Title 要素

コード スニペットのタイトルを指定します。 コード スニペットの `Title` 要素に格納されたタイトルは、**コード スニペット ピッカー**と、**コード スニペット マネージャー**内のコード スニペットの説明に表示されます。

```xml
<Title>
    Code Snippet Title
</Title>
```

|親要素|説明|
| - |-----------------|
|[Header 要素](../ide/code-snippets-schema-reference.md#header-element)|コード スニペットに関する全般的な情報を指定します。|

テキスト値が必要です。 このテキストでコード スニペットのタイトルを指定します。

## <a name="tooltip-element"></a>ToolTip 要素

コード スニペット内のリテラルまたはオブジェクトに指定される値と使用方法を説明します。これは、プロジェクトにコード スニペットを挿入するときに Visual Studio によって ToolTip に表示されます。 コード スニペットの挿入後、リテラルまたはオブジェクト上にマウスを重ねると、ツールヒントのテキストが表示されます。

```xml
<ToolTip>
    ToolTip description
</ToolTip>
```

|親要素|説明|
| - |-----------------|
|[Literal 要素](../ide/code-snippets-schema-reference.md#literal-element)|編集が可能なコード スニペットのリテラル フィールドを定義します。|
|[Object 要素](../ide/code-snippets-schema-reference.md#object-element)|編集が可能なコード スニペットのオブジェクト フィールドを定義します。|

テキスト値が必要です。 このテキストは、コード スニペットのオブジェクトまたはリテラルに関連付けられる ToolTip の説明を指定します。

## <a name="type-element"></a>型の要素

オブジェクトの種類を指定します。 `Object` 要素は、コード スニペット自体には定義されておらず、外部で定義する必要のある項目を指定するときに使用します。 たとえば、Windows フォーム コントロール、ASP.NET コントロール、オブジェクトのインスタンス、型のインスタンスなどをオブジェクトとして宣言します。 オブジェクトの宣言では、`Type` 要素で型を指定する必要があります。

```xml
<Type>
    Type
</Type>
```

|親要素|説明|
| - |-----------------|
|[Object 要素](../ide/code-snippets-schema-reference.md#object-element)|編集が可能なコード スニペットのオブジェクト フィールドを定義します。|

テキスト値が必要です。 このテキストでオブジェクトの型を指定します。 次に例を示します。

```xml
<Type>System.Data.SqlClient.SqlConnection</Type>
```

## <a name="url-element"></a>Url 要素

参照アセンブリの詳細情報を提供する URL を指定します。

> [!NOTE]
> `Url` 要素は、Visual Basic プロジェクトでのみサポートされます。

```xml
<Url>
    www.microsoft.com
</Url>
```

|親要素|説明|
| - |-----------------|
|[Reference 要素](../ide/code-snippets-schema-reference.md#reference-element)|コード スニペットで参照する必要のあるアセンブリを指定します。|

テキスト値が必要です。 このテキストで、参照アセンブリに関する詳細な情報の入手先 URL を指定します。 プロジェクトに参照を追加できない場合、この URL が表示されます。

## <a name="see-also"></a>関連項目

- [コード スニペット](../ide/code-snippets.md)
- [チュートリアル: コード スニペットを作成する](../ide/walkthrough-creating-a-code-snippet.md)
