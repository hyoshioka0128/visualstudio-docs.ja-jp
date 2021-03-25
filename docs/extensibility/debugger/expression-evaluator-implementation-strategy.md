---
title: 式エバリュエーターの実装方法 |Microsoft Docs
description: '[ローカル] ウィンドウでローカル変数を表示するコードを最初に実装して、式エバリュエーターを作成する方法について説明します。'
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- expression evaluation, implementation strategy
- debug engines, implementation strategies
ms.assetid: 1bccaeb3-8109-4128-ae79-16fd8fbbaaa2
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d10ce818e9df370b4484a0250525dbe9482b8b2c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105054986"
---
# <a name="expression-evaluator-implementation-strategy"></a>式エバリュエーターの実装方法
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターを実装するこの方法は非推奨とされます。 CLR 式エバリュエーターの実装の詳細については、「 [clr 式](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) エバリュエーターと [マネージ式エバリュエーターサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

 式エバリュエーター (EE) を迅速に作成する方法の1つは、最初 **に [ローカル] ウィンドウ** でローカル変数を表示するために必要な最小限のコードを実装することです。 [ **ローカル] ウィンドウの** 各行には、ローカル変数の名前、型、および値が表示され、3つすべてが [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) オブジェクトによって表されることに注意してください。 ローカル変数の名前、型、および値は、 `IDebugProperty2` [GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md) メソッドを呼び出すことによってオブジェクトから取得されます。 ローカル変数 **を [ローカル] ウィンドウに** 表示する方法の詳細につい [ては、「ローカル](../../extensibility/debugger/displaying-locals.md)変数の表示」を参照してください。

## <a name="discussion"></a>ディスカッション
 考えられる実装シーケンスは、 [IDebugExpressionEvaluator](../../extensibility/debugger/reference/idebugexpressionevaluator.md)の実装で始まります。 ローカルを表示するには、 [Parse](../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md) および [getmethodproperty](../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodproperty.md) メソッドを実装する必要があります。 を呼び出すと、 `IDebugExpressionEvaluator::GetMethodProperty` `IDebugProperty2` メソッド (つまり、 [IDebugMethodField](../../extensibility/debugger/reference/idebugmethodfield.md) オブジェクト) を表すオブジェクトが返されます。 メソッド自体は、[ **ローカル** ] ウィンドウには表示されません。

 次に、 [Enumchildren](../../extensibility/debugger/reference/idebugproperty2-enumchildren.md) メソッドを実装する必要があります。 デバッグエンジン (DE) は、このメソッドを呼び出して、の引数を渡してローカル変数と引数のリストを取得し `IDebugProperty2::EnumChildren` `guidFilter` `guidFilterLocalsPlusArgs` ます。 `IDebugProperty2::EnumChildren`[Enumarguments](../../extensibility/debugger/reference/idebugmethodfield-enumarguments.md)と[enumarguments](../../extensibility/debugger/reference/idebugmethodfield-enumlocals.md)を呼び出して、結果を単一の列挙に結合します。 詳細については、「 [ローカルの表示](../../extensibility/debugger/displaying-locals.md) 」を参照してください。

## <a name="see-also"></a>こちらもご覧ください
- [式エバリュエーターを実装する](../../extensibility/debugger/implementing-an-expression-evaluator.md)
- [ローカルの表示](../../extensibility/debugger/displaying-locals.md)
