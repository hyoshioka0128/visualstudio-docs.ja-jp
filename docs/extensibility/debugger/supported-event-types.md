---
title: サポートされるイベントの種類 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], supported events
ms.assetid: a3c0386d-551e-4734-9a0c-368d1c2e6671
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 94e26897c50fd7e10a8b831655610848cb93043f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80712797"
---
# <a name="supported-event-types"></a>サポートされているイベントの種類
Visual Studio のデバッグでは、現在、次の種類のイベントがサポートされています。

- 非同期イベント

   デバッグ中のアプリケーションの状態が変更されていることをセッション デバッグ マネージャー (SDM) と IDE に通知します。 これらのイベントは、SDM と IDE の余暇に処理されます。 イベントが処理されると、デバッグ エンジン (DE) に応答は送信されません。 インターフェイス[は非同期](../../extensibility/debugger/reference/idebugoutputstringevent2.md)イベントの例です。 [IDebugMessageEvent2](../../extensibility/debugger/reference/idebugmessageevent2.md)

- 同期イベント

   デバッグ中のアプリケーションの状態が変化していることを SDM および IDE に通知します。 これらのイベントと非同期イベントの唯一の違いは、応答が[ContinueFromSynchronousEvent](../../extensibility/debugger/reference/idebugengine2-continuefromsynchronousevent.md)メソッドを使用して送信されるということです。

   同期イベントの送信は、IDE がイベントを受信して処理した後に、DE が処理を続行する必要がある場合に便利です。

- 同期停止イベントまたは停止イベント

   デバッグ中のアプリケーションがコードの実行を停止したことを SDM と IDE に通知します。 メソッド[イベント](../../extensibility/debugger/reference/idebugeventcallback2-event.md)を使用して停止イベントを送信する場合は[、IDebugThread2](../../extensibility/debugger/reference/idebugthread2.md)パラメーターが必要です。 停止イベントは、次のいずれかのメソッドの呼び出しによって継続されます。

  - [実行](../../extensibility/debugger/reference/idebugprogram2-execute.md)

  - [Step](../../extensibility/debugger/reference/idebugprogram2-step.md)

  - [続行](../../extensibility/debugger/reference/idebugprogram2-continue.md)

    インターフェイス[IDebugBreakpointEvent2](../../extensibility/debugger/reference/idebugbreakpointevent2.md)および[IDebugExceptionEvent2](../../extensibility/debugger/reference/idebugexceptionevent2.md)は、イベントを停止する例です。

  > [!NOTE]
  > 非同期停止イベントはサポートされていません。 非同期停止イベントを送信するとエラーになります。

## <a name="discussion"></a>ディスカッション
 イベントの実際の実装は、DE の設計によって異なります。 送信される各イベントのタイプは、DE を設計するときに設定される属性によって決まります。 たとえば、ある DE は非同期イベントとして[IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md)を送信し、別の DE は停止イベントとして送信できます。

 次の表は、イベントの種類と同様に、どのプログラムパラメーターとスレッド パラメーターが必要かを示しています。 どのイベントでも同期できます。 同期する必要のあるイベントはありません。

> [!NOTE]
> すべてのイベントに[対して IDebugEngine2](../../extensibility/debugger/reference/idebugengine2.md)インターフェイスが必要です。

