---
title: エラーブレークポイント2をデバッグする |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugErrorBreakpoint2
helpviewer_keywords:
- IDebugErrorBreakpoint2 interface
ms.assetid: 1f2a4b94-3713-46e9-8272-3917187792bd
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 17b20d0f3545b0f7266ad6d0c6423d581233dd3c
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80730085"
---
# <a name="idebugerrorbreakpoint2"></a>IDebugErrorBreakpoint2
このインターフェイスは、無効な場所、無効な式、保留中のブレークポイントがバインドされていない理由 (コードがまだ読み込まれていないなど) などのエラーまたは警告のブレークポイントを表します。

## <a name="syntax"></a>構文

```
IDebugErrorBreakpoint2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 デバッグ エンジンは、ブレークポイントのサポートの一部としてこのインターフェイスを実装します。 このインターフェイスは、ブレークポイントのバインドに関する問題を報告するために使用されます。

## <a name="notes-for-callers"></a>発信者向けのメモ
 [呼](../../../extensibility/debugger/reference/idebugbreakpointerrorevent2-geterrorbreakpoint.md)び出しは、このインターフェイスを取得します。 このインターフェイスは[、CanBind](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-canbind.md)または列挙エラー[ブレークポイント](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumerrorbreakpoints.md)の呼び出しによって[(IEnumDebugErrorBreakpoints2](../../../extensibility/debugger/reference/ienumdebugerrorbreakpoints2.md)インターフェイスによって表されるリストの一部として) 返すこともできます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に`IDebugErrorBreakpoint2`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[GetPendingBreakpoint](../../../extensibility/debugger/reference/idebugerrorbreakpoint2-getpendingbreakpoint.md)|エラーの原因となった保留中のブレークポイントを取得します。|
|[GetBreakpointResolution](../../../extensibility/debugger/reference/idebugerrorbreakpoint2-getbreakpointresolution.md)|エラーを記述するブレークポイント エラー解決を取得します。|

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [IDebugBreakpointErrorEvent2](../../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md)
- [GetErrorBreakpoint](../../../extensibility/debugger/reference/idebugbreakpointerrorevent2-geterrorbreakpoint.md)
- [IEnumDebugErrorBreakpoints2](../../../extensibility/debugger/reference/ienumdebugerrorbreakpoints2.md)
- [次へ](../../../extensibility/debugger/reference/ienumdebugerrorbreakpoints2-next.md)
- [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)
- [IDebugErrorBreakpointResolution2](../../../extensibility/debugger/reference/idebugerrorbreakpointresolution2.md)
