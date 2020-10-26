---
title: スキーマセットを検索しています |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: ec1395e0-d03c-4130-810d-f2db656937bd
caps.latest.revision: 12
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 0e3a8563d5e2cd29c9c521761498d7ef87b7cbab
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72656156"
---
# <a name="searching-the-schema-set"></a>スキーマ セットの検索
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

XML スキーマ エクスプローラーでは、次の方法でスキーマ セットを検索できます。

- キーワード検索

- スキーマ固有の検索

## <a name="keyword-search"></a>キーワード検索
 キーワード検索を実行するには、XML スキーマ エクスプローラーのツール バーにある **[スキーマ セットの検索]** テキスト ボックスに部分文字列を入力します。

 ![XML スキーマ エクスプローラー キーワード検索](../xml-tools/media/schemaexplorersearch.gif "SchemaExplorerSearch")

 XML スキーマ エクスプローラーは、次のようにスキーマ セットを検索します。

- 指定したキーワードに一致する `name` 属性または `ref` 属性。 これを使用すると、要素、属性、型などを名前で検索することができます。

- include ステートメントの `schemaLocation` 属性。

- import ステートメントの `namespace` 属性。

## <a name="schema-specific-search"></a>スキーマ固有の検索
 XML スキーマ エクスプローラーには、XML スキーマ エクスプローラーのコンテキスト メニューを使用してアクセスできる組み込みの検索機能もあります。 使用できるコンテキストメニューの詳細については、「 [コンテキストメニュー](../xml-tools/context-menus-xml-schema-explorer.md)」を参照してください。 スタート ビューからもスキーマ固有の検索を実行できます。詳細については、「[スタート ビュー](../xml-tools/start-view.md)」トピックの「スキーマ セットの詳細」セクションを参照してください。

## <a name="displaying-and-navigating-search-results"></a>検索結果の表示および移動
 検索が終了すると、ツール バーに概要結果ペインが追加され、検索結果が表示されます。 検索結果は XML スキーマ エクスプローラーでも強調表示され、垂直スクロール バーの目盛りでマークされます。 検索結果を参照するには、XML スキーマエクスプローラーのツールバーの [概要] 結果ペインで、[ **次の検索結果に移動** ] ボタンと [ **前の検索結果** に移動] ボタンを使用します。キーボードのキーを使用して F3 と Shift + F3または、スクロールバーの目盛りをクリックします。

 概要結果ペインの **[強調表示されたノードをワークスペースに追加]** ボタンをクリックして、ワークスペースに検索結果を追加できます。

 ![XML スキーマ エクスプローラー検索結果](../xml-tools/media/schemaexplorersearchresult.gif "SchemaExplorerSearchResult")

## <a name="clearing-search-results"></a>検索結果のクリア
 検索結果をクリアするには、XML スキーマ エクスプローラーの検索ツール バーの概要結果ペインにある **[x]** ボタンをクリックします。

## <a name="see-also"></a>参照
 [XML スキーマ エクスプローラー](../xml-tools/xml-schema-explorer.md)
