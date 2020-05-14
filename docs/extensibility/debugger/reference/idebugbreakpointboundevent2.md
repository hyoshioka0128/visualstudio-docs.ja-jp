---
title: イベントのデバッグのブレークポイントを指定するイベント 2 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBreakpointBoundEvent2
helpviewer_keywords:
- IDebugBreakpointBoundEvent2
ms.assetid: 24ba362e-5be1-481a-b071-e1ebd3cae6e8
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7943addb4334710da3252a4d822330e45b6e0f80
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80735300"
---
# <a name="idebugbreakpointboundevent2"></a>IDebugBreakpointBoundEvent2
このインターフェイスは、保留中のブレークポイントが読み込まれたプログラムに正常にバインドされたことをセッション デバッグ マネージャー (SDM) に通知します。

## <a name="syntax"></a>構文

```
IDebugBreakpointBoundEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 DE は、ブレークポイントのサポートの一部としてこのインターフェイスを実装します。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)インターフェイスは、このインターフェイスと同じオブジェクトに実装する必要があります (SDM は、インターフェイス`IDebugEvent2`にアクセスするのに[QueryInterface](/cpp/atl/queryinterface)を使用します)。

## <a name="notes-for-callers"></a>発信者向けのメモ
 デは、保留中のブレークポイントがデバッグ中のプログラムに正常にバインドされたときに、このイベント オブジェクトを作成して送信します。 イベントは、デバッグ中のプログラムにアタッチされたときに、SDM によって提供される[IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)コールバック関数を使用して送信されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に`IDebugBreakpointBoundEvent2`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[GetPendingBreakpoint](../../../extensibility/debugger/reference/idebugbreakpointboundevent2-getpendingbreakpoint.md)|バインドされている保留中のブレークポイントを取得します。|
|[EnumBoundBreakpoints](../../../extensibility/debugger/reference/idebugbreakpointboundevent2-enumboundbreakpoints.md)|このイベントにバインドされたブレークポイントの列挙子を作成します。|

## <a name="remarks"></a>Remarks
 ブレークポイントがバインドされると、イベントが SDM に送信されます。 ブレークポイントをバインドできない場合は[、IDebugBreakpointErrorEvent2](../../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md)が送信されます。それ以外の`IDebugBreakpointBoundEvent2`場合は、 が送信されます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [IDebugBreakpointErrorEvent2](../../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md)
