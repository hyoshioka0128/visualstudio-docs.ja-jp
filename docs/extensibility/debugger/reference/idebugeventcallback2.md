---
title: イベントコールバック2 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEventCallback2
helpviewer_keywords:
- IDebugEventCallback2
ms.assetid: 2c935ee0-2e22-4be0-a852-73736f33c8c9
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a74825a955afdde03e63673c4b1b6afda5904953
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80729887"
---
# <a name="idebugeventcallback2"></a>IDebugEventCallback2
このインターフェイスは、デバッグ エンジン (DE) セッション デバッグ マネージャー (SDM) にデバッグ イベントを送信するために使用されます。

## <a name="syntax"></a>構文

```
IDebugEventCallback2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]デバッグ エンジンからイベントを受信するには、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 デバッグ エンジンは、通常、SDM が[アタッチ](../../../extensibility/debugger/reference/idebugprogram2-attach.md)、[アタッチ](../../../extensibility/debugger/reference/idebugengine2-attach.md)、または[LaunchSuspended](../../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)を呼び出したときにこのインターフェイスを受け取ります。 デバッグ エンジンは、イベントを呼び出すことによって SDM に[イベント](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)を送信します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に`IDebugEventCallback2`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)|デバッグ イベントの通知を SDM に送信します。|

## <a name="remarks"></a>Remarks
 [EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)と[EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)はインターフェイスを`IDebugEventCallback2`受け取ることを指定していますが、これは当てはまらず、インターフェイス ポインタは常に null 値になります。 代わりに、デバッグ エンジンは[、呼](../../../extensibility/debugger/reference/idebugprogram2-attach.md)び出しで受信した[Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md)`IDebugEventCallback2`インターフェイスを使用する必要があります。 [LaunchSuspended](../../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)

 パッケージがマネージ コードで[IDebugEventCallback](../../../extensibility/debugger/reference/idebugeventcallback2.md)を実装している場合は<xref:System.Runtime.InteropServices.Marshal.ReleaseComObject%2A>[、Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)に渡されるさまざまなインターフェイスで呼び出すことを強くお勧めします。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [LaunchSuspended](../../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)
- [Attach](../../../extensibility/debugger/reference/idebugprogram2-attach.md)
- [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md)
