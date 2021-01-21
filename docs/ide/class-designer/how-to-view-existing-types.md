---
title: '方法: 既存の型を表示する (クラス デザイナー)'
description: 既存の型とそのメンバーを表示するために、その図形をクラス ダイアグラムに追加する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.classdesigner.CannotShowBaseType
helpviewer_keywords:
- types [Visual Studio], visualizing
- types [Visual Studio], class diagrams
- class diagrams, types
ms.assetid: de110a4e-5b51-4a40-9dee-615df4d8f999
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6b4660c4efc7c22431b7c9f0d9180576d524a372
ms.sourcegitcommit: 86e98df462b574ade66392f8760da638fe455aa0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/19/2020
ms.locfileid: "94901168"
---
# <a name="how-to-view-existing-types-in-class-designer"></a>方法: クラス デザイナーで既存の型を表示する

既存の型とそのメンバーを表示するには、その図形をクラス ダイアグラムに追加します。

ローカル型と参照型を表示できます。 ローカル型は現在開いているプロジェクトに含まれ、読み取りと書き込みができます。 参照型は別のプロジェクトまたは参照アセンブリに含まれ、読み取り専用です。

クラス ダイアグラムで新しい型を設計する場合は、「[方法: クラス デザイナーを使用して型を作成する](how-to-create-types.md)」を参照してください。

## <a name="to-see-types-in-a-project-on-a-class-diagram"></a>プロジェクトの型をクラス ダイアグラムで表示するには

1. **ソリューション エクスプローラー** のプロジェクトから、既存のクラス ダイアグラム (.cd) ファイルを開きます。 クラス ダイアグラムが存在しない場合は、プロジェクトに新しいクラス ダイアグラムを追加します。 「[方法:プロジェクトにクラス ダイアグラムを追加する](how-to-add-class-diagrams-to-projects.md)」を参照してください。

2. **ソリューション エクスプローラー** のプロジェクトから、ソース コード ファイルをクラス ダイアグラムにドラッグします。

    > [!NOTE]
    > ソリューションに複数のアプリでコードを共有しているプロジェクトがある場合、次のソースからのみファイルまたはコードをクラス ダイアグラムにドラッグできます。
    >
    > - ダイアグラムを含むアプリ プロジェクト
    > - アプリ プロジェクトによりインポートされた共有プロジェクト
    > - 参照プロジェクト
    > - アセンブリ

    ソース コード ファイルで定義された型を表す図形が、クラス ダイアグラムのファイルをドラッグした場所に表示されます。

**クラス ビュー** のプロジェクト ノードから 1 つ以上の型をクラス ダイアグラムにドラッグしてプロジェクトの型を表示することもできます。

> [!TIP]
> **クラスビュー** が開いていない場合は、**ビュー** メニューから **クラスビュー** を開きます。

ダイアグラムの既定の場所で型を表示するには、**クラス ビュー** で 1 つ以上の型を選択し、選択した型を右クリックし、 **[クラス ダイアグラムで表示]** を選択します。

> [!NOTE]
> 型を含む閉じられたクラス ダイアグラムが既にプロジェクトに存在する場合は、クラス ダイアグラムが開いて型シェイプが表示されます。 ただし、型を含むクラス ダイアグラムがプロジェクトに存在しない場合は、**クラス デザイナー** によって新しいクラス ダイアグラムがプロジェクトに作成されて開かれ、型が表示されます。

最初にダイアグラムで型を表示すると、図形は既定で縮小表示されます。 図形を展開して内容を表示できます。

### <a name="to-display-the-contents-of-a-project-in-a-class-diagram"></a>クラス ダイアグラムで、プロジェクトの内容を表示するには

**ソリューション エクスプローラー** または **クラス ビュー** で、プロジェクトを右クリックし、 **[表示]** を選択してから **[クラス ダイアグラムの表示]** を選択します。 自動設定されたクラス ダイアグラムが作成されます。

## <a name="see-also"></a>関連項目

- [方法: 型の間の継承を表示する](how-to-view-inheritance-between-types.md)
- [方法: クラス ダイアグラムをカスタマイズする](how-to-customize-class-diagrams.md)
- [型およびリレーションシップの表示](designing-and-viewing-classes-and-types.md)
