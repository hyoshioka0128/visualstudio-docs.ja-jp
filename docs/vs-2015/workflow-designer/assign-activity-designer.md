---
title: Assign アクティビティデザイナー |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Assign.UI
ms.assetid: ba3feb3c-f144-47ea-926d-cf752b804153
caps.latest.revision: 6
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 40ebe465d5eeb12a956d285a8313b0acdbcfb8d5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72659184"
---
# <a name="assign-activity-designer"></a>Assign アクティビティ デザイナー
**Assign**アクティビティデザイナーは、アクティビティを作成および構成するために使用され <xref:System.Activities.Statements.Assign> ます。

## <a name="the-assign-activity"></a>Assign アクティビティ
 <xref:System.Activities.Statements.Assign> アクティビティで、変数または引数に値を割り当てます。

### <a name="using-the-assign-activity-designer"></a>Assign アクティビティ デザイナーの使用
 **Assign**アクティビティデザイナーは、[**ツールボックス]** の [**プリミティブ**] カテゴリにあります。このカテゴリにアクセスするには、[**ツール**ボックス] タブをクリックします (または、[**表示**] メニューの [**ツールボックス**] を選択するか、CTRL + ALT + X キーを押します)。

 **Assign**アクティビティデザイナーは、[**ツールボックス**] からドラッグして、 [!INCLUDE[wfd2](../includes/wfd2-md.md)] アクティビティを通常配置している画面 (内など) にドロップできます <xref:System.Activities.Statements.Sequence> 。 これ <xref:System.Activities.Statements.Assign> により、Assign という既定の **DisplayName** を持つアクティビティが作成されます。 は、 <xref:System.Activities.Activity.DisplayName%2A> **Assign** アクティビティデザイナーのヘッダー、またはプロパティグリッドの [ **DisplayName** ] ボックスで編集できます。

### <a name="the-assign-properties"></a>Assign のプロパティ
 次の表に、<xref:System.Activities.Statements.Assign> のプロパティと、デザイナーでのその使用方法を示します。 これらのプロパティは、プロパティ グリッドで編集できます。また、その一部は[!INCLUDE[wfd2](../includes/wfd2-md.md)]画面で編集できます。

|プロパティ名|必須|使用|
|-------------------|--------------|-----------|
|<xref:System.Activities.Activity.DisplayName%2A>|×|<xref:System.Activities.Statements.Assign> アクティビティの表示名。 既定値は Assign です。 <xref:System.Activities.Activity.DisplayName%2A> 値は必須ではありませんが、使用することをお勧めします。|
|<xref:System.Activities.Statements.Assign.To%2A>|○|<xref:System.Activities.Statements.Assign.Value%2A> を割り当てる変数または引数。 有効な Visual Basic 識別子を指定する必要があります。 プロパティを設定するには、 **Assign**アクティビティデザイナーまたはプロパティグリッドの [ **To** ] ボックスに Visual Basic 式を入力します。|
|<xref:System.Activities.Statements.Assign.Value%2A>|○|変数に割り当てられる値。 を設定するに <xref:System.Activities.Statements.Assign.Value%2A> は、 **Assign**アクティビティデザイナーまたはプロパティグリッドの [**値**] ボックスに Visual Basic 式を入力します。|

## <a name="see-also"></a>参照
 [プリミティブ](../workflow-designer/primitives-activity-designers.md)[遅延](../workflow-designer/delay-activity-designer.md) [InvokeMethod](../workflow-designer/invokemethod-activity-designer.md) [WriteLine](../workflow-designer/writeline-activity-designer.md)