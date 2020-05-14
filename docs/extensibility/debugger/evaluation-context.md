---
title: 評価コンテキスト |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], expression evaluation
- expression evaluation, context
ms.assetid: 008a20c7-1b27-4013-bf96-d6a3f510da02
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5e3d02bd652d6c46b5aabe00e049e425f0921c27
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738801"
---
# <a name="evaluation-context"></a>評価コンテキスト
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターのこの実装方法は非推奨になりました。 CLR 式エバリュエーターの実装については[、「CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) 」および「[マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

 デバッグ エンジン (DE) が式エバリュエーター (EE) を呼び出すと[、EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)に渡される 3 つの引数によって、次の表に示すように、シンボルを検索および評価するためのコンテキストが決定されます。

## <a name="arguments"></a>引数

|引数|説明|
|--------------|-----------------|
|`pSymbolProvider`|シンボル[を識別](../../extensibility/debugger/reference/idebugsymbolprovider.md)するために使用するシンボル ハンドラー (SH) を指定するインターフェイス。|
|`pAddress`|現在の実行ポイントを指定する[IDebugAddress](../../extensibility/debugger/reference/idebugaddress.md)インターフェイス。 このインターフェイスは、実行されるコードを含むメソッドを検索します。|
|`pBinder`|名前を指定したシンボルの値と型を検索する[IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md)インターフェイス。|

 `IDebugParsedExpression::EvaluateSync`結果の値とその型を表す[IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)インターフェイスを返します。

## <a name="see-also"></a>関連項目
- [キー式エバリュエーター インターフェイス](../../extensibility/debugger/key-expression-evaluator-interfaces.md)
- [ローカルの表示](../../extensibility/debugger/displaying-locals.md)
- [EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)
- [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)
- [IDebugSymbolProvider](../../extensibility/debugger/reference/idebugsymbolprovider.md)
- [IDebugAddress](../../extensibility/debugger/reference/idebugaddress.md)
- [IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md)
