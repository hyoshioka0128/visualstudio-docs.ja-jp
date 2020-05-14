---
title: '方法: コレクションの関連付けをビジュアル化する (クラス デザイナー)'
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.classdesigner.collectionassociationline
- vs.classdesigner.ShowAssociationException
helpviewer_keywords:
- collection associations
- collections, collection associations
- Class Designer [Visual Studio], collection associations
ms.assetid: 54e39838-2fc9-4dc2-85b6-7e88a743108e
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7ba237b9c763421287e3878a6a98f59032bfd092
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "75590775"
---
# <a name="how-to-visualize-a-collection-association-in-class-designer"></a>方法: クラス デザイナーでコレクションの関連付けをビジュアル化する

他の型のコレクションであるプロパティとフィールドを、クラス ダイアグラムでコレクションの関連付けとして表示できます。 フィールドの型に所有しているクラスをリンクする行としてフィールドまたはプロパティを表示する通常の関連付けとは異なり、コレクションの関連付けは、収集された型に所有しているクラスをリンクする行として表示されます。

## <a name="to-create-a-collection-association"></a>コレクションの関連付けを作成するには

1. コードで、型自体が厳密に型指定されるコレクションであるプロパティまたはフィールドを作成します。

2. クラス ダイアグラムで、プロパティとフィールドが表示されるようにクラスを展開します。

3. クラスで、フィールドまたはプロパティを右クリックし、 **[コレクションの関連として表示]** を選択します。

プロパティまたはフィールドは、収集された型にリンクする関連行として表示されます。

## <a name="see-also"></a>参照

- [方法: 型の間の関連付けを作成する](how-to-create-associations-between-types.md)
- [クラスおよび型のデザイン](designing-and-viewing-classes-and-types.md)
