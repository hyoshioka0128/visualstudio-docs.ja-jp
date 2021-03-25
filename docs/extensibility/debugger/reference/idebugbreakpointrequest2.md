---
description: IDebugBreakPointRequest2 インターフェイスは、任意の種類のブレークポイントを作成およびバインドするために必要な情報を表します。
title: IDebugBreakpointRequest2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBreakpointRequest2
helpviewer_keywords:
- IDebugBreakpointRequest2 interface
ms.assetid: 01ac4013-96f9-4235-b289-f55f9e99558f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8788e7a78bcd4c03567e5d07c96a310fa6970fb1
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105054453"
---
# <a name="idebugbreakpointrequest2"></a>IDebugBreakpointRequest2
このインターフェイスは、任意の種類のブレークポイントを作成およびバインドするために必要な情報を表します。

## <a name="syntax"></a>Syntax

```
IDebugBreakpointRequest2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 通常、セッションデバッグマネージャー (SDM) は、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 デバッグエンジン (DE) は、保留中のブレークポイントを作成するために、 [Creatependingbreakpoint ポイント](../../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md) の呼び出しによってこのインターフェイスを受信します。 [Getbreakpointrequest](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-getbreakpointrequest.md)を呼び出すと、このインターフェイスを DE から取得できます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、のメソッドを示し `IDebugBreakpointRequest2` ます。

|メソッド|説明|
|------------|-----------------|
|[GetLocationType](../../../extensibility/debugger/reference/idebugbreakpointrequest2-getlocationtype.md)|このブレークポイント要求のブレークポイントの位置の種類を取得します。|
|[GetRequestInfo](../../../extensibility/debugger/reference/idebugbreakpointrequest2-getrequestinfo.md)|このブレークポイント要求を説明するブレークポイント要求情報を取得します。|

## <a name="remarks"></a>注釈
 デバッグ中のプログラムが読み込まれると、 [バインド](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md) を呼び出すと、保留中のブレークポイントがプログラム内の要求された場所にバインドされます。

## <a name="requirements"></a>要件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>こちらもご覧ください
- [CreatePendingBreakpoint](../../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md)
- [GetBreakpointRequest](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-getbreakpointrequest.md)
- [束縛](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)
