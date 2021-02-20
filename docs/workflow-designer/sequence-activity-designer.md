---
title: ワークフローデザイナーシーケンスアクティビティデザイナー
description: Sequence アクティビティに、順番に実行される子アクティビティの順序付けられたコレクションが含まれていることを確認します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Sequence.UI
ms.assetid: 51c8d3cb-4d43-458f-9631-b63755f9ac94
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: c7bfc8c850cee9273af2af3b28f71b9d27209d9a
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99943641"
---
# <a name="sequence-activity-designer"></a>Sequence アクティビティ デザイナー

<xref:System.Activities.Statements.Sequence> アクティビティには、子アクティビティの順序付きコレクションが含まれており、これらのコレクションが順番に実行されます。

他の方法でアクティビティのセットを順番に実行するには、<xref:System.Activities.Statements.Flowchart> アクティビティを使用します。 フローチャートを作成する単純な分岐またはループプログラムフローがある場合は、 [フローチャート](../workflow-designer/flowchart-activity-designer.md) の使用を検討してください。

## <a name="using-the-sequence-activity-designer"></a>Sequence アクティビティ デザイナーの使用

アクティビティを追加するには <xref:System.Activities.Statements.Sequence> 、[**ツールボックス**] から **Sequence** アクティビティデザイナーをドラッグし、ワークフローデザイナー画面にドロップします。 このアクティビティに子アクティビティを追加するには <xref:System.Activities.Statements.Sequence> 、[ **ツールボックス** ] から他のアクティビティをドラッグし、[ここにアクティビティをドロップします] というヒントテキストが表示されているボックス内の三角形にドロップします。

### <a name="sequence-activity-properties-in-the-workflow-designer"></a>ワークフロー デザイナーでの Sequence アクティビティのプロパティ

次の表に、<xref:System.Activities.Statements.Sequence> のプロパティと、デザイナーでのその使用方法を示します。 これらのプロパティは、プロパティ グリッドまたはデザイナー画面で編集できます。

|プロパティ名|必須|使用|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|False|ヘッダーの <xref:System.Activities.Statements.Sequence> アクティビティ デザイナーの表示名を指定します。 既定値は Sequence です。 この値は、プロパティ グリッドで編集することも、アクティビティ デザイナーのヘッダーで直接編集することもできます。<br /><br /> <xref:System.Activities.Activity.DisplayName%2A> は必須ではありませんが、使用することをお勧めします。|

## <a name="see-also"></a>関連項目

- [フローチャート](../workflow-designer/flowchart-activity-designer.md)
- [制御フロー](../workflow-designer/control-flow-activity-designers.md)