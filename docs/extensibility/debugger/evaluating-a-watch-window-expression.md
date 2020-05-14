---
title: ウォッチ ウィンドウ式の評価 |マイクロソフトドキュメント
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
ms.openlocfilehash: 9cef2f27eec095ee7b136153ecb764feba9effbb
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738841"
---
# <a name="evaluate-a-watch-window-expression"></a>ウォッチ ウィンドウ式を評価する
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターのこの実装方法は非推奨になりました。 CLR 式エバリュエーターの実装については[、「CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) 」および「[マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

 実行が一時停止すると、Visual Studio はデバッグ エンジン (DE) を呼び出して、ウォッチ リスト内の各式の現在の値を確認します。 DE は式エバリュエーター (EE) を使用して各式を評価し、Visual Studio では、その値を**ウォッチ**ウィンドウに表示します。

 ウォッチ リスト式の評価方法の概要を次に示します。

1. 式の評価に使用できる式コンテキストを取得するために、DE の[GetExpressionContext](../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md)を呼び出します。

2. ウォッチ リスト内の各式に対して[、ParseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)を呼び出して、式テキストを解析された式に変換します。

3. `IDebugExpressionContext2::ParseText`[テキストを解析](../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md)する実際の作業を行い[、IDebugParsedExpression](../../extensibility/debugger/reference/idebugparsedexpression.md)オブジェクトを生成する Parse を呼び出します。

4. `IDebugExpressionContext2::ParseText`[オブジェクト](../../extensibility/debugger/reference/idebugexpression2.md)を作成し、オブジェクトをそのオブジェクトに`IDebugParsedExpression`配置します。 この`DebugExpression2`I オブジェクトは、Visual Studio に返されます。

5. 解析された式を評価するために[EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)を呼び出します。

6. `IDebugExpression2::EvaluateSync`呼び出しを[渡す EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)実際の評価を行い、Visual Studio に返される[IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)オブジェクトを生成します。

7. 呼び出し[GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md)ウォッチ リストに表示される式の値を取得します。

## <a name="parse-then-evaluate"></a>解析してから評価する
 複雑な式の解析は評価よりもはるかに時間がかかるため、式を評価するプロセスは、1) 式の解析と 2) 解析された式の評価の 2 つのステップに分割されます。 この方法では、評価は何度も行われますが、式は 1 回だけ解析する必要があります。 中間解析された式は、カプセル化され[、IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md)オブジェクトとして DE から返される[IDebugParsedExpression](../../extensibility/debugger/reference/idebugparsedexpression.md)オブジェクトの EE から返されます。 オブジェクト`IDebugExpression`は、すべての評価をオブジェクトに`IDebugParsedExpression`延期します。

> [!NOTE]
> この 2 段階のプロセスを EE が遵守する必要はありません。[評価同期](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)が呼び出されたときに、EE は同じ手順で解析および評価できます (たとえば、MyCEE サンプルの動作方法)。 言語が複雑な式を形成できる場合は、解析ステップを評価ステップから分離することができます。 これにより、多くのウォッチ式が表示されている場合、Visual Studio デバッガーのパフォーマンスが向上します。

## <a name="in-this-section"></a>このセクションの内容
 [式評価のサンプル実装](../../extensibility/debugger/sample-implementation-of-expression-evaluation.md)MyCEE サンプルを使用して、式の評価プロセスを段階的に実行します。

 [ウォッチ式の評価](../../extensibility/debugger/evaluating-a-watch-expression.md)式解析が成功した後に何が起こるかを説明します。

## <a name="related-sections"></a>関連項目
 [評価コンテキスト](../../extensibility/debugger/evaluation-context.md)デバッグ エンジン (DE) が式エバリュエーター (EE) を呼び出すときに渡される引数を提供します。

## <a name="see-also"></a>関連項目
 [CLR 式エバリュエーターの記述](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
