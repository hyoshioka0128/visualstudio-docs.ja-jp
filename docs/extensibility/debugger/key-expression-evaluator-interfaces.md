---
title: キー式エバリュエーターインターフェイス |Microsoft Docs
description: 評価コンテキストと共に、式エバリュエーターを記述するときに理解しておく必要があるインターフェイスについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], expression evaluation
- expression evaluation, interfaces
ms.assetid: 1cac9aa3-0867-4e12-a16e-1e90abbc0fb6
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 95c32b76893e0de7f31e56df81bf12c831452bfe
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99945930"
---
# <a name="key-expression-evaluator-interfaces"></a>キー式エバリュエーターインターフェイス
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターを実装するこの方法は非推奨とされます。 CLR 式エバリュエーターの実装の詳細については、「 [clr 式](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) エバリュエーターと [マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

 評価コンテキストと共に式エバリュエーター (EE) を記述する場合は、次のインターフェイスについて理解しておく必要があります。

## <a name="interface-descriptions"></a>インターフェイスの説明

- [IDebugAddress](../../extensibility/debugger/reference/idebugaddress.md)

     には、 [Getaddress](../../extensibility/debugger/reference/idebugaddress-getaddress.md)という1つのメソッドがあります。このメソッドは、現在の実行ポイントを表すデータ構造を取得します。 このデータ構造は、式を評価するためにデバッグエンジン (DE) が [EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md) メソッドに渡す3つの引数のうちの1つです。 このインターフェイスは、通常、シンボルプロバイダーによって実装されます。

- [IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md)

     には、 [バインド](../../extensibility/debugger/reference/idebugbinder-bind.md) メソッドがあります。これは、シンボルの現在の値を含むメモリ領域を取得します。 [IDebugObject](../../extensibility/debugger/reference/idebugobject.md)オブジェクトによって表される外側のメソッドと、 [IDebugField](../../extensibility/debugger/reference/idebugfield.md)オブジェクトによって表されるシンボル自体の両方を指定すると、 `IDebugBinder::Bind` シンボルの値が返されます。 `IDebugBinder` は通常、DE によって実装されます。

- [IDebugField](../../extensibility/debugger/reference/idebugfield.md)

     単純データ型を表します。 配列やメソッドなどのより複雑な型については、それぞれ derived [IDebugArrayField](../../extensibility/debugger/reference/idebugarrayfield.md) インターフェイスと [IDebugMethodField](../../extensibility/debugger/reference/idebugmethodfield.md) インターフェイスを使用します。 [IDebugContainerField](../../extensibility/debugger/reference/idebugcontainerfield.md) は、メソッドやクラスなどの他のシンボルを含むシンボルを表すもう1つの重要な派生インターフェイスです。 `IDebugField`インターフェイス (およびその派生元) は、通常、シンボルプロバイダーによって実装されます。

     `IDebugField`オブジェクトを使用すると、シンボルの名前と型を検索できます。また、 [IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md)オブジェクトと共に使用して、その値を検索することもできます。

- [IDebugObject](../../extensibility/debugger/reference/idebugobject.md)

     シンボルの実行時の値の実際のビットを表します。 [Bind](../../extensibility/debugger/reference/idebugbinder-bind.md) は、シンボルを表す [IDebugField](../../extensibility/debugger/reference/idebugfield.md) オブジェクトを受け取り、 [IDebugObject](../../extensibility/debugger/reference/idebugobject.md) オブジェクトを返します。 [GetValue](../../extensibility/debugger/reference/idebugobject-getvalue.md)メソッドは、メモリバッファー内のシンボルの値を返します。 通常、DE は、メモリ内のプロパティの値を表すために、このインターフェイスを実装します。

- [IDebugExpressionEvaluator](../../extensibility/debugger/reference/idebugexpressionevaluator.md)

     このインターフェイスは、式エバリュエーター自体を表します。 キーメソッドは [Parse](../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md)で、 [IDebugParsedExpression](../../extensibility/debugger/reference/idebugparsedexpression.md) インターフェイスを返します。

- [IDebugParsedExpression](../../extensibility/debugger/reference/idebugparsedexpression.md)

     このインターフェイスは、評価の準備ができている解析済みの式を表します。 キーメソッドは [EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md) で、式の値と型を表す IDebugProperty2 を返します。

- [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)

     このインターフェイスは、値とその型を表し、式の評価の結果です。

## <a name="see-also"></a>関連項目
- [評価コンテキスト](../../extensibility/debugger/evaluation-context.md)
