---
title: ワークフローデザイナー-ClearCollection &lt; T &gt; アクティビティデザイナー
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.ClearCollection`1.UI
ms.assetid: db0e5da2-7b5a-4f1a-864c-f3aeeeeb51a7
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 710e221441736ecb2415aec32c7f0bfb9a2d99ac
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "88711626"
---
# <a name="clearcollectiont-activity-designer"></a>ClearCollection\<T> アクティビティ デザイナー

**Clearcollection \<T> **アクティビティデザイナーは、アクティビティを作成および構成するために使用され <xref:System.Activities.Statements.ClearCollection%601> ます。

## <a name="the-clearcollectiont-activity"></a>ClearCollection \<T> アクティビティ

<xref:System.Activities.Statements.ClearCollection%601> アクティビティで、指定したすべての項目のコレクションをクリアします。

### <a name="using-the-clearcollectiont-activity-designer"></a>ClearCollection \<T> アクティビティデザイナーの使用

** \<T> Clearcollection**アクティビティデザイナーは、[**ツールボックス**] の [**コレクション**] カテゴリにあります。このカテゴリにアクセスするには、ワークフローデザイナーの [**ツールボックス**] タブをクリックします。 または、[**表示**] メニューの [**ツールボックス**] を選択するか、 **Ctrl** + **Alt** + **X**キーを押します。

**Clearcollection \<T> **アクティビティデザイナーは、[**ツールボックス**] からドラッグして、アクティビティが配置されている任意の場所 (内など) にワークフローデザイナー画面にドロップできます <xref:System.Activities.Statements.Sequence> 。 アクティビティデザイナーを削除する <xref:System.Activities.Statements.ClearCollection%601> と、既定値 <xref:System.Activities.Activity.DisplayName%2A> の clearcollection<Int32 を持つアクティビティが作成さ \> れます。 (既定では、 *Typeargument* は **Int32**です。 TypeArgument は、プロパティグリッドで変更できます)。この <xref:System.Activities.Activity.DisplayName%2A> 値は、 **clearcollection \><T**アクティビティデザイナーのヘッダー、またはプロパティグリッドの [ **DisplayName** ] ボックスで編集できます。 他のプロパティは、プロパティ グリッドで編集する必要があります。

### <a name="the-clearcollectiont-properties"></a>ClearCollection \<T> プロパティ

次の表に、<xref:System.Activities.Statements.ClearCollection%601> のプロパティと、デザイナーでのその使用方法を示します。

|プロパティ名|必須|使用法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|×|<xref:System.Activities.Statements.ClearCollection%601> アクティビティの表示名を指定します (省略可能)。 既定値は ClearCollection<Int32 \> です。 <xref:System.Activities.Activity.DisplayName%2A> 値は必須ではありませんが、使用することをお勧めします。|
|<xref:System.Activities.Statements.ClearCollection%601.Collection%2A>|○|クリアする項目のコレクションを指定します。 このコレクションの型は **ICollection \<TypeArgument> です。** コレクションを指定するには、プロパティ グリッドで Visual Basic の式を入力します。|
|*TypeArgument*|○|<xref:System.Collections.Generic.ICollection%601> に格納される項目の T 型を指定します。 既定では、この *Typeargument* 型は **Int32**に設定されています。 型を変更するには、プロパティグリッドで、コンボボックスの *Typeargument* の値を変更します。|

## <a name="see-also"></a>関連項目

- [コレクション](../workflow-designer/collection-activity-designers.md)
- [AddToCollection\<T>](../workflow-designer/addtocollection-t-activity-designer.md)
- [ExistsInCollection\<T>](../workflow-designer/existsincollection-t-activity-designer.md)
- [RemoveFromCollection\<T>](../workflow-designer/removefromcollection-t-activity-designer.md)