---
title: IDebugBreakpointResolution2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBreakpointResolution2
helpviewer_keywords:
- IDebugBreakpointRequest2 interface
ms.assetid: 451d5bce-b9c1-48ff-beaa-2b4c3e1ceea0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: bb5e4f9e32017cfb493aae00a24f9f8184605d1d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80734750"
---
# <a name="idebugbreakpointresolution2"></a>IDebugBreakpointResolution2
このインターフェイスは、バインドされたブレークポイントを説明する情報を表します。

## <a name="syntax"></a>構文

```
IDebugBreakpointResolution2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグエンジン (DE) は、ブレークポイントのサポートの一部としてこのインターフェイスを実装します。 このインターフェイスは、ユーザーがブレークポイントのプロパティを表示するときにセッションデバッグマネージャーが使用するバインドされたブレークポイントの説明を提供します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 [Getbreakpointresolution](../../../extensibility/debugger/reference/idebugboundbreakpoint2-getbreakpointresolution.md)を呼び出すと、このインターフェイスが返されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、のメソッドを示し `IDebugBreakpointResolution2` ます。

|Method|説明|
|------------|-----------------|
|[GetBreakpointType](../../../extensibility/debugger/reference/idebugbreakpointresolution2-getbreakpointtype.md)|この解像度によって表されるブレークポイントの型を取得します。|
|[GetResolutionInfo](../../../extensibility/debugger/reference/idebugbreakpointresolution2-getresolutioninfo.md)|このブレークポイントを説明するブレークポイントの解決情報を取得します。|

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [GetBreakpointResolution](../../../extensibility/debugger/reference/idebugboundbreakpoint2-getbreakpointresolution.md)
