---
title: ワークフローデザイナー-DoWhile アクティビティデザイナー
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
ms.openlocfilehash: c56a9ab8b46f8f7ee36875dda507cb9f288136cf
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "86875606"
---
# <a name="dowhile-activity-designer"></a>DoWhile アクティビティ デザイナー

アクティビティは、 <xref:System.Activities.Statements.DoWhile> <xref:System.Activities.Statements.DoWhile.Body%2A> 指定された条件が **false**と評価されるまで、少なくとも1回に含まれるアクティビティを実行します。 ループの本体に含まれるアクティビティを 0 回以上実行する必要がある場合は、代わりに、<xref:System.Activities.Statements.While> アクティビティを使用します。

## <a name="dowhile-properties-in-the-workflow-designer"></a>ワークフロー デザイナーでの DoWhile のプロパティ

次の表に、最も役に立つ <xref:System.Activities.Statements.DoWhile> アクティビティのプロパティと、デザイナーでのそれらの使用方法について説明します。

|プロパティ名|必須|使用法|
|-|--------------|-|
|<xref:System.Activities.Statements.DoWhile.Body%2A>|×|条件が **true**のときに実行するアクティビティ。 アクティビティを追加するには <xref:System.Activities.Statements.DoWhile.Body%2A> 、"ここにアクティビティをドロップします" というヒントテキストが表示された**dowhile**アクティビティデザイナーの [ **Body** ] ボックスに、[ツールボックス] からアクティビティをドロップします。|
|<xref:System.Activities.Statements.DoWhile.Condition%2A>|○|ループの各繰り返しの後に評価する条件。 を設定するには <xref:System.Activities.Statements.DoWhile.Condition%2A> 、 **dowhile**アクティビティデザイナーまたはプロパティグリッドの [**条件**] ボックスに Visual Basic 式を入力します。|

## <a name="see-also"></a>関連項目

- [While](../workflow-designer/while-activity-designer.md)
- [制御フロー](../workflow-designer/control-flow-activity-designers.md)