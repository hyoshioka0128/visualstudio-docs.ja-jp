---
title: スキーマ セットの検索結果のノードを追加する
description: キーワード検索の結果、XML スキーマ エクスプローラーに強調表示されたノードをワークスペースに追加する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: ff33b3cc-4db9-4b4e-9378-b45ed5999b18
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 762992ab2649e59055af8fd656514f3e82e9e8de
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99879216"
---
# <a name="how-to-add-schema-set-search-result-nodes-to-the-workspace"></a>方法: スキーマ セットの検索結果のノードをワークスペースに追加する

このトピックでは、キーワード検索の結果、**XML スキーマ エクスプローラー** に強調表示されたノードをワークスペースに追加する方法について説明します。

> [!NOTE]
> [ワークスペース](../xml-tools/xml-schema-designer-workspace.md)に追加できるのは、グローバル ノードだけです。

この例では、サンプルの[購買発注書のスキーマ](../xml-tools/sample-xsd-file-purchase-order-schema.md)を使用します。

## <a name="to-add-schema-set-result-nodes"></a>スキーマ セットの検索結果のノードを追加するには

1. 「[方法:XSD スキーマ ファイルを作成して編集する](../xml-tools/how-to-create-and-edit-an-xsd-schema-file.md)」の手順に従います。

2. [XML エクスプローラー](../xml-tools/xml-schema-explorer.md)のツール バーの検索テキスト ボックスに「purchaseOrder」と入力して検索ボタンをクリックします。

     ![XML スキーマ エクスプローラー キーワード検索](../xml-tools/media/schemaexplorersearch.gif)

     検索結果が **XML スキーマ エクスプローラー** で強調表示され、垂直スクロール バーの目盛りでマークされます。

3. 概要結果ペインの **[強調表示されたノードをワークスペースに追加]** ボタンをクリックして、ワークスペースに検索結果を追加します。

     ![XML スキーマ エクスプローラー検索結果](../xml-tools/media/schemaexplorersearchresult.gif)

     `purchaseOrder` ノードおよび `PurchaseOrderType` ノードが[グラフ ビュー](../xml-tools/graph-view.md)のデザイン サーフェイスに並べて表示されます。 2 つのノードは関連があるため (`purchaseOrder` 要素は `PurchaseOrderType` 型)、これらの間に矢印が引かれます。
