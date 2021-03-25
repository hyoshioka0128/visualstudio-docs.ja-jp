---
description: このインターフェイスは、評価の準備ができている解析済みの式を表します。
title: IDebugParsedExpression |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugParsedExpression
helpviewer_keywords:
- IDebugParsedExpression interface
ms.assetid: be6486ed-b070-4898-95b1-58581bcb4447
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 00daeac20d621657d61aa802d79a46a3ee0e7aa7
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105084585"
---
# <a name="idebugparsedexpression"></a>IDebugParsedExpression
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターを実装するこの方法は非推奨とされます。 CLR 式エバリュエーターの実装の詳細については、「 [Clr 式](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) エバリュエーターと [マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

 このインターフェイスは、評価の準備ができている解析済みの式を表します。

## <a name="syntax"></a>Syntax

```
IDebugParsedExpression : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 式エバリュエーターは、評価の準備ができている解析済みの式を表すために、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 [Parse](../../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md)を呼び出すと、このインターフェイスが返されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表は、のメソッドを示して `IDebugParsedExpression` います。

|メソッド|説明|
|------------|-----------------|
|[EvaluateSync](../../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)|解析された式を評価します。|

## <a name="remarks"></a>注釈
 呼び出し元が式を評価する準備ができたら、 [EvaluateSync](../../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md) を呼び出して、評価の結果を含む [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) を返します。 この2つの部分から評価されるアプローチ、解析、評価を行うことで、解析された式を複数回評価できるようになり、式を解析するための時間のかかるプロセスを回避できます。

## <a name="requirements"></a>要件
 ヘッダー: ee

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>こちらもご覧ください
- [Parse](../../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md)
- [EvaluateSync](../../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
