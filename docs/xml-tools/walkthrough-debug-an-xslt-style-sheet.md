---
title: XSLT スタイル シートをデバッグする
description: このチュートリアルの手順に従って Visual Studio の XSLT デバッガーを使用し、XSLT スタイル シートをデバッグする方法について学習します。
ms.custom: SEO-VS-2020
ms.date: 03/05/2019
ms.topic: how-to
ms.assetid: 3db9fa5a-f619-4cb6-86e7-64b364e58e5d
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3a6f1efc85366bc74206dc8637c992f249c4eb44
ms.sourcegitcommit: e443866e3468f838bc3655ad56a83a552013ceed
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/28/2021
ms.locfileid: "98925880"
---
# <a name="walkthrough-debug-an-xslt-style-sheet"></a>チュートリアル: XSLT スタイル シートのデバッグ

このチュートリアルの手順では、XSLT デバッガーを使用する方法を示します。 変数の表示、ブレークポイントの設定、コードのステップ実行などの手順が含まれます。 デバッガーでは、コードを一度に 1 行ずつ実行することができます。

このチュートリアルを準備するには、まず、2 つの [サンプル ファイル](#sample-files)をローカル コンピューターにコピーします。 1 つはスタイル シートで、もう 1 つはスタイル シートへの入力として使用する XML ファイルです。 このチュートリアルで使用するスタイル シートでは、コストが平均書籍価格を下回るすべての書籍が検索されます。

> [!NOTE]
> XSLT デバッガーは、Visual Studio の Professional および Enterprise エディションでのみ使用できます。

## <a name="start-debugging"></a>[デバッグ開始]

1. **[ファイル]** メニューの **[開く]**  >  **[ファイル]** を選択します。

2. *below-average.xsl* ファイルを見つけて、 **[開く]** を選択します。

   XML エディターでスタイル シートが開かれます。

3. ドキュメントのプロパティ ウィンドウの **[入力]** フィールドで、参照ボタン **[...]** をクリックします。 ( **[プロパティ]** ウィンドウが表示されていない場合は、エディターで開いているファイルの任意の場所を右クリックし、 **[プロパティ]** を選択します)。

4. *books.xml* ファイルを見つけ、 **[開く]** を選択します。

   これで、XSLT 変換のために使用されるソース ドキュメント ファイルが設定されます。

5. *below-average.xsl* の 12 行目に [ブレークポイント](../debugger/using-breakpoints.md)を設定します。 次のいずれかの方法でできます。

   - エディターで 12 行目の余白をクリックします。

   - 12 行目の任意の場所をクリックし、**F9** キーを押します。

   - `xsl:if` 開始タグを右クリックし、 **[ブレークポイント]**  >  **[ブレークポイントの挿入]** を選択します。

      ![Visual Studio で XSL ファイルにブレークポイントを挿入する](media/insert-breakpoint.PNG)

6. メニュー バーで、 **[XML]**  >  **[XSLT デバッグを開始]** を選択します (または、**Alt** + **F5** キーを押します)。

   デバッグ プロセスが開始されます。

   エディターで、デバッガーがスタイル シートの `xsl:if` 要素に配置されます。 エディターで *below-average.xml* という名前の別のファイルが開かれます。これは出力ファイルであり、入力ファイル *books.xml* の各ノードが処理されるたびに設定されます。

   Visual Studio ウィンドウの下部に、 **[自動変数]** 、 **[ローカル]** 、および **[ウォッチ 1]** ウィンドウが表示されます。 **[ローカル]** ウィンドウには、すべてのローカル変数と、それらの現在の値が表示されます。 ここには、スタイル シートで定義されている変数や、コンテキスト内に現在存在するノードを追跡するためにデバッガーが使用する変数なども表示されます。

## <a name="watch-window"></a>[ウォッチ] ウィンドウ

2 つの変数を **[ウォッチ 1]** ウィンドウに追加し、入力ファイルが処理されるときに値を調べることができるようにします。 ( **[ローカル]** ウィンドウを使用して、ウォッチする変数が既に存在する場合に値を確認することもできます)。

1. **[デバッグ]** メニューの **[ウィンドウ]**  >  **[ウォッチ]**  >  **[ウォッチ 1]** を選択します。

   **[ウォッチ 1]** ウィンドウが表示されるようになります。

2. **[名前]** フィールドに「`$bookAverage`」と入力して、**Enter** キーを押します。

   `$bookAverage` 変数の値が、 **[値]** フィールドに表示されます。

3. 次の行の **[名前]** フィールドに「`self::node()`」と入力して、**Enter** キーを押します。

   `self::node()` は、現在のコンテキスト ノードに評価される XPath 式です。 `self::node()` XPath 式の値は、最初の book ノードです。 この値は、変換処理の進行につれて変化します。

4. `self::node()` ノードを展開し、値が `price` であるノードを展開します。

   ![Visual Studio での XSLT デバッグ時の [ウォッチ] ウィンドウ](media/xslt-debugging-watch-window.png)

   現在の book ノードの書籍価格の値を確認でき、それを `$bookAverage` の値と比較できます。 この書籍価格は平均値より低いため、デバッグ プロセスを続けると `xsl:if` 条件は成功するはずです。

## <a name="step-through-the-code"></a>コードをステップ実行する

1. **F5** キーを押して続行します。

   最初の book ノードは `xsl:if` の条件を満たしたため、この book ノードは *below-average.xml* 出力ファイルに追加されます。 デバッガーは、再度スタイル シートの `xsl:if` 要素に到達するまで、引き続き実行されます。 今度は、デバッガーが、*books.xml* ファイルの 2 番目の book ノードに到達して中断します。

   **[ウォッチ 1]** ウィンドウでは、`self::node()` の値が 2 番目の book ノードに変化します。 price 要素の値を調べることで、価格が平均値より高いことを判断できるため、`xsl:if` 条件は失敗します。

2. **F5** キーを押して続行します。

   2 番目の book ノードは `xsl:if` の条件を満たしていないため、この book ノードは *below-average.xml* 出力ファイルに追加されません。 デバッガーは、再度スタイル シートの `xsl:if` 要素に到達するまで、引き続き実行されます。 今度は、デバッガーが、*books.xml* ファイルの 3 番目の `book` ノードに到達して中断します。

   **[ウォッチ 1]** ウィンドウでは、`self::node()` の値が 3 番目の book ノードに変化します。 `price` 要素の値を調べると、価格が平均値未満です。 `xsl:if` の条件が満たされています。

3. **F5** キーを押して続行します。

   `xsl:if` の条件が満たされたため、3 番目の book ノードは *below-average.xml* 出力ファイルに追加されます。 XML ドキュメント内の書籍がすべて処理され、デバッガーが停止します。

## <a name="sample-files"></a>サンプル ファイル

このチュートリアルでは、次の 2 つのファイルを使用します。

### <a name="below-averagexsl"></a>below-average.xsl

```xml
<?xml version='1.0'?>
<xsl:stylesheet version="1.0"
      xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
  <xsl:output method="xml" encoding="utf-8"/>
  <xsl:template match="/">
    <xsl:variable name="bookCount" select="count(/bookstore/book)"/>
    <xsl:variable name="bookTotal" select="sum(/bookstore/book/price)"/>
    <xsl:variable name="bookAverage" select="$bookTotal div $bookCount"/>
    <books>
      <!--Books That Cost Below Average-->
      <xsl:for-each select="/bookstore/book">
        <xsl:if test="price &lt; $bookAverage">
          <xsl:copy-of select="."/>
        </xsl:if>
      </xsl:for-each>
    </books>
  </xsl:template>
</xsl:stylesheet>
```

### <a name="booksxml"></a>books.xml

```xml
<?xml version='1.0'?>
<!-- This file represents a fragment of a book store inventory database -->
<bookstore>
  <book genre="autobiography" publicationdate="1981" ISBN="1-861003-11-0">
    <title>The Autobiography of Benjamin Franklin</title>
    <author>
      <first-name>Benjamin</first-name>
      <last-name>Franklin</last-name>
    </author>
    <price>8.99</price>
  </book>
  <book genre="novel" publicationdate="1967" ISBN="0-201-63361-2">
    <title>The Confidence Man</title>
    <author>
      <first-name>Herman</first-name>
      <last-name>Melville</last-name>
    </author>
    <price>11.99</price>
  </book>
  <book genre="philosophy" publicationdate="1991" ISBN="1-861001-57-6">
    <title>The Gorgias</title>
    <author>
      <name>Plato</name>
    </author>
    <price>9.99</price>
  </book>
</bookstore>
```

## <a name="see-also"></a>関連項目

- [XSLT のデバッグ](../xml-tools/debugging-xslt.md)
