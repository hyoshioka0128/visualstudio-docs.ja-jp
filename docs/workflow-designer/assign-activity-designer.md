---
title: ワークフローデザイナー-Assign アクティビティデザイナー
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Assign.UI
ms.assetid: ba3feb3c-f144-47ea-926d-cf752b804153
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 83a01c96b64dcd55adfd775efc266063efbab27d
ms.sourcegitcommit: 186c0c250d85ac74274fa1e438b4c7c7108d8a36
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/22/2020
ms.locfileid: "86875944"
---
# <a name="assign-activity-designer"></a>Assign アクティビティ デザイナー

**Assign**アクティビティデザイナーは、アクティビティを作成および構成するために使用され <xref:System.Activities.Statements.Assign> ます。

## <a name="the-assign-activity"></a>Assign アクティビティ

<xref:System.Activities.Statements.Assign> アクティビティで、変数または引数に値を割り当てます。

### <a name="using-the-assign-activity-designer"></a>Assign アクティビティ デザイナーの使用

**Assign**アクティビティデザイナーは、[**ツールボックス]** の [**プリミティブ**] カテゴリにあります。このカテゴリにアクセスするには、[**ツール**ボックス] タブをクリックします (または、[**表示**] メニューの [**ツールボックス**] を選択するか、CTRL + ALT + X キーを押します)。

**Assign**アクティビティデザイナーは、[**ツールボックス**] からドラッグして、アクティビティが配置されているワークフローデザイナー画面 (内など) にドロップできます <xref:System.Activities.Statements.Sequence> 。 **Assign**アクティビティデザイナーを削除する <xref:System.Activities.Statements.Assign> と、assign という既定の**DisplayName**を持つアクティビティが作成されます。 は、 <xref:System.Activities.Activity.DisplayName%2A> **Assign**アクティビティデザイナーのヘッダー、またはプロパティグリッドの [ **DisplayName** ] ボックスで編集できます。

### <a name="the-assign-properties"></a>Assign のプロパティ

次の表に、<xref:System.Activities.Statements.Assign> のプロパティと、デザイナーでのその使用方法を示します。 これらのプロパティは、プロパティグリッドで編集することができ、一部のプロパティはワークフローデザイナー画面で編集できます。

|プロパティ名|必須|使用|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|誤り|<xref:System.Activities.Statements.Assign> アクティビティの表示名。 既定値は Assign です。 <xref:System.Activities.Activity.DisplayName%2A> 値は必須ではありませんが、使用することをお勧めします。|
|<xref:System.Activities.Statements.Assign.To%2A>|正しい|<xref:System.Activities.Statements.Assign.Value%2A> を割り当てる変数または引数。 この値は、有効な Visual Basic 識別子である必要があります。 プロパティを設定するには、 **Assign**アクティビティデザイナーまたはプロパティグリッドの [ **To** ] ボックスに Visual Basic 式を入力します。|
|<xref:System.Activities.Statements.Assign.Value%2A>|正しい|変数に割り当てられる値。 を設定するに <xref:System.Activities.Statements.Assign.Value%2A> は、 **Assign**アクティビティデザイナーまたはプロパティグリッドの [**値**] ボックスに Visual Basic 式を入力します。|

## <a name="see-also"></a>こちらもご覧ください

- [プリミティブ](../workflow-designer/primitives-activity-designers.md)
- [[遅延]](../workflow-designer/delay-activity-designer.md)
- [InvokeMethod](../workflow-designer/invokemethod-activity-designer.md)
- [WriteLine](../workflow-designer/writeline-activity-designer.md)