|Event|IDebugProgram2|IDebugThread2|イベントの停止|
|-----------|--------------------|-------------------|---------------------|
|[IDebugActivateDocumentEvent2](../../extensibility/debugger/reference/idebugactivatedocumentevent2.md)|許可されているが必須ではない|許可されているが必須ではない|いいえ|
|[IDebugBreakEvent2](../../extensibility/debugger/reference/idebugbreakevent2.md)|必須|必須|はい|
|[IDebugBreakpointBoundEvent2](../../extensibility/debugger/reference/idebugbreakpointboundevent2.md)|許可されているが必須ではない|許可されているが必須ではない|いいえ|
|[IDebugBreakpointErrorEvent2](../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md)|許可されているが必須ではない|許可されているが必須ではない|いいえ|
|[IDebugBreakpointUnboundEvent2](../../extensibility/debugger/reference/idebugbreakpointunboundevent2.md)|許可されているが必須ではない|許可されているが必須ではない|いいえ|
|[IDebugBreakpointEvent2](../../extensibility/debugger/reference/idebugbreakpointevent2.md)|必須|必須|はい|
|[IDebugCanStopEvent2](../../extensibility/debugger/reference/idebugcanstopevent2.md)|必須|必須|いいえ|
|[IDebugDocumentTextEvents2](../../extensibility/debugger/reference/idebugdocumenttextevents2.md)|禁止|禁止|いいえ|
|[IDebugEngineCreateEvent2](../../extensibility/debugger/reference/idebugenginecreateevent2.md)|禁止|禁止|いいえ|
|[IDebugEntryPointEvent2](../../extensibility/debugger/reference/idebugentrypointevent2.md)|必須|必須|はい|
|[IDebugErrorEvent2](../../extensibility/debugger/reference/idebugerrorevent2.md)|許可されているが必須ではない|許可されているが必須ではない|シリアル化|
|[IDebugExceptionEvent2](../../extensibility/debugger/reference/idebugexceptionevent2.md)|必須|必須|はい|
|[IDebugExpressionEvaluationCompleteEvent2](../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md)|許可されているが必須ではない|許可されているが必須ではない|シリアル化|
|[IDebugInterceptExceptionCompleteEvent2](../../extensibility/debugger/reference/idebuginterceptexceptioncompleteevent2.md)|必須|必須|はい|
|[IDebugLoadCompleteEvent2](../../extensibility/debugger/reference/idebugloadcompleteevent2.md)|必須|必須|はい|
|[IDebugMessageEvent2](../../extensibility/debugger/reference/idebugmessageevent2.md)|許可されているが必須ではない|許可されているが必須ではない|シリアル化|
|[IDebugModuleLoadEvent2](../../extensibility/debugger/reference/idebugmoduleloadevent2.md)|必須|許可されているが必須ではない|いいえ|
|[IDebugOutputStringEvent2](../../extensibility/debugger/reference/idebugoutputstringevent2.md)|許可されているが必須ではない|許可されているが必須ではない|いいえ|
|[IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md)|必須|許可されているが必須ではない|いいえ|
|[IDebugProgramDestroyEvent2](../../extensibility/debugger/reference/idebugprogramdestroyevent2.md)|必須|許可されているが必須ではない|いいえ|
|[IDebugPropertyCreateEvent2](../../extensibility/debugger/reference/idebugpropertycreateevent2.md)|必須|許可されているが必須ではない|いいえ|
|[IDebugPropertyDestroyEvent2](../../extensibility/debugger/reference/idebugpropertydestroyevent2.md)|必須|許可されているが必須ではない|いいえ|
|[IDebugReturnValueEvent2](../../extensibility/debugger/reference/idebugreturnvalueevent2.md)|許可されているが必須ではない|許可されているが必須ではない|いいえ|
|IDebugStopCompleteEvent2|必須|必須|はい|
|[IDebugStepCompleteEvent2](../../extensibility/debugger/reference/idebugstepcompleteevent2.md)|必須|必須|はい|
|[IDebugSymbolSearchEvent2](../../extensibility/debugger/reference/idebugsymbolsearchevent2.md)|許可されているが必須ではない|許可されているが必須ではない|いいえ|
|[IDebugThreadCreateEvent2](../../extensibility/debugger/reference/idebugthreadcreateevent2.md)|必須|必須|いいえ|
|[IDebugThreadDestroyEvent2](../../extensibility/debugger/reference/idebugthreaddestroyevent2.md)|必須|必須|いいえ|
|[IDebugThreadNameChangedEvent2](../../extensibility/debugger/reference/idebugthreadnamechangedevent2.md)|許可されているが必須ではない|許可されているが必須ではない|いいえ|

## <a name="see-also"></a>関連項目
- [イベントの送信](../../extensibility/debugger/sending-events.md)
