---
description: このインターフェイスは、保留中のブレークポイントまたはブレークポイントバインドイベントに関連付けられているバインドされたブレークポイントを列挙します。
title: IEnumDebugBoundBreakpoints2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugBoundBreakpoints2
helpviewer_keywords:
- IEnumDebugBoundBreakpoints2
ms.assetid: ea03e7e1-28d6-40b7-8097-bbb61d3b7caa
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d6942bb8388afd596221325f86c3934b684af6f9
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105080191"
---
# <a name="ienumdebugboundbreakpoints2"></a>IEnumDebugBoundBreakpoints2
このインターフェイスは、保留中のブレークポイントまたはブレークポイントバインドイベントに関連付けられているバインドされたブレークポイントを列挙します。

## <a name="syntax"></a>Syntax

```
IEnumDebugBoundBreakpoints2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグエンジン (DE) は、ブレークポイントのサポートの一部としてこのインターフェイスを実装します。 ブレークポイントがサポートされている場合は、このインターフェイスを実装する必要があります。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 Visual Studio の呼び出し:

- [Enumbreakpoints](../../../extensibility/debugger/reference/idebugbreakpointevent2-enumbreakpoints.md) ポイントは、トリガーされたすべてのブレークポイントのリストを表すこのインターフェイスを取得します。

- [Enumboundbreakpoints ポイント](../../../extensibility/debugger/reference/idebugbreakpointboundevent2-enumboundbreakpoints.md) は、バインドされたすべてのブレークポイントのリストを表すこのインターフェイスを取得します。

- [Enumboundbreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumboundbreakpoints.md) ポイントは、保留中のブレークポイントにバインドされているすべてのブレークポイントのリストを表すこのインターフェイスを取得します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、のメソッドを示し `IEnumDebugBoundBreakpoints2` ます。

|メソッド|説明|
|------------|-----------------|
|[次へ](../../../extensibility/debugger/reference/ienumdebugboundbreakpoints2-next.md)|列挙シーケンス内の指定した数のバインドされたブレークポイントを取得します。|
|[Skip](../../../extensibility/debugger/reference/ienumdebugboundbreakpoints2-skip.md)|列挙シーケンス内の指定した数のバインドされたブレークポイントをスキップします。|
|[リセット](../../../extensibility/debugger/reference/ienumdebugboundbreakpoints2-reset.md)|列挙シーケンスを先頭にリセットします。|
|[複製](../../../extensibility/debugger/reference/ienumdebugboundbreakpoints2-clone.md)|現在の列挙子と同じ列挙状態を含む列挙子を作成します。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugboundbreakpoints2-getcount.md)|列挙子内のバインドされたブレークポイントの数を取得します。|

## <a name="remarks"></a>注釈
 Visual Studio では、このインターフェイスによって表されるバインドされたブレークポイントを使用して、IDE 内のブレークポイントの表示を更新します。

## <a name="requirements"></a>要件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>こちらもご覧ください
- [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [EnumBoundBreakpoints](../../../extensibility/debugger/reference/idebugbreakpointboundevent2-enumboundbreakpoints.md)
- [EnumBoundBreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumboundbreakpoints.md)
- [EnumBoundBreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumboundbreakpoints.md)
