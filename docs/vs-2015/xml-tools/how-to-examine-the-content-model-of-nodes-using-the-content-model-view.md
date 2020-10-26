---
title: '方法: コンテンツモデルビューを使用してノードのコンテンツモデルを調べるMicrosoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: c42ddac8-b0e3-48d6-9832-112a19d6c104
caps.latest.revision: 10
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: ddadcb0fbd772a5638bf6023b8cf6c18fbd270d7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72670850"
---
# <a name="how-to-examine-the-content-model-of-nodes-using-the-content-model-view"></a>方法: コンテンツ モデル ビューを使用してノードのコンテンツ モデルを調べる
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このトピックでは、[コンテンツ モデル ビュー](../xml-tools/content-model-view.md)を使用してノードを調べる方法について説明します。

### <a name="to-create-a-new-xsd-file-and-display-the-root-element-in-the-content-model-view"></a>新しい XSD ファイルを作成してコンテンツ モデル ビューにルート要素を表示するには

1. 新しい XML スキーマ ファイルを作成します。

2. [XML エディターを使用して、スタートビューで **基になる Xml スキーマファイルを表示および編集する] を** クリックします。

3. [「サンプル Xml スキーマ: Purchase Order スキーマ](../xml-tools/sample-xsd-file-purchase-order-schema.md)」から xml スキーマのサンプルコードをコピーして貼り付け、新しい XSD ファイルに既定で追加されたコードに置き換えます。

4. `purchaseOrder` `purchaseOrder` Xml エディターで要素を右クリックし、[ **Xml エクスプローラーで表示]** を選択して、スキーマエクスプローラーで要素を選択します。

5. XML エクスプローラーで `purchaseOrder` を右クリックし、 **[コンテンツ モデル ビューで表示]** をクリックします。

     コンテンツ モデル ビューのデザイン サーフェイスに `purchaseOrder` 要素が表示されます。

6. `shipTo` ノード、`billTo` ノード、および `items` ノードをダブルクリックするか、各ノードの右側にある二重矢印をクリックして、各ノードを展開します。

     これにより `purchaseOrder` 要素のノードが展開され、要素のコンテンツ モデルを確認できます。

7. `purchaseOrder` 要素のノードをクリックし、階層リンク バーで選択したノードが存在するスキーマ セットの場所を確認します。

8. ドキュメントを切り替えるには、XSD ツールバーの [ **ドキュメントの表示** ] ボタンをクリックします。 デザイン サーフェイスを右クリックして、ドキュメントを切り替えることもできます。

9. Rick-ノードをクリックし、 `purchaseOrder` [ **サンプル Xml の生成** ] を選択して xml インスタンスドキュメントを表示します。
