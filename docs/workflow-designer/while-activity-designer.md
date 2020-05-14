---
title: ワークフローデザイナー-While アクティビティデザイナー
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.While.UI
ms.assetid: ea008091-2e4c-4f64-bfa5-afb919552446
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 77954925533c51885a056f7156121e68851ad769
ms.sourcegitcommit: f3f668ecaf11b4c2738ebc91923c6b5e38e74670
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/16/2020
ms.locfileid: "76115170"
---
# <a name="while-activity-designer"></a>While アクティビティ デザイナー

<xref:System.Activities.Statements.While> アクティビティは、指定された <xref:System.Activities.Statements.While.Condition%2A> が**true**と評価される間、<xref:System.Activities.Statements.While.Body%2A> に含まれるアクティビティを実行します。 場合によっては、含まれているアクティビティが実行されない可能性があります。 含まれているアクティビティを少なくとも 1 回は実行する必要がある場合は、<xref:System.Activities.Statements.DoWhile> アクティビティを代わりに使用します。

## <a name="while-properties-in-workflow-designer"></a>ワークフロー デザイナーでの While のプロパティ

次の表に、最も役に立つ <xref:System.Activities.Statements.While> アクティビティのプロパティと、デザイナーでのその使用方法を示します。

|プロパティ名|必須|使用状況|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|[False]|ヘッダーの <xref:System.Activities.Statements.While> アクティビティ デザイナーの表示名を指定します。 既定値は While です。 この値は、 **[プロパティ]** ウィンドウで編集することも、アクティビティデザイナーのヘッダーで直接編集することもできます。<br /><br /> <xref:System.Activities.Activity.DisplayName%2A> は必須ではありませんが、使用することをお勧めします。|
|<xref:System.Activities.Statements.While.Body%2A>|[False]|<xref:System.Activities.Statements.While.Condition%2A> が**true**と評価されたときに実行するアクティビティを格納します。|
|<xref:System.Activities.Statements.While.Condition%2A>|True|<xref:System.Activities.Statements.While.Body%2A> 内のアクティビティを実行するかどうかを判断するために評価される Visual Basic 式を格納します。|

## <a name="see-also"></a>関連項目

- [制御フロー](../workflow-designer/control-flow-activity-designers.md)
- [DoWhile](../workflow-designer/dowhile-activity-designer.md)
