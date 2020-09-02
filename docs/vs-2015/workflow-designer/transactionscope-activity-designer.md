---
title: TransactionScope アクティビティデザイナー |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Statements.TransactionScope.UI
ms.assetid: 8d7ebfc6-7478-4888-b3b0-b14f296096af
caps.latest.revision: 8
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: b5a1d38ea37896cedcd2166c42f37ce037a1c4cd
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72670172"
---
# <a name="transactionscope-activity-designer"></a>TransactionScope アクティビティ デザイナー
**TransactionScope**アクティビティデザイナーは、アクティビティを作成および構成するために使用され <xref:System.Activities.Statements.TransactionScope> ます。

## <a name="the-transactionscope-activity"></a>TransactionScope アクティビティ
 <xref:System.Activities.Statements.TransactionScope> アクティビティでは、含まれているアクティビティを単一のトランザクションで実行します。 <xref:System.Activities.Statements.TransactionScope.Body%2A> アクティビティおよびトランザクションの他のすべての参加要素が正常に完了すると、トランザクションはコミットされます。

### <a name="using-the-transactionscope-activity-designer"></a>TransactionScope アクティビティ デザイナーの使用
 **TransactionScope**アクティビティデザイナーは、**ツールボックス**の [**トランザクション**] カテゴリにあります。このカテゴリにアクセスするには、の [**ツールボックス**] タブをクリックします [!INCLUDE[wfd2](../includes/wfd2-md.md)] (または、[**表示**] メニューの [**ツールバー** ] を選択するか、CTRL + ALT + X キーを押します)。

 **TransactionScope**アクティビティデザイナーは、[**ツールボックス**] からドラッグして、 [!INCLUDE[wfd2](../includes/wfd2-md.md)] アクティビティを通常配置している画面の任意の場所 (内など) にドロップできます <xref:System.Activities.Statements.Sequence> 。 この操作により、TransactionScope という既定の <xref:System.Activities.Statements.TransactionScope> を持つ <xref:System.Activities.Activity.DisplayName%2A> アクティビティが作成されます。 この <xref:System.Activities.Activity.DisplayName%2A> 値は、 **TransactionScope** アクティビティデザイナーのヘッダー、またはプロパティグリッドの [ **DisplayName** ] ボックスで編集できます。

### <a name="the-transactionscope-properties"></a>TransactionScope プロパティ
 次の表に、<xref:System.Activities.Statements.TransactionScope> のプロパティと、デザイナーでのその使用方法を示します。 <xref:System.Activities.Activity.DisplayName%2A> プロパティと <xref:System.Activities.Statements.TransactionScope.Body%2A> プロパティは、[!INCLUDE[wfd2](../includes/wfd2-md.md)]画面で編集できます。 ただし、他のプロパティは、プロパティ グリッドで編集する必要があります。

|プロパティ名|必須|使用|
|-------------------|--------------|-----------|
|<xref:System.Activities.Activity.DisplayName%2A>|×|<xref:System.Activities.Statements.TransactionScope> アクティビティの省略可能な表示名。 既定値は、TransactionScope です。 <xref:System.Activities.Activity.DisplayName%2A> 値は必須ではありませんが、使用することをお勧めします。|
|<xref:System.Activities.Statements.TransactionScope.Body%2A>|○|単一のトランザクションで実行するアクティビティを指定します。 アクティビティを追加するには <xref:System.Activities.Statements.TransactionScope.Body%2A> 、"ここにアクティビティをドロップします" というヒントテキストが表示された**TransactionScope**アクティビティデザイナーの [ **Body** ] ボックスに、[**ツールボックス**] からアクティビティをドロップします。|
|<xref:System.Activities.Statements.TransactionScope.IsolationLevel%2A>|○|この <xref:System.Transactions.IsolationLevel> の <xref:System.Activities.Statements.TransactionScope> を指定します。|
|<xref:System.Activities.Statements.TransactionScope.Timeout%2A>|×|トランザクションが完了するまでの時間間隔を "00:00:00" (時:分:秒) という形式で指定します。 既定値は 1 分 (00:01:00) です。|
|<xref:System.Activities.Statements.TransactionScope.AbortInstanceOnTransactionFailure?qualifyHint=False&autoUpgrade=True>|○|トランザクションが中止した場合にワークフローを中止する必要があるかどうかを示す値を指定します。|

## <a name="see-also"></a>参照
 [Transaction](../workflow-designer/transaction-activity-designers.md) [TerminateWorkflow](../workflow-designer/terminateworkflow-activity-designer.md) [CompensableActivity](../workflow-designer/compensableactivity-activity-designer.md) [Compensate](../workflow-designer/compensate-activity-designer.md) [Confirm](../workflow-designer/confirm-activity-designer.md)