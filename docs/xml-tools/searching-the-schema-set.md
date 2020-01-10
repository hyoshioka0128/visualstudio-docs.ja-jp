---
title: XML スキーマエクスプローラー-スキーマセットの検索
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: ec1395e0-d03c-4130-810d-f2db656937bd
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8378ebaccefaedfcc3d83f23bcab56f7417264dd
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75592504"
---
# <a name="search-the-schema-set"></a>スキーマ セットを検索する

**XML スキーマエクスプローラー**では、次の方法でスキーマセットを検索できます。

- キーワード検索

- スキーマ固有の検索

## <a name="keyword-search"></a>キーワード検索

キーワード検索を実行するには、 **XML スキーマエクスプローラー**のツールバーの **[検索 schemaset]** テキストボックスに部分文字列を入力します。

![XML スキーマ エクスプローラー キーワード検索](../xml-tools/media/schemaexplorersearch.gif)

**XML スキーマエクスプローラー**では、スキーマセット内の次の属性が検索されます。

- 指定したキーワードに一致する `name` 属性または `ref` 属性。 要素、属性、型などを名前で検索できます。

- include ステートメントの `schemaLocation` 属性。

- import ステートメントの `namespace` 属性。

## <a name="schema-specific-search"></a>スキーマ固有の検索

**Xml スキーマエクスプローラー**には、 **xml スキーマエクスプローラー**のコンテキスト (右クリック) メニューを使用してアクセスできる、組み込みの検索機能も用意されています。 使用できるコンテキストメニューの詳細については、「[コンテキストメニュー](../xml-tools/context-menus-xml-schema-explorer.md)」を参照してください。 また、スキーマ固有の検索をスタートビューから実行することもできます。詳細については、「[スタートビュー](../xml-tools/start-view.md) 」トピックの「スキーマセットの詳細」セクションを参照してください。

## <a name="display-and-navigate-search-results"></a>検索結果の表示と移動

検索が終了すると、ツール バーに概要結果ペインが追加され、検索結果が表示されます。 検索結果は、 **XML スキーマエクスプローラー**でも強調表示され、垂直スクロールバーの目盛りでマークされます。 検索結果を参照するには、 **XML スキーマエクスプローラー**のツールバーの 概要 結果ペインで、**次の検索結果に移動** ボタンと **前の検索結果**に移動 ボタンを使用します。キーボードのキーを使用して**f3**キーを**押し**+または、スクロールバーの目盛りをクリックします。

概要結果ペインの [強調表示された**ノードをワークスペースに追加**] ボタンをクリックすると、ワークスペースに検索結果を追加できます。

![XML スキーマ エクスプローラー検索結果](../xml-tools/media/schemaexplorersearchresult.gif)

## <a name="clear-search-results"></a>検索結果のクリア

検索結果を消去するには、 **XML スキーマエクスプローラー**の 検索 ツールバーの 概要 結果ペインにある  **x** ボタンをクリックします。

## <a name="see-also"></a>関連項目

- [XML スキーマ エクスプローラー](../xml-tools/xml-schema-explorer.md)
