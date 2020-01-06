---
title: デバッグ中に XPath 式を評価する
ms.date: 03/05/2019
ms.topic: conceptual
ms.assetid: 159ba4ef-75e4-4ac8-80dc-e064e0bec345
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c2e0b6c84fa9447dc38aa7976fa59bb5aa67d5c3
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75592725"
---
# <a name="evaluate-xpath-expressions"></a>XPath 式の評価

XPath 式を評価するには、デバッグ中に **[クイックウォッチ]** ウィンドウを使用します。 XPath 式は、W3C XPath 1.0 勧告に沿って有効である必要があります。 現在の XSLT コンテキスト ( **[ローカル]** ウィンドウの [`self::node()`] ノード) は、XPath 式の評価コンテキストを提供します。

XPath 式を評価する場合:

- 組み込みの XPath 関数はサポートされます。

- 組み込みの XSLT 関数およびユーザー定義関数はサポートされていません。

> [!NOTE]
> XSLT デバッグは、Visual Studio の Enterprise edition でのみ使用できます。

## <a name="evaluate-an-xpath-expression"></a>XPath 式を評価する

次の手順では、 [「チュートリアル: XSLT スタイルシートのデバッグ](../xml-tools/walkthrough-debug-an-xslt-style-sheet.md#sample-files)」ページの*below-average*ファイルと*books.xml*ファイルを使用します。

1. `xsl:if` 開始タグにブレークポイントを挿入します。

2. デバッグを開始するには、メニューバーで  **XML** > **XSLT デバッグの開始** を選択します (または、F5**キーを押し+** **F5**キーを押します)。

   デバッガーが起動され、`xsl:if` タグで実行が中断されます。

3. 右クリックして **[クイックウォッチ]** を選択します。

   **[クイックウォッチ]** ウィンドウが開きます。

4. **[クイックウォッチ]** ダイアログボックスの **[式]** フィールドに `./price/text()` を入力し、再 **[評価]** を選択します。

   **[値]** ボックスに、現在の book ノードの価格が表示されます。

   ![[クイックウォッチ] ウィンドウで XPath 式を評価する](media/quickwatch-price.png)

5. XPath 式を `./price/text() < $bookAverage` に変更し、[再**評価**] をクリックします。

   **[値]** ボックスに、XPath 式が `true`として評価されたことが表示されます。

## <a name="see-also"></a>関連項目

- [XSLT のデバッグ](../xml-tools/debugging-xslt.md)
