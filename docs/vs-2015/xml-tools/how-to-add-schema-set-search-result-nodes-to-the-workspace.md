---
title: '方法: ワークスペースにスキーマセット検索結果ノードを追加するMicrosoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: ff33b3cc-4db9-4b4e-9378-b45ed5999b18
caps.latest.revision: 10
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: b34be331ad3ec67e2c3bd8d9ecc500cd256b1b09
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72666552"
---
# <a name="how-to-add-schema-set-search-result-nodes-to-the-workspace"></a>方法: スキーマ セットの検索結果のノードをワークスペースに追加する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このトピックでは、キーワード検索の結果、XML スキーマ エクスプローラーに強調表示されたノードをワークスペースに追加する方法について説明します。

> [!NOTE]
> [ワークスペース](../xml-tools/xml-schema-designer-workspace.md)に追加できるのは、グローバル ノードだけです。

 この例では、サンプルの注文 [書スキーマ](../xml-tools/sample-xsd-file-purchase-order-schema.md)を使用します。

### <a name="to-add-schema-set-result-nodes"></a>スキーマ セットの検索結果のノードを追加するには

1. [「方法: XSD スキーマファイルを作成および編集する](../xml-tools/how-to-create-and-edit-an-xsd-schema-file.md)」の手順に従います。

2. [XML エクスプローラー](../xml-tools/xml-schema-explorer.md)のツール バーの検索テキスト ボックスに「purchaseOrder」と入力して検索ボタンをクリックします。

     ![XML スキーマ エクスプローラー キーワード検索](../xml-tools/media/schemaexplorersearch.gif "SchemaExplorerSearch")

     検索結果が XML スキーマ エクスプローラーで強調表示され、垂直スクロール バーのチックでマークされます。

3. 概要結果ペインの **[強調表示されたノードをワークスペースに追加]** ボタンをクリックして、ワークスペースに検索結果を追加します。

     ![XML スキーマ エクスプローラー検索結果](../xml-tools/media/schemaexplorersearchresult.gif "SchemaExplorerSearchResult")

     `purchaseOrder` ノードおよび `PurchaseOrderType` ノードが[グラフ ビュー](../xml-tools/graph-view.md)のデザイン サーフェイスに並べて表示されます。 2 つのノードは関連があるため (`purchaseOrder` 要素は `PurchaseOrderType` 型)、これらの間に矢印が引かれます。
