---
title: スキーマ セットの概要を取得する
description: XML スキーマ デザイナー:XML スキーマ エクスプローラーでグラフ ビューを使用して、スキーマ セット内のノードの概要とノード間のリレーションシップを表示する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: c0df4b0d-52ef-4a6c-9676-1d8311aad7c7
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 699167f8fe3662bbb162706f3f9fc6e5d53d82dc
ms.sourcegitcommit: d10f37dfdba5d826e7451260c8370fd1efa2c4e4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2020
ms.locfileid: "96995292"
---
# <a name="how-to-get-an-overview-of-a-schema-set-by-using-the-graph-view"></a>方法:グラフ ビューを使用してスキーマ セットの概要を表示する

このトピックでは、[グラフ ビュー](../xml-tools/graph-view.md)を使用して、スキーマ セット内のノードの概要とノード間のリレーションシップを表示する方法について説明します。

## <a name="to-create-a-new-xsd-file-and-display-the-root-element-in-the-content-model-view"></a>新しい XSD ファイルを作成してコンテンツ モデル ビューにルート要素を表示するには

1. 新しい XML スキーマ ファイルを作成して、*Relationships.xsd* という名前でファイルを保存します。

2. スタート ビューの **[XML エディターを使用して基になる XML スキーマ ファイルを表示および編集する]** リンクをクリックします。

3. [サンプル XML スキーマ: リレーションシップ](../xml-tools/sample-xsd-file-relationships.md)に関するページから XML スキーマのサンプル コードをコピーして、新しい XSD ファイルに既定で追加されたコードの代わりに貼り付けます。

4. XML エディター内を右クリックして **[ビュー デザイナー]** をクリックします。

5. **XSD ツール バー** からグラフ ビューを選択します。

6. **XML スキーマ エクスプローラー** の **[スキーマ セット]** ノードを選択し、グラフ ビューのデザイン サーフェイスにノードをドラッグします。 すべてのグローバル ノードが表示され、リレーションシップを持つノード間に矢印が引かれます。

     ![グラフ ビュー](../xml-tools/media/relationshipingraphview.gif)

7. デザイン サーフェイスでノードをクリックし、階層リンク バーで選択したノードが存在するスキーマ セットの場所を確認します。

8. デザイン サーフェイスで任意の要素ノードを右クリックし、 **[サンプル XML の生成]** をクリックして XML インスタンス ドキュメントを表示します。
