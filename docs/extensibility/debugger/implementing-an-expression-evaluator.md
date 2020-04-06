---
title: 式エバリュエーターの実装 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- expression evaluators
- debugging [Debugging SDK], expression evaluators
ms.assetid: e9ada7be-845e-4baa-bf8f-e4890e7ba490
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a8c7c9a1130794dd4c28f212afd6cb3c030f5a1b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738545"
---
# <a name="implement-an-expression-evaluator"></a>式エバリュエーターの実装
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターのこの実装方法は非推奨になりました。 CLR 式エバリュエーターの実装については[、「CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) 」および「[マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

 式の評価は、デバッグ エンジン (DE)、シンボル プロバイダー (SP)、バインダー オブジェクト、および式エバリュエーター (EE) 間の複雑な相互作用です。 これらの 4 つのコンポーネントは、1 つのコンポーネントによって実装され、別のコンポーネントによって使用されるインターフェイスによって接続されます。

 EE は、DE から文字列の形式で式を取得し、それを解析または評価します。 EE は、DE によって消費される次のインターフェイスを実行します。

- [IDebugExpressionEvaluator](../../extensibility/debugger/reference/idebugexpressionevaluator.md)

- [IDebugParsedExpression](../../extensibility/debugger/reference/idebugparsedexpression.md)

  EE は、DE によって提供されるバインダー・オブジェクトを呼び出して、シンボルとオブジェクトの値を取得します。 EE は、DE によって実装される次のインターフェイスを使用します。

- [IDebugObject](../../extensibility/debugger/reference/idebugobject.md)

- [IDebugArrayObject](../../extensibility/debugger/reference/idebugarrayobject.md)

- [IDebugFunctionObject](../../extensibility/debugger/reference/idebugfunctionobject.md)

- [IDebugPointerObject](../../extensibility/debugger/reference/idebugpointerobject.md)

- [IDebugManagedObject](../../extensibility/debugger/reference/idebugmanagedobject.md)

- [IEnumDebugObjects](../../extensibility/debugger/reference/ienumdebugobjects.md)

- [IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md)

  EE は[IDebugProperty2 を](../../extensibility/debugger/reference/idebugproperty2.md)実行します。 `IDebugProperty2`には、ローカル変数、プリミティブ、または Visual Studio のオブジェクトなどの式の評価の**結果を記述**するための機構が用意されています。 **Locals** **Immediate**

  SPは、情報を求めるとDEによってEEに渡されます。 SPは、次のインタフェースとその派生物など、アドレスとフィールドを記述するインタフェースを実行します。

- [IDebugSymbolProvider](../../extensibility/debugger/reference/idebugsymbolprovider.md)

- [IDebugAddress](../../extensibility/debugger/reference/idebugaddress.md)

- [IDebugField](../../extensibility/debugger/reference/idebugfield.md)

  EE は、これらのインターフェイスをすべて使用します。

## <a name="in-this-section"></a>このセクションの内容
 [式エバリュエーター実装戦略](../../extensibility/debugger/expression-evaluator-implementation-strategy.md)式エバリュエーター (EE) 実装戦略の 3 段階のプロセスを定義します。

## <a name="see-also"></a>関連項目
- [CLR 式エバリュエーターの記述](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
