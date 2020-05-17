---
title: '方法: クラス デザイナーを使用して型を作成する'
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- VS.Clr.ClrAttributesDialog
helpviewer_keywords:
- custom attributes, applying
- class diagrams, creating types
- classes [Visual Studio], creating with Class Designer
- Class Designer [Visual Studio], creating classes
- types [Visual Studio], class diagrams
- attributes [Visual Studio], applying custom
ms.assetid: 94458c31-28bc-40e2-9737-85868788a0e5
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 881a8ed7f1aceb5f97eaed1f0b9285951d1d39f6
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "75590177"
---
# <a name="how-to-create-types-by-using-class-designer"></a>方法: クラス デザイナーを使用して型を作成する

C# および Visual Basic プロジェクトの新しい型を設計するには、これらをクラス ダイアグラム上で作成します。 既存の型を見る場合は、「[方法: 既存の型を表示する](how-to-view-existing-types.md)」をご覧ください。

## <a name="create-a-new-type"></a><a name="CreateType"></a> 新しい型を作成する

1. **クラス デザイナー**の**ツールボックス**から、いずれかをクラス ダイアグラムにドラッグします。

    - **[クラス]** または **[抽象クラス]**

    - **Enum**

    - **インターフェイス**

    - **[構造体]** (VB) または **[構造体]** (C#)

    - **Delegate**

    - **[モジュール]** (VB のみ)

2. 型の名前を付けます。 それからアクセス レベルを選択します。

3. 型の初期コードを追加するファイルを選択します。

    - 新しいクラス ファイルを作成して、そのファイルを現在のプロジェクトに追加するには、 **[新しいファイルの作成]** をクリックし、ファイル名を入力します。

    - 既存のファイルにコードを追加するには、 **[存在するファイルに追加]** をクリックします。

         ソリューションに複数のアプリでコードを共有しているプロジェクトがある場合、対応するクラス ファイルが同じアプリ プロジェクトまたは共有プロジェクトにある場合にのみ、アプリケーション プロジェクトで新しい型をクラス ダイアグラムに追加できます。

4. 次に、型を定義するために他の項目を追加します。

    |||
    |-|-|
    |**対象**|**[追加]**|
    |クラス、抽象クラス、構造体|型を定義するメソッド、プロパティ、フィールド、イベント、コンストラクター (メソッド)、デストラクター (メソッド)、および定数|
    |列挙型|列挙型を構成するフィールド値|
    |インターフェイス|インターフェイスを構成するメソッド、プロパティ、イベント|
    |Delegate|デリゲートを定義するパラメーター|
    |[Module]|モジュールを定義するメソッド、プロパティ、フィールド、イベント、コンストラクター (メソッド)、および定数|

     「[メンバーの作成](creating-and-configuring-type-members.md#create-members)」をご覧ください。

## <a name="apply-a-custom-attribute-to-a-type"></a><a name="CustAttributeType"></a> カスタム属性を型に適用する

1. クラス ダイアグラムで型の図形をクリックします。

2. **[プロパティ]** で、型の **[カスタム属性]** プロパティの横の省略記号 (...) ボタンをクリックします。

3. 1 つ以上のカスタム属性を 1 行あたり 1 つ追加します。 角かっこで閉じません。

   カスタム属性が型に適用されます。

## <a name="apply-a-custom-attribute-to-a-type-member"></a><a name="CustAttributeMember"></a> カスタム属性を型のメンバーに適用する

1. クラス ダイアグラムの型の図形でメンバーの名前をクリックするか、[クラスの詳細] ウィンドウでその行をクリックします。

2. **[プロパティ]** で、メンバーの **[カスタム属性]** プロパティを探します。

3. 1 つ以上のカスタム属性を 1 行あたり 1 つ追加します。 角かっこで閉じません。

   カスタム属性が型に適用されます。

## <a name="see-also"></a>参照

- [方法: 型の間の継承を作成する](how-to-create-inheritance-between-types.md)
- [方法: 型の間の関連付けを作成する](how-to-create-associations-between-types.md)
- [型のメンバーの作成と構成](creating-and-configuring-type-members.md)
- [クラスおよび型のデザイン](designing-and-viewing-classes-and-types.md)
