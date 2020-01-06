---
title: XML スキーマデザイナーのコンテンツモデルビューを使用してノードを確認する
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: c42ddac8-b0e3-48d6-9832-112a19d6c104
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f5a7e6e311a4fbd02973edf94c6eb117f69d6cea
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75592712"
---
# <a name="how-to-examine-the-content-model-of-nodes-using-the-content-model-view"></a>方法: コンテンツモデルビューを使用してノードのコンテンツモデルを調べる

このトピックでは、[コンテンツモデルビュー](../xml-tools/content-model-view.md)を使用してノードを探索する方法について説明します。

## <a name="to-create-a-new-xsd-file-and-display-the-root-element-in-the-content-model-view"></a>新しい XSD ファイルを作成してコンテンツ モデル ビューにルート要素を表示するには

1. 新しい XML スキーマ ファイルを作成します。

2. [XML エディターを使用して、スタートビューで**基になる Xml スキーマファイルを表示および編集する] を**クリックします。

3. [「サンプル xml スキーマ: purchase order スキーマ](../xml-tools/sample-xsd-file-purchase-order-schema.md)」から xml スキーマのサンプルコードをコピーして貼り付け、新しい XSD ファイルに既定で追加されたコードに置き換えます。

4. XML エディターで `purchaseOrder` 要素を右クリックし、[ **Xml エクスプローラーで表示]** を選択して、スキーマエクスプローラーで `purchaseOrder` 要素を選択します。

5. XML エクスプローラーで `purchaseOrder` を右クリックし、 **[コンテンツモデルビューで表示]** をクリックします。

     コンテンツ モデル ビューのデザイン サーフェイスに `purchaseOrder` 要素が表示されます。

6. `shipTo` ノード、`billTo` ノード、および `items` ノードをダブルクリックするか、各ノードの右側にある二重矢印をクリックして、各ノードを展開します。

     これにより `purchaseOrder` 要素のノードが展開され、要素のコンテンツ モデルを確認できます。

7. `purchaseOrder` 要素のノードをクリックし、階層リンク バーで選択したノードが存在するスキーマ セットの場所を確認します。

8. ドキュメントを切り替えるには、XSD ツールバーの **[ドキュメントの表示]** ボタンをクリックします。 デザイン サーフェイスを右クリックして、ドキュメントを切り替えることもできます。

9. [`purchaseOrder`] ノードを右クリックし、 **[サンプル xml の生成]** を選択して xml インスタンスドキュメントを表示します。
