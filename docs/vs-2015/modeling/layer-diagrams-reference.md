---
title: 'Layer Diagrams: Reference | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: reference
f1_keywords:
- vs.teamarch.layerdiagram.layerexplorer.artifactlink
- vs.teamarch.layerdiagram.layerexplorer.artifactlink.properties
- vs.teamarch.layerdiagram.diagram
- vs.teamarch.UMLModelExplorer.layerdiagram
- vs.teamarch.layerdiagram.layerexplorer
- vs.teamarch.layerdiagram.shapes.properties
- vs.teamarch.layerdiagram.toolbox
helpviewer_keywords:
- architecture, layer diagrams
- layer diagrams
- diagrams - modeling, layer
- constraints, architectural
ms.assetid: f26c986c-1e79-420e-b29a-a283e6d8a71d
caps.latest.revision: 35
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: dd2b2d19e55cbaf9af63ddeafdbdf9f6d677c5bc
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74301610"
---
# <a name="layer-diagrams-reference"></a>レイヤー図: リファレンス
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

In Visual Studio, you can use a *layer diagram* to visualize the high-level, logical architecture of your system. A layer diagram organizes the physical artifacts in your system into logical, abstract groups called *layers*. これらのレイヤーは成果物が実行する主要タスクまたはシステムの主要コンポーネントについて説明します。 各レイヤーには、より詳細なタスクを示す入れ子になったレイヤーを含めることもできます。

 この機能をサポートする Visual Studio のバージョンを確認するには、「 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)」を参照してください。

 レイヤー間の必要とされる依存関係、または既存の依存関係を指定できます。 矢印で表されるこれらの依存関係は、どのレイヤーが、他のレイヤーが表す機能を使用できるか、または現在使用しているかを示します。 システムを個別のロールおよび機能を記述するレイヤーに分けて整理したレイヤー図を使用すると、コードを簡単に理解、再利用、および保守できるようになります。

 レイヤー図は、次のタスクを実行するために使用します。

- システムの既存の論理アーキテクチャまたは必要とされる論理アーキテクチャを伝達する。

- 既存のコードと必要とされるアーキテクチャの間の不整合を見つける。

- システムのリファクタリング、更新、または進化によって必要とされるアーキテクチャにもたらされる変更の影響を視覚化する。

- チェックイン操作とビルド操作による検証を追加することによって、必要とされるアーキテクチャをコードの開発中および保守中に補強する。

  このトピックでは、レイヤー図で使用できる要素について説明します。 For more detailed information about how to create and draw layer diagrams, see [Layer Diagrams: Guidelines](../modeling/layer-diagrams-guidelines.md). For more information about layering patterns, visit the [Patterns & Practices site](https://go.microsoft.com/fwlink/?LinkId=145794).

## <a name="reading-layer-diagrams"></a>レイヤー図の解説
 ![Elements on layer diagrams](../modeling/media/uml-layerrefreading.png "UML_LayerRefReading")

 レイヤー図で使用できる要素を次の表に示します。

|**Shape**|**要素**|**説明**|
|---------------|-----------------|---------------------|
|1|**Layer**|システム内の物理的な成果物の論理グループ。 このような成果物には、名前空間、プロジェクト、クラス、メソッドなどがあります。<br /><br /> To see the artifacts that are linked to a layer, open the shortcut menu for the layer, and then choose **View Links** to open **Layer Explorer**.<br /><br /> For more information, see [Layer Explorer](#Explorer).<br /><br /> -   **Forbidden Namespace Dependencies** - Specifies that artifacts associated with this layer cannot depend on the specified namespaces.<br />-   **Forbidden Namespaces** - Specifies that artifacts associated with this layer must not belong to the specified namespaces.<br />-   **Required Namespaces** - Specifies that artifacts associated with this layer must belong to one of the specified namespaces.|
|2|**Dependency**|あるレイヤーが別のレイヤーの機能を使用することはできても、その逆はできないことを示します。<br /><br /> -   **Direction** - Specifies the direction of the dependency.|
|3|**Bidirectional Dependency**|あるレイヤーが別のレイヤーの機能を使用でき、その逆もできることを示します。<br /><br /> -   **Direction** - Specifies the direction of the dependency.|
|4|**コメント**|全般的なノートを図または図の要素に追加するために使用します。|
|5|**Comment Link**|コメントを図の要素にリンクするために使用します。|

## <a name="Explorer"></a> Layer Explorer
 各レイヤーをソリューション内の成果物 (たとえば、プロジェクト、クラス、名前空間、プロジェクト ファイル、またはソフトウェアのその他のパート) にリンクすることができます。 レイヤーの数字は、レイヤーにリンクされている成果物の数を示します。 ただし、レイヤーの成果物の数を読み取るときには、次の点に注意してください。

- 1 つのレイヤーが他の成果物を含む 1 つの成果物にリンクされているが、他の成果物に直接リンクされていない場合、その数字にはリンクされた成果物のみが含まれます。 ただし、レイヤー検証時の分析にはそれらの他の成果物も含まれます。

   たとえば、1 つのレイヤーが 1 つの名前空間にリンクされている場合、その名前空間に複数のクラスが含まれていても、リンクされた成果物の数は 1 です。 レイヤーに名前空間の各クラスへのリンクもある場合、その数字にはリンクされたクラスが含まれます。

- 1 つのレイヤーに成果物にリンクされた他のレイヤーが含まれている場合は、そのコンテナー レイヤーの数字にそれらの成果物が含まれていなくても、コンテナー レイヤーはそれらの成果物にリンクされます。

  レイヤーと成果物のリンクの詳細については、次のドキュメントを参照してください。

- [レイヤー図: ガイドライン](../modeling/layer-diagrams-guidelines.md)

- [コードからのレイヤー図の作成](../modeling/create-layer-diagrams-from-your-code.md)

#### <a name="to-examine-the-linked-artifacts"></a>リンクされた成果物を確認するには

- On the layer diagram, open the shortcut menu for one or more layers, and then choose **View Links**.

     **Layer Explorer** opens and shows the artifacts that are linked to the selected layers. **Layer Explorer** has a column that shows each of the properties of the artifact links.

    > [!NOTE]
    > If you cannot see all of these properties, expand the **Layer Explorer** window.

    |**Column in Layer Explorer**|**説明**|
    |----------------------------------|---------------------|
    |**Categories**|クラス、名前空間、ソース ファイルなどの成果物の種類|
    |**Layer**|成果物にリンクしているレイヤー|
    |**Supports Validation**|If **True**, then the layer validation process can verify that the project conforms to dependencies to or from this element.<br /><br /> If **False**, then the link does not participate in the layer validation process.<br /><br /> For more information, see [Layer Diagrams: Guidelines](../modeling/layer-diagrams-guidelines.md).|
    |**識別子**|リンクされた成果物への参照|

## <a name="see-also"></a>参照
 [アプリのモデルを生成する](../modeling/create-models-for-your-app.md)
