---
title: 'UML Class Diagrams: Reference | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: reference
f1_keywords:
- vs.teamarch.common.generalization.properties
- vs.teamarch.logicalclassdiagram.toolbox
- vs.teamarch.UMLModelExplorer.association
- vs.teamarch.common.unspecifiedtype.properties
- vs.teamarch.logicalclassdiagram.diagram
- vs.teamarch.UMLModelExplorer.logicalclassdiagram
- vs.teamarch.UMLModelExplorer.generalization
- vs.teamarch.common.unspecifiedtype
helpviewer_keywords:
- UML diagrams, class
- diagrams - modeling, class
- UML, class diagrams
- class diagrams - UML
- diagrams - modeling, UML class
ms.assetid: b7c88be0-0d86-4d65-af74-f37e8812d20f
caps.latest.revision: 43
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: da4e0e3bab904b660f3d843e105b7d256a63a1b5
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74297220"
---
# <a name="uml-class-diagrams-reference"></a>UML クラス図: リファレンス
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

UML クラス図は、アプリケーションが内部的に使用したり、ユーザーとのやり取りにおいて使用したりするオブジェクトおよび情報の構造を記述するものです。 そこで情報を記述する際に、詳細な実装は考慮されません。 クラスおよび関係は、データベース テーブル、XML ノード、ソフトウェア オブジェクトの組み合わせ、といったさまざまな方法で実装できます。

> [!NOTE]
> このトピックでは、UML クラス図について説明します。 .NET クラス図と呼ばれる別の種類のクラス図もあります。これは、プログラム コードを視覚化するために使用します。 For more information, see [Designing and Viewing Classes and Types](https://go.microsoft.com/fwlink/?LinkId=142231).

 To create a UML class diagram, on the **Architecture** menu, choose **New UML or Layer Diagram**. For more information about how to draw UML class diagrams, see [UML Class Diagrams: Guidelines](../modeling/uml-class-diagrams-guidelines.md). For more information about how to create and draw modeling diagrams, see [Edit UML models and diagrams](../modeling/edit-uml-models-and-diagrams.md).

 この機能をサポートする Visual Studio のバージョンを確認するには、「 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)」を参照してください。

## <a name="reading-class-diagrams"></a>クラス図の見方
 このセクションでは、UML クラス図に表示される要素について表で説明します。 これらの要素のプロパティについては、次のトピックを参照してください。

- [UML クラス ダイアグラムの型のプロパティ](../modeling/properties-of-types-on-uml-class-diagrams.md)

- [UML クラス図の属性のプロパティ](../modeling/properties-of-attributes-on-uml-class-diagrams.md)

- [UML クラス ダイアグラムの操作のプロパティ](../modeling/properties-of-operations-on-uml-class-diagrams.md)

- [UML クラス ダイアグラムの関連のプロパティ](../modeling/properties-of-associations-on-uml-class-diagrams.md)

  ![Three classes showing relationships and properties](../modeling/media/uml-classovreading.png "UML_ClassOvReading")

