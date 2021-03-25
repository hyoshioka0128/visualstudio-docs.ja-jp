---
description: このインターフェイスは、デバッグエンジン (DE) がデバッグイベントをセッションデバッグマネージャー (SDM) に送信するために使用されます。
title: IDebugEventCallback2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEventCallback2
helpviewer_keywords:
- IDebugEventCallback2
ms.assetid: 2c935ee0-2e22-4be0-a852-73736f33c8c9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d00c970c522adf232f9a18b762c7d6cf3cf3b794
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105084897"
---
# <a name="idebugeventcallback2"></a>IDebugEventCallback2
このインターフェイスは、デバッグエンジン (DE) がデバッグイベントをセッションデバッグマネージャー (SDM) に送信するために使用されます。

## <a name="syntax"></a>Syntax

```
IDebugEventCallback2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] デバッグエンジンからイベントを受信するために、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 通常、デバッグエンジンは、SDM が [attach](../../../extensibility/debugger/reference/idebugprogram2-attach.md)、 [attach](../../../extensibility/debugger/reference/idebugengine2-attach.md)、または [launchsuspended](../../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)を呼び出したときに、このインターフェイスを受け取ります。 デバッグエンジンは、 [イベント](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)を呼び出すことによって、イベントを SDM に送信します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、のメソッドを示し `IDebugEventCallback2` ます。

|メソッド|説明|
|------------|-----------------|
|[Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)|SDM にデバッグイベントの通知を送信します。|

## <a name="remarks"></a>注釈
 [EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)および[evaluateasync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)はインターフェイスを受け取ることを指定します `IDebugEventCallback2` が、これは当てはまりません。インターフェイスポインターは常に null 値になります。 代わりに、デバッグエンジンは、 `IDebugEventCallback2` [attach](../../../extensibility/debugger/reference/idebugprogram2-attach.md)、 [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md)、または [launchsuspended](../../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)の呼び出しで受信したインターフェイスを使用する必要があります。

 パッケージがマネージコードで [IDebugEventCallback](../../../extensibility/debugger/reference/idebugeventcallback2.md) を実装している場合は、 <xref:System.Runtime.InteropServices.Marshal.ReleaseComObject%2A> [イベント](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)に渡されるさまざまなインターフェイスで呼び出されることを強くお勧めします。

## <a name="requirements"></a>要件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>こちらもご覧ください
- [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [LaunchSuspended](../../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)
- [[アタッチ]](../../../extensibility/debugger/reference/idebugprogram2-attach.md)
- [[アタッチ]](../../../extensibility/debugger/reference/idebugengine2-attach.md)
