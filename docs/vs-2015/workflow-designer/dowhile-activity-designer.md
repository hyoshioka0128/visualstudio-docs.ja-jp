---
title: DoWhile アクティビティデザイナー |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Statements.DoWhile.UI
ms.assetid: 948deb35-d72f-462b-bea6-4b119c10a148
caps.latest.revision: 7
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: b63c3e2e0907bcaf13ada4cbb20ce5527a240fe3
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72656766"
---
# <a name="dowhile-activity-designer"></a>DoWhile アクティビティ デザイナー
アクティビティは、 <xref:System.Activities.Statements.DoWhile> <xref:System.Activities.Statements.DoWhile.Body%2A> 指定された条件が **false**と評価されるまで、少なくとも1回に含まれるアクティビティを実行します。 ループの本体に含まれるアクティビティを 0 回以上実行する必要がある場合は、代わりに、<xref:System.Activities.Statements.While> アクティビティを使用します。

## <a name="dowhile-properties-in-the-workflow-designer"></a>ワークフロー デザイナーでの DoWhile のプロパティ
 次の表に、最も役に立つ <xref:System.Activities.Statements.DoWhile> アクティビティのプロパティと、デザイナーでのその使用方法を示します。

|プロパティ名|必須|使用|
|-------------------|--------------|-----------|
|<xref:System.Activities.Statements.DoWhile.Body%2A>|×|条件が **true**のときに実行するアクティビティ。 アクティビティを追加するには <xref:System.Activities.Statements.DoWhile.Body%2A> 、"ここにアクティビティをドロップします" というヒントテキストが表示された**dowhile**アクティビティデザイナーの [ **Body** ] ボックスに、[ツールボックス] からアクティビティをドロップします。|
|<xref:System.Activities.Statements.DoWhile.Condition%2A>|○|ループの各繰り返しの後に評価する条件。 を設定するに <xref:System.Activities.Statements.DoWhile.Condition%2A> は、 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] **dowhile**アクティビティデザイナーまたはプロパティグリッドの [**条件**] ボックスに式を入力します。|

## <a name="see-also"></a>参照
 [While](../workflow-designer/while-activity-designer.md) [制御フロー](../workflow-designer/control-flow-activity-designers.md)中