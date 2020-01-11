---
title: 'UML クラス図: Reference |Microsoft Docs'
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
ms.openlocfilehash: 06e83e254cad77d4ede9716a18a51f6476fb51ad
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/10/2020
ms.locfileid: "75850176"
---
# <a name="uml-class-diagrams-reference"></a>UML クラス図: リファレンス
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

UML クラス図は、アプリケーションが内部的に使用したり、ユーザーとのやり取りにおいて使用したりするオブジェクトおよび情報の構造を記述するものです。 そこで情報を記述する際に、詳細な実装は考慮されません。 クラスおよび関係は、データベース テーブル、XML ノード、ソフトウェア オブジェクトの組み合わせ、といったさまざまな方法で実装できます。

> [!NOTE]
> このトピックでは、UML クラス図について説明します。 .NET クラス図と呼ばれる別の種類のクラス図もあります。これは、プログラム コードを視覚化するために使用します。 詳細については、「[クラスと型の設計と表示](https://msdn.microsoft.com/library/ab7aty24.aspx)」を参照してください。

 UML クラス図を作成するには、 **[アーキテクチャ]** メニューの **[新しい Uml またはレイヤー図]** をクリックします。 UML クラス図を描画する方法の詳細については、「 [Uml クラス図: ガイドライン](../modeling/uml-class-diagrams-guidelines.md)」を参照してください。 モデリング図を作成して描画する方法の詳細については、「 [UML モデルとダイアグラムの編集](../modeling/edit-uml-models-and-diagrams.md)」を参照してください。

 この機能をサポートする Visual Studio のバージョンを確認するには、「 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)」を参照してください。

## <a name="reading-class-diagrams"></a>クラス図の見方
 このセクションでは、UML クラス図に表示される要素について表で説明します。 これらの要素のプロパティについては、次のトピックを参照してください。

- [UML クラス ダイアグラムの型のプロパティ](../modeling/properties-of-types-on-uml-class-diagrams.md)

- [UML クラス図の属性のプロパティ](../modeling/properties-of-attributes-on-uml-class-diagrams.md)

- [UML クラス ダイアグラムの操作のプロパティ](../modeling/properties-of-operations-on-uml-class-diagrams.md)

- [UML クラス ダイアグラムの関連のプロパティ](../modeling/properties-of-associations-on-uml-class-diagrams.md)

  ![リレーションシップとプロパティを示す3つのクラス](../modeling/media/uml-classovreading.png "UML_ClassOvReading")

| **オート** |       **要素**        |                                                                                                                                                             **説明**                                                                                                                                                              |
|-----------|--------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     1     |        **クラス**         |                                                           特定の構造上または動作上の特性を共有するオブジェクトの定義。 詳細については、「 [UML クラス図の型のプロパティ](../modeling/properties-of-types-on-uml-class-diagrams.md)」を参照してください。                                                            |
|     1     |        分類子        |                                                                                                             クラス、インターフェイス、または列挙の総称。 コンポーネント、ユース ケース、およびアクターも分類子です。                                                                                                             |
|     2     | 折りたたみ/展開コントロール |                                                                                         分類子の詳細が表示されていない場合は、分類子の左上にあるエキスパンダーをクリックします。 場合によっては、各セグメントの [+] をクリックする必要もあります。                                                                                         |
|     3     |      **属性**       |   分類子の各インスタンスにアタッチされている、型指定された値。<br /><br /> 属性を追加するには、 **[属性]** セクションをクリックし、 **enter キーを**押します。 属性のシグネチャを入力します。 詳細については、「 [UML クラス図の属性のプロパティ](../modeling/properties-of-attributes-on-uml-class-diagrams.md)」を参照してください。   |
|     4     |      **操作**       | 分類子のインスタンスが実行できるメソッドまたは関数。 操作を追加するには、 **[操作]** セクションをクリックし、 **enter キーを**押します。 操作のシグネチャを入力します。 詳細については、「 [UML クラス図の操作のプロパティ](../modeling/properties-of-operations-on-uml-class-diagrams.md)」を参照してください。 |
|     5     |     **づける**      |                                                                  2 つの分類子のメンバー間の関係。 詳細については、「 [UML クラス図の関連付けのプロパティ](../modeling/properties-of-associations-on-uml-class-diagrams.md)」を参照してください。                                                                   |
|    5a     |     **集計**      |                                                                                                    所有権を共有する関係を表す関連付け。 所有者ロールの**Aggregation**プロパティが**Shared**に設定されています。                                                                                                     |
|    5b     |     **構成**      |                                                                                                      「全体 - 部分」の関係を表す関連付け。 Owner ロールの**Aggregation**プロパティは、**複合**に設定されます。                                                                                                      |
|     6     |   **関連付け名**   |                                                                                                                                         関連付けの名前。 名前は空白にすることができます。                                                                                                                                          |
|     7     |      **ロール名**       |                       ロールの名前。つまり、関連付けの一方の端部の名前。 関連付けられているオブジェクトを参照するために使用できます。 前の図の Order `O` にとっては、`O.ChosenMenu` が、関連付けられている Menu です。<br /><br /> ロールごとに独自のプロパティを持ち、これらは関連付けのプロパティの下に表示されます。                       |
|     8     |     **カーディナリティ**     |                                         もう一方の端部の各オブジェクトに対してリンクできる、この端部のオブジェクトの数を示します。 この例では、各 Order を正確に 1 つの Menu にリンクする必要があります。<br /><br /> **\\** \* は、作成できるリンクの数に上限がないことを意味します。                                         |
|     9     |    **汎化**    |  *特定*の分類子は、*一般的な*分類子から定義の一部を継承します。 コネクタの矢じり付きの端部にある方が、一般的な分類子です。 属性、関連付け、および操作が、特定の分類子に継承されます。<br /><br /> **継承**ツールを使用して、2つの分類子の間の汎化を作成します。   |

 ![インターフェイスと列挙を含むパッケージ](../modeling/media/uml-classovpackage.png "UML_ClassOvPackage")

