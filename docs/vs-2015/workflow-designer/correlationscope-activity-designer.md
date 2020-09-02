---
title: CorrelationScope アクティビティデザイナー |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.ServiceModel.Activities.CorrelationScope.UI
ms.assetid: 75f20664-9042-464d-8e2b-148d365a2286
caps.latest.revision: 6
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: b6ffcfd63d60ab6f085b5cb2a793e8bf17a50d8e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72656912"
---
# <a name="correlationscope-activity-designer"></a>CorrelationScope アクティビティ デザイナー
**Correlationscope**アクティビティデザイナーは、 <xref:System.ServiceModel.Activities.CorrelationScope> オブジェクトを使用して、子メッセージングアクティビティを暗黙的に管理するアクティビティを作成および構成するために使用し <xref:System.ServiceModel.Activities.CorrelationHandle> ます。

## <a name="the-correlationscope-activity"></a>CorrelationScope アクティビティ
 <xref:System.ServiceModel.Activities.CorrelationScope.CorrelatesWith%2A> プロパティでは、子メッセージング アクティビティの管理に使用する <xref:System.ServiceModel.Activities.CorrelationHandle> を指定します。 <xref:System.ServiceModel.Activities.Send> に含まれる <xref:System.ServiceModel.Activities.Receive> アクティビティおよび <xref:System.ServiceModel.Activities.CorrelationScope.Body%2A> アクティビティは、親 <xref:System.ServiceModel.Activities.CorrelationScope.CorrelatesWith%2A> アクティビティの <xref:System.ServiceModel.Activities.CorrelationScope> プロパティを使用して関連付けを行うように構成されます。

### <a name="using-the-correlationscope-activity-designer"></a>CorrelationScope アクティビティ デザイナーの使用
 **Correlationscope**アクティビティデザイナーは、[**ツールボックス**] の [**メッセージング**] カテゴリにあります。これにアクセスするには、の左側にある [**ツールボックス**] タブをクリックします [!INCLUDE[wfd2](../includes/wfd2-md.md)] (または、[**表示**] メニューの [**ツールバー** ] を選択するか、CTRL + ALT + X キーを押します)。

 **Correlationscope**アクティビティデザイナーは、[**ツールボックス**] からドラッグして、画面にドロップでき [!INCLUDE[wfd2](../includes/wfd2-md.md)] ます。 これ <xref:System.ServiceModel.Activities.CorrelationScope> により、CorrelationScope という既定の **DisplayName** を持つアクティビティが作成されます。 は、 <xref:System.Activities.Activity.DisplayName%2A> **correlationscope**アクティビティデザイナーのヘッダー、または [**プロパティ**] ウィンドウの [ **DisplayName** ] ボックスで編集できます。

 <xref:System.ServiceModel.Activities.CorrelationHandle>子メッセージングアクティビティによって使用されるを指定するには、[**プロパティ**] ウィンドウの [ **CorrelatesWith** ] フィールドの横にある省略記号ボタンをクリックして、[**式エディター** ] ダイアログボックスを表示します。 このプロパティは、アクティビティ デザイナー画面で設定することもできます。

 関連付けに含まれるアクティビティは、 **Correlationscope**デザイナー内の [**本文**] ボックス内のデザイナーを削除することによって指定します。

### <a name="the-correlationscope-properties"></a>CorrelationScope プロパティ
 次の表に、<xref:System.ServiceModel.Activities.CorrelationScope> のプロパティと、デザイナーでのその使用方法を示します。 これらのプロパティは、[ **プロパティ** ] ウィンドウまたは [!INCLUDE[wfd2](../includes/wfd2-md.md)] デザイナー画面で編集でき、多くの場合、両方で編集できます。

|プロパティ名|必須|使用|
|-------------------|--------------|-----------|
|<xref:System.Activities.Activity.DisplayName%2A>|×|<xref:System.ServiceModel.Activities.InitializeCorrelation> アクティビティの省略可能な表示名。|
|<xref:System.ServiceModel.Activities.CorrelationScope.CorrelatesWith%2A>|×|子メッセージング アクティビティの管理に使用する <xref:System.ServiceModel.Activities.CorrelationHandle> を指定します。 このプロパティを設定しない場合は、<xref:System.ServiceModel.Activities.CorrelationScope> に、暗黙の <xref:System.ServiceModel.Activities.CorrelationHandle> が自動的に作成されます。|
|<xref:System.ServiceModel.Activities.CorrelationScope.Body%2A>|×|相関関係のスコープ内のアクティビティを指定します。|

## <a name="see-also"></a>参照
 [InitializeCorrelation](../workflow-designer/initializecorrelation-activity-designer.md) [Receive](../workflow-designer/receive-activity-designer.md) [receiveandsendreply](../workflow-designer/receiveandsendreply-template-designer.md) [Send](../workflow-designer/send-activity-designer.md) [sendandreceivereply](../workflow-designer/sendandreceivereply-template-designer.md) [TransactedReceiveScope](../workflow-designer/transactedreceivescope-activity-designer.md)