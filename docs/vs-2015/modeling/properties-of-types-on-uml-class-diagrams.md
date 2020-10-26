---
title: UML クラス図の型のプロパティ |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: reference
f1_keywords:
- vs.teamarch.logicalclassdiagram.shapes.properties
helpviewer_keywords:
- UML, element properties
ms.assetid: 6e1ef2d0-d67a-401a-bd64-d5e034decd2c
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 9881393e792cf8bf49dc6d0b9459b18969dea171
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72671327"
---
# <a name="properties-of-types-on-uml-class-diagrams"></a>UML クラス ダイアグラムの型のプロパティ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

UML クラス図では、 *型* はクラス、インターフェイス、または列挙体です。

> [!NOTE]
> このトピックでは、UML クラス図における型のプロパティについて説明します。 詳細については、次のトピックを参照してください。

- [UML クラス図: リファレンス](../modeling/uml-class-diagrams-reference.md)

- [UML クラス図: ガイドライン](../modeling/uml-class-diagrams-guidelines.md)

- [UML クラス図の属性のプロパティ](../modeling/properties-of-attributes-on-uml-class-diagrams.md)

- [UML クラス ダイアグラムの操作のプロパティ](../modeling/properties-of-operations-on-uml-class-diagrams.md)

- [UML クラス ダイアグラムの関連のプロパティ](../modeling/properties-of-associations-on-uml-class-diagrams.md)

## <a name="properties"></a>Properties
 クラス、インターフェイス、または列挙のプロパティを次に示します。

 型のプロパティを表示するには、図または **UML モデルエクスプローラー**で型を右クリックし、[ **プロパティ**] をクリックします。 プロパティが [ **プロパティ** ] ウィンドウに表示されます。

|**プロパティ**|**既定**|表示される場所|説明|
|------------------|-----------------|----------------|-----------------|
|**名前**|既定名|すべての要素|要素を指定します。|
|**修飾名**|格納元のパッケージ :: 型名|すべての要素|要素を一意に識別します。 要素を格納するパッケージの修飾名が先頭につきます。|
|**色**|型の種類の既定値|すべての要素|この図形の色。 他のプロパティとは異なり、これは基になるモデル要素のプロパティではありません。 同じ型の異なるビューで異なる色を表示できます。|
|**抽象型**|×|クラス|true の場合、クラスはインスタンス化できず、基本クラスとして使用されることになります。|
|**リーフ**|×|クラス、インターフェイス|true の場合、型は派生型を持たないことになります。|
|**アクティブ**|×|クラス|true の場合、この型の各インスタンスはコントロールのスレッドに関連付けられます。|
|**可視性**|パブリック|クラス、インターフェイス、列挙|-Public-グローバルに表示されます。<br />-Private-この型は、それを所有するパッケージ内に表示されます。<br />-Package-パッケージ内に表示されます。|
|**作業項目**|関連付けなし|すべての要素|この要素に関連付けられている作業項目の数。 作業項目を関連付けるには、「 [モデル要素と作業項目のリンク](../modeling/link-model-elements-and-work-items.md)」を参照してください。|
|**説明**|(空白)|すべての要素|ここに、項目に関する一般的なメモを作成できます。|
|**テンプレートのバインド**|(なし)|クラス、インターフェイス、列挙|空でない場合、この型はこのテンプレート クラスに対するバインディング パラメーター値によって定義されます。 プロパティを展開すると、テンプレート パラメーターのバインディングが表示されます。|
|**テンプレートパラメーター**|(なし)|クラス、インターフェイス、列挙|空でない場合、これは、ここに一覧表示されているパラメーターを持つテンプレート クラスです。 パラメーターを追加したり、個々のパラメーターのプロパティを表示したりするには、[ **...]** をクリックします。|

## <a name="see-also"></a>参照
 Uml[クラス図の属性の](../modeling/properties-of-attributes-on-uml-class-diagrams.md)プロパティ uml クラス図の[操作の](../modeling/properties-of-operations-on-uml-class-diagrams.md)プロパティ uml クラス図の[関連の](../modeling/properties-of-associations-on-uml-class-diagrams.md)プロパティ[uml クラス図: ガイドライン](../modeling/uml-class-diagrams-guidelines.md)
