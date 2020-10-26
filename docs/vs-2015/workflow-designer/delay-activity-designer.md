---
title: Delay アクティビティデザイナー |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Delay.UI
ms.assetid: f51742a8-2c9a-47d1-8a23-18459d03ae19
caps.latest.revision: 8
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: a47279bc68503ba645fea3ef23a04ce9d5ef4c41
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72656795"
---
# <a name="delay-activity-designer"></a>Delay アクティビティ デザイナー
**Delay**アクティビティデザイナーは、アクティビティを作成および構成するために使用され <xref:System.Activities.Statements.Delay> ます。

## <a name="the-delay-activity"></a>Delay アクティビティ
 <xref:System.Activities.Statements.Delay> アクティビティで、ワークフローの実行を、指定した時間だけ遅らせます。

### <a name="using-the-delay-activity-designer"></a>Delay アクティビティ デザイナーの使用
 **Delay**アクティビティデザイナーは、[**ツール**ボックス] の [**プリミティブ**] カテゴリにあります。このカテゴリにアクセスするには、の [**ツールボックス**] タブをクリックします [!INCLUDE[wfd2](../includes/wfd2-md.md)] (または、[**表示**] メニューの [**ツールバー** ] を選択するか、CTRL + ALT + X キーを押します)。

 **Delay**アクティビティデザイナーは、[**ツールボックス**] からドラッグして、 [!INCLUDE[wfd2](../includes/wfd2-md.md)] アクティビティを通常配置している画面の任意の場所 (内など) にドロップできます <xref:System.Activities.Statements.Sequence> 。 この操作により、Delay という既定の <xref:System.Activities.Statements.Delay> を持つ <xref:System.Activities.Activity.DisplayName%2A> アクティビティが作成されます。 は、 <xref:System.Activities.Activity.DisplayName%2A> **Delay** アクティビティデザイナーのヘッダー、またはプロパティグリッドの [ **DisplayName** ] ボックスで編集できます。

### <a name="the-delay-properties"></a>Delay のプロパティ
 次の表に、<xref:System.Activities.Statements.Delay> のプロパティと、デザイナーでのその使用方法を示します。 これらのプロパティは、プロパティ グリッドで編集できます。また、その一部は[!INCLUDE[wfd2](../includes/wfd2-md.md)]のデザイナー画面で編集できます。

|プロパティ名|必須|使用|
|-------------------|--------------|-----------|
|<xref:System.Activities.Activity.DisplayName%2A>|×|<xref:System.Activities.Statements.Delay> アクティビティの表示名。 既定値は Delay です。 <xref:System.Activities.Activity.DisplayName%2A> 値は必須ではありませんが、使用することをお勧めします。|
|<xref:System.Activities.Statements.Delay.Duration%2A>|○|ワークフローの実行を遅らせる時間の長さ。 このプロパティは、プロパティ グリッドで設定します。 時間の長さを指定するには、00:00:00 という形式のリテラル <xref:System.TimeSpan>、または Visual Basic の式を入力します。|

## <a name="see-also"></a>参照
 [プリミティブ](../workflow-designer/primitives-activity-designers.md) [Assign](../workflow-designer/assign-activity-designer.md) [Delay アクティビティデザイナー](../workflow-designer/delay-activity-designer.md) [InvokeMethod](../workflow-designer/invokemethod-activity-designer.md) [WriteLine](../workflow-designer/writeline-activity-designer.md)