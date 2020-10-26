---
title: XML エディターとの統合 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: 43d7a8e6-bd94-4407-a800-15a145c74223
caps.latest.revision: 10
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 8c0d1088e9932613466209ef8517ac5035c0b613
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72656252"
---
# <a name="integration-with-xml-editor"></a>XML エディターとの統合
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

XML スキーマ デザイナーは、XML エディターと統合されています。 XML エディターで XSD ファイルを変更すると、 [Xml スキーマエクスプローラー](../xml-tools/xml-schema-explorer.md)に変更が反映されます。 [グラフ ビュー](../xml-tools/graph-view.md)または[コンテンツ モデル ビュー](../xml-tools/content-model-view.md)が開いている場合には、これらにも変更が反映されます。 次の方法を使用して XML スキーマ デザイナーと XML エディターの間を移動できます。

- XML エディターでノードを右クリックし、[ **Xml スキーマエクスプローラーで表示**] をクリックします。

- グラフビューと XML スキーマエクスプローラーで、ノードをダブルクリックするか、ノードを右クリックして [コードの **表示**] を選択します。 コンテンツ モデル ビューでは、ノードを右クリックして **[コードの表示]** を選択します。

  次のスクリーン ショットは、XML スキーマが表示されている XML スキーマ エクスプローラーを示しています。 XML スキーマ エクスプローラーでは、スキーマ セットがツリー ビューに表示されます。 XML エディターには、XML スキーマ エクスプローラーで現在アクティブになっているノードのテキスト ビューが表示されます。

  ![XSDDesignerWithXMLEditor](../xml-tools/media/xsddesignerwithxmleditor.gif "XSDDesignerWithXMLEditor")

  場合によっては、XML エディターとグラフィカルなデザイナーのコードを並べて表示すると便利です。 両方のファイルを同時に表示するには、XML エディター内の任意の場所を右クリックし、[ **デザイナーの表示**] をクリックします。 Visual Studio Windows メニューで、 **[水平 (または垂直) タブ グループの新規作成]** を選択します。

  ![XSDDesignerWithXMLEditorAndCMV](../xml-tools/media/xsddesignerwithxmleditorandcmv.gif "XSDDesignerWithXMLEditorAndCMV")

## <a name="see-also"></a>参照
 [XML スキーマ エクスプローラー](../xml-tools/xml-schema-explorer.md)
