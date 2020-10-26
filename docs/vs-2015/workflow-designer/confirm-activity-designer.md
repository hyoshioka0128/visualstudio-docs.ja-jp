---
title: Confirm アクティビティデザイナー |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Confirm.UI
ms.assetid: c753b67b-b0e7-462a-bb4e-ba8db04a078d
caps.latest.revision: 5
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: b3835c6cb537e7ac74862ac4a6794dd7b0bd5003
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72656969"
---
# <a name="confirm-activity-designer"></a>Confirm アクティビティ デザイナー
**Confirm**アクティビティデザイナーは、アクティビティを作成および構成するために使用され <xref:System.Activities.Statements.Confirm> ます。

## <a name="the-confirm-activity"></a>Confirm アクティビティ
 <xref:System.Activities.Statements.Confirm> アクティビティは、<xref:System.Activities.Statements.CompensableActivity.ConfirmationHandler%2A> に含まれているアクティビティの <xref:System.Activities.Statements.CompensableActivity> を明示的に呼び出します。 <xref:System.Activities.Statements.Confirm> アクティビティが <xref:System.Activities.Statements.CompensableActivity.CancellationHandler%2A> の <xref:System.Activities.Statements.CompensableActivity.CompensationHandler%2A> 内、<xref:System.Activities.Statements.CompensableActivity.ConfirmationHandler%2A> 内、および <xref:System.Activities.Statements.CompensableActivity> 内のいずれでも使用されていない場合は、<xref:System.Activities.Statements.Confirm.Target%2A> プロパティを指定する必要があります。

 <xref:System.Activities.Statements.CompensationToken> で指定された <xref:System.Activities.Statements.Compensate.Target%2A> は、<xref:System.Activities.Statements.CompensableActivity> の <xref:System.Activities.Statements.CompensableActivity.Body%2A> が正常に完了した後に <xref:System.Activities.Statements.CompensableActivity> を明示的に確認または補正する手段を提供します。

### <a name="using-the-confirm-activity-designer"></a>Confirm アクティビティ デザイナーの使用
 **Confirm**アクティビティデザイナーは、[**ツールボックス**] の [**トランザクション**] カテゴリにあります。このカテゴリにアクセスするには、の左側にある [**ツールボックス**] タブをクリックします [!INCLUDE[wfd2](../includes/wfd2-md.md)] (または、[**表示**] メニューの [**ツールバー** ] を選択するか、CTRL + ALT + X キーを押します)。

 **Confirm**アクティビティデザイナーは、[**ツールボックス**] からドラッグして、 [!INCLUDE[wfd2](../includes/wfd2-md.md)] アクティビティを通常配置している画面の任意の場所 (内など) にドロップできます <xref:System.Activities.Statements.Sequence> 。 この操作により、Confirm という既定の <xref:System.Activities.Statements.Confirm> を持つ <xref:System.Activities.Activity.DisplayName%2A> アクティビティが作成されます。 この <xref:System.Activities.Activity.DisplayName%2A> 値は、 **Confirm** アクティビティデザイナーのヘッダーか、プロパティグリッドの [ **DisplayName** ] ボックスで編集できます。

### <a name="the-confirm-properties"></a>Confirm のプロパティ
 次の表に、<xref:System.Activities.Statements.Confirm> のプロパティと、デザイナーでのその使用方法を示します。 <xref:System.Activities.Activity.DisplayName%2A> プロパティはプロパティ グリッドまたは[!INCLUDE[wfd2](../includes/wfd2-md.md)]画面で編集できますが、<xref:System.Activities.Statements.Confirm.Target%2A> プロパティはプロパティ グリッドで編集する必要があります。

|プロパティ名|必須|使用|
|-------------------|--------------|-----------|
|<xref:System.Activities.Activity.DisplayName%2A>|×|<xref:System.Activities.Statements.CancellationScope> アクティビティの表示名を指定します (省略可能)。 既定値は Confirm です。|
|<xref:System.Activities.Statements.Confirm.Target%2A>|○|この <xref:System.Activities.InArgument%601> アクティビティの <xref:System.Activities.Statements.CompensationToken> を含む <xref:System.Activities.Statements.Confirm> を指定します。|

## <a name="see-also"></a>参照
 [Transaction](../workflow-designer/transaction-activity-designers.md) [CancellationScope](../workflow-designer/cancellationscope-activity-designer.md) [CompensableActivity](../workflow-designer/compensableactivity-activity-designer.md) [Compensate](../workflow-designer/compensate-activity-designer.md) [TransactionScope](../workflow-designer/transactionscope-activity-designer.md)