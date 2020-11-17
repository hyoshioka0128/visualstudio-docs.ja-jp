---
title: '方法: ビューと XML エディターを切り替える'
description: XML スキーマ デザイナー (XSD デザイナー) のビューと XML エディターを切り替える方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: cb69fbbd-d99c-439e-9498-5df9050f8df0
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ef64617591da0790a26e4728cd138d2224deed8e
ms.sourcegitcommit: f4b49f1fc50ffcb39c6b87e2716b4dc7085c7fb5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2020
ms.locfileid: "93400129"
---
# <a name="how-to-switch-between-views-and-the-xml-editor"></a>方法: ビューと XML エディターを切り替える

このトピックでは、XML スキーマ デザイナー (XSD デザイナー) のビューと XML エディターを切り替える方法について説明します。 この例では、[購買発注書のスキーマ](../xml-tools/sample-xsd-file-simple-schema.md)を使用します。

## <a name="to-switch-between-the-views-and-the-xml-editor"></a>ビューと XML エディターを切り替えるには

1. 新しい XML スキーマ ファイルを作成して編集するには、「[方法:XSD スキーマ ファイルを作成して編集する](../xml-tools/how-to-create-and-edit-an-xsd-schema-file.md)」の手順に従います。

2. XML エディターから XML スキーマ デザイナーに切り替えるには、XML エディター内を右クリックし、 **[デザイナーの表示]** をクリックします。

3. ウォーターマークを使用してグラフ ビューに切り替えるには、スタート ビューの **[ノード間のリレーションシップを表示するには、グラフ ビューを使用します]** リンクをクリックします。

4. **XML スキーマ エクスプローラー** からグラフ ビューに `USAddress` ノードをドラッグします。 グラフ ビューで `USAddress` ノードを右クリックし、コンテキスト メニューの **[コンテンツ モデル ビューで表示]** をクリックします。

     `USAddress` ノードの詳細を示したコンテンツ モデル ビューが表示されます。

5. ツール バーを使用してコンテンツ モデル ビューからスタート ビューに切り替えるには、XSD ツール バーの **スタート ビュー** ボタンをクリックします。

6. ホットキーを使用してビューを切り替える場合、スタート ビューに切り替えるには **Ctrl**+**1**、グラフ ビューに切り替えるには **Ctrl**+**2**、コンテンツ モデル ビューに切り替えるには **Ctrl**+**3** を押します。

7. コンテンツ モデル ビューから XML エディターに切り替えるには、ノードを右クリックし、コンテキスト メニューの **[コードの表示]** をクリックします。
