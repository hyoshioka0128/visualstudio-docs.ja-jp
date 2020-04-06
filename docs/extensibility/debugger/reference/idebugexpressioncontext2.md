---
title: をクリックします。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExpressionContext2
helpviewer_keywords:
- IDebugExpressionContext2 interface
ms.assetid: 577fdaae-4b2d-4112-9839-ab899535fa6f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 344ae287b3784ceca87fbbab09ad2b2e0a304205
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80729643"
---
# <a name="idebugexpressioncontext2"></a>IDebugExpressionContext2
このインターフェイスは、式の評価のコンテキストを表します。

## <a name="syntax"></a>構文

```
IDebugExpressionContext2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 デバッグ エンジン (DE) は、式を評価できるコンテキストを表すために、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 [呼](../../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md)び出しは、このインターフェイスを返します。 このインターフェイスは、デバッグ中のプログラムが一時停止され、スタック フレームが使用可能な場合にのみアクセスできます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に`IDebugExpressionContext2`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[GetName](../../../extensibility/debugger/reference/idebugexpressioncontext2-getname.md)|評価コンテキストの名前を取得します。|
|[ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)|評価用のテキスト ベースの式を解析します。|

## <a name="remarks"></a>Remarks
 評価コンテキストは、式評価を実行するためのスコープと考えることができます。

 プログラムが停止すると、セッション デバッグ マネージャー (SDM) は、呼び出しを使用して DE からスタック フレームを[取得 EnumFrameInfo。](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md) SDM は、インターフェイス[を取得するために GetExpressionContext](../../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md)を呼び出します`IDebugExpressionContext2`。 その後[、ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)を呼び出して[IDebugExpression2](../../../extensibility/debugger/reference/idebugexpression2.md)インターフェイスを作成します。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [GetExpressionContext](../../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md)
- [IDebugExpression2](../../../extensibility/debugger/reference/idebugexpression2.md)
