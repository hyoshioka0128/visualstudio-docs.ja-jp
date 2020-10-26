---
title: TerminateWorkflow アクティビティデザイナー |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Statements.TerminateWorkflow.UI
ms.assetid: 08e632ed-0724-4fb4-9df1-f8d443eaf0ac
caps.latest.revision: 4
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: c204c14818a9c6e6fb0a46e6234b550838f3b1a4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72607092"
---
# <a name="terminateworkflow-activity-designer"></a>TerminateWorkflow アクティビティ デザイナー
**TerminateWorkflow**アクティビティデザイナーは、アクティビティを作成および構成するために使用され <xref:System.Activities.Statements.TerminateWorkflow> ます。

## <a name="the-terminateworkflow-activity"></a>TerminateWorkflow アクティビティ
 <xref:System.Activities.Statements.TerminateWorkflow> アクティビティは、ワークフローの実行を停止します。

### <a name="using-the-terminateworkflow-activity-designer"></a>TerminateWorkflow アクティビティ デザイナーの使用
 **TerminateWorkflow**アクティビティデザイナーは、 **[ツールボックス**] の [**ランタイム**] カテゴリにあります。このカテゴリにアクセスするには、[**ツール**ボックス] タブをクリックします (または、[**表示**] メニューの [**ツールボックス**] を選択するか、CTRL + ALT + X キーを押します)。

 **TerminateWorkflow**アクティビティデザイナーは、[**ツールボックス**] からドラッグして、 [!INCLUDE[wfd2](../includes/wfd2-md.md)] アクティビティを通常配置している画面の任意の場所 (内など) にドロップできます <xref:System.Activities.Statements.Sequence> 。 これ <xref:System.Activities.Statements.TerminateWorkflow> により、TerminateWorkflow という既定の **DisplayName** を持つアクティビティが作成されます。 は、 <xref:System.Activities.Activity.DisplayName%2A> **TerminateWorkflow** アクティビティデザイナーのヘッダー、またはプロパティグリッドの [ **DisplayName** ] ボックスで編集できます。

### <a name="the-terminateworkflow-properties"></a>TerminateWorkflow のプロパティ
 次の表に、<xref:System.Activities.Statements.TerminateWorkflow> のプロパティと、デザイナーでのその使用方法を示します。 これらのプロパティは、プロパティ グリッドで編集できます。また、その一部は[!INCLUDE[wfd2](../includes/wfd2-md.md)]画面で編集できます。

|プロパティ名|必須|使用法|
|-------------------|--------------|-----------|
|<xref:System.Activities.Activity.DisplayName%2A>|×|<xref:System.Activities.Statements.TerminateWorkflow> アクティビティの表示名。 既定値は TerminateWorkflow です。 表示名は必須ではありませんが、使用することをお勧めします。|
|<xref:System.Activities.Statements.TerminateWorkflow.Exception%2A>|×|ワークフローが停止されたときにスローする例外。 このプロパティは、プロパティ グリッドで設定します。|
|<xref:System.Activities.Statements.TerminateWorkflow.Reason%2A>|×|ワークフローが停止された理由。 このプロパティは、プロパティ グリッドで設定します。|

## <a name="see-also"></a>参照
 [ランタイム](../workflow-designer/runtime-activity-designers.md)の[永続](../workflow-designer/persist-activity-designer.md)化