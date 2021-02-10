---
title: 式エバリュエーター | を実装するMicrosoft Docs
description: 式を評価する方法について説明します。これには、デバッグエンジン、シンボルプロバイダー、バインダーオブジェクト、および式エバリュエーターが含まれます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- expression evaluators
- debugging [Debugging SDK], expression evaluators
ms.assetid: e9ada7be-845e-4baa-bf8f-e4890e7ba490
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 121bd17e2343cfbba509e85d78ba37b57964f895
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99947672"
---
# <a name="implement-an-expression-evaluator"></a>式エバリュエーターを実装する
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターを実装するこの方法は非推奨とされます。 CLR 式エバリュエーターの実装の詳細については、「 [clr 式](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) エバリュエーターと [マネージ式エバリュエーターサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

 式の評価は、デバッグエンジン (DE)、シンボルプロバイダー (SP)、バインダーオブジェクト、および式エバリュエーター (EE) の間での複雑なプレイです。 これら4つのコンポーネントは、1つのコンポーネントによって実装され、別のコンポーネントによって使用されるインターフェイスによって接続されます。

 EE は、文字列形式で DE から式を取得し、それを解析または評価します。 EE は、DE によって使用される次のインターフェイスを実行します。

- [IDebugExpressionEvaluator](../../extensibility/debugger/reference/idebugexpressionevaluator.md)

- [IDebugParsedExpression](../../extensibility/debugger/reference/idebugparsedexpression.md)

  EE は、DE によって提供されるバインダーオブジェクトを呼び出して、シンボルとオブジェクトの値を取得します。 EE は、DE によって実装される次のインターフェイスを使用します。

- [IDebugObject](../../extensibility/debugger/reference/idebugobject.md)

- [IDebugArrayObject](../../extensibility/debugger/reference/idebugarrayobject.md)

- [IDebugFunctionObject](../../extensibility/debugger/reference/idebugfunctionobject.md)

- [IDebugPointerObject](../../extensibility/debugger/reference/idebugpointerobject.md)

- [IDebugManagedObject](../../extensibility/debugger/reference/idebugmanagedobject.md)

- [IEnumDebugObjects](../../extensibility/debugger/reference/ienumdebugobjects.md)

- [IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md)

  EE は [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)を実行します。 `IDebugProperty2` ローカル変数、プリミティブ、または Visual Studio へのオブジェクトなど、式の評価結果を記述するための機構を提供します。これに **より、[ローカル]、**[ **ウォッチ**]、または [ **イミディエイト** ] ウィンドウに適切な情報が表示されます。

  SP は、情報を要求するときに DE によって EE に与えられます。 SP は、次のインターフェイスやその派生物などのアドレスとフィールドを記述するインターフェイスを実行します。

- [IDebugSymbolProvider](../../extensibility/debugger/reference/idebugsymbolprovider.md)

- [IDebugAddress](../../extensibility/debugger/reference/idebugaddress.md)

- [IDebugField](../../extensibility/debugger/reference/idebugfield.md)

  EE は、これらのインターフェイスのすべてを使用します。

## <a name="in-this-section"></a>このセクションの内容
 [式エバリュエーターの実装方法](../../extensibility/debugger/expression-evaluator-implementation-strategy.md) 式エバリュエーター (EE) 実装戦略の3段階のプロセスを定義します。

## <a name="see-also"></a>関連項目
- [CLR 式エバリュエーターの記述](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
