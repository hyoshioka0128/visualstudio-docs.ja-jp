---
title: コード スニペットの関数
description: C# コード スニペットで使用できる GenerateSwitchCases(EnumerationLiteral)、ClassName()、および SimpleTypeName(TypeName) 関数について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- code snippets [Visual Studio], functions
- snippets [Visual Studio], functions
- IntelliSense code snippets, functions
ms.assetid: c0a2bf21-8fa5-4457-9281-f599beb53e7d
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e6529f4f82f7a8a6862ae85adbf170d2fb6f8706
ms.sourcegitcommit: 66cda27b63c9b55782b1db223a6dbda9f8cabe13
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2020
ms.locfileid: "95006511"
---
# <a name="code-snippet-functions"></a>コード スニペットの関数

C# コード スニペットで使用できる関数は 3 つあります。 関数は、コード スニペットの [Function](../ide/code-snippets-schema-reference.md#function-element) 要素で指定されています。 コード スニペットの作成については、「[コード スニペット](../ide/code-snippets.md)」を参照してください。

## <a name="functions"></a>機能

次の表で、コード スニペットの `Function` 要素で使用できる関数について説明します。

|関数|説明|Language|
|--------------|-----------------|--------------|
|`GenerateSwitchCases(EnumerationLiteral)`|`EnumerationLiteral` パラメーターで指定された列挙体のメンバー用に、switch ステートメントおよび一連の case ステートメントを生成します。 `EnumerationLiteral` パラメーターは、列挙体リテラルまたは列挙型のいずれかへの参照にする必要があります。|C#|
|`ClassName()`|挿入されたスニペットを含むクラスの名前を返します。|C#|
|`SimpleTypeName(TypeName)`|*TypeName* パラメーターを、スニペットが呼び出されたコンテキストで最も単純な形式に縮小します。|C#|

## <a name="generateswitchcases-example"></a>GenerateSwitchCases の例

次の例は、`GenerateSwitchCases` 関数の使用法を示しています。 このスニペットが挿入され、列挙体が `$switch_on$` リテラルに入力されると、`$cases$` リテラルによって列挙体の値ごとに `case` ステートメントが生成されます。

```xml
<CodeSnippets xmlns="http://schemas.microsoft.com/VisualStudio/2005/CodeSnippet">
    <CodeSnippet Format="1.0.0">
        <Header>
            <Title>switch</Title>
            <Shortcut>switch</Shortcut>
            <Description>Code snippet for switch statement</Description>
            <Author>Microsoft Corporation</Author>
            <SnippetTypes>
                <SnippetType>Expansion</SnippetType>
            </SnippetTypes>
        </Header>
        <Snippet>
            <Declarations>
                <Literal>
                    <ID>expression</ID>
                    <ToolTip>Expression to switch on</ToolTip>
                    <Default>switch_on</Default>
                </Literal>
                <Literal Editable="false">
                    <ID>cases</ID>
                    <Function>GenerateSwitchCases($expression$)</Function>
                    <Default>default:</Default>
                </Literal>
            </Declarations>
            <Code Language="csharp">
                <![CDATA[
                    switch ($expression$)
                    {
                        $cases$
                    }
                ]]>
            </Code>
        </Snippet>
    </CodeSnippet>
</CodeSnippets>
```

## <a name="classname-example"></a>ClassName の例

次の例は、`ClassName` 関数の使用法を示しています。 このスニペットが挿入されると、`$classname$` リテラルは、コード ファイルでその位置にある外側のクラスの名前で置換されます。

```xml
<CodeSnippets xmlns="http://schemas.microsoft.com/VisualStudio/2005/CodeSnippet">
    <CodeSnippet Format="1.0.0">
        <Header>
            <Title>Common constructor pattern</Title>
            <Shortcut>ctor</Shortcut>
            <Description>Code Snippet for a constructor</Description>
            <Author>Microsoft Corporation</Author>
            <SnippetTypes>
                <SnippetType>Expansion</SnippetType>
            </SnippetTypes>
        </Header>
        <Snippet>
            <Declarations>
                <Literal>
                    <ID>type</ID>
                    <Default>int</Default>
                </Literal>
                <Literal>
                    <ID>name</ID>
                    <Default>field</Default>
                </Literal>
                <Literal default="true" Editable="false">
                    <ID>classname</ID>
                    <ToolTip>Class name</ToolTip>
                    <Function>ClassName()</Function>
                    <Default>ClassNamePlaceholder</Default>
                </Literal>
            </Declarations>
            <Code Language="csharp" Format="CData">
                <![CDATA[
                    public $classname$ ($type$ $name$)
                    {
                        this._$name$ = $name$;
                    }
                    private $type$ _$name$;
                ]]>
            </Code>
        </Snippet>
    </CodeSnippet>
</CodeSnippets>
```

## <a name="simpletypename-example"></a>SimpleTypeName の例

この例では、`SimpleTypeName` 関数の使用方法を示します。 このスニペットがコード ファイルに挿入されると、`$SystemConsole$` リテラルは、このスニペットが呼び出されたコンテキストで最も単純な形式の <xref:System.Console> 型で置換されます。

```xml
<CodeSnippets xmlns="http://schemas.microsoft.com/VisualStudio/2005/CodeSnippet">
    <CodeSnippet Format="1.0.0">
        <Header>
            <Title>Console_WriteLine</Title>
            <Shortcut>cw</Shortcut>
            <Description>Code snippet for Console.WriteLine</Description>
            <Author>Microsoft Corporation</Author>
            <SnippetTypes>
                <SnippetType>Expansion</SnippetType>
            </SnippetTypes>
        </Header>
        <Snippet>
            <Declarations>
                <Literal Editable="false">
                    <ID>SystemConsole</ID>
                    <Function>SimpleTypeName(global::System.Console)</Function>
                </Literal>
            </Declarations>
            <Code Language="csharp">
                <![CDATA[
                    $SystemConsole$.WriteLine();
                ]]>
            </Code>
        </Snippet>
    </CodeSnippet>
</CodeSnippets>
```

## <a name="see-also"></a>関連項目

- [Function 要素](../ide/code-snippets-schema-reference.md#function-element)
- [コード スニペット スキーマ リファレンス](../ide/code-snippets-schema-reference.md)
