---
title: XML スキーマ エクスプローラー - スキーマ セットの検索
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
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75592504"
---
# <a name="search-the-schema-set"></a>スキーマ セットを検索する

**XML スキーマ エクスプローラー**では、次の方法でスキーマ セットを検索できます。

- キーワード検索

- スキーマ固有の検索

## <a name="keyword-search"></a>キーワード検索

キーワード検索を実行するには、**XML スキーマ エクスプローラー**のツール バーにある **[スキーマ セットの検索]** テキスト ボックスに部分文字列を入力します。

![XML スキーマ エクスプローラー キーワード検索](../xml-tools/media/schemaexplorersearch.gif)

**XML スキーマ エクスプローラー**では、次の属性のスキーマ セットが検索されます。

- 指定したキーワードに一致する `name` 属性または `ref` 属性。 要素、属性、型などを名前で検索することができます。

- include ステートメントの `schemaLocation` 属性。

- import ステートメントの `namespace` 属性。

## <a name="schema-specific-search"></a>スキーマ固有の検索

**XML スキーマ エクスプローラー**には、**XML スキーマ エクスプローラー**のコンテキスト (右クリック) メニューを使用してアクセスできる組み込みの検索機能もあります。 使用できるコンテキスト メニューの詳細については、[コンテキスト メニュー](../xml-tools/context-menus-xml-schema-explorer.md)に関する記事を参照してください。 スタート ビューからもスキーマ固有の検索を実行できます。詳細については、「[スタート ビュー](../xml-tools/start-view.md)」トピックの「スキーマ セットの詳細」セクションを参照してください。

## <a name="display-and-navigate-search-results"></a>検索結果の表示とナビゲート

検索が終了すると、ツール バーに概要結果ペインが追加され、検索結果が表示されます。 検索結果は **XML スキーマ エクスプローラー**でも強調表示され、垂直スクロール バーの目盛りでマークされます。 各検索結果を表示するには、**XML スキーマ エクスプローラー**のツール バーの概要結果ペインにある **[次の検索結果に移動]** ボタンおよび **[前の検索結果に移動]** ボタンを使用するか、キーボードの **F3** キーおよび **Shift**+**F3** キーを使用するか、スクロール バーの目盛りをクリックします。

概要結果ペインの **[強調表示されたノードをワークスペースに追加]** ボタンをクリックして、ワークスペースに検索結果を追加できます。

![XML スキーマ エクスプローラー検索結果](../xml-tools/media/schemaexplorersearchresult.gif)

## <a name="clear-search-results"></a>検索結果のクリア

検索結果をクリアするには、**XML スキーマ エクスプローラー**の検索ツール バーの概要結果ペインにある **[x]** ボタンをクリックします。

## <a name="see-also"></a>関連項目

- [XML スキーマ エクスプローラー](../xml-tools/xml-schema-explorer.md)
