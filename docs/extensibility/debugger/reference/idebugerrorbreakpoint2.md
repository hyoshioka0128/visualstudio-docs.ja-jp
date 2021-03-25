---
description: このインターフェイスは、無効な場所、無効な式、保留中のブレークポイントがバインドされていない理由 (まだコードが読み込まれていないなど) などの、エラーまたは警告のブレークポイントを表します。
title: IDebugErrorBreakpoint2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugErrorBreakpoint2
helpviewer_keywords:
- IDebugErrorBreakpoint2 interface
ms.assetid: 1f2a4b94-3713-46e9-8272-3917187792bd
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 9c2ceedbf0fad2141f978420909d31be2260818c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105065932"
---
# <a name="idebugerrorbreakpoint2"></a>IDebugErrorBreakpoint2
このインターフェイスは、無効な場所、無効な式、保留中のブレークポイントがバインドされていない理由 (まだコードが読み込まれていないなど) などの、エラーまたは警告のブレークポイントを表します。

## <a name="syntax"></a>Syntax

```
IDebugErrorBreakpoint2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグエンジンは、ブレークポイントのサポートの一部としてこのインターフェイスを実装します。 このインターフェイスは、ブレークポイントのバインドに関する問題を報告するために使用されます。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 [GetErrorBreakpoint](../../../extensibility/debugger/reference/idebugbreakpointerrorevent2-geterrorbreakpoint.md)を呼び出すと、このインターフェイスが取得されます。 このインターフェイスは、 [Canbind](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-canbind.md)または[enumerrorbreakpoints ポイント](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumerrorbreakpoints.md)の呼び出しによって、( [IEnumDebugErrorBreakpoints2](../../../extensibility/debugger/reference/ienumdebugerrorbreakpoints2.md)インターフェイスによって表されるリストの一部として) 返すこともできます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、のメソッドを示し `IDebugErrorBreakpoint2` ます。

|メソッド|説明|
|------------|-----------------|
|[GetPendingBreakpoint](../../../extensibility/debugger/reference/idebugerrorbreakpoint2-getpendingbreakpoint.md)|エラーの原因となった保留中のブレークポイントを取得します。|
|[GetBreakpointResolution](../../../extensibility/debugger/reference/idebugerrorbreakpoint2-getbreakpointresolution.md)|エラーを説明するブレークポイントエラーの解決方法を取得します。|

## <a name="requirements"></a>要件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>こちらもご覧ください
- [IDebugBreakpointErrorEvent2](../../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md)
- [GetErrorBreakpoint](../../../extensibility/debugger/reference/idebugbreakpointerrorevent2-geterrorbreakpoint.md)
- [IEnumDebugErrorBreakpoints2](../../../extensibility/debugger/reference/ienumdebugerrorbreakpoints2.md)
- [次へ](../../../extensibility/debugger/reference/ienumdebugerrorbreakpoints2-next.md)
- [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)
- [IDebugErrorBreakpointResolution2](../../../extensibility/debugger/reference/idebugerrorbreakpointresolution2.md)
