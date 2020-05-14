---
title: Iデバッグ保留中のブレークポイント2 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPendingBreakpoint2
helpviewer_keywords:
- IDebugPendingBreakpoint2 interface
ms.assetid: d416b095-917e-475e-b796-ec0a03ffb8da
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4e6f2c1df37e953a5d8c66bad9d0a3574a463fad
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80725644"
---
# <a name="idebugpendingbreakpoint2"></a>IDebugPendingBreakpoint2
このインターフェイスは、コードの場所にバインドする準備ができたブレークポイントを表します。

## <a name="syntax"></a>構文

```
IDebugPendingBreakpoint2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 デバッグ エンジン (DE) は、ブレークポイントのサポートの一部としてこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 呼び出しは[、IDebugBreakpointRequest2](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md)インターフェイスから保留中のブレークポイントを作成します。 [CreatePendingBreakpoint](../../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md) [Bind](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)の呼び出`IDebugBreakpoint2`しは、プログラム内のバインドされたブレークポイントを表すインターフェイスを作成します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に`IDebugPendingBreakpoint2`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[CanBind](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-canbind.md)|この保留中のブレークポイントがコードの場所にバインドできるかどうかを判断します。|
|[Bind](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)|この保留中のブレークポイントを 1 つ以上のコードの場所にバインドします。|
|[Getstate](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-getstate.md)|この保留中のブレークポイントの状態を取得します。|
|[GetBreakpointRequest](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-getbreakpointrequest.md)|この保留中のブレークポイントの作成に使用されたブレークポイント要求を取得します。|
|[仮想](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-virtualize.md)|この保留中のブレークポイントの仮想化状態を切り替えます。|
|[有効化](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enable.md)|この保留中のブレークポイントの有効な状態を切り替えます。|
|[SetCondition](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-setcondition.md)|この保留中のブレークポイントに関連付けられている条件を設定または変更します。|
|[SetPassCount](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-setpasscount.md)|この保留中のブレークポイントに関連付けられているパス数を設定または変更します。|
|[EnumBoundBreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumboundbreakpoints.md)|この保留中のブレークポイントからバインドされているすべてのブレークポイントを列挙します。|
|[EnumErrorBreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumerrorbreakpoints.md)|この保留中のブレークポイントから発生したすべてのエラー ブレークポイントを列挙します。|
|[削除](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-delete.md)|この保留中のブレークポイントと、そこからバインドされているすべてのブレークポイントを削除します。|

## <a name="remarks"></a>Remarks
 `IDebugPendingBreakpoint2`1 つまたは複数のプログラムに適用できるコードにブレークポイントをバインドするために必要なすべての情報のプロバイダーと考えることができます。

 保留中のブレークポイントは、バインドされた複数のブレークポイントを生成する可能性があります。 たとえば、C++ スタイルのテンプレートのブレークポイントは、そのテンプレートの一意のインスタンスごとにバインドされたブレークポイントを生成できます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [CreatePendingBreakpoint](../../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md)
- [GetPendingBreakpoint](../../../extensibility/debugger/reference/idebugbreakpointboundevent2-getpendingbreakpoint.md)
- [GetPendingBreakpoint](../../../extensibility/debugger/reference/idebugboundbreakpoint2-getpendingbreakpoint.md)
- [GetPendingBreakpoint](../../../extensibility/debugger/reference/idebugerrorbreakpoint2-getpendingbreakpoint.md)
