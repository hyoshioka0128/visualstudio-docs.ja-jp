---
title: IDebugBreakpointRequest2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBreakpointRequest2
helpviewer_keywords:
- IDebugBreakpointRequest2 interface
ms.assetid: 01ac4013-96f9-4235-b289-f55f9e99558f
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d31b7cfe2480fa3b16a4d3c8c08185194fec6b79
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99951200"
---
# <a name="idebugbreakpointrequest2"></a>IDebugBreakpointRequest2
このインターフェイスは、任意の種類のブレークポイントを作成およびバインドするために必要な情報を表します。

## <a name="syntax"></a>構文

```
IDebugBreakpointRequest2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 通常、セッションデバッグマネージャー (SDM) は、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 デバッグエンジン (DE) は、保留中のブレークポイントを作成するために、 [Creatependingbreakpoint ポイント](../../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md) の呼び出しによってこのインターフェイスを受信します。 [Getbreakpointrequest](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-getbreakpointrequest.md)を呼び出すと、このインターフェイスを DE から取得できます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、のメソッドを示し `IDebugBreakpointRequest2` ます。

|Method|説明|
|------------|-----------------|
|[GetLocationType](../../../extensibility/debugger/reference/idebugbreakpointrequest2-getlocationtype.md)|このブレークポイント要求のブレークポイントの位置の種類を取得します。|
|[GetRequestInfo](../../../extensibility/debugger/reference/idebugbreakpointrequest2-getrequestinfo.md)|このブレークポイント要求を説明するブレークポイント要求情報を取得します。|

## <a name="remarks"></a>解説
 デバッグ中のプログラムが読み込まれると、 [バインド](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md) を呼び出すと、保留中のブレークポイントがプログラム内の要求された場所にバインドされます。

## <a name="requirements"></a>要件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [CreatePendingBreakpoint](../../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md)
- [GetBreakpointRequest](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-getbreakpointrequest.md)
- [束縛](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)
