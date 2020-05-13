---
title: Iデバッグイベント2 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEvent2
helpviewer_keywords:
- IDebugEvent2 interface
ms.assetid: de3d714d-96fb-4e12-b66b-a75391472153
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a6341f8003b962a7f45420b076b23623ebdaf861
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80729912"
---
# <a name="idebugevent2"></a>IDebugEvent2
このインターフェイスは、ブレークポイントで停止するなどの重要なデバッグ情報と、デバッグ メッセージなどの重要でない情報の両方を通信するために使用されます。

## <a name="syntax"></a>構文

```
IDebugEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 デバッグ エンジン (DE) とカスタム ポート サプライヤーは、他のすべてのイベント インターフェイスと同じオブジェクトにこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 [イベント](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)または[イベント](../../../extensibility/debugger/reference/idebugportevents2-event.md)に指定されたインターフェイス ID (IID) 引数を使用して、セッション デバッグ マネージャー (SDM) は`IDebugEvent2`、適切なイベント インターフェイスを取得するインターフェイスで[QueryInterface](/cpp/atl/queryinterface)を呼び出します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に`IDebugEvent2`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[GetAttributes](../../../extensibility/debugger/reference/idebugevent2-getattributes.md)|このデバッグ イベントの属性を取得します。|

## <a name="remarks"></a>Remarks
 [IDebugBreakpointEvent2](../../../extensibility/debugger/reference/idebugbreakpointevent2.md)などのより具体的なイベント インターフェイスは、IDebugEvent2 インターフェイスから派生するのではなく、同じオブジェクトに対して別のインターフェイスとして実装されます`IDebugEvent2`。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [Event](../../../extensibility/debugger/reference/idebugportevents2-event.md)
- [Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
