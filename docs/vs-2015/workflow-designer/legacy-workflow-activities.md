---
title: 従来のワークフロー活動 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
helpviewer_keywords:
- workflows, activities
- activities
- workflow activities
ms.assetid: 4af7a06b-1e82-43c8-aec8-0dc5fb63d08a
caps.latest.revision: 8
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: fb741afd7488717ba85e68ea7fd982e3e1d5adf8
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/10/2020
ms.locfileid: "75849245"
---
# <a name="legacy-workflow-activities"></a>従来のワークフロー アクティビティ
[!INCLUDE[wf](../includes/wf-md.md)] には、制御フロー、条件、イベント処理、状態管理、およびアプリケーションとサービスとの通信のための機能を提供する既定のアクティビティセットが含まれています。 ワークフローを設計するとき、[!INCLUDE[wfd1](../includes/wfd1-md.md)]に付属しているシステム標準のアクティビティを使用することも、独自のカスタム アクティビティを作成することもできます。

 次の表は、[!INCLUDE[wf2](../includes/wf2-md.md)] フレームワークに付属ですぐに使用できるアクティビティ セットの一覧です。 これらのアクティビティの多くは、すべてではなく、[!INCLUDE[wfd2](../includes/wfd2-md.md)]の**ツールボックス**からアクセスできるアクティビティデザイナーによって表されます。 アクティビティを作成するには、**ツールボックス**からデザイナーをドラッグし、デザインサーフェイスにドロップします。

