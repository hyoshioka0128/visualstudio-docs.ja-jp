---
title: XML スキーマ エクスプローラーからワークスペースにノードを追加する
description: XML スキーマ エクスプローラーからコンテキスト メニューを使用するか、ノードをドラッグしてビューにドロップすることにより、XML スキーマ デザイナーのワークスペースにノードを追加する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 3b5a5749-9693-4b29-b0c2-8e07e0e55514
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: baa4d32d14a85e27bb0bb453c8c81f0bab486379
ms.sourcegitcommit: 1a36533f385e50c05f661f440380fda6386ed3c1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2020
ms.locfileid: "93045726"
---
# <a name="how-to-add-nodes-to-the-workspace-from-the-xml-schema-explorer"></a>方法: XML スキーマ エクスプローラーからワークスペースにノードを追加する

このトピックでは、 **XML スキーマ エクスプローラー** から [XML スキーマ デザイナーのワークスペース](../xml-tools/xml-schema-designer-workspace.md)にノードを追加する方法について説明します。 これは、 **XML スキーマ エクスプローラー** から XSD デザイナーのビューにノードをドラッグ アンド ドロップするか、 **XML スキーマ エクスプローラー** のコンテキスト メニューを使用することによって行うことができます。 さらに、 **XML スキーマ エクスプローラー** の検索結果で強調表示されたノードを追加することもできます。 詳細については、「[方法:スキーマ セットの検索結果のノードをワークスペースに追加する](../xml-tools/how-to-add-schema-set-search-result-nodes-to-the-workspace.md)」を参照してください。

> [!NOTE]
> [XML スキーマ デザイナー ワークスペース](../xml-tools/xml-schema-designer-workspace.md)に追加できるのは、グローバル ノードだけです。

## <a name="to-add-nodes-through-the-xml-explorer-context-menu"></a>XML エクスプローラーのコンテキスト メニューからノードを追加するには

1. 「[方法:XSD スキーマ ファイルを作成して編集する](../xml-tools/how-to-create-and-edit-an-xsd-schema-file.md)」の手順に従います。

2. XSD エクスプローラーで `PurchaseOrderType` ノードを右クリックします。 **[グラフ ビューで表示]** を選択します。

     `purchaseOrderType` ノードがグラフ ビューのデザイン サーフェイスに表示されます。

## <a name="to-drag-and-drop-a-node-on-to-a-view"></a>ビューにノードをドラッグ アンド ドロップするには

1. グラフ ビューで `PurchaseOrderType` ノードを右クリックします。 **[XML スキーマ エクスプローラーで表示]** を選択します。

     **XML スキーマ エクスプローラー** にノードが強調表示されます。

2. **XML スキーマ エクスプローラー** で `PurchaseOrderType` ノードを右クリックし、 **[すべての参照の表示]** をクリックします。

     `purchaseOrder` ノードが強調表示されます。

3. `purchaseOrder` ノードをグラフ ビューにドラッグします。

     `purchaseOrder` ノードおよび `PurchaseOrderType` ノードがグラフ ビューのデザイン サーフェイスに並べて表示されます。 2 つのノードは関連があるため (`purchaseOrder` 要素は `PurchaseOrderType` 型)、これらの間に矢印が引かれます。

## <a name="to-add-nodes-using-the-schema-explorer-search-capability"></a>スキーマ エクスプローラーの検索機能を使用してノードを追加するには

1. [XML エクスプローラー](../xml-tools/xml-schema-explorer.md)のツール バーの検索テキスト ボックスに「purchaseOrder」と入力して検索ボタンをクリックします。

     ![XML スキーマ エクスプローラー キーワード検索](../xml-tools/media/schemaexplorersearch.gif)

     検索結果が **XML スキーマ エクスプローラー** で強調表示され、垂直スクロール バーの目盛りでマークされます。

2. 概要結果ペインの **[強調表示されたノードをワークスペースに追加]** ボタンをクリックして、ワークスペースに検索結果を追加します。

     ![XML スキーマ エクスプローラー検索結果](../xml-tools/media/schemaexplorersearchresult.gif)

     `purchaseOrder` ノードおよび `PurchaseOrderType` ノードが[グラフ ビュー](../xml-tools/graph-view.md)のデザイン サーフェイスに並べて表示されます。 2 つのノードは関連があるため (`purchaseOrder` 要素は `PurchaseOrderType` 型)、これらの間に矢印が引かれます。

## <a name="see-also"></a>関連項目

- [XML スキーマ エクスプローラー](../xml-tools/xml-schema-explorer.md)
