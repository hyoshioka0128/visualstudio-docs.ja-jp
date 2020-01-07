---
title: サポートされているイベントの種類 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], supported events
ms.assetid: a3c0386d-551e-4734-9a0c-368d1c2e6671
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9c4ee45e1a3a7efeb990fcb6f9073420a99dbe7c
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66351090"
---
# <a name="supported-event-types"></a>サポートされているイベントの種類
Visual Studio のデバッグでは、次のイベントの種類現在サポートしています。

- 非同期のイベント

   セッション デバッグ マネージャー (SDM) に通知し、デバッグ中のアプリケーションの状態を変更する IDE。 これらのイベントは、SDM と、IDE の都合のよいタイミングで処理されます。 コンソール アプリケーションは、イベントが処理されると、デバッグ エンジン (DE) に、応答は送信されません。 [IDebugOutputStringEvent2](../../extensibility/debugger/reference/idebugoutputstringevent2.md)と[IDebugMessageEvent2](../../extensibility/debugger/reference/idebugmessageevent2.md)インターフェイスは非同期イベントの例を示します。

- 同期イベント

   SDM と IDE のデバッグ中のアプリケーションの状態が変更されていることを通知します。 これらのイベントと非同期イベントの唯一の違いは、によって、応答が送信されること、 [ContinueFromSynchronousEvent](../../extensibility/debugger/reference/idebugengine2-continuefromsynchronousevent.md)メソッド。

   同期イベントを送信するは、DE、IDE を受け取り、イベントを処理した後に処理を続行する必要がある場合に便利です。

- 同期イベントを停止または停止イベント

   デバッグ中のアプリケーションのコードの実行が停止したこと、SDM と、IDE に通知します。 メソッドを使用して停止イベントを送信する[イベント](../../extensibility/debugger/reference/idebugeventcallback2-event.md)、 [IDebugThread2](../../extensibility/debugger/reference/idebugthread2.md)パラメーターが必要です。 停止イベントは、次のメソッドのいずれかを呼び出して継続します。

  - [Execute](../../extensibility/debugger/reference/idebugprogram2-execute.md)

  - [Step](../../extensibility/debugger/reference/idebugprogram2-step.md)

  - [Continue](../../extensibility/debugger/reference/idebugprogram2-continue.md)

    インターフェイス[IDebugBreakpointEvent2](../../extensibility/debugger/reference/idebugbreakpointevent2.md)と[IDebugExceptionEvent2](../../extensibility/debugger/reference/idebugexceptionevent2.md)停止イベントの例を示します。

  > [!NOTE]
  > 非同期の停止イベントがサポートされていません。 非同期の停止イベントを送信するエラーになります。

## <a name="discussion"></a>説明
 イベントの実際の実装は、DE の設計に依存します。 送信される各イベントの種類は、DE を設計する際に、その属性によって決定されます。 たとえば、1 つ DE が送信可能性があります、 [IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md) stopping イベントとして送信することがあります別中に、非同期のイベントとして。

 次の表では、どのプログラムとスレッドのパラメーターは、どのイベントとイベントの種類に必要なを指定します。 すべてのイベントは、同期されることができます。 イベントを同期する必要はありません。

> [!NOTE]
> [IDebugEngine2](../../extensibility/debugger/reference/idebugengine2.md)インターフェイスがすべてのイベントが必要です。

