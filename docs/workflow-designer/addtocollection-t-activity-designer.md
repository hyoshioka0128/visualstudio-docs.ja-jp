---
title: ワークフローデザイナー-AddToCollection &lt; T &gt; アクティビティデザイナー
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.AddToCollection`1.UI
ms.assetid: f7fc0702-164e-4370-8946-bb2f9f9384b7
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1ffa24dce2691f061c5947e15d7fc7923d632b38
ms.sourcegitcommit: de98ed7edc81383e47b87ae6e61143fbbbe7bc56
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2020
ms.locfileid: "88706543"
---
# <a name="addtocollectiont-activity-designer"></a>AddToCollection\<T> アクティビティ デザイナー

**Addtocollection \<T> **アクティビティデザイナーは、アクティビティを作成および構成するために使用され <xref:System.Activities.Statements.AddToCollection%601> ます。

## <a name="the-addtocollectiont-activity"></a>AddToCollection \<T> アクティビティ

<xref:System.Activities.Statements.AddToCollection%601> アクティビティでは、項目をコレクションに追加します。

### <a name="using-the-addtocollectiont-activity-designer"></a>AddToCollection \<T> アクティビティデザイナーの使用

** \<T> Addtocollection**アクティビティデザイナーは、[**ツールボックス**] の [**コレクション**] カテゴリにあります。このカテゴリにアクセスするには、ワークフローデザイナーの [**ツールボックス**] タブをクリックします。 または、[**表示**] メニューの [**ツールボックス**] を選択するか、 **Ctrl** + **Alt** + **X**キーを押します。

**Addtocollection \<T> **アクティビティデザイナーは、[**ツールボックス**] からドラッグして、アクティビティが配置されている任意の場所 (内など) にワークフローデザイナー画面にドロップできます <xref:System.Activities.Statements.Sequence> 。 **Addtocollection \<T> **アクティビティデザイナーを削除する <xref:System.Activities.Statements.AddToCollection%601> と、既定値 <xref:System.Activities.Activity.DisplayName%2A> の addtocollection<Int32 を持つアクティビティが作成さ \> れます。 (既定では、 *Typeargument* は **Int32**です。 TypeArgument は、プロパティグリッドで変更できます)。この <xref:System.Activities.Activity.DisplayName%2A> 値は、 **addtocollection \><T**アクティビティデザイナーのヘッダー、またはプロパティグリッドの [ **DisplayName** ] ボックスで編集できます。 他のプロパティは、プロパティ グリッドで編集する必要があります。

### <a name="the-addtocollectiont-properties"></a>AddToCollection \<T> プロパティ

次の表に、<xref:System.Activities.Statements.AddToCollection%601> のプロパティと、デザイナーでのその使用方法を示します。

|プロパティ名|必須|使用法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|False|<xref:System.Activities.Statements.AddToCollection%601> アクティビティの表示名。 既定値は AddToCollection<Int32 \> です。 <xref:System.Activities.Activity.DisplayName%2A> 値は必須ではありませんが、使用することをお勧めします。|
|<xref:System.Activities.Statements.AddToCollection%601.Item%2A>|True|コレクションに追加する項目 \<T> 。 この項目の型は *T*で、 *typeargument*型です。 項目を指定するには、プロパティ グリッドで Visual Basic の式を入力します。|
|<xref:System.Activities.Statements.AddToCollection%601.Collection%2A>|True|項目の追加先のコレクション。 このコレクションの型は**ICollection<TypeArgument \> **です。 コレクションを指定するには、プロパティ グリッドで Visual Basic の式を入力します。|
|*TypeArgument*|True|<xref:System.Collections.Generic.ICollection%601> に格納される項目の T 型。 既定では、この *Typeargument* 型は **Int32**に設定されています。 型を変更するには、プロパティグリッドで、コンボボックスの *Typeargument* の値を変更します。|

## <a name="see-also"></a>関連項目

- [コレクション](../workflow-designer/collection-activity-designers.md)
- [AddToCollection \<T> アクティビティデザイナー](../workflow-designer/addtocollection-t-activity-designer.md)
- [ClearCollection\<T>](../workflow-designer/clearcollection-t-activity-designer.md)
- [ExistsInCollection\<T>](../workflow-designer/existsincollection-t-activity-designer.md)
- [RemoveFromCollection\<T>](../workflow-designer/removefromcollection-t-activity-designer.md)
