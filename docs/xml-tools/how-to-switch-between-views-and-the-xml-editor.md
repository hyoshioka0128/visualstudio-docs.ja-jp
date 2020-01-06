---
title: '方法: ビューと XML エディターを切り替える'
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: cb69fbbd-d99c-439e-9498-5df9050f8df0
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 54e43b00c877f5453d1dc28bbc9d5546fcef056f
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75592629"
---
# <a name="how-to-switch-between-views-and-the-xml-editor"></a>方法: ビューと XML エディターを切り替える

このトピックでは、XML スキーマデザイナー (XSD デザイナー) ビューと XML エディターを切り替える方法について説明します。 この例では、注文[書スキーマ](../xml-tools/sample-xsd-file-simple-schema.md)を使用します。

## <a name="to-switch-between-the-views-and-the-xml-editor"></a>ビューと XML エディターを切り替えるには

1. 新しい XML スキーマファイルを作成および編集するには、「[方法: XSD スキーマファイルを作成および編集](../xml-tools/how-to-create-and-edit-an-xsd-schema-file.md)する」の手順に従います。

2. Xml エディターから XML スキーマデザイナーに切り替えるには、XML エディター内の任意の場所を右クリックし、 **[ビューデザイナー]** をクリックします。

3. 透かしを使用してグラフビューに切り替えるには、**グラフビューを使用する** をクリックして、スタートビューの ノード リンクの関係を確認します。

4. **XML スキーマエクスプローラー**からグラフビューに [`USAddress`] ノードをドラッグします。 グラフビューの [`USAddress`] ノードを右クリックし、コンテキストメニューの **[コンテンツモデルビューで表示]** をクリックします。

     `USAddress` ノードの詳細を示したコンテンツ モデル ビューが表示されます。

5. ツールバーを使用してコンテンツモデルビューからスタートビューに切り替えるには、XSD ツールバーの **[ビューの開始]** ボタンをクリックします。

6. ホットキーを使用してビューを切り替えるには、[スタート] ビューの場合は**ctrl**+**1** 、グラフビューの場合は Ctrl+**2** **、コンテンツ**モデルビューの場合は**ctrl+** **3**を押します。

7. コンテンツモデルビューから XML エディターにアクセスするには、ノードを右クリックし、コンテキストメニューの **[コードの表示]** をクリックします。
