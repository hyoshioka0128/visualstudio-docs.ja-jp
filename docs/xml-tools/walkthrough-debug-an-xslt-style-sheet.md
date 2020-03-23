---
title: XSLT スタイル シートのデバッグ
ms.date: 03/05/2019
ms.topic: conceptual
ms.assetid: 3db9fa5a-f619-4cb6-86e7-64b364e58e5d
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: cd5882cc606bf241a281940464ba028e77986807
ms.sourcegitcommit: 95f26af1da51d4c83ae78adcb7372b32364d8a2b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79300943"
---
# <a name="walkthrough-debug-an-xslt-style-sheet"></a>チュートリアル: XSLT スタイル シートのデバッグ

このチュートリアルの手順では、XSLT デバッガーを使用する方法を示します。 変数の表示、ブレークポイントの設定、コードのステップ実行などの手順が含まれます。 デバッガーでは、コードを一度に 1 行ずつ実行できます。

このチュートリアルの準備として、まず 2 つの[サンプル ファイル](#sample-files)をローカル コンピューターにコピーします。 1 つはスタイル シートで、1 つはスタイル シートへの入力として使用する XML ファイルです。 このチュートリアルでは、使用するスタイル シートは、コストが平均書籍価格を下回るすべての書籍を検索します。

> [!NOTE]
> XSLT デバッガーは、Visual Studio のエンタープライズ エディションでのみ使用できます。

## <a name="start-debugging"></a>デバッグを開始する

1. [**ファイル]** メニューの [ファイルを**開く** > ]**を**クリックします。

2. *平均以下の.xsl*ファイルを見つけ、[**開く**]を選択します。

   スタイル シートが XML エディタで開きます。

3. ドキュメント プロパティ ウィンドウの **[入力**] フィールドで、参照ボタン **(.)** をクリックします。 **([プロパティ]** ウィンドウが表示されていない場合は、エディタで開いているファイルの任意の場所を右クリックし、[**プロパティ]** を選択します)。

4. *books.xml*ファイルを見つけて、[**開く**] を選択します。

   これにより、XSLT 変換に使用されるソース ドキュメント ファイルが設定されます。

5. *平均以下の 12*行目に[ブレークポイント](../debugger/using-breakpoints.md)を設定します。 これは、次のいずれかの方法で実行できます。

   - 12 行目のエディターの余白をクリックします。

   - 12 行目の任意の場所をクリックし **、F9**キーを押します。

   - 開始`xsl:if`タグを右クリックし、ブレークポイント**挿入ブレークポイント****を選択** > します。

      ![XSL ファイルにブレークポイントを挿入します。](media/insert-breakpoint.PNG)

6. メニュー バーで **、[XML** > **の XSLT デバッグの開始**] を選択します (または **、Alt キーを**+**F5**押します。

   デバッグ プロセスが開始されます。

   エディターでは、デバッガーは、スタイル シートの`xsl:if`要素に配置されます。 *「平均以下」* という名前の別のファイルがエディタで開きます。これは、入力ファイル*books.xml*の各ノードが処理される時に設定される出力ファイルです。

   [**自動**]、[**ローカル]、** および **[ウォッチ 1]** ウィンドウは、Visual Studio ウィンドウの下部に表示されます。 **[ローカル]** ウィンドウには、すべてのローカル変数とその現在の値が表示されます。 ここには、スタイル シートで定義されている変数や、コンテキスト内に現在存在するノードを追跡するためにデバッガーが使用する変数なども表示されます。

## <a name="watch-window"></a>[ウォッチ] ウィンドウ

**[ウォッチ 1]** ウィンドウに 2 つの変数を追加して、入力ファイルの処理時に値を調べることができます。 (**また、[ローカル**] ウィンドウを使用して、監視する変数が既に存在する場合は、値を調べることもできます。

1. [**デバッグ**] メニューの [ウォッチ**ウォッチ** >  **1]** > をクリックします。**Watch 1**

   **[ウォッチ 1]** ウィンドウが表示されます。

2. [`$bookAverage`**名前]** フィールドに入力し **、Enter**キーを押します。

   変数の値が`$bookAverage`**[値]** フィールドに表示されます。

3. 次の行で、`self::node()`**名前**フィールドに入力し **、Enter**キーを押します。

   `self::node()`は、現在のコンテキスト ノードに評価される XPath 式です。 `self::node()` XPath 式の値は、最初の book ノードです。 この値は、変換処理の進行につれて変化します。

4. ノードを`self::node()`展開し、値が`price`のノードを展開します。

   ![Visual Studio での XSLT デバッグ中にウィンドウを見る](media/xslt-debugging-watch-window.png)

   現在の帳簿ノードの簿価の値を表示し、その`$bookAverage`値と比較することができます。 書籍価格が平均値を下回るため、デバッグ`xsl:if`プロセスを続行すると条件は成功するはずです。

## <a name="step-through-the-code"></a>コードをステップ実行する

1. **F5** キーを押して続行します。

   最初のブックノードが条件を`xsl:if`満たすため、ブックノードは*平均以下の.xml*出力ファイルに追加されます。 デバッガーは、再度スタイル シートの `xsl:if` 要素に到達するまで、引き続き実行されます。 これで、デバッガーは*books.xml*ファイルの 2 番目のブック ノードに配置されます。

   **[ウォッチ 1]** ウィンドウ`self::node()`で、値が 2 番目のブック ノードに変わります。 price 要素の値を調べることで、価格が平均値より高いことを判断できるため、`xsl:if` 条件は失敗します。

2. **F5** キーを押して続行します。

   2 番目のブック ノードは条件`xsl:if`を満たさないため、ブック ノードは*平均以下の*出力ファイルに追加されません。 デバッガーは、スタイル シート内の`xsl:if`要素に再度配置されるまで実行を続けます。 これで、デバッガーは`book`*books.xml*ファイルの 3 番目のノードに配置されます。

   **[ウォッチ 1]** ウィンドウ`self::node()`で、値が 3 番目のブック ノードに変わります。 要素の値を`price`調べることで、価格が平均値を下回っていることを判断できます。 条件`xsl:if`は成功するはずです。

3. **F5** キーを押して続行します。

   条件が`xsl:if`満たされているため、3 冊目の書籍が*平均以下の.xml*出力ファイルに追加されます。 XML ドキュメント内の書籍がすべて処理され、デバッガーが停止します。

## <a name="sample-files"></a>サンプル ファイル

このチュートリアルでは、次の 2 つのファイルを使用します。

### <a name="below-averagexsl"></a>平均以下.xsl

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
