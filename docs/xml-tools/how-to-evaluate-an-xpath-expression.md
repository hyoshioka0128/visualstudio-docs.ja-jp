---
title: デバッグ中に XPath 式を評価する
ms.date: 03/05/2019
description: デバッグ中に [クイックウォッチ] ウィンドウを使用して XPath 式を評価する方法について説明します。
ms.custom: SEO-VS-2020
ms.topic: how-to
ms.assetid: 159ba4ef-75e4-4ac8-80dc-e064e0bec345
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 068362f88d801d44a1a6b6a85c74f97ba2d3c773
ms.sourcegitcommit: f4b49f1fc50ffcb39c6b87e2716b4dc7085c7fb5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2020
ms.locfileid: "93399742"
---
# <a name="evaluate-xpath-expressions"></a>XPath 式を評価する

デバッグ中に **[クイック ウォッチ]** ウィンドウを使用して、XPath 式を評価できます。 XPath 式は、W3C XPath 1.0 勧告に沿って有効である必要があります。 XPath 式を評価するためのコンテキストは、現在の XSLT コンテキスト (つまり、 **[ローカル]** ウィンドウに表示される `self::node()` ノード) によって提供されます。

XPath 式を評価する場合:

- 組み込みの XPath 関数はサポートされます。

- 組み込みの XSLT 関数とユーザー定義関数はサポートされません。

> [!NOTE]
> XSLT デバッグは、Visual Studio の Enterprise Edition でのみ使用できます。

## <a name="evaluate-an-xpath-expression"></a>XPath 式を評価する

次の手順では、*below-average.xsl* と *books.xml* ファイル (「[チュートリアル:XSLT スタイル シートのデバッグ](../xml-tools/walkthrough-debug-an-xslt-style-sheet.md#sample-files)」ページ) を使用します。

1. `xsl:if` 開始タグにブレークポイントを挿入します。

2. デバッグを開始するには、メニュー バーの **[XML]**  >  **[XSLT デバッグを開始]** を選択します (または、**Alt**+**F5** キーを押します)。

   デバッガーが起動され、`xsl:if` タグで実行が中断されます。

3. 右クリックして **[クイック ウォッチ]** を選択します。

   **[クイック ウォッチ]** ウィンドウが開きます。

4. **[クイック ウォッチ]** ダイアログ ボックスの **[式]** フィールドに「`./price/text()`」と入力し、 **[再評価]** を選択します。

   現在の book ノードの価格が **[値]** ボックスに表示されます。

   ![[クイック ウォッチ] ウィンドウで XPath 式を評価する](media/quickwatch-price.png)

5. XPath 式を `./price/text() < $bookAverage` に変更し、 **[再評価]** をクリックします。

   **[値]** ボックスに、XPath 式が `true` に評価されたことが示されます。

## <a name="see-also"></a>関連項目

- [XSLT のデバッグ](../xml-tools/debugging-xslt.md)
