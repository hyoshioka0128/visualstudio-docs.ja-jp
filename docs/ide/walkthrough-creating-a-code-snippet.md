---
title: 'チュートリアル: コード スニペットを作成する'
ms.date: 03/31/2020
ms.topic: conceptual
helpviewer_keywords:
- code snippets, creating
- code snippets, shortcut
- code snippets, template
- code snippets, replacements
- code snippets, references
- code snippets, imports
ms.assetid: 0dcaae11-39cf-4463-9c90-2494321251c2
author: TerryGLee
ms.author: tglee
manager: jillfra
dev_langs:
- VB
ms.workload:
- multiple
ms.openlocfilehash: 1bfadb4b8d1836d131b669ea43f28f522f3fbd8b
ms.sourcegitcommit: ce3d0728ec1063ab548dac71c8eaf26d20450acc
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/01/2020
ms.locfileid: "80472816"
---
# <a name="walkthrough-create-a-code-snippet"></a>チュートリアル: コード スニペットを作成する

コード スニペットは、わずかな手順で作成できます。 必要な操作は、XML ファイルを作成し、適切な要素を指定して、コードを追加するだけです。 必要に応じて、置換パラメーターとプロジェクト参照を利用できます。 ご利用の Visual Studio インストールにスニペットをインポートするには、**コード スニペット マネージャー** ( **[ツール]**  >  **[コード スニペット マネージャー]** ) の **[インポート]** ボタンを使用します。

## <a name="snippet-template"></a>スニペット テンプレート

基本的な XML スニペット テンプレートを次に示します。

