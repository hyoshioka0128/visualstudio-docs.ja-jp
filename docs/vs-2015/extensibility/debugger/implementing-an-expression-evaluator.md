---
title: 式エバリュエーター | を実装するMicrosoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- expression evaluators
- debugging [Debugging SDK], expression evaluators
ms.assetid: e9ada7be-845e-4baa-bf8f-e4890e7ba490
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: e82e6f1fb4e6f78c7fb1f614144f9a836d9676fb
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841501"
---
# <a name="implementing-an-expression-evaluator"></a>式エバリュエーターの実装
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターを実装するこの方法は非推奨とされます。 CLR 式エバリュエーターの実装の詳細については、「 [Clr 式](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) エバリュエーターと [マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。  
  
 式を評価することは、デバッグエンジン (DE)、シンボルプロバイダー (SP)、バインダーオブジェクト、および式エバリュエーター (EE) 自体の複雑なゲームです。 これら4つのコンポーネントは、1つのコンポーネントによって実装され、別のコンポーネントによって使用されるインターフェイスによって接続されます。  
  
 EE は、文字列形式で DE から式を取得し、それを解析または評価します。 EE は、DE によって使用される次のインターフェイスを実装します。  
  
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
  
  EE は [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)を実装します。 `IDebugProperty2`ローカル変数、プリミティブ、オブジェクトなどの式の評価結果を Visual Studio に記述するための機構を提供します。これに**より、[ローカル]、[****ウォッチ**]、または [**イミディエイト**] ウィンドウに適切な情報が表示されます。  
  
  SP は、情報を要求するときに DE によって EE に与えられます。 SP は、次のインターフェイスやその派生物などのアドレスとフィールドを記述するインターフェイスを実装します。  
  
- [IDebugSymbolProvider](../../extensibility/debugger/reference/idebugsymbolprovider.md)  
  
- [IDebugAddress](../../extensibility/debugger/reference/idebugaddress.md)  
  
- [IDebugField](../../extensibility/debugger/reference/idebugfield.md)  
  
  EE は、これらのインターフェイスのすべてを使用します。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [式エバリュエーターの実装方法](../../extensibility/debugger/expression-evaluator-implementation-strategy.md)  
 式エバリュエーター (EE) 実装戦略の3段階のプロセスを定義します。  
  
## <a name="see-also"></a>参照  
 [CLR 式エバリュエーターの書き込み](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
