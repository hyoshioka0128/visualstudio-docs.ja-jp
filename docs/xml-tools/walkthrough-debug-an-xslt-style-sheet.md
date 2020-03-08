---
title: XSLT スタイルシートのデバッグ
ms.date: 03/05/2019
ms.topic: conceptual
ms.assetid: 3db9fa5a-f619-4cb6-86e7-64b364e58e5d
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: cd5882cc606bf241a281940464ba028e77986807
ms.sourcegitcommit: 3154387056160bf4c36ac8717a7fdc0cd9faf3f9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78410111"
---
# <a name="walkthrough-debug-an-xslt-style-sheet"></a>チュートリアル: XSLT スタイルシートのデバッグ

このチュートリアルの手順では、XSLT デバッガーを使用する方法を示します。 変数の表示、ブレークポイントの設定、コードのステップ実行などの手順が含まれます。 デバッガーを使用すると、一度に1行ずつコードを実行できます。

このチュートリアルを準備するには、最初に2つの[サンプルファイル](#sample-files)をローカルコンピューターにコピーします。 1つはスタイルシートで、もう1つはスタイルシートへの入力として使用する XML ファイルです。 このチュートリアルでは、使用するスタイルシートで、コストが平均書籍価格を下回るすべての書籍が検索されます。

> [!NOTE]
> XSLT デバッガーは、Visual Studio の Enterprise edition でのみ使用できます。

## <a name="start-debugging"></a>デバッグを開始する

1. **[ファイル]** メニューの [ > **ファイル**を**開く**] を選択します。

2. *Below-average*ファイルを見つけ、 **[開く]** を選択します。

   XML エディターでスタイルシートが開きます。

3. ドキュメントのプロパティウィンドウの **[入力]** フィールドで、参照ボタン (. **[..]** ) をクリックします。 ( **[プロパティ]** ウィンドウが表示されていない場合は、エディターで開いているファイルの任意の場所を右クリックし、 **[プロパティ]** をクリックします)。

4. *Books.xml*ファイルを見つけて、 **[開く]** を選択します。

   これにより、XSLT 変換に使用するソースドキュメントファイルが設定されます。

5. *Below-average*の12行目に[ブレークポイント](../debugger/using-breakpoints.md)を設定します。 これは、次のいずれかの方法で行うことができます。

   - 12行目のエディターの余白をクリックします。

   - 12行目の任意の場所をクリックし、 **F9**キーを押します。

   - `xsl:if` 開始タグを右クリックし、 **[ブレークポイント]** を選択して**ブレークポイント > 挿入**します。

      ![Visual Studio で XSL ファイルにブレークポイントを挿入する](media/insert-breakpoint.PNG)

6. メニューバーで  **XML** > **XSLT デバッグの開始** を選択します (または、F5 キーを押し+**F5**キーを押します)。

   デバッグプロセスが開始されます。

   エディターでは、デバッガーはスタイルシートの `xsl:if` 要素に配置されます。 Below-average という名前の別のファイルがエディターに表示さ*れ*ます。これは、入力ファイル*books .xml*の各ノードが処理されるときに設定される出力ファイルです。

   **[自動変数]** 、 **[ローカル]** 、 **[ウォッチ 1]** の各ウィンドウは、Visual Studio ウィンドウの下部に表示されます。 [**ローカル] ウィンドウには、** すべてのローカル変数とその現在の値が表示されます。 ここには、スタイル シートで定義されている変数や、コンテキスト内に現在存在するノードを追跡するためにデバッガーが使用する変数なども表示されます。

## <a name="watch-window"></a>監視ウィンドウ

2つの変数を **[ウォッチ 1]** ウィンドウに追加して、入力ファイルが処理されるときに値を調べることができるようにします。 (ウォッチする変数が既に存在する場合は、 **[ローカル]** ウィンドウを使用して値を確認することもできます)。

1. **[デバッグ]** メニューの [ **Windows** > **watch** ] をクリックし > **ウォッチ 1**をクリックします。

   **[ウォッチ 1]** ウィンドウが表示されます。

2. **[名前]** フィールドに「`$bookAverage`」**と入力し、enter キーを**押します。

   `$bookAverage` 変数の値は、 **[値]** フィールドに表示されます。

3. 次の行で、 **[名前]** フィールドに「`self::node()`」と入力し **、enter キーを押します。**

   `self::node()` は、現在のコンテキストノードに評価される XPath 式です。 `self::node()` XPath 式の値は、最初の book ノードです。 この値は、変換処理の進行につれて変化します。

4. [`self::node()`] ノードを展開し、[値の `price`] ノードを展開します。

   ![Visual Studio での XSLT デバッグ時のウォッチウィンドウ](media/xslt-debugging-watch-window.png)

   現在の book ノードの書籍価格の値を確認し、`$bookAverage` の値と比較することができます。 本の価格は平均値を下回っているため、デバッグプロセスを続行すると `xsl:if` 条件が成功します。

## <a name="step-through-the-code"></a>コードをステップ実行する

1. **F5** キーを押して続行します。

   最初の book ノードが `xsl:if` 条件を満たしているため、 *below-average*出力ファイルに book ノードが追加されます。 デバッガーは、再度スタイル シートの `xsl:if` 要素に到達するまで、引き続き実行されます。 これで、デバッガーが*books.xml*ファイルの2番目の book ノードに配置されました。

   **[ウォッチ 1]** ウィンドウで、`self::node()` の値が2番目の book ノードに変わります。 price 要素の値を調べることで、価格が平均値より高いことを判断できるため、`xsl:if` 条件は失敗します。

2. **F5** キーを押して続行します。

   2番目の book ノードは `xsl:if` 条件を満たしていないため、book ノードは*below-average*出力ファイルに追加されません。 デバッガーは、スタイルシートの `xsl:if` 要素に再度配置されるまで実行を続けます。 これで、デバッガーが*books.xml*ファイルの3番目の `book` ノードに配置されました。

   **[ウォッチ 1]** ウィンドウで、`self::node()` の値が3番目の book ノードに変わります。 `price` 要素の値を調べることにより、価格が平均値未満であることを確認できます。 `xsl:if` 条件は成功します。

3. **F5** キーを押して続行します。

   `xsl:if` 条件が満たされたため、 *below-average*出力ファイルに3番目の書籍が追加されます。 XML ドキュメント内の書籍がすべて処理され、デバッガーが停止します。

## <a name="sample-files"></a>サンプル ファイル

このチュートリアルでは、次の 2 つのファイルを使用します。

### <a name="below-averagexsl"></a>below-average

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

## <a name="see-also"></a>参照

- [XSLT のデバッグ](../xml-tools/debugging-xslt.md)
