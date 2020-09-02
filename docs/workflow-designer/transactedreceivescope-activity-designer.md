---
title: ワークフローデザイナー TransactedReceiveScope アクティビティデザイナー
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
ms.openlocfilehash: 75fb1da392bce7dbd0cd7849d83b3b452521e0c7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "86875931"
---
# <a name="transactedreceivescope-activity-designer"></a>TransactedReceiveScope アクティビティ デザイナー

**TransactedReceiveScope**デザイナーは、アクティビティを作成および構成するために使用され <xref:System.ServiceModel.Activities.TransactedReceiveScope> ます。

## <a name="the-transactedreceivescope-activity"></a>TransactedReceiveScope アクティビティ

<xref:System.ServiceModel.Activities.TransactedReceiveScope> アクティビティを使用すると、ワークフローまたはディスパッチャーによって作成されたサーバー トランザクションにトランザクションをフローできます。

### <a name="using-the-transactedreceivescope-activity-designer"></a>TransactedReceiveScope アクティビティ デザイナーの使用

**ツールボックス**の [**メッセージング**] カテゴリの**TransactedReceiveScope**アクティビティデザイナーにアクセスします。 **TransactedReceiveScope**アクティビティデザイナーは、[**ツールボックス**] からドラッグして、アクティビティを通常配置している任意の場所のワークフローデザイナー画面にドロップできます。 これ <xref:System.ServiceModel.Activities.TransactedReceiveScope> により、TransactedReceiveScope という既定の **DisplayName** を持つアクティビティが作成されます。 は、 <xref:System.Activities.Activity.DisplayName%2A> **TransactedReceiveScope** アクティビティデザイナーのヘッダー、またはプロパティグリッドの [ **DisplayName** ] ボックスで編集できます。

**TransactedReceiveScope**デザイナーには、[**要求**] ボックスと [**本文**] ボックスがあります。 これらは、<xref:System.ServiceModel.Activities.TransactedReceiveScope.Request%2A> プロパティを構成するために使用します。このプロパティでは、<xref:System.ServiceModel.Activities.Receive> アクティビティと、他の <xref:System.ServiceModel.Activities.TransactedReceiveScope.Body%2A> を指定する <xref:System.Activities.Activity> プロパティを指定します。 <xref:System.ServiceModel.Activities.TransactedReceiveScope.Request%2A> によって、トランザクションが作成されます。 その後、トランザクションはこのスコープのアンビエント トランザクションになり、<xref:System.ServiceModel.Activities.TransactedReceiveScope.Body%2A> のスコープ内のあらゆるアクティビティは、このトランザクション内で実行されます。

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
- [送信](../workflow-designer/send-activity-designer.md)
- [SendAndReceiveReply](../workflow-designer/sendandreceivereply-template-designer.md)