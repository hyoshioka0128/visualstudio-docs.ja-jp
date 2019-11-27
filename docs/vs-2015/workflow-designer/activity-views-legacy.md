---
title: アクティビティビュー (レガシ) |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
helpviewer_keywords:
- activities, activity views
- views, activity
- activity views
ms.assetid: 83dc68cd-2cb2-45c2-9a6e-10d82053171a
caps.latest.revision: 5
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 9b65a46d5d0061eeaf3ad707affea1423e5fca5d
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74297540"
---
# <a name="activity-views-legacy"></a>アクティビティ ビュー (レガシ)
[!INCLUDE[wf](../includes/wf-md.md)] が提供するアクティビティの多くには、従来の [!INCLUDE[wfd1](../includes/wfd1-md.md)]で使用できるデザイン ビューが複数あります。ワークフローは、これらのアクティビティを使用して作成されます。 アクティビティデザイナーを**ツールボックス**からデザインサーフェイスにドラッグした後、アクティビティを選択するたびに、 **[ワークフロー]** メニューを使用するか、選択したアクティビティを右クリックして、さまざまなデザインビューを切り替えることができます。 さらに、選択したアクティビティの名前の上にポインタを移動すると、ドロップダウン タブのセットが表示され、これを使ってさまざまなビューに切り替えることができます。

 すべてのアクティビティには少なくとも1つのビューがあります。これは、アクティビティデザイナーを **[ツールボックス]** からデザインサーフェイスにドラッグしたときに表示される既定のビューです。 このアクティビティの既定のビューは、メニューとタブの **[表示] [アクティビティの種類]** オプションとして使用できます。たとえば、 **[並列の表示]** を選択します。 ほとんどのアクティビティには他にもビューがあり、ビューの種類はアクティビティによってさまざまに異なります。 たとえば、 [TransactionScopeActivity](https://go.microsoft.com/fwlink?LinkID=65093)アクティビティには補正ビューがあり、 [EventHandlingScopeActivity](https://go.microsoft.com/fwlink?LinkID=65030)アクティビティにはイベントビューがあります。 Windows Workflow Foundation に付属するアクティビティの多くには、**ビューキャンセルハンドラー**とビュー**フォールト**デザインビューがあり、関連付けられている[CancellationHandlerActivity](https://go.microsoft.com/fwlink?LinkID=65050)と[FaultHandlersActivity](https://go.microsoft.com/fwlink?LinkID=65055)が表示されます。

 各ビューの名前と説明の一覧を次の表に示します。

|メニュー/タブ オプション|説明|
|----------------------|-----------------|
|**表示 [アクティビティの種類]**|このメニュー オプションまたはタブ オプションをクリックすると、選択したアクティビティの既定のビューがグラフィック表示されます。|
|**キャンセルハンドラーの表示**|このメニューまたはタブのオプションビューを選択すると、選択したアクティビティに関連付けられている[CancellationHandlerActivity](https://go.microsoft.com/fwlink?LinkID=65050)が表示されます。|
|**エラーハンドラーの表示**|このメニューまたはタブのオプションビューを選択すると、選択したアクティビティに関連付けられている[FaultHandlersActivity](https://go.microsoft.com/fwlink?LinkID=65055)が表示されます。|
|**補正ハンドラーの表示**|このメニューまたはタブのオプションビューを選択すると、選択した[TransactionScopeActivity](https://go.microsoft.com/fwlink?LinkID=65093)に関連付けられている[CompensationHandlerActivity](https://go.microsoft.com/fwlink?LinkID=65053)が表示されます。|
|**イベントハンドラーの表示**|このメニューまたはタブのオプションビューを選択すると、選択した[EventHandlingScopeActivity](https://go.microsoft.com/fwlink?LinkID=65030)に関連付けられている[EventHandlersActivity](https://go.microsoft.com/fwlink?LinkID=65018)が表示されます。|

 類似ビューの詳細については、「[シーケンシャルワークフロービュー (レガシ)](../workflow-designer/sequential-workflow-views-legacy.md)」を参照してください。

## <a name="see-also"></a>関連項目
 [従来のワークフローアクティビティ](../workflow-designer/legacy-workflow-activities.md)[シーケンシャルワークフロービュー (レガシ)](../workflow-designer/sequential-workflow-views-legacy.md)