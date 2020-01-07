---
title: ワークフローデザイナー CompensableActivity アクティビティデザイナー
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.CompensableActivity.UI
ms.assetid: e0340d89-d39e-4a52-8557-13e27040d7b5
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7ec70c22ae195dc6dd58aa2cfa893cee35fe6ca8
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75597101"
---
# <a name="compensableactivity-activity-designer"></a>CompensableActivity アクティビティ デザイナー

**CompensableActivity**アクティビティデザイナーは、<xref:System.Activities.Statements.CompensableActivity> アクティビティを作成および構成するために使用されます。

## <a name="the-compensableactivity-activity"></a>CompensableActivity アクティビティ
 <xref:System.Activities.Statements.CompensableActivity> で、正常に完了した後に確認または補正できる作業単位を定義します。

### <a name="using-the-compensableactivity-activity-designer"></a>CompensableActivity アクティビティ デザイナーの使用
 **CompensableActivity**アクティビティデザイナーは、 **[ツールボックス]** の **[トランザクション]** カテゴリにあります。 **ツールボックス**を開くには、ワークフローデザイナーの左側にある **[ツールボックス]** タブを選択します。 または、 **[表示]** メニューの **[ツールボックス]** を選択するか、 **ctrl**+**Alt**+**X**キーを押します。

 **CompensableActivity**アクティビティデザイナーは、 **[ツールボックス]** からドラッグしてワークフローデザイナー画面にドロップできます。 アクティビティデザイナーは <xref:System.Activities.Statements.Sequence>内にドロップできます。 アクティビティデザイナーを削除すると、既定の <xref:System.Activities.Activity.DisplayName%2A> CompensableActivity の <xref:System.Activities.Statements.CompensableActivity> アクティビティが作成されます。 **CompensableActivity**アクティビティデザイナーのヘッダーで <xref:System.Activities.Activity.DisplayName%2A> 値を編集します。 また、プロパティグリッドの **[DisplayName]** ボックスで編集することもできます。

### <a name="the-compensableactivity-properties"></a>CompensableActivity のプロパティ
 次の表に、<xref:System.Activities.Statements.CompensableActivity> のプロパティと、デザイナーでのその使用方法を示します。 <xref:System.Activities.Activity.DisplayName%2A> および <xref:System.Activities.Activity%601.Result%2A> プロパティはプロパティグリッドで編集できますが、他のプロパティはワークフローデザイナーサーフェイスで編集する必要があります。

|プロパティ名|必須|使用状況|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|[False]|<xref:System.Activities.Statements.CompensableActivity> アクティビティの省略可能な表示名。 既定値は CompensableActivity です。|
|<xref:System.Activities.Activity%601.Result%2A>|[False]|<xref:System.Activities.Statements.CompensableActivity> の戻り値を指定します。 このプロパティは、プロパティ グリッドで編集する必要があります。|
|<xref:System.Activities.Statements.CompensableActivity.Body%2A>|True|補正、取り消し、および確認の各ロジックの提供対象のアクティビティを指定します。 <xref:System.Activities.Statements.CompensableActivity.Body%2A> アクティビティを追加するには、 **CompensableActivity**アクティビティデザイナーの **[Body]** ボックスに、 **[ツールボックス]** からアクティビティをドロップします。 "ここにアクティビティをドロップします" というヒントテキストを追加します。|
|<xref:System.Activities.Statements.CompensableActivity.CancellationHandler%2A>|[False]|取り消しが発生したときに実行されるアクティビティを指定します。 アクティビティを追加するには、**ツールボックス**から**CompensableActivity**アクティビティデザイナーの **[CancellationHandler]** ボックスにデザイナーをドロップします。 "ここにアクティビティをドロップします" というヒントテキストを追加します。|
|<xref:System.Activities.Statements.CompensableActivity.CompensationHandler%2A>|[False]|<xref:System.Activities.Statements.CompensableActivity.Body%2A> アクティビティの補正を行うときに実行されるアクティビティを指定します。 このハンドラーは、<xref:System.Activities.Statements.Compensate> アクティビティを使用して明示的に呼び出すことができます。<br /><br /> アクティビティを追加するには、アクティビティデザイナーを **[ツールボックス]** から**CompensableActivity**アクティビティデザイナーの **[CompensationHandler]** ボックスにドロップします。 "ここにアクティビティをドロップします" というヒントテキストを追加します。|
|<xref:System.Activities.Statements.CompensableActivity.ConfirmationHandler%2A>|[False]|<xref:System.Activities.Statements.CompensableActivity.Body%2A> アクティビティを確認するときに実行されるアクティビティを指定します。 このハンドラーは、<xref:System.Activities.Statements.Confirm> アクティビティを使用して明示的に呼び出すことができます。<br /><br /> アクティビティを追加するには、アクティビティデザイナーを **ツールボックス** から**CompensableActivity**アクティビティデザイナーの  **confirmationhandler**  ボックスにドロップします。 "ここにアクティビティをドロップします" というヒントテキストを追加します。|

## <a name="see-also"></a>関連項目

- [トランザクション](../workflow-designer/transaction-activity-designers.md)
- [CancellationScope](../workflow-designer/cancellationscope-activity-designer.md)
- [Compensate](../workflow-designer/compensate-activity-designer.md)
- [Confirm](../workflow-designer/confirm-activity-designer.md)
- [TransactionScope](../workflow-designer/transactionscope-activity-designer.md)