|[利用状況]|説明|
|--------------|-----------------|
|[CallExternalMethodActivity](https://msdn2.microsoft.com/library/system.workflow.activities.callexternalmethodactivity.aspx)|ローカルサービスとの入出力通信に**HandleExternalEventActivity**アクティビティと共に使用されます。 [CallExternalMethodActivity アクティビティを使用して](https://msdn2.microsoft.com/library/bb628493.aspx)[!INCLUDE[crdefault](../includes/crdefault-md.md)]します。|
|[CancellationHandlerActivity](https://msdn2.microsoft.com/library/system.workflow.componentmodel.cancellationhandleractivity.aspx)|複合アクティビティのすべての子の実行が完了する前に取り消された複合アクティビティのクリーンアップ ロジックを格納するために使用されます。 [CancellationHandlerActivity アクティビティを使用して](https://msdn2.microsoft.com/library/bb628604.aspx)[!INCLUDE[crdefault](../includes/crdefault-md.md)]します。|
|[CodeActivity](https://msdn2.microsoft.com/library/system.workflow.activities.codeactivity.aspx)|Visual Basic または C# のコードをワークフローに追加できます。 [CodeActivity アクティビティを使用して](https://msdn2.microsoft.com/library/bb675249.aspx)[!INCLUDE[crdefault](../includes/crdefault-md.md)]します。|
|[CompensatableSequenceActivity](https://msdn2.microsoft.com/library/system.workflow.activities.compensatablesequenceactivity.aspx)|[Sequenceactivity](https://msdn2.microsoft.com/library/system.workflow.activities.sequenceactivity.aspx)の補正可能バージョン。 [CompensatableSequenceActivity アクティビティを使用して](https://msdn2.microsoft.com/library/bb675224.aspx)[!INCLUDE[crdefault](../includes/crdefault-md.md)]します。|
|[CompensatableTransactionScopeActivity](https://msdn2.microsoft.com/library/system.workflow.componentmodel.compensatabletransactionscopeactivity.aspx)|**TransactionScopeActivity**の補正可能バージョン。 [CompensatableTransactionScopeActivity アクティビティを使用して](https://msdn2.microsoft.com/library/bb628592.aspx)[!INCLUDE[crdefault](../includes/crdefault-md.md)]します。|
|[CompensateActivity](https://msdn2.microsoft.com/library/system.workflow.componentmodel.compensateactivity.aspx)|エラー発生時に、ワークフローによって実行された操作を取り消すか補正するコードを呼び出すことができます。 [CompensateActivity アクティビティを使用して](https://msdn2.microsoft.com/library/bb628608.aspx)[!INCLUDE[crdefault](../includes/crdefault-md.md)]します。|
|[CompensationHandlerActivity](https://msdn2.microsoft.com/library/system.workflow.componentmodel.compensationhandleractivity.aspx)|[CompensationHandlerActivity アクティビティ [!INCLUDE[crdefault](../includes/crdefault-md.md)]使用して](https://msdn2.microsoft.com/library/bb675279.aspx)、完了した TransactionScopeActivity アクティビティに対して補正を実行する1つ以上のアクティビティのラッパー。|
|[ConditionedActivityGroup](https://msdn2.microsoft.com/library/system.workflow.activities.conditionedactivitygroup.aspx)|[Conditionedactivitygroup](https://msdn2.microsoft.com/library/system.workflow.activities.conditionedactivitygroup.aspx)アクティビティ自体に適用される条件に基づいて子アクティビティを実行し、各子に個別に適用される条件に基づいて実行します。 [ConditionedActivityGroup アクティビティを使用して](https://msdn2.microsoft.com/library/bb675237.aspx)[!INCLUDE[crdefault](../includes/crdefault-md.md)]します。|
|[DelayActivity](https://msdn2.microsoft.com/library/system.workflow.activities.delayactivity.aspx)|タイムアウト期間に基づいて、ワークフロー内に遅延を作成できます。 [Delayactivity アクティビティを使用して](https://msdn2.microsoft.com/library/bb628484.aspx)[!INCLUDE[crdefault](../includes/crdefault-md.md)]します。|
|[EventDrivenActivity](https://msdn2.microsoft.com/library/system.workflow.activities.eventdrivenactivity.aspx)|指定されたイベントが発生すると実行される 1 つまたは複数のアクティビティをラップします。 [EventDrivenActivity アクティビティを使用して](https://msdn2.microsoft.com/library/bb628466.aspx)[!INCLUDE[crdefault](../includes/crdefault-md.md)]します。|
|[EventHandlersActivity](https://msdn2.microsoft.com/library/system.workflow.activities.eventhandlersactivity.aspx)|イベントをアクティビティに関連付けるフレームワークを提供します。 [EventHandlersActivity アクティビティを使用して](https://msdn2.microsoft.com/library/bb628537.aspx)[!INCLUDE[crdefault](../includes/crdefault-md.md)]します。|
|[EventHandlingScopeActivity](https://msdn2.microsoft.com/library/system.workflow.activities.eventhandlingscopeactivity.aspx)|[EventHandlersActivity](https://msdn2.microsoft.com/library/system.workflow.activities.eventhandlersactivity.aspx)を使用して、メインの子アクティビティを同時に実行します。 [EventHandlingScopeActivity アクティビティを使用して](https://msdn2.microsoft.com/library/bb628463.aspx)[!INCLUDE[crdefault](../includes/crdefault-md.md)]します。|
|[FaultHandlerActivity](https://msdn2.microsoft.com/library/system.workflow.componentmodel.faulthandleractivity.aspx)|指定した種類の例外を処理するために使用します。 [FaultHandlerActivity アクティビティを使用して](https://msdn2.microsoft.com/library/bb628479.aspx)[!INCLUDE[crdefault](../includes/crdefault-md.md)]します。|
|[FaultHandlersActivity](https://msdn2.microsoft.com/library/system.workflow.componentmodel.faulthandlersactivity.aspx)|[FaultHandlerActivity](https://msdn2.microsoft.com/library/system.workflow.componentmodel.faulthandleractivity.aspx)型の子アクティビティの順序付きリストを持つ複合アクティビティを表します。 [FaultHandlersActivity アクティビティを使用して](https://msdn2.microsoft.com/library/bb675252.aspx)[!INCLUDE[crdefault](../includes/crdefault-md.md)]します。|
|[HandleExternalEventActivity](https://msdn2.microsoft.com/library/system.workflow.activities.handleexternaleventactivity.aspx)|ローカルサービスとの入出力通信のために、 [Callexternalmethodactivity](https://msdn2.microsoft.com/library/system.workflow.activities.callexternalmethodactivity.aspx)アクティビティと組み合わせて使用されます。 [HandleExternalEventActivity アクティビティを使用して](https://msdn2.microsoft.com/library/bb628446.aspx)[!INCLUDE[crdefault](../includes/crdefault-md.md)]します。|
|[IfElseActivity](https://msdn2.microsoft.com/library/system.workflow.activities.ifelseactivity.aspx)|各分岐の条件をテストし、条件が**true**に等しい最初の分岐に対してアクティビティを実行します。 [IfElseActivity アクティビティを使用して](https://msdn2.microsoft.com/library/bb628472.aspx)[!INCLUDE[crdefault](../includes/crdefault-md.md)]します。|
|[IfElseBranchActivity](https://msdn2.microsoft.com/library/system.workflow.activities.ifelsebranchactivity.aspx)|[IfElseActivity](https://msdn2.microsoft.com/library/system.workflow.activities.ifelseactivity.aspx)の分岐を表します。 [IfElseBranchActivity アクティビティを使用して](https://msdn2.microsoft.com/library/bb628465.aspx)[!INCLUDE[crdefault](../includes/crdefault-md.md)]します。|
|[InvokeWebServiceActivity](https://msdn2.microsoft.com/library/system.workflow.activities.invokewebserviceactivity.aspx)|ワークフローから Web サービスを呼び出すことができます。 [InvokeWebServiceActivity アクティビティを使用して](https://msdn2.microsoft.com/library/bb628576.aspx)[!INCLUDE[crdefault](../includes/crdefault-md.md)]します。|
|[InvokeWorkflowActivity](https://msdn2.microsoft.com/library/system.workflow.activities.invokeworkflowactivity.aspx)|ワークフローから別のワークフローを呼び出すことができます。 [InvokeWorkflowActivity アクティビティを使用して](https://msdn2.microsoft.com/library/bb628557.aspx)[!INCLUDE[crdefault](../includes/crdefault-md.md)]します。|
|[ListenActivity](https://msdn2.microsoft.com/library/system.workflow.activities.listenactivity.aspx)|[EventDrivenActivity](https://msdn2.microsoft.com/library/system.workflow.activities.eventdrivenactivity.aspx)子アクティビティだけを含む複合アクティビティ。 [ListenActivity アクティビティを使用して](https://msdn2.microsoft.com/library/bb628468.aspx)[!INCLUDE[crdefault](../includes/crdefault-md.md)]します。|
|[ParallelActivity](https://msdn2.microsoft.com/library/system.workflow.activities.parallelactivity.aspx)|2つ以上の子**sequenceactivity**アクティビティ分岐を同時に処理するようにスケジュールする方法を提供します。 [Parallelactivity アクティビティを使用して](https://msdn2.microsoft.com/library/bb628494.aspx)[!INCLUDE[crdefault](../includes/crdefault-md.md)]します。|
|[PolicyActivity](https://msdn2.microsoft.com/library/system.workflow.activities.policyactivity.aspx)|ルールのコレクションを表すために使用されます。 ルールは、条件とその結果としてのアクションから構成されます。 [Policyactivity アクティビティを使用して](https://msdn2.microsoft.com/library/bb675229.aspx)[!INCLUDE[crdefault](../includes/crdefault-md.md)]します。|
|[ReplicatorActivity](https://msdn2.microsoft.com/library/system.workflow.activities.replicatoractivity.aspx)|1 つの子アクティビティから複数のインスタンスを作成します。 [ReplicatorActivity アクティビティを使用して](https://msdn2.microsoft.com/library/bb628544.aspx)[!INCLUDE[crdefault](../includes/crdefault-md.md)]します。|
|[SequenceActivity](https://msdn2.microsoft.com/library/system.workflow.activities.sequenceactivity.aspx)|複数のアクティビティをまとめて順次実行するための簡単な方法を提供します。 [Sequenceactivity アクティビティを使用して](https://msdn2.microsoft.com/library/bb628551.aspx)[!INCLUDE[crdefault](../includes/crdefault-md.md)]します。|
|[SetStateActivity](https://msdn2.microsoft.com/library/system.workflow.activities.setstateactivity.aspx)|新しいステート (状態) への移行を指定します。 [SetStateActivity アクティビティを使用して](https://msdn2.microsoft.com/library/bb628469.aspx)[!INCLUDE[crdefault](../includes/crdefault-md.md)]します。|
|[StateActivity](https://msdn2.microsoft.com/library/system.workflow.activities.stateactivity.aspx)|ステート マシン ワークフローにおける状態を表します。 [Stateactivity アクティビティを使用して](https://msdn2.microsoft.com/library/bb628612.aspx)[!INCLUDE[crdefault](../includes/crdefault-md.md)]します。|
|[StateFinalizationActivity](https://msdn2.microsoft.com/library/system.workflow.activities.statefinalizationactivity.aspx)|**Stateactivity**アクティビティを終了するときに実行される子アクティビティのコンテナーとして[stateactivity](https://msdn2.microsoft.com/library/system.workflow.activities.stateactivity.aspx)アクティビティで使用されます。 [StateFinalizationActivity アクティビティを使用して](https://msdn2.microsoft.com/library/bb675278.aspx)[!INCLUDE[crdefault](../includes/crdefault-md.md)]します。|
|[StateInitializationActivity](https://msdn2.microsoft.com/library/system.workflow.activities.stateinitializationactivity.aspx)|**Stateactivity**アクティビティの開始時に実行される子アクティビティのコンテナーとして[stateactivity](https://msdn2.microsoft.com/library/system.workflow.activities.stateactivity.aspx)アクティビティ内で使用されます。 [StateInitializationActivity アクティビティを使用して](https://msdn2.microsoft.com/library/bb675253.aspx)[!INCLUDE[crdefault](../includes/crdefault-md.md)]します。|
|[SuspendActivity](https://msdn2.microsoft.com/library/system.workflow.componentmodel.suspendactivity.aspx)|特に注意が必要なエラー条件が発生したとき、ワークフローの実行を保留して介入できるようにします。 [SuspendActivity アクティビティを使用して](https://msdn2.microsoft.com/library/bb628533.aspx)[!INCLUDE[crdefault](../includes/crdefault-md.md)]します。|
|[SynchronizationScopeActivity](https://msdn2.microsoft.com/library/system.workflow.componentmodel.synchronizationscopeactivity.aspx)|同期されたドメイン内に含まれるアクティビティを順次実行します。 [SynchronizationScopeActivity アクティビティを使用して](https://msdn2.microsoft.com/library/bb675276.aspx)[!INCLUDE[crdefault](../includes/crdefault-md.md)]します。|
|[TerminateActivity](https://msdn2.microsoft.com/library/system.workflow.componentmodel.terminateactivity.aspx)|エラー条件が発生したとき、ワークフローの実行を即座に終了できます。 [TerminateActivity アクティビティを使用して](https://msdn2.microsoft.com/library/bb675261.aspx)[!INCLUDE[crdefault](../includes/crdefault-md.md)]します。|
|[ThrowActivity](https://msdn2.microsoft.com/library/system.workflow.componentmodel.throwactivity.aspx)|ワークフローのプロセス メタデータの一部としてスローされた業務処理例外をキャプチャできます。 [ThrowActivity アクティビティを使用して](https://msdn2.microsoft.com/library/bb628490.aspx)[!INCLUDE[crdefault](../includes/crdefault-md.md)]します。|
|[TransactionScopeActivity](https://msdn2.microsoft.com/library/system.workflow.componentmodel.transactionscopeactivity.aspx)|トランザクションおよび例外処理のフレームワークを提供します。 詳細については、「 [TransactionScopeActivity アクティビティの使用](https://msdn2.microsoft.com/library/bb675241.aspx)」を参照してください。|
|[WebServiceFaultActivity](https://msdn2.microsoft.com/library/system.workflow.activities.webservicefaultactivity.aspx)|Web サービスで発生するエラーをモデル化できます。 [WebServiceFaultActivity アクティビティを使用して](https://msdn2.microsoft.com/library/bb628568.aspx)[!INCLUDE[crdefault](../includes/crdefault-md.md)]します。|
|[WebServiceInputActivity](https://msdn2.microsoft.com/library/system.workflow.activities.webserviceinputactivity.aspx)|Web サービスからデータを取得します。 [WebServiceInputActivity アクティビティを使用して](https://msdn2.microsoft.com/library/bb628508.aspx)[!INCLUDE[crdefault](../includes/crdefault-md.md)]します。|
|[WebServiceOutputActivity](https://msdn2.microsoft.com/library/system.workflow.activities.webserviceoutputactivity.aspx)|Web サービスからワークフローに対する要求に応答します。 [WebServiceOutputActivity アクティビティを使用して](https://msdn2.microsoft.com/library/bb628594.aspx)[!INCLUDE[crdefault](../includes/crdefault-md.md)]します。|
|[WhileActivity](https://msdn2.microsoft.com/library/system.workflow.activities.whileactivity.aspx)|条件が満たされるまで、ワークフローをループさせることができます。 [!INCLUDE[crdefault](../includes/crdefault-md.md)][、アクティビティアクティビティを使用](https://msdn2.microsoft.com/library/bb628552.aspx)します。|

 カスタムアクティビティの作成方法に [!INCLUDE[crabout](../includes/crabout-md.md)] ては、「[カスタムアクティビティの開発](https://msdn2.microsoft.com/library/bb675248.aspx)」および「[従来のアクティビティデザイナーの使用](../workflow-designer/using-the-legacy-activity-designer.md)」を参照してください。

## <a name="in-this-section"></a>このセクションの内容
 [アクティビティビュー (レガシ)](../workflow-designer/activity-views-legacy.md)アクティビティのさまざまなデザインビューについて説明します。

 [方法: ツールボックスにアクティビティを追加する (レガシ)](../workflow-designer/how-to-add-activities-to-the-toolbox-legacy.md)ツールボックスにアクティビティを追加する方法について説明します。

 [方法: 宣言的ルール条件を作成する (レガシ)](../workflow-designer/how-to-create-a-declarative-rule-condition-legacy.md)宣言型の規則の条件を作成する手順を示します。

 [方法: PolicyActivity 規則セットを作成する (レガシ)](../workflow-designer/how-to-create-a-policyactivity-rule-set-legacy.md)PolicyActivity ルールセットを作成する手順について説明します。

 [方法: WCF コントラクト操作を実装する (レガシ)](../workflow-designer/how-to-implement-a-windows-communication-foundation-contract-operation-legacy.md)[!INCLUDE[indigo2](../includes/indigo2-md.md)] コントラクト操作を実装する手順について説明します。

 [方法: WCF コントラクト操作を呼び出す (レガシ)](../workflow-designer/how-to-invoke-a-windows-communication-foundation-contract-operation-legacy.md)[!INCLUDE[indigo2](../includes/indigo2-md.md)] コントラクト操作を呼び出す手順を示します。

## <a name="see-also"></a>参照
 [Windows Workflow Foundation アクティビティ](https://msdn2.microsoft.com/library/bb675247.aspx)ワークフローの[開発](https://msdn2.microsoft.com/library/bb628448.aspx)[ワークフローアクティビティの開発](https://msdn2.microsoft.com/library/bb675248.aspx)
