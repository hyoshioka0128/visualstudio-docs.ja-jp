---
description: このインターフェイスは、ブレークポイントでの停止などの重要なデバッグ情報と、デバッグメッセージなどの重要でない情報の両方を通知するために使用されます。
title: IDebugEvent2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEvent2
helpviewer_keywords:
- IDebugEvent2 interface
ms.assetid: de3d714d-96fb-4e12-b66b-a75391472153
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e162e276fc93c9e2c0d4333ac0f5c2630f75618e
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102152950"
---
# <a name="idebugevent2"></a>IDebugEvent2
このインターフェイスは、ブレークポイントでの停止などの重要なデバッグ情報と、デバッグメッセージなどの重要でない情報の両方を通知するために使用されます。

## <a name="syntax"></a>構文

```
IDebugEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグエンジン (DE) とカスタムポート供給業者は、他のすべてのイベントインターフェイスと同じオブジェクトにこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 [イベント](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)または[イベント](../../../extensibility/debugger/reference/idebugportevents2-event.md)に指定されたインターフェイス ID (IID) 引数を使用して、セッションデバッグマネージャー (SDM) はインターフェイスの[QueryInterface](/cpp/atl/queryinterface)を呼び出し、 `IDebugEvent2` 適切なイベントインターフェイスを取得します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、のメソッドを示し `IDebugEvent2` ます。

|メソッド|説明|
|------------|-----------------|
|[GetAttributes](../../../extensibility/debugger/reference/idebugevent2-getattributes.md)|このデバッグイベントの属性を取得します。|

## <a name="remarks"></a>解説
 [IDebugBreakpointEvent2](../../../extensibility/debugger/reference/idebugbreakpointevent2.md)など、より具体的なイベントインターフェイスは IDebugEvent2 インターフェイスから派生していませんが、代わりにと同じオブジェクトに個別のインターフェイスとして実装され `IDebugEvent2` ます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [Event](../../../extensibility/debugger/reference/idebugportevents2-event.md)
- [Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
