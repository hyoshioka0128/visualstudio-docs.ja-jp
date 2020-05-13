---
title: キー式エバリュエーター インターフェイス |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], expression evaluation
- expression evaluation, interfaces
ms.assetid: 1cac9aa3-0867-4e12-a16e-1e90abbc0fb6
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 01527edac4000f0b2f7b89fdd507fc093f0d7734
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738492"
---
# <a name="key-expression-evaluator-interfaces"></a>キー式エバリュエーター インターフェイス
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターのこの実装方法は非推奨になりました。 CLR 式エバリュエーターの実装については、「 [CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) 」および「[マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

 式エバリュエーター (EE) を評価コンテキストと共に記述する場合は、次のインターフェイスに精通している必要があります。

## <a name="interface-descriptions"></a>インターフェイスの説明

- [IDebugAddress](../../extensibility/debugger/reference/idebugaddress.md)

     現在の実行ポイントを表すデータ構造体を取得する単一のメソッド[GetAddress](../../extensibility/debugger/reference/idebugaddress-getaddress.md)を持ちます。 このデータ構造体は、式を評価する評価を評価する[EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)メソッドにデバッグ エンジン (DE) が渡す 3 つの引数の 1 つです。 このインターフェイスは、通常、シンボル プロバイダーによって実装されます。

- [IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md)

     シンボルの現在の値を格納するメモリ領域を取得する[Bind](../../extensibility/debugger/reference/idebugbinder-bind.md)メソッドを持ちます。 [IDebugObject](../../extensibility/debugger/reference/idebugobject.md)オブジェクトで表される包含メソッドと[、IDebugField](../../extensibility/debugger/reference/idebugfield.md)オブジェクトで表されるシンボル自体の両方が、シンボル`IDebugBinder::Bind`の値を返します。 `IDebugBinder`通常は DE によって実装されます。

- [IDebugField](../../extensibility/debugger/reference/idebugfield.md)

     単純なデータ型を表します。 配列やメソッドなど、より複雑な型の場合は、それぞれ派生した[IDebugArrayField](../../extensibility/debugger/reference/idebugarrayfield.md)インターフェイスと[IDebugMethodField](../../extensibility/debugger/reference/idebugmethodfield.md)インターフェイスを使用します。 [メソッド](../../extensibility/debugger/reference/idebugcontainerfield.md)やクラスなど、他のシンボルを含むシンボルを表すもう 1 つの重要な派生インターフェイスです。 `IDebugField`インターフェイス (およびその派生) は、通常、シンボル プロバイダーによって実装されます。

     オブジェクト`IDebugField`を使用してシンボルの名前と型を検索し[、IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md)オブジェクトと共に、その値を見つけることができます。

- [IDebugObject](../../extensibility/debugger/reference/idebugobject.md)

     シンボルの実行時の値の実際のビットを表します。 [バインド](../../extensibility/debugger/reference/idebugbinder-bind.md)は、シンボルを表す[IDebugField](../../extensibility/debugger/reference/idebugfield.md)オブジェクトを受け取り[、IDebugObject](../../extensibility/debugger/reference/idebugobject.md)オブジェクトを返します。 [GetValue](../../extensibility/debugger/reference/idebugobject-getvalue.md)メソッドは、メモリ バッファー内のシンボルの値を返します。 デは通常、メモリ内のプロパティの値を表すために、このインターフェイスを実装します。

- [IDebugExpressionEvaluator](../../extensibility/debugger/reference/idebugexpressionevaluator.md)

     このインターフェイスは、式エバリュエーター自体を表します。 キー メソッドは[、IDebugParsedExpression](../../extensibility/debugger/reference/idebugparsedexpression.md)インターフェイスを返す[解析](../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md)です。

- [IDebugParsedExpression](../../extensibility/debugger/reference/idebugparsedexpression.md)

     このインターフェイスは、解析済みの式を評価する準備が整った式を表します。 キー メソッドは、式の値と型を表す IDebugProperty2 を返す[EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)です。

- [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)

     このインターフェイスは、値とその型を表し、式の評価の結果です。

## <a name="see-also"></a>関連項目
- [評価コンテキスト](../../extensibility/debugger/evaluation-context.md)
