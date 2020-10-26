---
title: シーケンシャルワークフロービュー (レガシ) |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
helpviewer_keywords:
- sequential workflow views
- sequential workflows, views
ms.assetid: 135f24b9-1b37-442b-9ef8-f0f2108a3212
caps.latest.revision: 7
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 76d357c1f6ebc770d0e625e60bae237e37e0a6aa
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "75846216"
---
# <a name="sequential-workflow-views-legacy"></a>シーケンシャル ワークフロー ビュー (レガシ)
[!INCLUDE[vs2010](../includes/vs2010-md.md)][!INCLUDE[wfd1](../includes/wfd1-md.md)]またはを対象とするために使用できる従来のを提供し [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)] ます。

 [!INCLUDE[wfd2](../includes/wfd2-md.md)] では、使い慣れた [!INCLUDE[wf](../includes/wf-md.md)] ユーザー インターフェイスを使用して [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] アプリケーションをグラフィカルに作成できます。 [!INCLUDE[wf](../includes/wf-md.md)] アプリケーションは、アクティビティと呼ばれるワークフロー プロセス ステップで構成されます。 ワークフローを作成するには、それぞれのアクティビティデザイナーを [ **ツールボックス** ] からデザインサーフェイスにドラッグして、デザイン画面でアクティビティを作成します。

 シーケンシャルワークフロー ( [(sequentialworkflowactivity)](https://msdn2.microsoft.com/library/system.workflow.activities.sequentialworkflowactivity.aspx)) を作成すると、ワークフローの3つのビューを使用できるようになります。 これらのビューには、[ **ワークフロー** ] メニューおよびデザインサーフェイスのコンテキストメニューからアクセスできます。

 各ビューの名前と説明の一覧を次の表に示します。

|メニュー/タブ オプション|説明|
|----------------------|-----------------|
|**View SequentialWorkflow**|デザインサーフェイスを右クリックし、コンテキストメニューの [ **SequentialWorkflow の表示** ] オプションを選択して **、シーケンシャルワークフロービューを** 表示します。このビューには、シーケンシャルワークフローのアクティビティベースのグラフィック表現が表示されます。 または、[**ワークフロー** ] メニューの [ **SequentialWorkflow の表示**] を選択します。|
|**キャンセル ハンドラーの表示**|デザインサーフェイスを右クリックし、コンテキストメニューの **[キャンセルハンドラーの表示** ] オプションを選択すると、 **シーケンシャルワークフロー** ビューが表示されます。このビューには、ワークフローに関連付けられている [CancellationHandlerActivity](https://msdn2.microsoft.com/library/system.workflow.componentmodel.cancellationhandleractivity.aspx) アクティビティが表示されます。 または、[**ワークフロー** ] メニューの [**キャンセルハンドラーの表示**] をクリックします。|
|**エラー ハンドラーの表示**|デザインサーフェイスを右クリックし、コンテキストメニューの [ **エラーハンドラーの表示** ] オプションを選択すると、 **エラー** ビューが表示されます。このビューには、ワークフローに関連付けられている [FaultHandlersActivity](https://msdn2.microsoft.com/library/system.workflow.componentmodel.faulthandlersactivity.aspx) アクティビティが表示されます。 または、[**ワークフロー** ] メニューの [**エラーハンドラーの表示**] をクリックします。|

 類似ビューの詳細については、「 [アクティビティビュー (レガシ)](../workflow-designer/activity-views-legacy.md)」を参照してください。

## <a name="see-also"></a>参照
 [アクティビティビュー (レガシ)](../workflow-designer/activity-views-legacy.md) [従来のワークフロープロジェクトの作成](../workflow-designer/creating-legacy-workflow-projects.md)[ワークフロー作成モード](https://msdn2.microsoft.com/library/bb628440.aspx)
