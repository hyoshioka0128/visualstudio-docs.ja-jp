---
title: IDebug バウンドブレークポイント2 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBoundBreakpoint2
helpviewer_keywords:
- IDebugBoundBreakpoint2 interface
ms.assetid: df33c52e-ded2-48a0-951d-1f36c8fc922e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f4d22b10085baefeb3a0286c1b4edcb5876c0dac
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80735429"
---
# <a name="idebugboundbreakpoint2"></a>IDebugBoundBreakpoint2
このインターフェイスは、コードの場所にバインドされているブレークポイントを表します。

## <a name="syntax"></a>構文

```
IDebugBoundBreakpoint2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 デバッグ エンジン (DE) は、ブレークポイントのサポートの一部としてこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 [Bind](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)の呼び出しは、このインターフェイスを作成します。 [ブレークポイントの取得](../../../extensibility/debugger/reference/idebugbreakpointunboundevent2-getbreakpoint.md)と[次](../../../extensibility/debugger/reference/ienumdebugboundbreakpoints2-next.md)の呼び出しもこのインターフェイスを取得できます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に`IDebugBoundBreakpoint2`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[GetPendingBreakpoint](../../../extensibility/debugger/reference/idebugboundbreakpoint2-getpendingbreakpoint.md)|指定されたバインドされたブレークポイントの作成元の保留中のブレークポイントを取得します。|
|[Getstate](../../../extensibility/debugger/reference/idebugboundbreakpoint2-getstate.md)|このバインドされたブレークポイントの状態を取得します。|
|[GetHitCount](../../../extensibility/debugger/reference/idebugboundbreakpoint2-gethitcount.md)|このバインドされたブレークポイントの現在のヒット カウントを取得します。|
|[GetBreakpointResolution](../../../extensibility/debugger/reference/idebugboundbreakpoint2-getbreakpointresolution.md)|このブレークポイントを記述するブレークポイントの解像度を取得します。|
|[有効化](../../../extensibility/debugger/reference/idebugboundbreakpoint2-enable.md)|ブレークポイントを有効または無効にします。|
|[SetHitCount](../../../extensibility/debugger/reference/idebugboundbreakpoint2-sethitcount.md)|このバインドされたブレークポイントのヒット カウントを設定します。|
|[SetCondition](../../../extensibility/debugger/reference/idebugboundbreakpoint2-setcondition.md)|このバインドされたブレークポイントに関連付けられている条件を設定または変更します。|
|[SetPassCount](../../../extensibility/debugger/reference/idebugboundbreakpoint2-setpasscount.md)|このバインドされたブレークポイントに関連付けられているパスカウントを設定または変更します。|
|[削除](../../../extensibility/debugger/reference/idebugboundbreakpoint2-delete.md)|ブレークポイントを削除します。|

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [GetBreakpoint](../../../extensibility/debugger/reference/idebugbreakpointunboundevent2-getbreakpoint.md)
- [次へ](../../../extensibility/debugger/reference/ienumdebugboundbreakpoints2-next.md)
- [Bind](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)
