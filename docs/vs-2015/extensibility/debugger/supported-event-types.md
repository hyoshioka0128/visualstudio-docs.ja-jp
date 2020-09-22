---
title: サポートされているイベントの種類 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], supported events
ms.assetid: a3c0386d-551e-4734-9a0c-368d1c2e6671
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f671e8d0128bee2c52dc1191b33edb889c92d2e9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841996"
---
# <a name="supported-event-types"></a>サポートされているイベントの種類
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Visual Studio のデバッグでは、現在、次のイベントの種類がサポートされています。  
  
- 非同期イベント  
  
   デバッグ中のアプリケーションの状態が変化していることを、セッションデバッグマネージャー (SDM) と IDE に通知します。 これらのイベントは、SDM と IDE の都合がよいときに処理されます。 イベントが処理されると、応答はデバッグエンジン (DE) に送信されません。 [IDebugOutputStringEvent2](../../extensibility/debugger/reference/idebugoutputstringevent2.md)インターフェイスと[IDebugMessageEvent2](../../extensibility/debugger/reference/idebugmessageevent2.md)インターフェイスは、非同期イベントの例です。  
  
- 同期イベント  
  
   デバッグ対象のアプリケーションの状態が変化していることを SDM と IDE に通知します。 これらのイベントと非同期イベントの唯一の違いは、 [ContinueFromSynchronousEvent](../../extensibility/debugger/reference/idebugengine2-continuefromsynchronousevent.md) メソッドによって応答が送信されることです。  
  
   IDE がイベントを受け取って処理した後も処理を続行する必要がある場合は、同期イベントの送信が役立ちます。  
  
- 同期停止イベント、またはイベントの停止  
  
   アプリケーションがコードの実行を停止したことを SDM と IDE に通知します。 メソッド [イベント](../../extensibility/debugger/reference/idebugeventcallback2-event.md)を使用して停止イベントを送信する場合は、 [IDebugThread2](../../extensibility/debugger/reference/idebugthread2.md) パラメーターが必要です。 停止イベントは、次のいずれかのメソッドを呼び出すことによって継続されます。  
  
  - [実行](../../extensibility/debugger/reference/idebugprogram2-execute.md)  
  
  - [Step](../../extensibility/debugger/reference/idebugprogram2-step.md)  
  
  - [続行](../../extensibility/debugger/reference/idebugprogram2-continue.md)  
  
    インターフェイス [IDebugBreakpointEvent2](../../extensibility/debugger/reference/idebugbreakpointevent2.md) と [IDebugExceptionEvent2](../../extensibility/debugger/reference/idebugexceptionevent2.md) は、イベントを停止する例です。  
  
  > [!NOTE]
  > 非同期停止イベントはサポートされていません。 非同期停止イベントを送信すると、エラーになります。  
  
## <a name="discussion"></a>考察 (Discussion)  
 イベントの実際の実装は、DE の設計によって異なります。 送信される各イベントの種類は、その属性によって決まります。この属性は、DE をデザインするときに設定されます。 たとえば、ある DE が非同期イベントとして [IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md) を送信し、別の DE が停止イベントとして送信する場合があります。  
  
 次の表は、イベントとイベントの種類に必要なプログラムとスレッドのパラメーターを示しています。 イベントは同期できます。 同期する必要があるイベントはありません。  
  
> [!NOTE]
> すべてのイベントには、 [IDebugEngine2](../../extensibility/debugger/reference/idebugengine2.md) インターフェイスが必要です。  
  
