---
title: '方法: XML スキーマエクスプローラーからワークスペースにノードを追加するMicrosoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: 3b5a5749-9693-4b29-b0c2-8e07e0e55514
caps.latest.revision: 10
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: e0c8fe9d5ba8c096a03de7a9df85945f4aeb4a0a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72656343"
---
# <a name="how-to-add-nodes-to-the-workspace-from-the-xml-schema-explorer"></a>方法: XML スキーマ エクスプローラーからワークスペースにノードを追加する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このトピックでは、XML スキーマエクスプローラーから [Xml スキーマデザイナーワークスペース](../xml-tools/xml-schema-designer-workspace.md) にノードを追加する方法について説明します。 これは、XML スキーマ エクスプローラーから XSD デザイナーのビューにノードをドラッグ アンド ドロップするか、XML スキーマ エクスプローラーのコンテキスト メニューを使用することによって行うことができます。 さらに、XML スキーマ エクスプローラーの検索結果で強調表示されたノードを追加することができます。 詳細については、「 [方法: スキーマセットの検索結果ノードをワークスペースに追加する](../xml-tools/how-to-add-schema-set-search-result-nodes-to-the-workspace.md)」を参照してください。

> [!NOTE]
> [XML スキーマデザイナーのワークスペース](../xml-tools/xml-schema-designer-workspace.md)に追加できるのは、グローバルノードだけです。

### <a name="to-add-nodes-through-the-xml-explorer-context-menu"></a>XML スキーマ エクスプローラーのコンテキスト メニューからノードを追加するには

1. [「方法: XSD スキーマファイルを作成および編集する](../xml-tools/how-to-create-and-edit-an-xsd-schema-file.md)」の手順に従います。

2. XSD エクスプローラーで `PurchaseOrderType` ノードを右クリックします。 **[グラフ ビューで表示]** を選択します。

     `purchaseOrderType` ノードがグラフ ビューのデザイン サーフェイスに表示されます。

### <a name="to-drag-and-drop-a-node-on-to-a-view"></a>ビューにノードをドラッグ アンド ドロップするには

1. グラフ ビューで `PurchaseOrderType` ノードを右クリックします。 **[XML スキーマ エクスプローラーで表示]** を選択します。

     XML スキーマ エクスプローラーにノードが強調表示されます。

2. XML スキーマ エクスプローラーで `PurchaseOrderType` ノードを右クリックし、**[すべての参照の表示]** をクリックします。

     `purchaseOrder` ノードが強調表示されます。

3. `purchaseOrder` ノードをグラフ ビューにドラッグします。

     `purchaseOrder` ノードおよび `PurchaseOrderType` ノードがグラフ ビューのデザイン サーフェイスに並べて表示されます。 2 つのノードは関連があるため (`purchaseOrder` 要素は `PurchaseOrderType` 型)、これらの間に矢印が引かれます。

### <a name="to-add-nodes-using-the-schema-explorer-search-capability"></a>スキーマ エクスプローラーの検索機能を使用してノードを追加するには

1. [XML エクスプローラー](../xml-tools/xml-schema-explorer.md)のツール バーの検索テキスト ボックスに「purchaseOrder」と入力して検索ボタンをクリックします。

     ![XML スキーマ エクスプローラー キーワード検索](../xml-tools/media/schemaexplorersearch.gif "SchemaExplorerSearch")

     検索結果が XML スキーマ エクスプローラーで強調表示され、垂直スクロール バーのチックでマークされます。

2. 概要結果ペインの **[強調表示されたノードをワークスペースに追加]** ボタンをクリックして、ワークスペースに検索結果を追加します。

     ![XML スキーマ エクスプローラー検索結果](../xml-tools/media/schemaexplorersearchresult.gif "SchemaExplorerSearchResult")

     `purchaseOrder` ノードおよび `PurchaseOrderType` ノードが[グラフ ビュー](../xml-tools/graph-view.md)のデザイン サーフェイスに並べて表示されます。 2 つのノードは関連があるため (`purchaseOrder` 要素は `PurchaseOrderType` 型)、これらの間に矢印が引かれます。

## <a name="see-also"></a>参照
 [XML スキーマ エクスプローラー](../xml-tools/xml-schema-explorer.md)
