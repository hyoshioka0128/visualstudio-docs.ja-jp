---
title: XML スキーマ デザイナーと XML エディターの統合
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 43d7a8e6-bd94-4407-a800-15a145c74223
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 23a9220d84e2fb1a15545d1a880b0084952da77f
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75592582"
---
# <a name="integration-with-xml-editor"></a>XML エディターとの統合

XML スキーマ デザイナーは、XML エディターと統合されています。 XML エディターで XSD ファイルを変更すると、[XML スキーマ エクスプローラー](../xml-tools/xml-schema-explorer.md)にもその変更が反映されます。 [グラフ ビュー](../xml-tools/graph-view.md)または[コンテンツ モデル ビュー](../xml-tools/content-model-view.md)が開いている場合には、これらにも変更が反映されます。 次の方法を使用して XML スキーマ デザイナーと XML エディターの間を移動できます。

- XML エディターでノードを右クリックし、 **[XML スキーマ エクスプローラーで表示]** をクリックします。

- グラフ ビューと **XML スキーマ エクスプローラー**では、ノードをダブルクリックするか、ノードを右クリックして **[コードの表示]** をクリックします。 コンテンツ モデル ビューでは、ノードを右クリックして **[コードの表示]** を選択します。

次のスクリーン ショットは、XML スキーマが表示されている **XML スキーマ エクスプローラー**を示しています。 **XML スキーマ エクスプローラー**では、スキーマ セットがツリー ビューに表示されます。 XML エディターには、**XML スキーマ エクスプローラー**で現在アクティブになっているノードのテキスト ビューが表示されます。

![XSDDesignerWithXMLEditor](../xml-tools/media/xsddesignerwithxmleditor.gif)

場合によっては、XML エディターとグラフィカルなデザイナーのコードを並べて表示すると便利です。 2 つのファイルを同時に表示するには、XML エディター内を右クリックし、 **[デザイナーの表示]** をクリックします。 Visual Studio Windows メニューで、 **[水平 (または垂直) タブ グループの新規作成]** を選択します。

![XSDDesignerWithXMLEditorAndCMV](../xml-tools/media/xsddesignerwithxmleditorandcmv.gif)

## <a name="see-also"></a>関連項目

- [XML スキーマ エクスプローラー](../xml-tools/xml-schema-explorer.md)