|イベント|IDebugProgram2|IDebugThread2|停止、イベント|  
|-----------|--------------------|-------------------|---------------------|  
|[IDebugActivateDocumentEvent2](../../extensibility/debugger/reference/idebugactivatedocumentevent2.md)|許可されますが、必須ではありません|許可されますが、必須ではありません|No|  
|[IDebugBreakEvent2](../../extensibility/debugger/reference/idebugbreakevent2.md)|必須|必須|はい|  
|[IDebugBreakpointBoundEvent2](../../extensibility/debugger/reference/idebugbreakpointboundevent2.md)|許可されますが、必須ではありません|許可されますが、必須ではありません|No|  
|[IDebugBreakpointErrorEvent2](../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md)|許可されますが、必須ではありません|許可されますが、必須ではありません|No|  
|[IDebugBreakpointUnboundEvent2](../../extensibility/debugger/reference/idebugbreakpointunboundevent2.md)|許可されますが、必須ではありません|許可されますが、必須ではありません|No|  
|[IDebugBreakpointEvent2](../../extensibility/debugger/reference/idebugbreakpointevent2.md)|必須|必須|はい|  
|[IDebugCanStopEvent2](../../extensibility/debugger/reference/idebugcanstopevent2.md)|必須|必須|いいえ|  
|[IDebugDocumentTextEvents2](../../extensibility/debugger/reference/idebugdocumenttextevents2.md)|使用できません|使用できません|No|  
|[IDebugEngineCreateEvent2](../../extensibility/debugger/reference/idebugenginecreateevent2.md)|使用できません|使用できません|No|  
|[IDebugEntryPointEvent2](../../extensibility/debugger/reference/idebugentrypointevent2.md)|必須|必須|はい|  
|[IDebugErrorEvent2](../../extensibility/debugger/reference/idebugerrorevent2.md)|許可されますが、必須ではありません|許可されますが、必須ではありません|シリアル化|  
|[IDebugExceptionEvent2](../../extensibility/debugger/reference/idebugexceptionevent2.md)|必須|必須|はい|  
|[IDebugExpressionEvaluationCompleteEvent2](../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md)|許可されますが、必須ではありません|許可されますが、必須ではありません|シリアル化|  
|[IDebugInterceptExceptionCompleteEvent2](../../extensibility/debugger/reference/idebuginterceptexceptioncompleteevent2.md)|必須|必須|はい|  
|[IDebugLoadCompleteEvent2](../../extensibility/debugger/reference/idebugloadcompleteevent2.md)|必須|必須|はい|  
|[IDebugMessageEvent2](../../extensibility/debugger/reference/idebugmessageevent2.md)|許可されますが、必須ではありません|許可されますが、必須ではありません|シリアル化|  
|[IDebugModuleLoadEvent2](../../extensibility/debugger/reference/idebugmoduleloadevent2.md)|必須|許可されますが、必須ではありません|No|  
|[IDebugOutputStringEvent2](../../extensibility/debugger/reference/idebugoutputstringevent2.md)|許可されますが、必須ではありません|許可されますが、必須ではありません|No|  
|[IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md)|必須|許可されますが、必須ではありません|No|  
|[IDebugProgramDestroyEvent2](../../extensibility/debugger/reference/idebugprogramdestroyevent2.md)|必須|許可されますが、必須ではありません|No|  
|[IDebugPropertyCreateEvent2](../../extensibility/debugger/reference/idebugpropertycreateevent2.md)|必須|許可されますが、必須ではありません|No|  
|[IDebugPropertyDestroyEvent2](../../extensibility/debugger/reference/idebugpropertydestroyevent2.md)|必須|許可されますが、必須ではありません|No|  
|[IDebugReturnValueEvent2](../../extensibility/debugger/reference/idebugreturnvalueevent2.md)|許可されますが、必須ではありません|許可されますが、必須ではありません|No|  
|IDebugStopCompleteEvent2|必須|必須|はい|  
|[IDebugStepCompleteEvent2](../../extensibility/debugger/reference/idebugstepcompleteevent2.md)|必須|必須|はい|  
|[IDebugSymbolSearchEvent2](../../extensibility/debugger/reference/idebugsymbolsearchevent2.md)|許可されますが、必須ではありません|許可されますが、必須ではありません|No|  
|[IDebugThreadCreateEvent2](../../extensibility/debugger/reference/idebugthreadcreateevent2.md)|必須|必須|いいえ|  
|[IDebugThreadDestroyEvent2](../../extensibility/debugger/reference/idebugthreaddestroyevent2.md)|必須|必須|いいえ|  
|[IDebugThreadNameChangedEvent2](../../extensibility/debugger/reference/idebugthreadnamechangedevent2.md)|許可されますが、必須ではありません|許可されますが、必須ではありません|いいえ|  
  
## <a name="see-also"></a>関連項目  
 [イベントの送信](../../extensibility/debugger/sending-events.md)
