---
title: XML スキーマ デザイナーのコンテンツ モデル ビューを使用してノードを確認する
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: c42ddac8-b0e3-48d6-9832-112a19d6c104
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 81bf6294aeac9a23168bf9cf9aaec26efbfc6c1f
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85815982"
---
# <a name="how-to-examine-the-content-model-of-nodes-using-the-content-model-view"></a>方法: コンテンツ モデル ビューを使用してノードのコンテンツ モデルを調べる

このトピックでは、[コンテンツ モデル ビュー](../xml-tools/content-model-view.md)を使用してノードを調べる方法について説明します。

## <a name="to-create-a-new-xsd-file-and-display-the-root-element-in-the-content-model-view"></a>新しい XSD ファイルを作成してコンテンツ モデル ビューにルート要素を表示するには

1. 新しい XML スキーマ ファイルを作成します。

2. スタート ビューの **[XML エディターを使用して基になる XML スキーマ ファイルを表示および編集する]** をクリックします。

3. [サンプル XML スキーマ: 購買発注書のスキーマ](../xml-tools/sample-xsd-file-purchase-order-schema.md)に関する記事から XML スキーマのサンプル コードをコピーして、新しい XSD ファイルに既定で追加されたコードの代わりに貼り付けます。

4. XML エディターで `purchaseOrder` 要素を右クリックし、 **[XML スキーマ エクスプローラーで表示]** をクリックして、スキーマ エクスプローラーの `purchaseOrder` 要素を選択します。

5. XML エクスプローラーで `purchaseOrder` を右クリックし、 **[コンテンツ モデル ビューで表示]** をクリックします。

     コンテンツ モデル ビューのデザイン サーフェイスに `purchaseOrder` 要素が表示されます。

6. `shipTo` ノード、`billTo` ノード、および `items` ノードをダブルクリックするか、各ノードの右側にある二重矢印をクリックして、各ノードを展開します。

     これにより `purchaseOrder` 要素のノードが展開され、要素のコンテンツ モデルを確認できます。

7. `purchaseOrder` 要素のノードをクリックし、階層リンク バーで選択したノードが存在するスキーマ セットの場所を確認します。

8. ドキュメントを切り替えるには、XSD ツール バーの **[ドキュメントの表示]** ボタンをクリックします。 デザイン サーフェイスを右クリックして、ドキュメントを切り替えることもできます。

9. `purchaseOrder` ノードを右クリックし、 **[サンプル XML の生成]** をクリックして XML インスタンス ドキュメントを表示します。
