---
title: ワークフローデザイナー-DoWhile アクティビティデザイナー
description: 指定された条件が false と評価されるまで、DoWhile アクティビティが本文に含まれるアクティビティを少なくとも1回実行する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.DoWhile.UI
ms.assetid: 948deb35-d72f-462b-bea6-4b119c10a148
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8385fe376f56738d76e066dc172e7b6b516f9a08
ms.sourcegitcommit: ed26b6e313b766c4d92764c303954e2385c6693e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/10/2020
ms.locfileid: "94438062"
---
# <a name="dowhile-activity-designer"></a>DoWhile アクティビティ デザイナー

アクティビティは、 <xref:System.Activities.Statements.DoWhile> <xref:System.Activities.Statements.DoWhile.Body%2A> 指定された条件が **false** と評価されるまで、少なくとも1回に含まれるアクティビティを実行します。 ループの本体に含まれるアクティビティを 0 回以上実行する必要がある場合は、代わりに、<xref:System.Activities.Statements.While> アクティビティを使用します。

## <a name="dowhile-properties-in-the-workflow-designer"></a>ワークフロー デザイナーでの DoWhile のプロパティ

次の表に、最も役に立つ <xref:System.Activities.Statements.DoWhile> アクティビティのプロパティと、デザイナーでのそれらの使用方法について説明します。

|プロパティ名|必須|使用法|
|-|--------------|-|
|<xref:System.Activities.Statements.DoWhile.Body%2A>|×|条件が **true** のときに実行するアクティビティ。 アクティビティを追加するには <xref:System.Activities.Statements.DoWhile.Body%2A> 、"ここにアクティビティをドロップします" というヒントテキストが表示された **dowhile** アクティビティデザイナーの [ **Body** ] ボックスに、[ツールボックス] からアクティビティをドロップします。|
|<xref:System.Activities.Statements.DoWhile.Condition%2A>|○|ループの各繰り返しの後に評価する条件。 を設定するには <xref:System.Activities.Statements.DoWhile.Condition%2A> 、 **dowhile** アクティビティデザイナーまたはプロパティグリッドの [ **条件** ] ボックスに Visual Basic 式を入力します。|

## <a name="see-also"></a>関連項目

- [While](../workflow-designer/while-activity-designer.md)
- [制御フロー](../workflow-designer/control-flow-activity-designers.md)