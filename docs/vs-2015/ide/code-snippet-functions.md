---
title: コード スニペットの関数 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- code snippets [Visual Studio], functions
- snippets [Visual Studio], functions
- IntelliSense code snippets, functions
ms.assetid: c0a2bf21-8fa5-4457-9281-f599beb53e7d
caps.latest.revision: 15
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 92533b90e6a2da9f29a67d13c6e0eee2c31dbcfe
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72620234"
---
# <a name="code-snippet-functions"></a>コード スニペットの関数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[csprcs](../includes/csprcs-md.md)] コード スニペットで使用できる関数は 3 つあります。 関数は、コード スニペットの [Function](https://msdn.microsoft.com/572c5549-5821-4e15-8ecd-0fa86c1c65df) 要素で指定されています。 コード スニペットの作成については、「[コード スニペット](../ide/code-snippets.md)」を参照してください。

## <a name="functions"></a>関数
 次の表で、コード スニペットの `Function` 要素で使用できる関数について説明します。

|関数|説明|言語|
|--------------|-----------------|--------------|
|`GenerateSwitchCases(` `EnumerationLiteral` `)`|`EnumerationLiteral` パラメーターで指定された列挙体のメンバー用に、switch ステートメントおよび一連の case ステートメントを生成します。 `EnumerationLiteral` パラメーターは、列挙体リテラルまたは列挙型のいずれかへの参照にする必要があります。|[!INCLUDE[csprcs](../includes/csprcs-md.md)]|
|`ClassName()`|挿入されたスニペットを含むクラスの名前を返します。|[!INCLUDE[csprcs](../includes/csprcs-md.md)]|
|`SimpleTypeName(` `TypeName` `)`|*TypeName* パラメーターを、スニペットが呼び出されたコンテキストで最も単純な形式に縮小します。|[!INCLUDE[csprcs](../includes/csprcs-md.md)]|

## <a name="example"></a>例
 次の例は、`GenerateSwitchCases` 関数の使用法を示しています。 このスニペットが挿入され、列挙体が `$switch_on$` リテラルに入力されると、`$cases$` リテラルによって列挙体の値ごとに `case` ステートメントが生成されます。

```
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

## <a name="example"></a>例
 次の例は、`ClassName` 関数の使用法を示しています。 このスニペットが挿入されると、`$classname$` リテラルは、コード ファイルでその位置にある外側のクラスの名前で置換されます。

```
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
            <Code Language="vjsharp" Format="CData">
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

## <a name="example"></a>例
 この例では、`SimpleTypeName` 関数の使用方法を示します。 このスニペットがコード ファイルに挿入されると、`$SystemConsole$` リテラルは、このスニペットが呼び出されたコンテキストで最も単純な形式の <xref:System.Console> 型で置換されます。

```
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
 [Function 要素 (Intellisense コードスニペット)](https://msdn.microsoft.com/572c5549-5821-4e15-8ecd-0fa86c1c65df) [コードスニペットスキーマリファレンス](../ide/code-snippets-schema-reference.md)
