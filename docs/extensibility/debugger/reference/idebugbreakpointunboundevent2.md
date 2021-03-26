---
description: このインターフェイスは、バインドされたブレークポイントが読み込まれたプログラムからバインド解除されたことをセッションデバッグマネージャー (SDM) に通知します。
title: IDebugBreakpointUnboundEvent2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBreakpointUnboundEvent2
helpviewer_keywords:
- IDebugBreakpointUnboundEvent2
ms.assetid: 6b1e1863-0c64-4d85-8ab9-aface522fdea
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 27c032c1563bf208c378044b4e093529a2dba10c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105088641"
---
# <a name="idebugbreakpointunboundevent2"></a>IDebugBreakpointUnboundEvent2
このインターフェイスは、バインドされたブレークポイントが読み込まれたプログラムからバインド解除されたことをセッションデバッグマネージャー (SDM) に通知します。

## <a name="syntax"></a>Syntax

```
IDebugBreakpointUnboundEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグエンジン (DE) は、ブレークポイントのサポートの一部としてこのインターフェイスを実装します。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)インターフェイスは、このインターフェイスと同じオブジェクトに実装する必要があります (SDM は[QueryInterface](/cpp/atl/queryinterface)を使用してインターフェイスにアクセスし `IDebugEvent2` ます)。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 このイベントオブジェクトは、バインドされたブレークポイントのバインドが解除されると、DE によって作成され、送信されます。 イベントは、デバッグ対象のプログラムにアタッチされるときに、SDM によって提供される [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) callback 関数を使用して送信されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、のメソッドを示し `IDebugBreakpointUnboundEvent2` ます。

|メソッド|説明|
|------------|-----------------|
|[GetBreakpoint](../../../extensibility/debugger/reference/idebugbreakpointunboundevent2-getbreakpoint.md)|バインド解除されたブレークポイントを取得します。|
|[GetReason](../../../extensibility/debugger/reference/idebugbreakpointunboundevent2-getreason.md)|ブレークポイントがバインド解除された理由を取得します。|

## <a name="remarks"></a>注釈
 デバッグエンジンの DLL またはクラスがアンロードされると、そのモジュール内のコードにバインドされていたすべてのブレークポイントは、デバッグ中のプログラムからバインド解除される必要があります。 バインドされていない `IDebugBreakpointUnboundEvent2` 各ブレークポイントに対してが送信されます。

## <a name="requirements"></a>要件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>こちらもご覧ください
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugBoundBreakpoint2](../../../extensibility/debugger/reference/idebugboundbreakpoint2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
