---
title: '方法: ビューと XML エディターを切り替える |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: cb69fbbd-d99c-439e-9498-5df9050f8df0
caps.latest.revision: 9
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 28267f705dd9a747d0e3f3ac5dc2869ab7de8f6a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72656318"
---
# <a name="how-to-switch-between-views-and-the-xml-editor"></a>方法: ビューと XML エディターを切り替える
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このトピックでは、XML スキーマ デザイナー (XSD デザイナー) のビューと XML エディターを切り替える方法について説明します。 この例では、注文 [書スキーマ](../xml-tools/sample-xsd-file-simple-schema.md)を使用します。

### <a name="to-switch-between-the-views-and-the-xml-editor"></a>ビューと XML エディターを切り替えるには

1. 新しい XML スキーマファイルを作成および編集するには、「 [方法: XSD スキーマファイルを作成および編集](../xml-tools/how-to-create-and-edit-an-xsd-schema-file.md)する」の手順に従います。

2. Xml エディターから XML スキーマデザイナーに切り替えるには、XML エディター内の任意の場所を右クリックし、[ **ビューデザイナー**] をクリックします。

3. ウォーターマークを使用してグラフ ビューに切り替えるには、スタート ビューの **[ノード間のリレーションシップを表示するには、グラフ ビューを使用します]** リンクをクリックします。

4. XML スキーマ エクスプローラーからグラフ ビューに `USAddress` ノードをドラッグします。 グラフ ビューで `USAddress` ノードを右クリックし、コンテキスト メニューの **[コンテンツ モデル ビューで表示]** をクリックします。

     `USAddress` ノードの詳細を示したコンテンツ モデル ビューが表示されます。

5. ツール バーを使用してコンテンツ モデル ビューからスタート ビューに切り替えるには、XSD ツール バーのスタート ビュー ボタンをクリックします。

6. ホット キーを使用してビューを切り替える場合、スタート ビューに切り替えるには Ctrl + 1、グラフ ビューに切り替えるには Ctrl + 2、およびコンテンツ モデル ビューに切り替えるには Ctrl + 3 を押します。

7. コンテンツモデルビューから XML エディターにアクセスするには、ノードを右クリックし、コンテキストメニューの [ **コードの表示** ] をクリックします。
