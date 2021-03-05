---
description: このインターフェイスは、バインドおよび評価の準備ができている解析済みの式を表します。
title: IDebugExpression2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExpression2
helpviewer_keywords:
- IDebugExpression2 interface
ms.assetid: f5e4b124-1e30-47c8-a511-80084a02dba5
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 6fe6a6955f5d8d4ae42d51e3623b0c4f966dc416
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102152664"
---
# <a name="idebugexpression2"></a>IDebugExpression2
このインターフェイスは、バインドおよび評価の準備ができている解析済みの式を表します。

## <a name="syntax"></a>構文

```
IDebugExpression2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグエンジン (DE) は、評価の準備ができている解析済みの式を表すために、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 [Parsetext](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)を呼び出すと、このインターフェイスが返されます。 [Get式コンテキスト](../../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md) は、 [IDebugExpressionContext2](../../../extensibility/debugger/reference/idebugexpressioncontext2.md) インターフェイスを返します。 これらのインターフェイスは、デバッグ中のプログラムが一時停止され、スタックフレームが使用可能な場合にのみアクセスできます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、のメソッドを示し `IDebugExpression2` ます。

|メソッド|説明|
|------------|-----------------|
|[EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)|この式を非同期的に評価します。|
|[中止](../../../extensibility/debugger/reference/idebugexpression2-abort.md)|非同期式の評価を終了します。|
|[EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)|この式を同期的に評価します。|

## <a name="remarks"></a>解説
 プログラムが停止されると、セッションデバッグマネージャー (SDM) は、 [enumframe info](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)を呼び出すことで、DE からスタックフレームを取得します。 次に、SDM は [Get式コンテキスト](../../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md) を呼び出して、 [IDebugExpressionContext2](../../../extensibility/debugger/reference/idebugexpressioncontext2.md) インターフェイスを取得します。 この後に、 [Parsetext](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) を呼び出して、評価の `IDebugExpression2` 準備ができている解析済みの式を表すインターフェイスを作成します。

 SDM は、式を実際に評価して値を生成するために、 [EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) または [evaluateasync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md) を呼び出します。

 の実装では `IDebugExpressionContext2::ParseText` 、DE は COM の `CoCreateInstance` 関数を使用して式エバリュエーターをインスタンス化し、 [IDebugExpressionEvaluator](../../../extensibility/debugger/reference/idebugexpressionevaluator.md) インターフェイスを取得します (インターフェイスの例を参照してください `IDebugExpressionEvaluator` )。 次に、DE は [Parse](../../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md) を呼び出して、 [IDebugParsedExpression](../../../extensibility/debugger/reference/idebugparsedexpression.md) インターフェイスを取得します。 このインターフェイスは、およびの実装で `IDebugExpression2::EvaluateSync` `IDebugExpression2::EvaluateAsync` 評価を実行するために使用されます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [GetExpression](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2-getexpression.md)