|event|IDebugProgram2|IDebugThread2|停止イベント|
|-----------|--------------------|-------------------|---------------------|
|[IDebugActivateDocumentEvent2](../../extensibility/debugger/reference/idebugactivatedocumentevent2.md)|許可されているときに必要ありません。|許可されているときに必要ありません。|いいえ|
|[IDebugBreakEvent2](../../extensibility/debugger/reference/idebugbreakevent2.md)|必須|必須|はい|
|[IDebugBreakpointBoundEvent2](../../extensibility/debugger/reference/idebugbreakpointboundevent2.md)|許可されているときに必要ありません。|許可されているときに必要ありません。|いいえ|
|[IDebugBreakpointErrorEvent2](../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md)|許可されているときに必要ありません。|許可されているときに必要ありません。|いいえ|
|[IDebugBreakpointUnboundEvent2](../../extensibility/debugger/reference/idebugbreakpointunboundevent2.md)|許可されているときに必要ありません。|許可されているときに必要ありません。|いいえ|
|[IDebugBreakpointEvent2](../../extensibility/debugger/reference/idebugbreakpointevent2.md)|必須|必須|はい|
|[IDebugCanStopEvent2](../../extensibility/debugger/reference/idebugcanstopevent2.md)|必須|必須|いいえ|
|[IDebugDocumentTextEvents2](../../extensibility/debugger/reference/idebugdocumenttextevents2.md)|使用できません|使用できません|いいえ|
|[IDebugEngineCreateEvent2](../../extensibility/debugger/reference/idebugenginecreateevent2.md)|使用できません|使用できません|いいえ|
|[IDebugEntryPointEvent2](../../extensibility/debugger/reference/idebugentrypointevent2.md)|必須|必須|はい|
|[IDebugErrorEvent2](../../extensibility/debugger/reference/idebugerrorevent2.md)|許可されているときに必要ありません。|許可されているときに必要ありません。|シリアル化|
|[IDebugExceptionEvent2](../../extensibility/debugger/reference/idebugexceptionevent2.md)|必須|必須|はい|
|[IDebugExpressionEvaluationCompleteEvent2](../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md)|許可されているときに必要ありません。|許可されているときに必要ありません。|シリアル化|
|[IDebugInterceptExceptionCompleteEvent2](../../extensibility/debugger/reference/idebuginterceptexceptioncompleteevent2.md)|必須|必須|はい|
|[IDebugLoadCompleteEvent2](../../extensibility/debugger/reference/idebugloadcompleteevent2.md)|必須|必須|はい|
|[IDebugMessageEvent2](../../extensibility/debugger/reference/idebugmessageevent2.md)|許可されているときに必要ありません。|許可されているときに必要ありません。|シリアル化|
|[IDebugModuleLoadEvent2](../../extensibility/debugger/reference/idebugmoduleloadevent2.md)|必須|許可されているときに必要ありません。|いいえ|
|[IDebugOutputStringEvent2](../../extensibility/debugger/reference/idebugoutputstringevent2.md)|許可されているときに必要ありません。|許可されているときに必要ありません。|いいえ|
|[IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md)|必須|許可されているときに必要ありません。|いいえ|
|[IDebugProgramDestroyEvent2](../../extensibility/debugger/reference/idebugprogramdestroyevent2.md)|必須|許可されているときに必要ありません。|いいえ|
|[IDebugPropertyCreateEvent2](../../extensibility/debugger/reference/idebugpropertycreateevent2.md)|必須|許可されているときに必要ありません。|いいえ|
|[IDebugPropertyDestroyEvent2](../../extensibility/debugger/reference/idebugpropertydestroyevent2.md)|必須|許可されているときに必要ありません。|いいえ|
|[IDebugReturnValueEvent2](../../extensibility/debugger/reference/idebugreturnvalueevent2.md)|許可されているときに必要ありません。|許可されているときに必要ありません。|いいえ|
|IDebugStopCompleteEvent2|必須|必須|はい|
|[IDebugStepCompleteEvent2](../../extensibility/debugger/reference/idebugstepcompleteevent2.md)|必須|必須|はい|
|[IDebugSymbolSearchEvent2](../../extensibility/debugger/reference/idebugsymbolsearchevent2.md)|許可されているときに必要ありません。|許可されているときに必要ありません。|いいえ|
|[IDebugThreadCreateEvent2](../../extensibility/debugger/reference/idebugthreadcreateevent2.md)|必須|必須|いいえ|
|[IDebugThreadDestroyEvent2](../../extensibility/debugger/reference/idebugthreaddestroyevent2.md)|必須|必須|いいえ|
|[IDebugThreadNameChangedEvent2](../../extensibility/debugger/reference/idebugthreadnamechangedevent2.md)|許可されているときに必要ありません。|許可されているときに必要ありません。|いいえ|

## <a name="see-also"></a>関連項目
- [イベントの送信](../../extensibility/debugger/sending-events.md)
