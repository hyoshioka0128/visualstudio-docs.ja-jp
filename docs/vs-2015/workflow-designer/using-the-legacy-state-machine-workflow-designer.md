---
title: 従来のステートマシンワークフローデザイナーを使用する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
helpviewer_keywords:
- StateFinalizationActivity activity
- StateActivity activity
- SetStateActivity activity
- EventDrivenActivity activity
- state machine workflow designer
- state machine workflows, designer
- state machine workflows, activities
- StateInitializationActivity activity
ms.assetid: 2cd21123-35c2-4eaf-82f6-86fce7a8f04d
caps.latest.revision: 5
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 77bb2c7abb49dbf6fe973ebc80f8340000e4afbd
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/10/2020
ms.locfileid: "75846002"
---
# <a name="using-the-legacy-state-machine-workflow-designer"></a>従来のステート マシン ワークフロー デザイナーの使用
[!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] または [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)]を対象とする [!INCLUDE[vs2010](../includes/vs2010-md.md)] で新しいステートマシンワークフロープロジェクトを作成する場合は、**ステートマシンワークフローコンソールアプリケーション**または**ステートマシンワークフローライブラリ**レガシプロジェクトテンプレートのどちらを使用するかを選択できます。 これらのいずれかのステート マシン プロジェクト テンプレートを選択した場合、ステート マシン デザイナーが従来のワークフロー デザイナーのユーザー インターフェイスとして表示されます。 従来のステートマシンプロジェクトテンプレートの詳細については、「[方法: ステートマシンワークフローコンソールアプリケーションを作成する (レガシ)](../workflow-designer/how-to-create-state-machine-workflow-console-applications-legacy.md) 」および「[方法: ステートマシンワークフローライブラリを作成する (レガシ)](../workflow-designer/how-to-create-a-state-machine-workflow-library-legacy.md)」を参照してください。

 ステート マシン ワークフローは、ステート (状態) のセットで構成されます。 1 つのステートが初期状態として設定されます。 各ステートは特定のイベント セットを受信できます。 イベントに基づいて、別のステートへの移行を実行できます。 ステート マシン ワークフローには最終ステートを定義できます。 最終ステートに移行すると、ワークフローは完了します。

## <a name="state-machine-designer-views"></a>ステート マシン デザイナーのビュー
 ステート マシン デザイナーは自由度の高いデザイナーです。デザイン サーフェイス上でアクティビティを自由に移動することができます。 ステートマシンデザイナーには、*状態*ビューと*イベントドリブン*ビューの2つのビューがあります。

 ステート ビューには、ステート アクティビティ、およびステート アクティビティ内に格納されているイベントドリブン アクティビティが表示されます。 このビューでは、1 つのステートから別のステートへの移行が、1 つのステート内のイベントドリブン アクティビティから別のステートに伸びる線として表されます。 また、独自の線を描くことにより、移行を作成することもできます。 移行を描くには、イベントドリブン アクティビティを選択し、アクティビティ上のいずれかのハンドルを選択して、それをドラッグします。 この操作によって、線が描画されます。 次に、この線が移行先のステートに接続されて、2 つのステート間の移行を表します。

 イベントドリブン ビューにアクセスするには、いずれかのイベントドリブン アクティビティをダブルクリックします。 シーケンシャル ワークフロー デザイナーに似たデザイナーが表示されます。 デザイナー上部のナビゲーション バーには、表示されるイベントドリブン アクティビティまでのアクティビティ階層が示されます。 表示されている階層内のいずれかの要素をクリックすると、元のステート ビューに移動できます。 ステート ビューで 1 つのステートから別のステートへの移行を描画した後、そのアクティビティのイベントドリブン ビューを表示する場合は、設定済みのステート アクティビティがイベントドリブン アクティビティに自動的に追加されます。 設定済みのステート アクティビティのプロパティを変更すると、その変更が元のステート ビューに反映されます。

## <a name="state-machine-workflow-activities"></a>ステート マシン ワークフローのアクティビティ
 ステート マシン ワークフロー デザイナーで使用される主なアクティビティを次の表で説明します。

