---
title: R のコード スニペット
description: Visual Studio の R のコード スニペットでは、任意の長さのコード ブロックをすばやく挿入するショートカットが提供され、似たコードを何度も再入力しなくて済みます。
ms.date: 01/24/2018
ms.topic: conceptual
author: kraigb
ms.author: kraigb
manager: jillfra
ms.workload:
- data-science
ms.openlocfilehash: 31dfa975cea519d4d064856090a265b844f265f6
ms.sourcegitcommit: d8609a78b460d4783f5d59c0c89454910a4dbd21
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2020
ms.locfileid: "88238726"
---
# <a name="code-snippets-for-r"></a>R のコード スニペット

Visual Studio のコード スニペットでは、任意の長さのコード ブロックをすばやく挿入するショートカットが提供され、似たコードを何度も再入力しなくて済みます。 R Tools for Visual Studio (RTVS) では、多くの便利な R スニペットが Visual Studio のコレクションに追加されます。

スニペットを挿入するには、スニペットの省略名を入力して (IntelliSense が用意されています)、**Tab** キーを押します。

簡単な例をいくつか示します。

- 「`=`」と入力して Tab キーを押すと、RTVS はそれを `<-` 代入演算子に展開します。
- 「`>`」と入力して Tab キーを押すと、RTVS はそれを `%>%` パイプ演算子に展開します。

スニペットは、単なる文字入力候補以上のものです。 たとえば、`read.csv` 関数を使用して CSV ファイルを読み取るスニペットの場合、名前やパラメーターを覚える必要がなくなります。

![コード スニペットを使って read.csv の呼び出しを挿入するアニメーション](media/code-snippet-expansion.gif)

この場合、「`readc`」と入力すると、IntelliSense が入力候補を表示します。 ドロップダウンで候補を選んで **Tab** キーを押して `readc` を選び、もう一度 **Tab** キーを押すと、スニペットが展開されます (このため、スニペットの展開は "スニペットを入力して Tab キーを 2 回押す" ことと考えられることがよくあります)。 ほとんどの場合、最初の Tab で IntelliSense の選択が完了し、2 回目の Tab で展開されます。

使用可能なすべてのスニペットを表示するには、**[ツール]** > **[コード スニペット マネージャー]** ダイアログ ボックスを開き (**Ctrl **+** K**、**B**)、**[言語]** で **[R]** を選びます。 グループを展開して個々のスニペットを選ぶと、説明とショートカット テキストが表示されます。

![R の [コード スニペット マネージャー] ダイアログ ボックス](media/code-snippet-dialog.png)

カスタム コード スニペットを作成するには、「[チュートリアル: コード スニペットを作成する](../ide/walkthrough-creating-a-code-snippet.md)」の説明に従います。 結局のところ、コード スニペットは単なる XML ファイルです。 たとえば、次のコードはパイプ操作のスニペットです (ショートカット `>`)。

```xml
<?xml version="1.0" encoding="utf-8" ?>
<CodeSnippets  xmlns="http://schemas.microsoft.com/VisualStudio/2005/CodeSnippet">
  <CodeSnippet Format="1.0.0">
    <Header>
      <Title>Dplyr pipe</Title>
      <Shortcut>&gt;</Shortcut>
      <Description>Code snippet for '%&gt;%' operator</Description>
      <Author>Microsoft Corporation</Author>
      <SnippetTypes>
        <SnippetType>Expansion</SnippetType>
       </SnippetTypes>
    </Header>
    <Snippet>
      <Code Language="R">
        <![CDATA[ %>% $end$]]>
      </Code>
    </Snippet>
  </CodeSnippet>
</CodeSnippets>
```

すべてのコード スニペットの XML ファイルは、RTVS でインストールされます。**[コード スニペット マネージャー]** の **[場所]** フィールドでパスが示されます。 GitHub の [src/Package/Impl/Snippets](https://github.com/Microsoft/RTVS/tree/master/src/Package/Impl/Snippets) で RTVS のソース コードを見つけることもできます。
