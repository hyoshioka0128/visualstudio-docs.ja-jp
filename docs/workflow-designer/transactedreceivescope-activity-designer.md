---
title: ワークフローデザイナー TransactedReceiveScope アクティビティデザイナー
description: TransactedReceiveScope デザイナーを使用して TransactedReceiveScope アクティビティを作成および構成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.ServiceModel.Activities.TransactedReceiveScope.UI
ms.assetid: 7ca93aad-4e83-4d81-90f4-998ee114d9b6
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 70117ab8b27a23dfb2836800c41ff0844fb8de1c
ms.sourcegitcommit: ed26b6e313b766c4d92764c303954e2385c6693e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/10/2020
ms.locfileid: "94433779"
---
# <a name="transactedreceivescope-activity-designer"></a>TransactedReceiveScope アクティビティ デザイナー

**TransactedReceiveScope** デザイナーは、アクティビティを作成および構成するために使用され <xref:System.ServiceModel.Activities.TransactedReceiveScope> ます。

## <a name="the-transactedreceivescope-activity"></a>TransactedReceiveScope アクティビティ

<xref:System.ServiceModel.Activities.TransactedReceiveScope> アクティビティを使用すると、ワークフローまたはディスパッチャーによって作成されたサーバー トランザクションにトランザクションをフローできます。

### <a name="using-the-transactedreceivescope-activity-designer"></a>TransactedReceiveScope アクティビティ デザイナーの使用

**ツールボックス** の [ **メッセージング** ] カテゴリの **TransactedReceiveScope** アクティビティデザイナーにアクセスします。 **TransactedReceiveScope** アクティビティデザイナーは、[ **ツールボックス** ] からドラッグして、アクティビティを通常配置している任意の場所のワークフローデザイナー画面にドロップできます。 これ <xref:System.ServiceModel.Activities.TransactedReceiveScope> により、TransactedReceiveScope という既定の **DisplayName** を持つアクティビティが作成されます。 は、 <xref:System.Activities.Activity.DisplayName%2A> **TransactedReceiveScope** アクティビティデザイナーのヘッダー、またはプロパティグリッドの [ **DisplayName** ] ボックスで編集できます。

**TransactedReceiveScope** デザイナーには、[ **要求** ] ボックスと [ **本文** ] ボックスがあります。 これらは、<xref:System.ServiceModel.Activities.TransactedReceiveScope.Request%2A> プロパティを構成するために使用します。このプロパティでは、<xref:System.ServiceModel.Activities.Receive> アクティビティと、他の <xref:System.ServiceModel.Activities.TransactedReceiveScope.Body%2A> を指定する <xref:System.Activities.Activity> プロパティを指定します。 <xref:System.ServiceModel.Activities.TransactedReceiveScope.Request%2A> によって、トランザクションが作成されます。 その後、トランザクションはこのスコープのアンビエント トランザクションになり、<xref:System.ServiceModel.Activities.TransactedReceiveScope.Body%2A> のスコープ内のあらゆるアクティビティは、このトランザクション内で実行されます。

### <a name="the-transactedreceivescope-properties"></a>TransactedReceiveScope のプロパティ

次の表に、<xref:System.ServiceModel.Activities.TransactedReceiveScope> のプロパティと、デザイナーでのその使用方法を示します。 これらのプロパティは、 <xref:System.Activities.Activity.DisplayName%2A> プロパティグリッドまたはワークフローデザイナー画面で編集できますが、他のプロパティはデザインサーフェイスで編集する必要があります。

|プロパティ名|必須|使用法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|×|<xref:System.ServiceModel.Activities.TransactedReceiveScope> アクティビティの省略可能な表示名。 既定値は、TransactedReceiveScope です。<br /><br /> <xref:System.Activities.Activity.DisplayName%2A> 名は必須ではありませんが、使用することをお勧めします。|
|<xref:System.ServiceModel.Activities.TransactedReceiveScope.Request%2A>|○|アクティビティ <xref:System.ServiceModel.Activities.Receive> デザイナー画面の **要求** ブロックにアクティビティをドロップします。|
|<xref:System.ServiceModel.Activities.TransactedReceiveScope.Body%2A>|×|を <xref:System.Activities.Activity> アクティビティデザイナー画面の **Body** ブロックにドロップします。|

## <a name="see-also"></a>関連項目

- [CorrelationScope](../workflow-designer/correlationscope-activity-designer.md)
- [InitializeCorrelation](../workflow-designer/initializecorrelation-activity-designer.md)
- [受け取れ](../workflow-designer/receive-activity-designer.md)
- [ReceiveAndSendReply](../workflow-designer/receiveandsendreply-template-designer.md)
- [Send](../workflow-designer/send-activity-designer.md)
- [SendAndReceiveReply](../workflow-designer/sendandreceivereply-template-designer.md)