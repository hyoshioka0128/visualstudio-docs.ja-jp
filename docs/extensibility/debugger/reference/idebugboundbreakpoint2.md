---
description: このインターフェイスは、コードの場所にバインドされているブレークポイントを表します。
title: IDebugBoundBreakpoint2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBoundBreakpoint2
helpviewer_keywords:
- IDebugBoundBreakpoint2 interface
ms.assetid: df33c52e-ded2-48a0-951d-1f36c8fc922e
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c2726a2422c49335d9c95e7d500381ad1fdc0108
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102167478"
---
# <a name="idebugboundbreakpoint2"></a>IDebugBoundBreakpoint2
このインターフェイスは、コードの場所にバインドされているブレークポイントを表します。

## <a name="syntax"></a>構文

```
IDebugBoundBreakpoint2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグエンジン (DE) は、ブレークポイントのサポートの一部としてこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 [Bind](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)を呼び出すと、このインターフェイスが作成されます。 [Getbreakpoint ポイント](../../../extensibility/debugger/reference/idebugbreakpointunboundevent2-getbreakpoint.md)と[次](../../../extensibility/debugger/reference/ienumdebugboundbreakpoints2-next.md)の呼び出しは、このインターフェイスを取得することもできます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、のメソッドを示し `IDebugBoundBreakpoint2` ます。

|メソッド|説明|
|------------|-----------------|
|[GetPendingBreakpoint](../../../extensibility/debugger/reference/idebugboundbreakpoint2-getpendingbreakpoint.md)|指定したバインドされたブレークポイントが作成された、保留中のブレークポイントを取得します。|
|[GetState](../../../extensibility/debugger/reference/idebugboundbreakpoint2-getstate.md)|このバインドされたブレークポイントの状態を取得します。|
|[GetHitCount](../../../extensibility/debugger/reference/idebugboundbreakpoint2-gethitcount.md)|このバインドされたブレークポイントの現在のヒットカウントを取得します。|
|[GetBreakpointResolution](../../../extensibility/debugger/reference/idebugboundbreakpoint2-getbreakpointresolution.md)|このブレークポイントを説明するブレークポイントの解決を取得します。|
|[有効化](../../../extensibility/debugger/reference/idebugboundbreakpoint2-enable.md)|ブレークポイントを有効または無効にします。|
|[SetHitCount](../../../extensibility/debugger/reference/idebugboundbreakpoint2-sethitcount.md)|このバインドされたブレークポイントのヒットカウントを設定します。|
|[SetCondition](../../../extensibility/debugger/reference/idebugboundbreakpoint2-setcondition.md)|このバインドされたブレークポイントに関連付けられている条件を設定または変更します。|
|[SetPassCount](../../../extensibility/debugger/reference/idebugboundbreakpoint2-setpasscount.md)|このバインドされたブレークポイントに関連付けられているパスカウントを設定または変更します。|
|[削除](../../../extensibility/debugger/reference/idebugboundbreakpoint2-delete.md)|ブレークポイントを削除します。|

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [GetBreakpoint](../../../extensibility/debugger/reference/idebugbreakpointunboundevent2-getbreakpoint.md)
- [次へ](../../../extensibility/debugger/reference/ienumdebugboundbreakpoints2-next.md)
- [束縛](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)
