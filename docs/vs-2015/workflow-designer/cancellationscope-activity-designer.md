---
title: CancellationScope アクティビティデザイナー |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Statements.CancellationScope.UI
ms.assetid: 2c85d663-b219-4142-9866-7693ffd46379
caps.latest.revision: 8
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: fa41d63fa4f67037a8e98e72abc3e338ad894f70
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72659174"
---
# <a name="cancellationscope-activity-designer"></a>CancellationScope アクティビティ デザイナー
**CancellationScope**アクティビティデザイナーは、アクティビティを作成および構成するために使用され <xref:System.Activities.Statements.CancellationScope> ます。

## <a name="the-cancellationscope-activity"></a>CancellationScope アクティビティ
 <xref:System.Activities.Statements.CancellationScope> アクティビティを使用すると、実行のアクティビティと、そのアクティビティの取り消しロジックを指定できます。

### <a name="using-the-cancellationscope-activity-designer"></a>CancellationScope アクティビティ デザイナーの使用
 **CancellationScope**アクティビティデザイナーは、**ツールボックス**の [**トランザクション**] カテゴリにあります。このカテゴリにアクセスするには、の [**ツールボックス**] タブをクリックします [!INCLUDE[wfd2](../includes/wfd2-md.md)] (または、[**表示**] メニューの [**ツールバー** ] を選択するか、CTRL + ALT + X キーを押します)。

 **CancellationScope**アクティビティデザイナーは、[**ツールボックス**] からドラッグして、 [!INCLUDE[wfd2](../includes/wfd2-md.md)] アクティビティを通常配置している画面の任意の場所 (内など) にドロップできます <xref:System.Activities.Statements.Sequence> 。 この操作により、CancellationScope という既定の <xref:System.Activities.Statements.CancellationScope> を持つ <xref:System.Activities.Activity.DisplayName%2A> アクティビティが作成されます。 この <xref:System.Activities.Activity.DisplayName%2A> 値は、 **CancellationScope** アクティビティデザイナーのヘッダー、またはプロパティグリッドの [ **DisplayName** ] ボックスで編集できます。

### <a name="the-cancellationscope-properties"></a>CancellationScope プロパティ
 次の表に、<xref:System.Activities.Statements.CancellationScope> のプロパティと、デザイナーでのその使用方法を示します。 <xref:System.Activities.Activity.DisplayName%2A> プロパティはプロパティ グリッドで編集できますが、それ以外のプロパティは[!INCLUDE[wfd2](../includes/wfd2-md.md)]画面で編集する必要があります。

|プロパティ名|必須|使用|
|-------------------|--------------|-----------|
|<xref:System.Activities.Activity.DisplayName%2A>|×|<xref:System.Activities.Statements.CancellationScope> アクティビティの省略可能な表示名。 既定では、CancellationScope です。 <xref:System.Activities.Activity.DisplayName%2A> 値は必須ではありませんが、使用することをお勧めします。|
|<xref:System.Activities.Statements.CancellationScope.Body%2A>|○|取り消しロジックの対象となるアクティビティを指定します。 アクティビティを追加するには <xref:System.Activities.Statements.CancellationScope.Body%2A> 、"ここにアクティビティをドロップします" というヒントテキストが表示された**CancellationScope**アクティビティデザイナーの [ **Body** ] ボックスに、[**ツールボックス**] からアクティビティをドロップします。|
|<xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A>|○|取り消しの際に実行されるアクティビティを指定します。 アクティビティを追加するには <xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A> 、"ここにアクティビティをドロップします" というヒントテキストが表示された**CancellationScope**アクティビティデザイナーの [ **CancellationHandler** ] ボックスに、[**ツールボックス**] からアクティビティをドロップします。|

## <a name="see-also"></a>参照
 [トランザクション](../workflow-designer/transaction-activity-designers.md) [CompensableActivity](../workflow-designer/compensableactivity-activity-designer.md) [補正](../workflow-designer/compensate-activity-designer.md)の [確認](../workflow-designer/confirm-activity-designer.md) [TransactionScope](../workflow-designer/transactionscope-activity-designer.md)