---
title: ワークフローデザイナー-FinalState アクティビティデザイナー
description: FinalState デザイナーを使用して、ステートマシンインスタンスを終了する状態を作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: aa186893-8775-40dd-981f-8593ead831d0
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 0a6ec51d17453a13f8c3ab1adffc5447afb5db7e
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99894180"
---
# <a name="finalstate-activity-designer"></a>FinalState アクティビティ デザイナー

<xref:System.Activities.Core.Presentation.FinalState> デザイナーは、ステート マシンのインスタンスを終了する <xref:System.Activities.Statements.State> を作成するために使用されます。

## <a name="using-the-finalstate-activity-designer"></a>FinalState アクティビティ デザイナーの使用

**Finalstate** デザイナーは、 <xref:System.Activities.Statements.State> ステートマシンで終了状態として事前に構成されているを作成するために使用されます。 <xref:System.Activities.Statements.State>アクティビティデザイナーを使用して作成されたに <xref:System.Activities.Core.Presentation.FinalState> は、 <xref:System.Activities.Statements.State.IsFinal%2A> プロパティが **true** に設定されており、アクティビティはなく、 <xref:System.Activities.Statements.State.Exit%2A> それからの遷移もありません。 アクティビティデザイナーを使用し <xref:System.Activities.Core.Presentation.FinalState> <xref:System.Activities.Statements.State> て、ステートマシンで終了状態として事前に構成されているアクティビティを追加するには、[**ツールボックス**] の [**ステートマシン**] セクションから **finalstate** アクティビティデザイナーをドラッグし、ワークフローデザイナーにドロップします。 <xref:System.Activities.Core.Presentation.FinalState> アクティビティ デザイナーは、<xref:System.Activities.Statements.StateMachine> にドロップして遷移を後で追加できます。または遷移は、<xref:System.Activities.Core.Presentation.FinalState> アクティビティ デザイナーをドロップしたときに作成できます。 遷移の作成の詳細については、「 [Transition](../workflow-designer/transition-activity-designer.md)」を参照してください。

### <a name="state-activity-properties-in-the-workflow-designer"></a>ワークフロー デザイナーでの State アクティビティのプロパティ

次の表に、<xref:System.Activities.Core.Presentation.FinalState> デザイナーを使用して設定できるプロパティと、デザイナーでのその使用方法を示します。 これらのプロパティの中には、プロパティ グリッドで編集できるものがあります。また、その一部はデザイナー画面で編集できます。

|プロパティ名|必須|使用|
|-|--------------|-|
|<xref:System.Activities.Statements.State.DisplayName%2A>|False|ヘッダーの <xref:System.Activities.Statements.State> アクティビティ デザイナーの表示名を指定します。 既定値は **State** です。 この値は、プロパティ グリッドで編集することも、アクティビティ デザイナーのヘッダーで直接編集することもできます。 <xref:System.Activities.Statements.State.DisplayName%2A> は、ワークフロー デザイナーの上部に表示される階層リンク バーで使用されます。<br /><br /> <xref:System.Activities.Statements.State.DisplayName%2A> は必須ではありませんが、使用することをお勧めします。|
|<xref:System.Activities.Statements.State.Entry%2A>|False|この状態の遷移時に発生するアクションを指定します。 この値を設定するには、 **ツールボックス** からアクティビティをドラッグし、 <xref:System.Activities.Statements.State.Entry%2A> 状態のセクションにドロップします。|

## <a name="see-also"></a>関連項目

- [StateMachine](../workflow-designer/statemachine-activity-designer.md)
- [状態](../workflow-designer/state-activity-designer.md)
- [移行](../workflow-designer/transition-activity-designer.md)