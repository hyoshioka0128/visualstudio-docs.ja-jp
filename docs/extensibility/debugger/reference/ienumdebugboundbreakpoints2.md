---
title: をクリックして、ブレークポイントを指定します。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugBoundBreakpoints2
helpviewer_keywords:
- IEnumDebugBoundBreakpoints2
ms.assetid: ea03e7e1-28d6-40b7-8097-bbb61d3b7caa
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 421d46efbef189fd6ffc86812d2bfdd28f5da5ff
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80717446"
---
# <a name="ienumdebugboundbreakpoints2"></a>IEnumDebugBoundBreakpoints2
このインターフェイスは、保留中のブレークポイントまたはブレークポイントバインドイベントに関連付けられているバインドされたブレークポイントを列挙します。

## <a name="syntax"></a>構文

```
IEnumDebugBoundBreakpoints2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 デバッグ エンジン (DE) は、ブレークポイントのサポートの一部としてこのインターフェイスを実装します。 ブレークポイントがサポートされている場合は、このインターフェイスを実装する必要があります。

## <a name="notes-for-callers"></a>発信者向けのメモ
 ビジュアル スタジオ呼び出し:

- [列挙ブレークポイント](../../../extensibility/debugger/reference/idebugbreakpointevent2-enumbreakpoints.md)トリガーされたすべてのブレークポイントのリストを表すこのインターフェイスを取得します。

- バインドされたすべてのブレークポイントのリストを表すこのインターフェイスを取得するには、[列挙型ブレークポイント](../../../extensibility/debugger/reference/idebugbreakpointboundevent2-enumboundbreakpoints.md)です。

- [列挙バインドブレークポイントは、保留中の](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumboundbreakpoints.md)ブレークポイントにバインドされているすべてのブレークポイントのリストを表すこのインターフェイスを取得します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に`IEnumDebugBoundBreakpoints2`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[次へ](../../../extensibility/debugger/reference/ienumdebugboundbreakpoints2-next.md)|列挙シーケンス内のバインドされたブレークポイントの指定した数を取得します。|
|[スキップ](../../../extensibility/debugger/reference/ienumdebugboundbreakpoints2-skip.md)|列挙シーケンス内のバインドされたブレークポイントの指定した数をスキップします。|
|[リセット](../../../extensibility/debugger/reference/ienumdebugboundbreakpoints2-reset.md)|列挙シーケンスを先頭にリセットします。|
|[複製](../../../extensibility/debugger/reference/ienumdebugboundbreakpoints2-clone.md)|現在の列挙子と同じ列挙状態を含む列挙子を作成します。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugboundbreakpoints2-getcount.md)|列挙子のバインドされたブレークポイントの数を取得します。|

## <a name="remarks"></a>Remarks
 Visual Studio では、このインターフェイスで表されるバインドされたブレークポイントを使用して、IDE のブレークポイントの表示を更新します。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [EnumBoundBreakpoints](../../../extensibility/debugger/reference/idebugbreakpointboundevent2-enumboundbreakpoints.md)
- [EnumBoundBreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumboundbreakpoints.md)
- [EnumBoundBreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumboundbreakpoints.md)