|[図形]|要素|説明|
|-----------|-------------|-----------------|
|10|**Interface**|外部から認識できるオブジェクトの動作の一部の定義。 詳細については、「 [UML クラス図の型のプロパティ](../modeling/properties-of-types-on-uml-class-diagrams.md)」を参照してください。|
|11|**列挙**|リテラル値のセットで構成される分類子。|
|12|**パッケージ**|分類子、関連付け、アクション、生存線、コンポーネント、およびパッケージのグループ。 論理クラス図は、メンバー分類子およびパッケージがパッケージ内に含まれているようすを示します。<br /><br /> 名前はパッケージ内でスコープが設定されるため、 **Package1**内の**class1**は、そのパッケージの外部の**class1**とは区別されません。 パッケージの名前は、その内容の**修飾名**プロパティの一部として表示されます。<br /><br /> 任意の UML 図の リンクされた**パッケージ**のプロパティを設定して、パッケージを参照することができます。 この図に作成した要素はすべて、そのパッケージの一部となります。 これらは、 **UML モデルエクスプローラー**のパッケージの下に表示されます。|
|13|**Import**|あるパッケージが別のパッケージのすべての定義を含むことを示す、パッケージ間の関係。|
|14|**依存関係**|矢じり付きの端部側の分類子が変更された場合、これに依存する分類子の定義または実装が変更される可能性があります。|

 ![コネクタとロリポップで表示される実現](../modeling/media/uml-classovrealize.png "UML_ClassOvRealize")

|[図形]|**要素**|説明|
|-----------|-----------------|-----------------|
|16|**実現**|クラスは、インターフェイスによって定義される操作および属性を実装します。<br /><br /> **継承**ツールを使用して、クラスとインターフェイスの間の実現を作成します。|
|16|**実現**|同じ関係を示す別の表現形式。 ロリポップ シンボルのラベルによってインターフェイスを識別します。<br /><br /> この形式で表現するには、既存の実現関係を選択します。 関連付けの近くにアクション タグが表示されます。 アクションタグをクリックし、 **[ロリポップとして表示]** をクリックします。|

## <a name="see-also"></a>参照
 Uml[モデルとダイアグラムの編集](../modeling/edit-uml-models-and-diagrams.md)uml クラス図[:](../modeling/uml-class-diagrams-guidelines.md) uml クラス図の[型のガイドラインプロパティ](../modeling/properties-of-types-on-uml-class-diagrams.md)uml クラス図の[属性の](../modeling/properties-of-attributes-on-uml-class-diagrams.md)プロパティ uml クラス図の[操作の](../modeling/properties-of-operations-on-uml-class-diagrams.md)プロパティ uml クラス図[の関連付けの](../modeling/properties-of-associations-on-uml-class-diagrams.md)プロパティ
