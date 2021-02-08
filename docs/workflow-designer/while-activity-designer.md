---
title: ワークフローデザイナー-While アクティビティデザイナー
description: While アクティビティが本文に含まれるアクティビティを実行し、指定した条件が true と評価される方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.While.UI
ms.assetid: ea008091-2e4c-4f64-bfa5-afb919552446
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 9447d32f17283e7123e2f99490acc49c1613360d
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99837997"
---
# <a name="while-activity-designer"></a>While アクティビティ デザイナー

アクティビティは、 <xref:System.Activities.Statements.While> に含まれるアクティビティを実行し、 <xref:System.Activities.Statements.While.Body%2A> 指定されたは <xref:System.Activities.Statements.While.Condition%2A> **true** に評価されます。 場合によっては、含まれているアクティビティが実行されない可能性があります。 含まれているアクティビティを少なくとも 1 回は実行する必要がある場合は、<xref:System.Activities.Statements.DoWhile> アクティビティを代わりに使用します。

## <a name="while-properties-in-workflow-designer"></a>ワークフロー デザイナーでの While のプロパティ

次の表に、最も役に立つ <xref:System.Activities.Statements.While> アクティビティのプロパティと、デザイナーでのその使用方法を示します。

|プロパティ名|必須|使用|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|False|ヘッダーの <xref:System.Activities.Statements.While> アクティビティ デザイナーの表示名を指定します。 既定値は While です。 この値は、[ **プロパティ** ] ウィンドウで編集することも、アクティビティデザイナーのヘッダーで直接編集することもできます。<br /><br /> <xref:System.Activities.Activity.DisplayName%2A> は必須ではありませんが、使用することをお勧めします。|
|<xref:System.Activities.Statements.While.Body%2A>|False|が true と評価されたときに実行するアクティビティを格納し <xref:System.Activities.Statements.While.Condition%2A> ます。 |
|<xref:System.Activities.Statements.While.Condition%2A>|True|内のアクティビティを実行するかどうかを判断するために評価される Visual Basic 式を格納し <xref:System.Activities.Statements.While.Body%2A> ます。|

## <a name="see-also"></a>関連項目

- [制御フロー](../workflow-designer/control-flow-activity-designers.md)
- [DoWhile](../workflow-designer/dowhile-activity-designer.md)
