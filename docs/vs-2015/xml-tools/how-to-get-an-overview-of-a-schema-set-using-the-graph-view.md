---
title: '方法: グラフビューを使用してスキーマセットの概要を取得する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: c0df4b0d-52ef-4a6c-9676-1d8311aad7c7
caps.latest.revision: 10
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 7009e5772b4f4c6977d58d2c52d733999a0d9369
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72670889"
---
# <a name="how-to-get-an-overview-of-a-schema-set-using-the-graph-view"></a>方法: グラフ ビューを使用してスキーマ セットの概要を表示する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このトピックでは、[グラフ ビュー](../xml-tools/graph-view.md)を使用して、スキーマ セット内のノードの概要とノード間のリレーションシップを表示する方法について説明します。

### <a name="to-create-a-new-xsd-file-and-display-the-root-element-in-the-content-model-view"></a>新しい XSD ファイルを作成してコンテンツ モデル ビューにルート要素を表示するには

1. 新しい XML スキーマ ファイルを作成して、Relationships.xsd という名前でファイルを保存します。

2. [XML エディターを使用して、スタートビューの **基になる Xml スキーマファイルを表示および編集する** ] リンクをクリックします。

3. [「サンプル Xml スキーマ: リレーションシップ](../xml-tools/sample-xsd-file-relationships.md)」から xml スキーマのサンプルコードをコピーして貼り付け、新しい XSD ファイルに既定で追加されたコードを置き換えます。

4. XML エディター内の任意の場所を右クリックし、[ **ビューデザイナー**] をクリックします。

5. XSD ツール バーからグラフ ビューを選択します。

6. XML スキーマエクスプローラーで [ **スキーマセット** ] ノードを選択し、グラフビューの [デザイン] にノードをドラッグします。 すべてのグローバル ノードが表示され、リレーションシップを持つノード間に矢印が引かれます。

     ![グラフ ビュー](../xml-tools/media/relationshipingraphview.gif "RelationshipInGraphView")

7. デザイン サーフェイスでノードをクリックし、階層リンク バーで選択したノードが存在するスキーマ セットの場所を確認します。

8. Rick 画面で任意の要素ノードをクリックし、[ **サンプル xml の生成** ] を選択して xml インスタンスドキュメントを表示します。
