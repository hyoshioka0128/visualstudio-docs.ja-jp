---
title: 'チュートリアル: コード スニペットを作成する | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- code snippets, creating
- code snippets, shortcut
- code snippets, template
- code snippets, replacements
- code snippets, references
- code snippets, imports
ms.assetid: 0dcaae11-39cf-4463-9c90-2494321251c2
caps.latest.revision: 25
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 278858eb28e0db7edd2694397cc7b24f1cfec301
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74296830"
---
# <a name="walkthrough-creating-a-code-snippet"></a>チュートリアル: コード スニペットを作成する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

コード スニペットは、わずかな手順で作成できます。 必要な操作は、XML ファイルを作成し、適切な要素を指定して、コードを追加するだけです。 コードには、参照や置換パラメーターを追加することもできます。 Visual Studio インストールにスニペットを追加するには、コード スニペット マネージャー ( **[ツール]、[コード スニペット マネージャー]** ) の [インポート] を使用します。

> [!TIP]
> コード スニペットをより簡単に作成する方法の詳細については、CodePlex の Web サイトで、[Snippet Editor](https://go.microsoft.com/fwlink/?LinkId=251033) などのコミュニティ ツールを検索してください。

## <a name="snippet-template"></a>スニペット テンプレート
 基本的なスニペット テンプレートを次に示します。

```
<?xml version="1.0" encoding="utf-8"?>
<CodeSnippets
    xmlns="http://schemas.microsoft.com/VisualStudio/2005/CodeSnippet">
    <CodeSnippet Format="1.0.0">
        <Header>
            <Title></Title>
        </Header>
        <Snippet>
            <Code Language="">
                <![CDATA[]]>
            </Code>
        </Snippet>
    </CodeSnippet>
</CodeSnippets>

```

### <a name="to-create-a-code-snippet"></a>コード スニペットを作成するには

1. Visual Studio で新しい XML ファイルを作成し、上に示したテンプレートを追加します。

2. Title 要素に、スニペットのタイトル (「Hello World VB」など) を指定します。

3. Code 要素の Languages 属性に、スニペットの言語を指定します。 この例では、"VB" を使用します。

4. Code 要素内の CDATA セクションにコードを追加します。次に例を示します。

    ```
    <Code Language="VB">
        <![CDATA[Console.WriteLine("Hello, World!")]]>
    </Code>

    ```

5. VBCodeSnippet.snippet としてスニペットを保存します。

### <a name="to-add-a-code-snippet-to-visual-studio"></a>コード スニペットを Visual Studio に追加するには

1. コード スニペット マネージャーを使用すると、独自のスニペットを Visual Studio インストールに追加できます。 コード スニペット マネージャーを開きます ( **[ツール]、[コード スニペット マネージャー]** )。

2. [インポート] ボタンをクリックします。

3. 前の手順でコード スニペットを保存した場所に移動し、コード スニペットを選択して、 **[開く]** をクリックします。

4. **[コード スニペットのインポート]** ダイアログが開き、右ウィンドウの選択肢からスニペットを追加するように求められます。 選択肢の 1 つに **[マイ コード スニペット]** があります。 これを選択し、 **[完了]** 、 **[OK]** の順にクリックします。

5. スニペットが次の場所にコピーされます。

     `%USERPROFILE%\Documents\Visual Studio 2013\Code Snippets\Visual Basic\My Code Snippets`

6. Visual Basic プロジェクトを開き、コード ファイルを開くことによって、スニペットをテストします。 ファイル内でコンテキスト メニューの **[スニペットの挿入]** をクリックし、 **[マイ コード スニペット]** をクリックします。 **[My Visual Basic Code Snippet]** (マイ Visual Basic コード スニペット) という名前のスニペットが表示されます。 これをダブルクリックします。

7. コード内に `Console.WriteLine("Hello, World!")` が挿入されます。

### <a name="adding-description-and-shortcut-fields"></a>Description フィールドと Shortcut フィールドの追加

1. Description フィールドは、コード スニペット マネージャーに表示された際に、コード スニペットに関する詳しい情報を提供します。 ショートカットとは、スニペットを挿入するためにユーザーが入力できるタグです。 ファイル `%USERPROFILE%\Documents\Visual Studio 2013\Code Snippets\Visual Basic\My Code Snippet\VBCodeSnippet.snippet`を開いて、追加したスニペットを編集します。

2. Author 要素と Description 要素を Header 要素に追加し、情報を入力します。

3. Header 要素は次のようになります。

    ```
    <Header>
        <Title>Hello World VB</Title>
        <Author>Myself</Author>
        <Description>Says Hello to the world.</Description>
    </Header>

    ```

4. コード スニペット マネージャーを開き、コード スニペットを開きます。 右ペインで、Description フィールドと Author フィールドが指定されていることを確認します。

5. ショートカットを追加するには、Author 要素および Description 要素と共に Shortcut 要素を追加します。

    ```
    <Header>
        <Title>Hello World VB</Title>
        <Author>Myself</Author>
        <Description>Says Hello to the world.</Description>
        <Shortcut>hello</Shortcut>
    </Header>

    ```

6. スニペット ファイルを再度保存します。

7. ショートカットをテストするには、Visual Basic プロジェクトを開き、コード ファイルを開きます。 ファイルに「`hello`」と入力し、TAB キーを押します。 スニペット コードが挿入されます。

### <a name="to-add-references-and-imports"></a>参照とインポートを追加するには

1. Visual Basic スニペットでは、References 要素を使用してプロジェクトに参照を追加し、Imports 要素を使用して Imports 宣言を追加することができます (他の言語のスニペットには、この機能がありません)。たとえば、コード例の `Console.WriteLine` を `MessageBox.Show`に変更した場合は、プロジェクトに system.servicemodel アセンブリを追加する必要があります。

2. スニペットを開きます。

3. Snippet 要素の下に References 要素を追加します。

    ```
    <References>
        <Reference>
            <Assembly>System.Windows.Forms.dll</Assembly>
        </Reference>
    </References>

    ```

4. Snippet 要素の下に Imports 要素を追加します。

    ```
    <Imports>
        <Import>
           <Namespace>System.Windows.Forms</Namespace>
        </Import>
    </Imports>

    ```

5. CDATA セクションを次のように変更します。

    ```
    <![CDATA[MessageBox.Show("Hello, World!")]]>
    ```

6. スニペットを保存します。

7. Visual Basic プロジェクトを開き、スニペットを追加します。

8. コード ファイルの先頭で、次の Imports ステートメントを確認できます。

    ```
    Imports System.Windows.Forms

    ```

9. プロジェクトのプロパティを確認します。 References タブでには、System.Windows.Forms.dll への参照が含まれています。

### <a name="adding-replacements"></a>置換の追加

1. コード スニペットの一部をユーザーが置換できるように指定することができます。たとえば、変数を追加しておき、ユーザーが現在のプロジェクト内の変数に置換できるようにする場合などです。 使用できる置換には、リテラル置換とオブジェクト置換の 2 種類があります。 リテラルは、いずれかの種類 (文字列リテラル、変数名、数値の文字列形式) の文字列です。 オブジェクトは、文字列以外の型のインスタンスです。 この手順では、リテラル置換およびオブジェクト置換を宣言し、これらの置換が参照されるようにコードを変更します。

2. スニペットを開きます。

3. この例では、SQL 接続文字列を使用するため、Imports 要素と References 要素を変更して、適切な参照を追加する必要があります。

    ```
    <References>
        <Reference>
            <Assembly>System.Data.dll</Assembly>
        </Reference>
        <Reference>
            <Assembly>System.Xml.dll</Assembly>
        </Reference>
    </References>
    <Imports>
        <Import>
            <Namespace>System.Data</Namespace>
        </Import>
        <Import>
            <Namespace>System.Data.SqlClient</Namespace>
        </Import>
    </Imports>

    ```

4. SQL 接続文字列用のリテラル置換を宣言するには、Declarations 要素を Snippet 要素の下に追加し、その中に Literal 要素を追加します。さらにその中に、置換する ID、ツールヒント、および既定値を指定するためのサブ要素を追加します。

    ```
    <Declarations>
        <Literal>
            <ID>SqlConnString</ID>
            <ToolTip>Replace with a SQL connection string.</ToolTip>
            <Default>"SQL connection string"</Default>
        </Literal>
    </Declarations>

    ```

5. SQL 接続用のオブジェクト置換を宣言するには、Object 要素を Declarations 要素内に追加し、ID、オブジェクトの型、ツールヒント、および既定値を指定するためのサブ要素を追加します。 その結果、Declarations 要素は次のようになります。

    ```
    <Declarations>
        <Literal>
            <ID>SqlConnString</ID>
            <ToolTip>Replace with a SQL connection string.</ToolTip>
            <Default>"SQL connection string"</Default>
        </Literal>
        <Object>
            <ID>SqlConnection</ID>
            <Type>System.Data.SqlClient.SqlConnection</Type>
            <ToolTip>Replace with a connection object in your application.</ToolTip>
            <Default>dcConnection</Default>
        </Object>
    </Declarations>
    ```

6. Code セクションでは、置換項目を $ 記号で囲んで参照します (例: `$replacement$`)。

    ```
    <Code Language="VB" Kind="method body">
        <![CDATA[Dim daCustomers As SqlDataAdapter
            Dim selectCommand As SqlCommand

            daCustomers = New SqlClient.SqlDataAdapter()
            selectCommand = new SqlClient.SqlCommand($SqlConnString$)
            daCustomers.SelectCommand = selectCommand
            daCustomers.SelectCommand.Connection = $SqlConnection$]]>
    </Code>
    ```

7. スニペットを保存します。

8. Visual Basic プロジェクトを開き、スニペットを追加します。

9. コードは次のようになります。置換項目 `SQL connection string` と `dcConnection` は明るいオレンジ色で強調表示されます。 項目間を移動するには、Tab キーを押します。

    ```
    Dim daCustomers As SqlDataAdapter
    Dim selectCommand As SqlCommand

    daCustomers = New SqlClient.SqlDataAdapter()
    selectCommand = New SqlClient.SqlCommand("SQL connection string")
    daCustomers.SelectCommand = selectCommand
    daCustomers.SelectCommand.Connection = dcConnection

    ```

## <a name="see-also"></a>関連項目
 [コード スニペット スキーマ リファレンス](../ide/code-snippets-schema-reference.md)
