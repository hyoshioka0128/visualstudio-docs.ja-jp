---
title: ワークフローデザイナー TerminateWorkflow アクティビティデザイナー
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.TerminateWorkflow.UI
ms.assetid: 08e632ed-0724-4fb4-9df1-f8d443eaf0ac
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 078dfb43b5960580327448627a30eec20297d9f3
ms.sourcegitcommit: f3f668ecaf11b4c2738ebc91923c6b5e38e74670
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/16/2020
ms.locfileid: "76111780"
---
# <a name="terminateworkflow-activity-designer"></a>TerminateWorkflow アクティビティ デザイナー

**TerminateWorkflow**アクティビティデザイナーは、<xref:System.Activities.Statements.TerminateWorkflow> アクティビティを作成および構成するために使用されます。

## <a name="the-terminateworkflow-activity"></a>TerminateWorkflow アクティビティ

<xref:System.Activities.Statements.TerminateWorkflow> アクティビティは、ワークフローの実行を停止します。

### <a name="using-the-terminateworkflow-activity-designer"></a>TerminateWorkflow アクティビティ デザイナーの使用

**TerminateWorkflow**アクティビティデザイナーは、 **[ツールボックス**] の **[ランタイム]** カテゴリにあります。このカテゴリにアクセスするには、 **[ツール]** ボックス タブをクリックします (または、 **[表示]** メニューの **[ツールボックス]** を選択するか、CTRL + ALT + X キーを押します)。

**TerminateWorkflow**アクティビティデザイナーは、 **[ツールボックス]** からドラッグして、アクティビティを通常配置している任意の場所 (<xref:System.Activities.Statements.Sequence>内など) にドロップしてワークフローデザイナー画面にドロップできます。 これにより、TerminateWorkflow という既定の**DisplayName**を持つ <xref:System.Activities.Statements.TerminateWorkflow> アクティビティが作成されます。 <xref:System.Activities.Activity.DisplayName%2A> は、 **TerminateWorkflow**アクティビティデザイナーのヘッダー、またはプロパティグリッドの **[DisplayName]** ボックスで編集できます。

### <a name="the-terminateworkflow-properties"></a>TerminateWorkflow のプロパティ

次の表に、<xref:System.Activities.Statements.TerminateWorkflow> のプロパティと、デザイナーでのその使用方法を示します。 これらのプロパティは、プロパティグリッドで編集することができ、一部のプロパティはワークフローデザイナー画面で編集できます。

|プロパティ名|必須|使用状況|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|[False]|<xref:System.Activities.Statements.TerminateWorkflow> アクティビティの表示名。 既定値は TerminateWorkflow です。 表示名は必須ではありませんが、使用することをお勧めします。|
|<xref:System.Activities.Statements.TerminateWorkflow.Exception%2A>|[False]|ワークフローが停止されたときにスローする例外。 このプロパティは、プロパティ グリッドで設定します。|
|<xref:System.Activities.Statements.TerminateWorkflow.Reason%2A>|[False]|ワークフローが停止された理由。 このプロパティは、プロパティ グリッドで設定します。|

## <a name="see-also"></a>関連項目

- [ランタイム](../workflow-designer/runtime-activity-designers.md)
- [Persist](../workflow-designer/persist-activity-designer.md)
