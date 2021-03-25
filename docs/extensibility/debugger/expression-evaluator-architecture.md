---
title: 式エバリュエーターアーキテクチャ |Microsoft Docs
description: 式エバリュエーターやシンボルプロバイダー/バインダーインターフェイスなど、独自の言語を Visual Studio デバッグパッケージに統合する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- architecture, expression evaluators
- expression evaluators, architecture
- debugging [Debugging SDK], expression evaluators
ms.assetid: aad7c4c6-1dc1-4d32-b975-f1fdf76bdeda
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 31b382f4765a115657fb213f39530e88e4008c95
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105094732"
---
# <a name="expression-evaluator-architecture"></a>式エバリュエーターのアーキテクチャ
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターを実装するこの方法は非推奨とされます。 CLR 式エバリュエーターの実装の詳細については、「 [clr 式](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) エバリュエーターと [マネージ式エバリュエーターサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

 独自の言語を Visual Studio デバッグパッケージに統合するには、必要な式エバリュエーター (EE) インターフェイスを設定し、共通言語ランタイムシンボルプロバイダー (SP) とバインダーインターフェイスを呼び出す必要があります。 現在の実行アドレスと共に、SP オブジェクトと binder オブジェクトは、式が評価されるコンテキストです。 これらのインターフェイスが生成して使用する情報は、EE のアーキテクチャの主要概念を表します。

## <a name="overview"></a>概要

### <a name="parse-the-expression"></a>式を解析する
 プログラムをデバッグする場合、式はさまざまな理由で評価されますが、デバッグされているプログラムがブレークポイントで停止されている場合は常に (ユーザーによって設定されたブレークポイントまたは例外によって発生したブレークポイントのいずれか) になります。 この時点で、Visual Studio はデバッグエンジン (DE) から [IDebugStackFrame2](../../extensibility/debugger/reference/idebugstackframe2.md) インターフェイスによって表されるスタックフレームを取得します。 次に、Visual Studio は [Get式コンテキスト](../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md) を呼び出して、 [IDebugExpressionContext2](../../extensibility/debugger/reference/idebugexpressioncontext2.md) インターフェイスを取得します。 このインターフェイスは、式を評価できるコンテキストを表します。 [Parsetext](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) は、評価プロセスへのエントリポイントです。 この時点までは、すべてのインターフェイスは DE によって実装されています。

 が呼び出されると、 `IDebugExpressionContext2::ParseText` ブレークポイントが発生したソースファイルの言語に関連付けられている EE が逆インスタンス化されます (de はこの時点で SH もインスタンス化します)。 EE は、 [IDebugExpressionEvaluator](../../extensibility/debugger/reference/idebugexpressionevaluator.md) インターフェイスによって表されます。 次に、DE は [Parse](../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md) を呼び出して、式 (テキスト形式) を解析された式に変換し、評価できるようにします。 この解析された式は、 [IDebugParsedExpression](../../extensibility/debugger/reference/idebugparsedexpression.md) インターフェイスによって表されます。 通常、式は解析され、この時点では評価されません。

 DE は、 [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) インターフェイスを実装するオブジェクトを作成し、オブジェクトを `IDebugParsedExpression` オブジェクトに格納 `IDebugExpression2` し、からオブジェクトを返し `IDebugExpression2` `IDebugExpressionContext2::ParseText` ます。

### <a name="evaluate-the-expression"></a>式を評価する
 Visual Studio は、 [EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) または [evaluateasync](../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md) を呼び出して、解析された式を評価します。 これらのメソッドはいずれも [EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md) を呼び出し ( `IDebugExpression2::EvaluateSync` メソッドをすぐに呼び出し、 `IDebugExpression2::EvaluateAsync` バックグラウンドスレッドを通じてメソッドを呼び出します)、解析された式を評価し、解析された式の値と型を表す [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) インターフェイスを返します。 `IDebugParsedExpression::EvaluateSync` 指定された SH、address、および binder を使用して、解析された式を、インターフェイスによって表される実際の値に変換し `IDebugProperty2` ます。

### <a name="for-example"></a>次に例を示します。
 実行中のプログラムでブレークポイントにヒットすると、ユーザーは [ **クイックウォッチ** ] ダイアログボックスで変数を表示するように選択します。 このダイアログボックスには、変数の名前、値、およびその型が表示されます。 ユーザーは通常、値を変更できます。

 [ **クイックウォッチ** ] ダイアログボックスが表示されたら、検査対象の変数の名前がテキストとして [parsetext](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)に送信されます。 これにより、解析された式 (この場合は変数) を表す [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) オブジェクトが返されます。 その後、 [EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)を呼び出して、 `IDebugProperty2` 変数の値と型、およびその名前を表すオブジェクトを生成します。 この情報が表示されます。

 ユーザーが変数の値を変更すると、 [Setvalueasstring](../../extensibility/debugger/reference/idebugproperty2-setvalueasstring.md) が新しい値で呼び出されます。これにより、メモリ内の変数の値が変更され、プログラムの実行が再開されるときに使用されるようになります。

 変数の値を表示するこのプロセスの詳細については、「 [ローカルの表示](../../extensibility/debugger/displaying-locals.md) 」を参照してください。 変数の値の変更方法の詳細については [、「ローカルの値の変更](../../extensibility/debugger/changing-the-value-of-a-local.md) 」を参照してください。

## <a name="in-this-section"></a>このセクションの内容
 [評価コンテキスト](../../extensibility/debugger/evaluation-context.md) DE が EE を呼び出したときに渡される引数を提供します。

 [キー式エバリュエーターインターフェイス](../../extensibility/debugger/key-expression-evaluator-interfaces.md) 評価コンテキストと共に EE を記述するときに必要となる重要なインターフェイスについて説明します。

## <a name="see-also"></a>こちらもご覧ください
- [CLR 式エバリュエーターの記述](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
- [表示 (ローカルを)](../../extensibility/debugger/displaying-locals.md)
- [ローカルの値の変更](../../extensibility/debugger/changing-the-value-of-a-local.md)
