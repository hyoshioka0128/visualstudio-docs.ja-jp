---
title: ワークフローデザイナー CancellationScope アクティビティデザイナー
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.CancellationScope.UI
ms.assetid: 2c85d663-b219-4142-9866-7693ffd46379
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a6d1067b529dffec5a4e6a1f21d5489c32311c07
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "76112506"
---
# <a name="cancellationscope-activity-designer"></a>CancellationScope アクティビティ デザイナー

**CancellationScope**アクティビティデザイナーは、アクティビティを作成および構成するために使用され <xref:System.Activities.Statements.CancellationScope> ます。

## <a name="the-cancellationscope-activity"></a>CancellationScope アクティビティ

<xref:System.Activities.Statements.CancellationScope> アクティビティを使用すると、実行のアクティビティと、そのアクティビティの取り消しロジックを指定できます。

### <a name="using-the-cancellationscope-activity-designer"></a>CancellationScope アクティビティ デザイナーの使用

**CancellationScope**アクティビティデザイナーは、[**ツールボックス**] の [**トランザクション**] カテゴリにあります。 **ツールボックス**を開くには、ワークフローデザイナーの [**ツールボックス**] タブを選択します。 または、[**表示**] メニューの [**ツールボックス**] を選択するか、 **Ctrl** + **Alt** + **X**キーを押します。

**CancellationScope**アクティビティデザイナーは、[**ツールボックス**] からドラッグして、アクティビティが配置されている任意の場所 (内など) にワークフローデザイナー画面にドロップできます <xref:System.Activities.Statements.Sequence> 。 **CancellationScope**アクティビティデザイナーを削除する <xref:System.Activities.Statements.CancellationScope> と、既定値の CancellationScope を持つアクティビティが作成さ <xref:System.Activities.Activity.DisplayName%2A> れます。 <xref:System.Activities.Activity.DisplayName%2A> **CancellationScope**アクティビティデザイナーのヘッダーの値を編集します。 また、プロパティグリッドの [ **DisplayName** ] ボックスで編集することもできます。

### <a name="the-cancellationscope-properties"></a>CancellationScope プロパティ

次の表に、<xref:System.Activities.Statements.CancellationScope> のプロパティと、デザイナーでのその使用方法を示します。 プロパティは <xref:System.Activities.Activity.DisplayName%2A> プロパティグリッドで編集できますが、その他のプロパティはワークフローデザイナー画面で編集する必要があります。

|プロパティ名|必須|使用法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|×|<xref:System.Activities.Statements.CancellationScope> アクティビティの省略可能な表示名。 既定では、CancellationScope です。 <xref:System.Activities.Activity.DisplayName%2A> 値は必須ではありませんが、使用することをお勧めします。|
|<xref:System.Activities.Statements.CancellationScope.Body%2A>|○|取り消しロジックの対象となるアクティビティを指定します。 アクティビティを追加するには <xref:System.Activities.Statements.CancellationScope.Body%2A> 、 **CancellationScope**アクティビティデザイナーの [ **Body** ] ボックスに、[**ツールボックス**] からアクティビティをドロップします。 "ここにアクティビティをドロップします" というヒントテキストを追加します。|
|<xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A>|○|取り消しが発生した場合に実行されるアクティビティを指定します。 アクティビティを追加するには <xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A> 、 **CancellationScope**アクティビティデザイナーの [ **CancellationHandler** ] ボックスに、[**ツールボックス**] からアクティビティをドロップします。 "ここにアクティビティをドロップします" というヒントテキストを追加します。|

## <a name="see-also"></a>関連項目

- [トランザクション](../workflow-designer/transaction-activity-designers.md)
- [CompensableActivity](../workflow-designer/compensableactivity-activity-designer.md)
- [Compensate](../workflow-designer/compensate-activity-designer.md)
- [確認](../workflow-designer/confirm-activity-designer.md)
- [TransactionScope](../workflow-designer/transactionscope-activity-designer.md)
