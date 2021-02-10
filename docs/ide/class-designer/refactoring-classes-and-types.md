---
title: クラス デザイナーでのクラスと型の名前の変更および移動
description: クラス デザイナーと [クラスの詳細] ウィンドウを使用してクラスと型の名前変更と移動を行う方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.ClassDesigner.OverrideMembersDialog
helpviewer_keywords:
- members, overriding
- overriding members
- classes [Visual Studio], refactoring
- type members, overriding
- refactoring, types
- types [Visual Studio], refactoring
- Class Designer [Visual Studio], refactoring classes
- refactoring, classes
ms.assetid: dcf07bb4-fa3b-4224-9dec-566fd924a8ce
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 2f7941b3a2c9c3fe71119e3a4413ad97f56b6290
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99969855"
---
# <a name="refactor-classes-and-types-in-class-designer"></a>クラス デザイナーでのクラスと型のリファクタリング

コードをリファクタリングするときに、その外部動作ではなく、内部構造とオブジェクトの設計を変更することによって、コードが理解および保守しやすくなり、効率も向上します。 クラス デザイナーと [クラスの詳細] ウィンドウを使用すると、必要な作業の量を減らし、Visual Studio プロジェクト内の C#、Visual Basic、または C++ コードをリファクタリングするときに、バグが発生する可能性を低下させることができます。

> [!NOTE]
> プロジェクトはソース コードの管理下にあり、チェックアウトされていないので、プロジェクトのファイルは読み取り専用である可能性があります。このプロジェクトは、参照されているプロジェクトであるか、そのファイルがディスク上で読み取り専用としてマークされています。 これらの状態のいずれかに当てはまるプロジェクト内で作業する場合、プロジェクトの状態に応じて、さまざまな方法で作業を保存できます。 このことは、コードをリファクターする場合だけでなく、コードを直接編集するなど、別の方法でコードを変更する場合にも当てはまります。

## <a name="common-tasks"></a>一般的なタスク

|タスク|関連する参照先|
|----------| - |
|**クラスのリファクタリング:** リファクタリング操作を使用すると、クラスを部分クラスに分割したり、抽象基本クラスを実装したりできます。|-   [方法: 1 つのクラスを複数の部分クラスに分割する](how-to-split-a-class-into-partial-classes.md)|
|**インターフェイスの操作:** クラス デザイナーのクラス ダイアグラム上で、インターフェイス メソッド用のコードを提供するクラスに接続して、インターフェイスを実装できます。|-   [方法: インターフェイスを実装する](how-to-implement-an-interface.md)|
|**型、型のメンバー、およびパラメーターのリファクタリング:** クラス デザイナーを使用して、型の名前変更、型のメンバーのオーバーライド、またはメンバーを 1 つの型から別の型に移動することができます。 Null 許容型を作成することもできます。|-   [型および型のメンバーの名前変更](#rename-types-and-type-members)<br />-   [1 つの型から別の型への型のメンバーの移動](#move-type-members-from-one-type-to-another)<br />-   [方法: Null 許容型を作成する](how-to-create-a-nullable-type.md)|

## <a name="rename-types-and-type-members"></a>型および型のメンバーの名前変更

クラス デザイナーのクラス ダイアグラムまたは **[プロパティ]** ウィンドウで、型または型のメンバーの名前を変更できます。 **[クラスの詳細]** ウィンドウでは、メンバーの名前は変更できますが、型の名前は変更できません。 型または型のメンバーの名前を変更すると、以前の名前が表示されていた、すべてのウィンドウとコードの場所に変更が反映されます。

### <a name="rename-in-the-class-designer"></a>クラス デザイナーで名前を変更する

1. クラス ダイアグラムで、型またはメンバーを選択し、名前を選択します。

     メンバーの名前が編集可能になります。

2. 型または型のメンバーの新しい名前を入力します。

### <a name="rename-in-the-class-details-window"></a>[クラスの詳細] ウィンドウで名前を変更する

1. **[クラスの詳細]** ウィンドウを表示するには、型または型のメンバーを右クリックした後、**[クラスの詳細]** を選択します。

     **[クラスの詳細]** ウィンドウが表示されます。

2. **[名前]** 列で、型のメンバーの名前を変更します。

3. セルからフォーカスを移動するには、**Enter** キーを押すか、セルの外側をクリックします。

    > [!NOTE]
    > **[クラスの詳細]** ウィンドウでは、メンバーの名前は変更できますが、型の名前は変更できません。

### <a name="rename-in-the-properties-window"></a>[プロパティ] ウィンドウで名前を変更する

1. クラス ダイアグラムまたは **[クラスの詳細]** ウィンドウで、型またはメンバーを右クリックした後、**[プロパティ]** をクリックします。

     **[プロパティ]** ウィンドウが表示され、型または型のメンバーのプロパティが表示されます。

2. **[名前]** プロパティで、型または型のメンバーの名前を変更します。

     新しい名前は、以前の名前が表示されていた、現在のプロジェクト内のすべてのウィンドウとコードの場所に反映されます。

## <a name="move-type-members-from-one-type-to-another"></a>1 つの型から別の型への型のメンバーの移動

**クラス デザイナー** を使用すると、1 つの型から別の型に、型のメンバーを移動できます。 両方の型が、現在のクラス ダイアグラムに表示されている必要があります。

1. デザイン サーフェイスに表示されている型で、別の型に移動するメンバーを右クリックした後、 **[切り取り]** を選択します。

2. 移動先の型を右クリックした後、 **[貼り付け]** を選択します。

     プロパティが移動元の型から削除され、移動先の型に表示されます。

## <a name="see-also"></a>関連項目

- [クラスおよび型のデザイン](designing-and-viewing-classes-and-types.md)
