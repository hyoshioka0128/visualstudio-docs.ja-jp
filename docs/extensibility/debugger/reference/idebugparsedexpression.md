---
title: 式を解析する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugParsedExpression
helpviewer_keywords:
- IDebugParsedExpression interface
ms.assetid: be6486ed-b070-4898-95b1-58581bcb4447
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 22069b8eedb06d67eafaf7333f379a057c1b6f23
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80726000"
---
# <a name="idebugparsedexpression"></a>IDebugParsedExpression
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターのこの実装方法は非推奨になりました。 CLR 式エバリュエーターの実装については、「 [CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)と[マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

 このインターフェイスは、解析済みの式を評価する準備が整った式を表します。

## <a name="syntax"></a>構文

```
IDebugParsedExpression : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 式エバリュエーターは、評価の準備が整った解析済み式を表すために、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 [Parse](../../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md)の呼び出しは、このインターフェイスを返します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、 の`IDebugParsedExpression`方法を示します。

|Method|説明|
|------------|-----------------|
|[EvaluateSync](../../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)|解析された式を評価します。|

## <a name="remarks"></a>Remarks
 呼び出し元が式を評価する準備ができたら[、EvaluateSync](../../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)を呼び出して評価結果を含む[IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)を返します。 この 2 つの部分から構成される評価方法、解析後の評価では、解析された式を複数回評価し、時間のかかる式の解析プロセスをバイパスします。

## <a name="requirements"></a>必要条件
 ヘッダー: ee.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [解析](../../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md)
- [EvaluateSync](../../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
