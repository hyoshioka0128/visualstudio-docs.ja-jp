---
title: 式エバリュエーターの実装方法 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- expression evaluation, implementation strategy
- debug engines, implementation strategies
ms.assetid: 1bccaeb3-8109-4128-ae79-16fd8fbbaaa2
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a9c2ded111c371fc1a42c8f1ee08769f5b06aeda
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90842113"
---
# <a name="expression-evaluator-implementation-strategy"></a>式エバリュエーターの実装方法
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターを実装するこの方法は非推奨とされます。 CLR 式エバリュエーターの実装の詳細については、「 [Clr 式](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) エバリュエーターと [マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。  
  
 式エバリュエーター (EE) を迅速に作成する方法の1つは、最初 **に [ローカル] ウィンドウ** でローカル変数を表示するために必要な最小限のコードを実装することです。 [ **ローカル] ウィンドウの** 各行には、ローカル変数の名前、型、および値が表示され、3つすべてが [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) オブジェクトによって表されることに注意してください。 ローカル変数の名前、型、および値は、 `IDebugProperty2` [GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md) メソッドを呼び出すことによって、オブジェクトから取得できます。 ローカル変数 **を [ローカル] ウィンドウに** 表示する方法の詳細につい [ては、「ローカル](../../extensibility/debugger/displaying-locals.md)変数の表示」を参照してください。  
  
## <a name="discussion"></a>考察 (Discussion)  
 考えられる実装シーケンスは、 [IDebugExpressionEvaluator](../../extensibility/debugger/reference/idebugexpressionevaluator.md)の実装で始まります。 ローカルを表示するには、 [Parse](../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md) および [getmethodproperty](../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodproperty.md) メソッドを実装する必要があります。 を呼び出すと、 `IDebugExpressionEvaluator::GetMethodProperty` `IDebugProperty2` メソッド (つまり、 [IDebugMethodField](../../extensibility/debugger/reference/idebugmethodfield.md) オブジェクト) を表すオブジェクトが返されます。 メソッド自体は、[ **ローカル** ] ウィンドウには表示されません。  
  
 次に、 [Enumchildren](../../extensibility/debugger/reference/idebugproperty2-enumchildren.md) メソッドを実装する必要があります。 デバッグエンジン (DE) は、このメソッドを呼び出して、の引数を渡してローカル変数と引数のリストを取得し `IDebugProperty2::EnumChildren` `guidFilter` `guidFilterLocalsPlusArgs` ます。 `IDebugProperty2::EnumChildren`[Enumarguments](../../extensibility/debugger/reference/idebugmethodfield-enumarguments.md)と[enumarguments](../../extensibility/debugger/reference/idebugmethodfield-enumlocals.md)を呼び出して、結果を単一の列挙に結合します。 詳細については、「 [ローカルの表示](../../extensibility/debugger/displaying-locals.md) 」を参照してください。  
  
## <a name="see-also"></a>参照  
 [式エバリュエーターの実装](../../extensibility/debugger/implementing-an-expression-evaluator.md)   
 [ローカルの表示](../../extensibility/debugger/displaying-locals.md)
