---
title: Add stereotypes to UML model elements | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- UML model, stereotypes
ms.assetid: 82545252-83ce-4e11-a419-61373be75d16
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 67d489b1446e7205d72b53e160a8c7ca87f216d7
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74292330"
---
# <a name="add-stereotypes-to-uml-model-elements"></a>UML モデル要素にステレオタイプを追加する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

UML モデル要素にステレオタイプを追加して、注釈を付けたり、特別なプロパティを追加したりすることができます。 モデル要素にステレオタイプを追加するには、プロファイル内にステレオタイプを定義しておき、モデル要素が含まれているパッケージまたはモデルにそのプロファイルをリンクする必要があります。 ステレオタイプは、UML クラス、ユース ケース、コンポーネントなど、特定の種類のモデル要素にのみ追加できます。

 たとえば、«specification» ステレオタイプを持つ UML クラスを定義する場合は、標準プロファイル L2 にリンクされたパッケージまたはモデル内にそのクラスを作成する必要があります。

 既定では、すべてのモデルが UML 標準プロファイル L2 および L3 にリンクされます。

### <a name="to-link-a-profile-to-a-model-or-a-package"></a>プロファイルをモデルまたはパッケージにリンクするには

1. Open **UML Model Explorer**. On the **Architecture** menu, point to **Windows**, and then click **UML Model Explorer**.

2. プロファイル内のステレオタイプの適用先とする要素がすべて含まれるパッケージまたはモデルを見つけます。

3. Right-click the package or the model and then click **Properties**.

4. In the **Properties** window, set the **Profiles** property to the profiles that contain the stereotypes you want to use.

     これで、このプロファイルのステレオタイプを、モデルまたはパッケージに含まれているすべての要素で使用できるようになります。 パッケージに他のパッケージが含まれている場合、そのパッケージでも要素にステレオタイプを使用できるようになります。

### <a name="to-add-stereotypes-to-model-elements-or-relationships"></a>モデル要素または関係にステレオタイプを追加するには

1. Right-click the model element or relationship, either on a diagram or in **UML Model Explorer**, and then click **Properties**.

    > [!NOTE]
    > 複数の要素に同じステレオタイプを追加する場合は、複数の要素を選択してから、その中の 1 つを右クリックします。

2. Click the **Stereotypes** property and select the stereotypes that you want to apply.

     ほとんどの要素や関係では、選択したステレオタイプが &lt;&lt; &gt;&gt; に囲まれてモデル要素内に表示されます。

    > [!NOTE]
    > If you cannot see the **Stereotypes** property, or if the stereotype you want does not appear, verify that the model element is inside a package or a model to which the appropriate profile has been linked.

3. 一部のステレオタイプでは、モデル要素に対して追加のプロパティの値を設定できます。 To see these properties, expand the **Stereotypes** property.

### <a name="to-create-model-elements-within-a-package"></a>パッケージ内にモデル要素を作成するには

1. Create a package either in a UML Class Diagram, or in **UML Model Explorer**.

2. そのパッケージに、次のいずれかの方法でモデル要素を追加します。

    - UML クラス図で、要素を扱うツールをクリックし、図上のパッケージの内部をクリックします。

         \- または

    - In UML Model Explorer, right-click the package, point to **Add**, and then click an element type.

         \- または

    - UML モデル エクスプローラーで、既存の要素をパッケージにドラッグします。

         \- または

    - 図をパッケージにリンクさせた後、図内に要素を作成します。

         To do this, right-click a blank part of the diagram and then click **Properties**. In the **Properties** window, set **Linked Package** to the package you want.

         この図で作成した新しい要素はすべて、このパッケージ内に定義されることになります。

         この操作を実行できるのは、一部の種類の図に限られます。

## <a name="see-also"></a>参照
 [Define a profile to extend UML](../modeling/define-a-profile-to-extend-uml.md) [Customize your model with profiles and stereotypes](../modeling/customize-your-model-with-profiles-and-stereotypes.md) [Define packages and namespaces](../modeling/define-packages-and-namespaces.md)

