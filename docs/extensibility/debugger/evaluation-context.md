---
title: 評価コンテキスト |Microsoft Docs
description: デバッグエンジンが式エバリュエーターを呼び出すと、引数は、シンボルを検索して評価するためのコンテキスト (psymbols Provider、pAddress、および pBinder) を決定します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], expression evaluation
- expression evaluation, context
ms.assetid: 008a20c7-1b27-4013-bf96-d6a3f510da02
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 35ccfc921f8175a92b0a082798ce8ccc44990d2e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105096981"
---
# <a name="evaluation-context"></a>評価コンテキスト
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターを実装するこの方法は非推奨とされます。 CLR 式エバリュエーターの実装の詳細については、「 [clr 式](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) エバリュエーターと [マネージ式エバリュエーターサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

 デバッグエンジン (DE) が式エバリュエーター (EE) を呼び出すと、次の表に示すように、 [EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md) に渡される3つの引数によって、シンボルを検索して評価するためのコンテキストが決定されます。

## <a name="arguments"></a>引数

|引数|説明|
|--------------|-----------------|
|`pSymbolProvider`|シンボルを識別するために使用するシンボルハンドラー (SH) を指定する [IDebugSymbolProvider](../../extensibility/debugger/reference/idebugsymbolprovider.md) インターフェイス。|
|`pAddress`|現在の実行ポイントを指定する [IDebugAddress](../../extensibility/debugger/reference/idebugaddress.md) インターフェイス。 このインターフェイスは、実行されているコードを含むメソッドを検索します。|
|`pBinder`|名前を指定してシンボルの値と型を検索する [IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md) インターフェイス。|

 `IDebugParsedExpression::EvaluateSync` 結果の値とその型を表す [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) インターフェイスを返します。

## <a name="see-also"></a>こちらもご覧ください
- [キー式エバリュエーターインターフェイス](../../extensibility/debugger/key-expression-evaluator-interfaces.md)
- [表示 (ローカルを)](../../extensibility/debugger/displaying-locals.md)
- [EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)
- [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)
- [IDebugSymbolProvider](../../extensibility/debugger/reference/idebugsymbolprovider.md)
- [IDebugAddress](../../extensibility/debugger/reference/idebugaddress.md)
- [IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md)
