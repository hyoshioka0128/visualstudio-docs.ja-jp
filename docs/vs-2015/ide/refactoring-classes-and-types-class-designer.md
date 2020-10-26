---
title: クラスおよび型のリファクタリング (クラス デザイナー) | Microsoft ドキュメント
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
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
caps.latest.revision: 30
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 5803b720ae1271d8319310820d1f0dc159db8bf9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72670267"
---
# <a name="refactoring-classes-and-types-class-designer"></a>クラスおよび型のリファクタリング (クラス デザイナー)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

コードをリファクタリングするときに、その外部動作ではなく、内部構造とオブジェクトの設計を変更することによって、コードが理解および保守しやすくなり、効率も向上します。 クラス デザイナーと [クラスの詳細] ウィンドウを使用すると、必要な作業の量を減らし、Visual Studio プロジェクト内の Visual C# .NET、Visual Basic .NET、または C++ コードをリファクタリングするときに、バグが発生する可能性を低下させることができます。

> [!NOTE]
> プロジェクトはソース コードの管理下にあり、チェックアウトされていないので、プロジェクトのファイルは読み取り専用である可能性があります。このプロジェクトは、参照されているプロジェクトであるか、そのファイルがディスク上で読み取り専用としてマークされています。 これらの状態のいずれかに当てはまるプロジェクト内で作業する場合、プロジェクトの状態に応じて、さまざまな方法で作業を保存できます。 このことは、コードをリファクターする場合だけでなく、コードを直接編集するなど、別の方法でコードを変更する場合にも当てはまります。 詳細については、「 [読み取り専用の情報の表示 (クラス デザイナー)](https://msdn.microsoft.com/33e2d3a9-1668-4d10-ae56-fa09b3156e0a)を参照してください。

## <a name="common-tasks"></a>一般的なタスク

|タスク|関連する参照先|
|----------|------------------------|
|**クラスのリファクタリング:** リファクタリング操作を使用すると、クラスを部分クラスに分割したり、抽象基本クラスを実装したりできます。|-   [方法: クラスを部分クラスに分割する (クラスデザイナー)](../ide/how-to-split-a-class-into-partial-classes-class-designer.md)|
|**インターフェイスの操作:** クラス デザイナーのクラス ダイアグラム上で、インターフェイス メソッド用のコードを提供するクラスに接続して、インターフェイスを実装できます。|-   [方法: インターフェイスを実装する (クラスデザイナー)](../ide/how-to-implement-an-interface-class-designer.md)|
|**型、型のメンバー、およびパラメーターのリファクタリング:** クラス デザイナーを使用して、型の名前変更、型のメンバーのオーバーライド、またはメンバーを 1 つの型から別の型に移動することができます。 Null 許容型を作成することもできます。|-   [型と型のメンバーの名前変更](../ide/refactoring-classes-and-types-class-designer.md#RenamingTypesAndMembers)<br />-   [型のメンバーをある型から別の型に移動する](../ide/refactoring-classes-and-types-class-designer.md#MovingTypeMembers)<br />-   [方法: Null 許容型を作成する (クラスデザイナー)](../ide/how-to-create-a-nullable-type-class-designer.md)|

### <a name="renaming-types-and-type-members"></a><a name="RenamingTypesAndMembers"></a> 型と型のメンバーの名前変更
 クラス デザイナーのクラス ダイアグラムまたは [プロパティ] ウィンドウで、型または型のメンバーの名前を変更できます。 [クラスの詳細] ウィンドウでは、メンバーの名前は変更できますが、型の名前は変更できません。 型または型のメンバーの名前を変更すると、以前の名前が表示されていた、すべてのウィンドウとコードの場所に変更が反映されます。

##### <a name="to-rename-a-name-in-the-class-designer"></a>クラス デザイナーで名前を変更するには

1. クラス ダイアグラムで、型またはメンバーを選択し、名前をクリックします。

     メンバーの名前が編集可能になります。

2. 型または型のメンバーの新しい名前を入力します。

##### <a name="to-rename-a-name-in-the-class-details-window"></a>[クラスの詳細] ウィンドウで名前を変更するには

1. [クラスの詳細] ウィンドウを表示するには、型または型のメンバーを右クリックした後、 **[クラスの詳細]** をクリックします。

     [クラスの詳細] ウィンドウが表示されます。

2. **[名前]** 列で、型のメンバーの名前を変更します。

3. セルからフォーカスを移動するには、 **enter** キーを押すか、セルをクリックします。

    > [!NOTE]
    > [クラスの詳細] ウィンドウでは、メンバーの名前は変更できますが、型の名前は変更できません。

##### <a name="to-rename-a-name-in-the-properties-window"></a>[プロパティ] ウィンドウで名前を変更するには

1. クラス ダイアグラムまたは [クラスの詳細] ウィンドウで、型またはメンバーを右クリックした後、 **[プロパティ]** をクリックします。

     [プロパティ] ウィンドウが表示され、型または型のメンバーのプロパティが表示されます。

2. **[名前]** プロパティで、型または型のメンバーの名前を変更します。

     新しい名前は、以前の名前が表示されていた、現在のプロジェクト内のすべてのウィンドウとコードの場所に反映されます。

### <a name="moving-type-members-from-one-type-to-another"></a><a name="MovingTypeMembers"></a> 型のメンバーをある型から別の型に移動する
 **クラス デザイナー**を使用すると、両方が現在のクラス ダイアグラムに表示されている 1 つの型から別の型に、型のメンバーを移動できます。

##### <a name="to-move-a-type-member-from-one-type-to-another"></a>型のメンバーを 1 つの型から別の型に移動するには

1. デザイン サーフェイスに表示されている型で、別の型に移動するメンバーを右クリックした後、 **[切り取り]** をクリックします。

2. 移動先の型を右クリックした後、 **[貼り付け]** をクリックします。

     プロパティが移動元の型から削除され、移動先の型に表示されます。

## <a name="related-topics"></a>関連トピック

|Title|説明|
|-----------|-----------------|
|[型およびリレーションシップの表示 (クラス デザイナー)](../ide/viewing-types-and-relationships-class-designer.md)||
|[クラスおよび型のデザイン (クラス デザイナー)](../ide/designing-classes-and-types-class-designer.md)||