|ツールボックス名|[利用状況]|説明|
|------------------|--------------|-----------------|
|**状態**|[StateActivity](https://msdn2.microsoft.com/library/system.workflow.activities.stateactivity.aspx)|ステートマシンの状態を表します。追加の**Stateactivity**アクティビティを含めることができます。 詳細については、「 [Stateactivity アクティビティの使用](https://msdn2.microsoft.com/library/bb628612.aspx)」を参照してください。|
|**SetState**|[SetStateActivity](https://msdn2.microsoft.com/library/system.workflow.activities.setstateactivity.aspx)|新しいステート (状態) への移行を指定します。 詳細については、「 [SetStateActivity アクティビティの使用](https://msdn2.microsoft.com/library/bb628469.aspx)」を参照してください。|
|**StateInitialization**|[StateInitializationActivity](https://msdn2.microsoft.com/library/system.workflow.activities.stateinitializationactivity.aspx)|あるステートに移行する (他のアクティビティも同時に指定可) と実行されます。 詳細については、「 [StateInitialization アクティビティの使用](https://msdn2.microsoft.com/library/bb675253.aspx)」を参照してください。|
|**StateFinalization**|[StateFinalizationActivity](https://msdn2.microsoft.com/library/system.workflow.activities.statefinalizationactivity.aspx)|[Stateactivity](https://msdn2.microsoft.com/library/system.workflow.activities.stateactivity.aspx)アクティビティを終了するときに、含まれているアクティビティを実行します。 詳細については、「 [StateFinalizationActivity アクティビティの使用](https://msdn2.microsoft.com/library/bb675278.aspx)」を参照してください。|
|**EventDriven**|[EventDrivenActivity](https://msdn2.microsoft.com/library/system.workflow.activities.eventdrivenactivity.aspx)|外部イベントによって実行開始されるステートに使用されます。 **EventDrivenActivity**アクティビティは、 [ieventactivity](https://msdn2.microsoft.com/library/system.workflow.activities.ieventactivity.aspx)インターフェイスを実装するアクティビティを、最初の子アクティビティとして持つ必要があります。 詳細については、「 [EventDrivenActivity アクティビティの使用](https://msdn2.microsoft.com/library/bb628466.aspx)」を参照してください。|

 ステートマシンワークフローの主要なコンポーネントは、 [stateactivity](https://msdn2.microsoft.com/library/system.workflow.activities.stateactivity.aspx)アクティビティです。 ステート マシン ワークフロー内のさまざまなポイントでイベントがキャプチャされると、イベントに関連したタスクを処理するさまざまなステートに移行します。 有効期間中、ワークフローはいくつかの異なるステート間を遷移します。 これらの状態は、 [Setstateactivity](https://msdn2.microsoft.com/library/system.workflow.activities.setstateactivity.aspx)アクティビティを使用して相互に接続します。

 新しい**Stateactivity**をワークフローデザインサーフェイスにドラッグすると、 [EventDrivenActivity](https://msdn2.microsoft.com/library/system.workflow.activities.eventdrivenactivity.aspx)、 [StateInitializationActivity](https://msdn2.microsoft.com/library/system.workflow.activities.stateinitializationactivity.aspx)、 [statefinalizationactivity](https://msdn2.microsoft.com/library/system.workflow.activities.statefinalizationactivity.aspx)、またはその他の**stateactivity**アクティビティを子アクティビティとして追加できます。

> [!CAUTION]
> ステートマシンワークフローデザイナーを使用してワークフローを作成する場合は、 **[ドキュメントアウトライン]** ビューウィンドウでデザイン中のワークフローの構造を監視する必要があります。 **[ドキュメントアウトライン]** ビューウィンドウのステートマシンワークフローの構造のビューには、ワークフローマークアップファイル内のアクティビティの論理的なレイアウトが反映されます。 デザイン サーフェイスに表示されるワークフロー アクティビティの物理的レイアウトは、ワークフロー マークアップ ファイル内のアクティビティの論理的レイアウトを表さない可能性があります。
>
> **[ドキュメントアウトライン]** ウィンドウを開くには、 **[表示]** メニューの **[その他のウィンドウ]** をポイントし、 **[ドキュメントアウトライン]** を選択します。

## <a name="see-also"></a>参照
 [方法: ステートマシンワークフローコンソールアプリケーションを作成する (レガシ)](../workflow-designer/how-to-create-state-machine-workflow-console-applications-legacy.md) [方法: ステートマシンワークフローライブラリ (レガシ)](../workflow-designer/how-to-create-a-state-machine-workflow-library-legacy.md) [ステートマシン](https://msdn2.microsoft.com/library/bb628601.aspx)ワークフローを作成する[Stateactivity アクティビティ](https://msdn2.microsoft.com/library/bb628612.aspx)を使用して[StateInitializationActivity アクティビティ](https://msdn2.microsoft.com/library/bb675253.aspx)を使用する[Statefinalizationactivity アクティビティ](https://msdn2.microsoft.com/library/bb675278.aspx)を使用する[EventDrivenActivity アクティビティ](https://msdn2.microsoft.com/library/bb628466.aspx)を使用した[setstateactivity](https://msdn2.microsoft.com/library/bb628469.aspx)アクティビティの使用