```xml
<?xml version="1.0" encoding="utf-8"?>
<CodeSnippets xmlns="http://schemas.microsoft.com/VisualStudio/2005/CodeSnippet">
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

## <a name="create-a-code-snippet"></a>コード スニペットを作成する

1. Visual Studio で新しい XML ファイルを作成し、上に示したテンプレートを追加します。

2. **Title** 要素に、スニペットのタイトルを指定します。 タイトル **Square Root** を使用します。

3. **Code** 要素の **Language** 属性に、スニペットの言語を指定します。 C# の場合は **CSharp** を、Visual Basic の場合は **VB** を、C++ の場合は **CPP** を使用します。

   > [!TIP]
   > 使用できる言語値をすべて確認するには、「[コード スニペット スキーマ リファレンス](code-snippets-schema-reference.md)」ページの[コード要素の属性](code-snippets-schema-reference.md#attributes)に関するセクションを参照してください。

4. **Code** 要素内の **CDATA** セクションにスニペット コードを追加します。

   C# の場合 :

   ```xml
   <Code Language="CSharp">
       <![CDATA[double root = Math.Sqrt(16);]]>
   </Code>
   ```

   あるいは、Visual Basic の場合:

   ```xml
   <Code Language="VB">
       <![CDATA[Dim root = Math.Sqrt(16)]]>
   </Code>
   ```

   > [!NOTE]
   > コード スニペットの **CDATA** セクション内のコード行をインデントまたは書式設定する方法を指定することはできません。 挿入時に、言語サービスによって挿入されるコードの書式が自動的に設定されます。

5. スニペットを *SquareRoot.snippet* として保存します (任意の場所に保存できます)。

## <a name="import-a-code-snippet"></a>コード スニペットを挿入する

1. ご利用の Visual Studio インストールには、**コード スニペット マネージャー**を使用して、スニペットをインポートすることができます。 **[ツール]**  >  **[コード スニペット マネージャー]** の順に選択して開きます。

2. **[インポート]** ボタンをクリックします。

3. 前の手順でコード スニペットを保存した場所に移動し、コード スニペットを選択して、 **[開く]** をクリックします。

4. **[コード スニペットのインポート]** ダイアログが開き、右ウィンドウの選択肢からスニペットを追加するように求められます。 選択肢の 1 つに **[マイ コード スニペット]** があります。 これを選択し、 **[完了]** 、 **[OK]** の順にクリックします。

5. スニペットは、コード言語に応じて、次のいずれかの場所にコピーされます。

   ::: moniker range="vs-2017"

   *%USERPROFILE%\Documents\Visual Studio 2017\Code Snippets\Visual C#\My Code Snippets*
    *%USERPROFILE%\Documents\Visual Studio 2017\Code Snippets\Visual Basic\My Code Snippets*

   ::: moniker-end

   ::: moniker range=">=vs-2019"

   *%USERPROFILE%\Documents\Visual Studio 2019\Code Snippets\Visual C#\My Code Snippets*
    *%USERPROFILE%\Documents\Visual Studio 2019\Code Snippets\Visual Basic\My Code Snippets*

   ::: moniker-end

6. C# または Visual Basic プロジェクトを開いて、そのスニペットをテストします。 エディターでコード ファイルを開いた状態にして、右クリック メニューの **[スニペット]**  >  **[スニペットの挿入]** の順に選択し、次に **[マイ コード スニペット]** を選択します。 **Square Root** という名前のスニペットが表示されるはずです。 これをダブルクリックします。

   スニペット コードがコード ファイルに挿入されます。

## <a name="description-and-shortcut-fields"></a>Description フィールドと Shortcut フィールド

::: moniker range="vs-2017"

1. Description フィールドは、コード スニペット マネージャーに表示された際に、コード スニペットに関する詳しい情報を提供します。 ショートカットとは、スニペットを挿入するためにユーザーが入力できるタグです。 追加したスニペットを編集するために、 *%USERPROFILE%\Documents\Visual Studio 2017\Code Snippets\\[Visual C# or Visual Basic]\My Code Snippet\SquareRoot.snippet* ファイルを開きます。

::: moniker-end

::: moniker range=">=vs-2019"

1. Description フィールドは、コード スニペット マネージャーに表示された際に、コード スニペットに関する詳しい情報を提供します。 ショートカットとは、スニペットを挿入するためにユーザーが入力できるタグです。 追加したスニペットを編集するために、 *%USERPROFILE%\Documents\Visual Studio 2019\Code Snippets\\[Visual C# or Visual Basic]\My Code Snippet\SquareRoot.snippet* ファイルを開きます。

::: moniker-end

   > [!TIP]
   > 編集するファイルは、Visual Studio によってディレクトリに配置されているので、そのファイルを Visual Studio に再インポートする必要はありません。

2. **Author** 要素と **Description** 要素を **Header** 要素に追加し、情報を入力します。

3. **Header** 要素は次のようになります。

   ```xml
   <Header>
       <Title>Square Root</Title>
       <Author>Myself</Author>
       <Description>Calculates the square root of 16.</Description>
   </Header>
   ```

4. **コード スニペット マネージャー**を開き、コード スニペットを開きます。 右ペインで、**Description** フィールドと **Author** フィールドが指定されていることに注目してください。

   ![コード スニペット マネージャーでのコード スニペットの説明](media/code-snippet-description-author.png)

5. ショートカットを追加するには、次のように **Header** 要素内に **Shortcut** 要素を追加します。

   ```xml
   <Header>
      <Title>Square Root</Title>
      <Author>Myself</Author>
      <Description>Calculates the square root of 16.</Description>
      <Shortcut>sqrt</Shortcut>
    </Header>
   ```

6. スニペット ファイルを再度保存します。

7. ショートカットをテストするには、以前に使用したプロジェクトを開いて、エディターに「**sqrt** 」と入力し、**Tab** キーを押します (Visual Basic の場合は 1 回、C# の場合は 2 回)。

   スニペット コードが挿入されます。

## <a name="replacement-parameters"></a>置換パラメーター

コード スニペットの一部をユーザーによって置き換えられるようにすることができます。 たとえば、ユーザーが変数名をユーザーの現在のプロジェクトに含まれる名前に置き換えられるようにしたいとします。 使用できる置換には、リテラル置換とオブジェクト置換の 2 種類があります。 [Literal 要素](code-snippets-schema-reference.md#literal-element)を使用すれば、スニペット内に完全に含まれているがコードに挿入された後にカスタマイズされる可能性が高いコード (文字列や数値など) に対する置換が識別されます。 [Object 要素](code-snippets-schema-reference.md#object-element)を使用すると、コード スニペットで必須とされているがスニペット自体の外側で定義される可能性が高い項目 (オブジェクト インスタンスやコントロールなど) が識別されます。

1. ユーザーが平方根を計算する数値を簡単に置き換えることができるようにするには、*SquareRoot.snippet*  ファイルの **Snippet** 要素を次のように変更します。

   ```xml
   <Snippet>
     <Code Language="CSharp">
       <![CDATA[double root = Math.Sqrt($Number$);]]>
     </Code>
     <Declarations>
       <Literal>
         <ID>Number</ID>
         <ToolTip>Choose the number you want the square root of.</ToolTip>
         <Default>16</Default>
       </Literal>
     </Declarations>
   </Snippet>
   ```

   リテラル置換に ID (`Number`) が指定されていることに注目してください。 その ID は、`$` 文字を使用して囲むことで、コード スニペット内から参照されます。

   ```xml
   <![CDATA[double root = Math.Sqrt($Number$);]]>
   ```

2. スニペット ファイルを保存します。

3. プロジェクトを開き、スニペットを挿入します。

   コード スニペットが挿入され、編集可能なリテラルが置換対象として強調表示されます。 置換パラメーターにカーソルを合わせると、値のヒントが表示されます。

   ![Visual Studio でのコード スニペット置換パラメーターに関するヒント](media/snippet-replacement-parameter-tooltip.png)

   > [!TIP]
   > スニペット内に置換可能なパラメーターが複数存在する場合は、**Tab** キーを押すと、次のパラメーターに移動し、値が変化します。

## <a name="import-a-namespace"></a>名前空間をインポートする

コード スニペットを使用すれば、[Imports 要素](code-snippets-schema-reference.md#imports-element)を含めることで、`using` ディレクティブ (C#) または `Imports` ステートメント (Visual Basic) を追加できます。 .NET Framework プロジェクトの場合は、[References 要素](code-snippets-schema-reference.md#references-element)を使用してプロジェクトへの参照を追加することもできます。

次の XML で示すコード スニペットでは、System.IO 名前空間内に `File.Exists` メソッドが使用され、その結果として、System.IO 名前空間をインポートする **Imports** 要素が定義されています。

```xml
<?xml version="1.0" encoding="utf-8"?>
<CodeSnippets xmlns="http://schemas.microsoft.com/VisualStudio/2005/CodeSnippet">
  <CodeSnippet Format="1.0.0">
    <Header>
      <Title>File Exists</Title>
      <Shortcut>exists</Shortcut>
    </Header>
    <Snippet>
      <Code Language="CSharp">
        <![CDATA[var exists = File.Exists("C:\\Temp\\Notes.txt");]]>
      </Code>
      <Imports>
        <Import>
          <Namespace>System.IO</Namespace>
        </Import>
      </Imports>
    </Snippet>
  </CodeSnippet>
</CodeSnippets>
```

## <a name="see-also"></a>関連項目

- [コード スニペット スキーマ リファレンス](../ide/code-snippets-schema-reference.md)
