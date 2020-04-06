---
title: を使用する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExpression2
helpviewer_keywords:
- IDebugExpression2 interface
ms.assetid: f5e4b124-1e30-47c8-a511-80084a02dba5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c2e23ad4f673e4e150ea677d993c5b36a4e386c2
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80729695"
---
# <a name="idebugexpression2"></a>IDebugExpression2
このインターフェイスは、バインディングと評価の準備が整った解析済み式を表します。

## <a name="syntax"></a>構文

```
IDebugExpression2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 デバッグ エンジン (DE) は、解析された式を評価する準備が整った式を表すために、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 呼び出し[は、](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)このインターフェイスを返します。 [インターフェイス](../../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md)[を返](../../../extensibility/debugger/reference/idebugexpressioncontext2.md)します。 これらのインターフェイスは、デバッグ中のプログラムが一時停止され、スタック フレームが使用可能な場合にのみアクセスできます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に`IDebugExpression2`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)|この式を非同期的に評価します。|
|[中止](../../../extensibility/debugger/reference/idebugexpression2-abort.md)|非同期式の評価を終了します。|
|[EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)|この式を同期的に評価します。|

## <a name="remarks"></a>Remarks
 プログラムが停止すると、セッション デバッグ マネージャー (SDM) は、呼び出しを使用して DE からスタック フレームを[取得 EnumFrameInfo。](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md) その後、SDM は、インターフェイスを取得するために[GetExpressionContext](../../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md) [を](../../../extensibility/debugger/reference/idebugexpressioncontext2.md)呼び出します。 その後[、ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)を呼び出してインターフェイス`IDebugExpression2`を作成します。

 SDM は、式を実際に評価して値を生成するために[、EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)または[EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)を呼び出します。

 `IDebugExpressionContext2::ParseText`の実装では、DE は COM の`CoCreateInstance`関数を使用して式エバリュエーターをインスタンス化し[、IDebugExpressionEvaluator](../../../extensibility/debugger/reference/idebugexpressionevaluator.md)インターフェイス`IDebugExpressionEvaluator`を取得します (インターフェイスの例を参照)。 その後、DE は[パース](../../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md)を呼び出して[IDebugParsedExpression](../../../extensibility/debugger/reference/idebugparsedexpression.md)インターフェイスを取得します。 このインターフェイスは、評価の実装`IDebugExpression2::EvaluateSync`および`IDebugExpression2::EvaluateAsync`評価を実行するために使用されます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [GetExpression](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2-getexpression.md)
