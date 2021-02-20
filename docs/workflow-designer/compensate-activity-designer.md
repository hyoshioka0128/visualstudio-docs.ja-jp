---
title: ワークフローデザイナー-Compensate アクティビティデザイナー
description: Compensate アクティビティデザイナーについて、および compensate アクティビティデザイナーを使用して補正アクティビティを作成および構成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Compensate.UI
ms.assetid: 7347c947-bfff-4bad-becd-5cd23e7b24cd
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 36ab20854adb952d098f71904cdd3cb092e27ac9
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99955685"
---
# <a name="compensate-activity-designer"></a>Compensate アクティビティ デザイナー

**Compensate** アクティビティデザイナーは、アクティビティを作成および構成するために使用され <xref:System.Activities.Statements.Compensate> ます。

## <a name="the-compensate-activity"></a>Compensate アクティビティ

<xref:System.Activities.Statements.Compensate> アクティビティは、<xref:System.Activities.Statements.CompensableActivity.CompensationHandler%2A> に含まれているアクティビティの <xref:System.Activities.Statements.CompensableActivity> を明示的に呼び出します。 <xref:System.Activities.Statements.Compensate> アクティビティが <xref:System.Activities.Statements.CompensableActivity.CancellationHandler%2A> の <xref:System.Activities.Statements.CompensableActivity.CompensationHandler%2A> 内、<xref:System.Activities.Statements.CompensableActivity.ConfirmationHandler%2A> 内、および <xref:System.Activities.Statements.CompensableActivity> 内のいずれでも使用されていない場合は、<xref:System.Activities.Statements.Compensate.Target%2A> プロパティを指定する必要があります。

<xref:System.Activities.Statements.CompensationToken> で指定された <xref:System.Activities.Statements.Compensate.Target%2A> は、<xref:System.Activities.Statements.CompensableActivity> の <xref:System.Activities.Statements.CompensableActivity.Body%2A> が正常に完了した後に <xref:System.Activities.Statements.CompensableActivity> を明示的に確認または補正する手段を提供します。

### <a name="using-the-compensate-activity-designer"></a>Compensate アクティビティ デザイナーの使用

**Compensate** アクティビティデザイナーは、**ツールボックス** の [**トランザクション**] カテゴリにあります。 **ツールボックス** を開くには、ワークフローデザイナーの左側にある [**ツールボックス**] タブを選択します。 または、[**表示**] メニューの [**ツールボックス**] を選択するか、 **Ctrl** + **Alt** + **X** キーを押します。

**Compensate** アクティビティデザイナーは、[**ツールボックス**] からドラッグして、アクティビティが配置されている任意の場所 (内など) にワークフローデザイナー画面にドロップできます <xref:System.Activities.Statements.Sequence> 。 アクティビティデザイナーを削除する <xref:System.Activities.Statements.Compensate> と、補正の既定のを持つアクティビティが作成さ <xref:System.Activities.Activity.DisplayName%2A> れます。 この <xref:System.Activities.Activity.DisplayName%2A> 値は、 **補正** アクティビティデザイナーのヘッダー、またはプロパティグリッドの [ **DisplayName** ] ボックスで編集できます。

### <a name="the-compensate-properties"></a>Compensate のプロパティ

次の表に、<xref:System.Activities.Statements.CancellationScope> のプロパティと、デザイナーでのその使用方法を示します。 プロパティは、 <xref:System.Activities.Activity.DisplayName%2A> プロパティグリッドまたはワークフローデザイナー画面で編集できます。 <xref:System.Activities.Statements.Compensate.Target%2A>プロパティグリッドでプロパティを編集します。

|プロパティ名|必須|使用|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|False|<xref:System.Activities.Statements.Compensate> アクティビティの表示名を指定します (省略可能)。 既定値は Compensate です。|
|<xref:System.Activities.Statements.Compensate.Target%2A>|True|この <xref:System.Activities.InArgument%601> アクティビティの <xref:System.Activities.Statements.CompensationToken> を含む <xref:System.Activities.Statements.Compensate> を指定します。|

## <a name="see-also"></a>関連項目

- [トランザクション](../workflow-designer/transaction-activity-designers.md)
- [CompensableActivity](../workflow-designer/compensableactivity-activity-designer.md)
- [Compensate アクティビティ デザイナー](../workflow-designer/compensate-activity-designer.md)
- [Confirm](../workflow-designer/confirm-activity-designer.md)
- [TransactionScope](../workflow-designer/transactionscope-activity-designer.md)