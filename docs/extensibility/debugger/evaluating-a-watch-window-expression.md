---
title: ウォッチウィンドウの評価式 |Microsoft Docs
description: 実行が一時停止したときに、Visual Studio がデバッグエンジンを呼び出して、ウォッチリスト内の各式の現在の値を確認する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Watch window expressions
- Watch window, expressions
- expression evaluation, Watch window expressions
ms.assetid: b07e72c7-60d3-4b30-8e3f-6db83454c348
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 97fb2c11b94a97a5c7a00083aa61877bb68d377b
ms.sourcegitcommit: 8e9c38da7bcfbe9a461c378083846714933a0e1e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/09/2020
ms.locfileid: "96915649"
---
# <a name="evaluate-a-watch-window-expression"></a>ウォッチウィンドウの式の評価
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターを実装するこの方法は非推奨とされます。 CLR 式エバリュエーターの実装の詳細については、「 [clr 式](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) エバリュエーターと [マネージ式エバリュエーターサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

 実行が一時停止すると、Visual Studio はデバッグエンジン (DE) を呼び出して、ウォッチリスト内の各式の現在の値を確認します。 DE は式エバリュエーター (EE) を使用して各式を評価し、Visual Studio は **ウォッチ** ウィンドウでその値を表示します。

 ウォッチリスト式の評価方法の概要を次に示します。

1. Visual Studio は、式の評価に使用できる式のコンテキストを取得するために、DE の [Get式コンテキスト](../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md) を呼び出します。

2. ウォッチリストの式ごとに、Visual Studio は [Parsetext](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) を呼び出して、式のテキストを解析された式に変換します。

3. `IDebugExpressionContext2::ParseText` は、 [解析](../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md) を呼び出して、テキストを解析して [IDebugParsedExpression](../../extensibility/debugger/reference/idebugparsedexpression.md) オブジェクトを生成する実際の作業を行います。

4. `IDebugExpressionContext2::ParseText`[IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md)オブジェクトを作成し、オブジェクトをそのオブジェクトに格納し `IDebugParsedExpression` ます。 この I `DebugExpression2` オブジェクトが Visual Studio に返されます。

5. Visual Studio は [EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) を呼び出して、解析された式を評価します。

6. `IDebugExpression2::EvaluateSync`[EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)への呼び出しを渡して実際の評価を行い、Visual Studio に返される[IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)オブジェクトを生成します。

7. Visual Studio は [GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md) を呼び出して、ウォッチリストに表示される式の値を取得します。

## <a name="parse-then-evaluate"></a>解析して評価する
 複雑な式の解析は評価よりもかなり長くかかることがあるため、式を評価するプロセスは、1) 式を解析し、2) 解析された式を評価するという2つの手順に分かれます。 このように、評価は何回でも実行できますが、式を解析する必要があるのは1回だけです。 中間解析式は、 [IDebugParsedExpression](../../extensibility/debugger/reference/idebugparsedexpression.md) オブジェクトの EE から返されます。このオブジェクトは、逆にカプセル化され、 [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) オブジェクトとして DE から返されます。 オブジェクトは、 `IDebugExpression` すべての評価をオブジェクトに延期し `IDebugParsedExpression` ます。

> [!NOTE]
> Visual Studio では、この2段階のプロセスに従う必要はありません。EE は、 [EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md) が呼び出されたときと同じ手順で解析および評価を行うことができます (これは MyCEE サンプルの動作を示しています)。 言語で複雑な式を作成できる場合は、解析手順を評価手順から分離することができます。 これにより、多くのウォッチ式が表示されているときに、Visual Studio デバッガーのパフォーマンスが向上します。

## <a name="in-this-section"></a>このセクションの内容
 [式の評価の実装例](../../extensibility/debugger/sample-implementation-of-expression-evaluation.md) MyCEE サンプルを使用して、式の評価プロセスをステップ実行します。

 [ウォッチ式の評価](../../extensibility/debugger/evaluating-a-watch-expression.md) 式が正常に解析された後の動作について説明します。

## <a name="related-sections"></a>関連項目
 [評価コンテキスト](../../extensibility/debugger/evaluation-context.md) デバッグエンジン (DE) が式エバリュエーター (EE) を呼び出す場合に渡される引数を提供します。

## <a name="see-also"></a>関連項目
 [CLR 式エバリュエーターの記述](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