| **Shape** |       **要素**        |                                                                                                                                                             **説明**                                                                                                                                                              |
|-----------|--------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     1     |        **クラス**         |                                                           特定の構造上または動作上の特性を共有するオブジェクトの定義。 For more information, see [Properties of types on UML class diagrams](../modeling/properties-of-types-on-uml-class-diagrams.md).                                                            |
|     1     |        分類子        |                                                                                                             クラス、インターフェイス、または列挙の総称。 コンポーネント、ユース ケース、およびアクターも分類子です。                                                                                                             |
|     2     | 折りたたみ/展開コントロール |                                                                                         分類子の詳細が表示されていない場合は、分類子の左上にあるエキスパンダーをクリックします。 場合によっては、各セグメントの [+] をクリックする必要もあります。                                                                                         |
|     3     |      **属性**       |   分類子の各インスタンスにアタッチされている、型指定された値。<br /><br /> To add an attribute, click the **Attributes** section and then press **ENTER**. 属性のシグネチャを入力します。 For more information, see [Properties of attributes on UML class diagrams](../modeling/properties-of-attributes-on-uml-class-diagrams.md).   |
|     4     |      **Operation**       | 分類子のインスタンスが実行できるメソッドまたは関数。 To add an operation, click the **Operations** section and then press **ENTER**. 操作のシグネチャを入力します。 For more information, see [Properties of operations on UML class diagrams](../modeling/properties-of-operations-on-uml-class-diagrams.md). |
|     5     |     **Association**      |                                                                  2 つの分類子のメンバー間の関係。 For more information, see [Properties of associations on UML class diagrams](../modeling/properties-of-associations-on-uml-class-diagrams.md).                                                                   |
|    5a     |     **集計**      |                                                                                                    所有権を共有する関係を表す関連付け。 The **Aggregation** property of the owner role is set to **Shared**.                                                                                                     |
|    5b     |     **Composition**      |                                                                                                      「全体 - 部分」の関係を表す関連付け。 The **Aggregation** property of the owner role is set to **Composite**.                                                                                                      |
|     6     |   **Association Name**   |                                                                                                                                         関連付けの名前。 名前は空白にすることができます。                                                                                                                                          |
|     7     |      **Role Name**       |                       ロールの名前。つまり、関連付けの一方の端部の名前。 関連付けられているオブジェクトを参照するために使用できます。 前の図の Order `O` にとっては、`O.ChosenMenu` が、関連付けられている Menu です。<br /><br /> ロールごとに独自のプロパティを持ち、これらは関連付けのプロパティの下に表示されます。                       |
|     8     |     **Multiplicity**     |                                         もう一方の端部の各オブジェクトに対してリンクできる、この端部のオブジェクトの数を示します。 この例では、各 Order を正確に 1 つの Menu にリンクする必要があります。<br /><br /> **\\** \* means that there is no upper limit to the number of links that can be made.                                         |
|     9     |    **Generalization**    |  The *specific* classifier inherits part of its definition from the *general* classifier. コネクタの矢じり付きの端部にある方が、一般的な分類子です。 属性、関連付け、および操作が、特定の分類子に継承されます。<br /><br /> Use the **Inheritance** tool to create a generalization between two classifiers.   |

 ![Package containing interface and enumeration](../modeling/media/uml-classovpackage.png "UML_ClassOvPackage")

|形式|要素|説明|
|-----------|-------------|-----------------|
|10|**Interface**|外部から認識できるオブジェクトの動作の一部の定義。 For more information, see [Properties of types on UML class diagrams](../modeling/properties-of-types-on-uml-class-diagrams.md).|
|11|**Enumeration**|リテラル値のセットで構成される分類子。|
|12|**パッケージ**|分類子、関連付け、アクション、生存線、コンポーネント、およびパッケージのグループ。 論理クラス図は、メンバー分類子およびパッケージがパッケージ内に含まれているようすを示します。<br /><br /> Names are scoped within packages so that **Class1** within **Package1** is distinct from **Class1** outside that package. The name of the package appears as part of the **Qualified Name** properties of its contents.<br /><br /> You can set the **Linked Package** property of any UML diagram to refer to a package. この図に作成した要素はすべて、そのパッケージの一部となります。 They will appear under the package in **UML Model Explorer**.|
|13|**[インポート]**|あるパッケージが別のパッケージのすべての定義を含むことを示す、パッケージ間の関係。|
|14|**Dependency**|矢じり付きの端部側の分類子が変更された場合、これに依存する分類子の定義または実装が変更される可能性があります。|

 ![Realization shown with conector and lollipop](../modeling/media/uml-classovrealize.png "UML_ClassOvRealize")

|形式|**要素**|説明|
|-----------|-----------------|-----------------|
|16|**Realization**|クラスは、インターフェイスによって定義される操作および属性を実装します。<br /><br /> Use the **Inheritance** tool to create a realization between a class and an interface.|
|16|**Realization**|同じ関係を示す別の表現形式。 ロリポップ シンボルのラベルによってインターフェイスを識別します。<br /><br /> この形式で表現するには、既存の実現関係を選択します。 関連付けの近くにアクション タグが表示されます。 Click the action tag, and then click **Show as Lollipop**.|

## <a name="see-also"></a>参照
 [Edit UML models and diagrams](../modeling/edit-uml-models-and-diagrams.md) [UML Class Diagrams: Guidelines](../modeling/uml-class-diagrams-guidelines.md) [Properties of types on UML class diagrams](../modeling/properties-of-types-on-uml-class-diagrams.md) [Properties of attributes on UML class diagrams](../modeling/properties-of-attributes-on-uml-class-diagrams.md) [Properties of operations on UML class diagrams](../modeling/properties-of-operations-on-uml-class-diagrams.md) [Properties of associations on UML class diagrams](../modeling/properties-of-associations-on-uml-class-diagrams.md)
