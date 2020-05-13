---
title: 式エバリュエータアーキテクチャ |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- architecture, expression evaluators
- expression evaluators, architecture
- debugging [Debugging SDK], expression evaluators
ms.assetid: aad7c4c6-1dc1-4d32-b975-f1fdf76bdeda
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: aac782c653f230d5598a49d43eb70f548de6dc41
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738700"
---
# <a name="expression-evaluator-architecture"></a>式エバリュエーター アーキテクチャ
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターのこの実装方法は非推奨になりました。 CLR 式エバリュエーターの実装については[、「CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) 」および「[マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

 Visual Studio デバッグ パッケージに独自の言語を統合する必要があります式エバリュエーター (EE) インターフェイスを設定し、共通言語ランタイム シンボル プロバイダー (SP) とバインダー インターフェイスを呼び出す必要があります。 SP オブジェクトとバインダー オブジェクトは、現在の実行アドレスと共に、式が評価されるコンテキストです。 これらのインターフェイスが生成および使用する情報は、EE のアーキテクチャにおける重要な概念を表します。

## <a name="overview"></a>概要

### <a name="parse-the-expression"></a>式の解析
 プログラムをデバッグする場合、式はさまざまな理由で評価されますが、デバッグ中のプログラムがブレークポイント (ユーザーによって配置されたブレークポイントまたは例外によって発生したブレークポイント) で停止した場合には常に式が評価されます。 この時点で、Visual Studio はデバッグ エンジン (DE) から[IDebugStackFrame2](../../extensibility/debugger/reference/idebugstackframe2.md)インターフェイスで表されるスタック フレームを取得します。 その後、インターフェイスを取得するために[GetExpressionContext](../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md) [を](../../extensibility/debugger/reference/idebugexpressioncontext2.md)呼び出します。 このインターフェイスは、式を評価できるコンテキストを表します。[解析テキスト](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)は、評価プロセスへのエントリ ポイントです。 ここまでは、すべてのインターフェイスが DE によって実装されます。

 DE`IDebugExpressionContext2::ParseText`が呼び出されると、デはブレークポイントが発生したソース ファイルの言語に関連付けられた EE をインスタンス化します (DE はこの時点で SH もインスタンス化します)。 EE は[、IDebug 式エバリュエーター インターフェイス](../../extensibility/debugger/reference/idebugexpressionevaluator.md)によって表されます。 DE は[Parse](../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md)を呼び出して、式 (テキスト形式) を解析済み式に変換し、評価の準備が整います。 この解析された式は、インターフェイスによって表[されます](../../extensibility/debugger/reference/idebugparsedexpression.md)。 通常、式は解析され、この時点では評価されません。

 DE は[、IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md)インターフェイスを実装`IDebugParsedExpression`するオブジェクトを作成し、オブジェクトを`IDebugExpression2`オブジェクトに配置し、`IDebugExpression2`オブジェクトを`IDebugExpressionContext2::ParseText`返します。

### <a name="evaluate-the-expression"></a>式を評価する
 Visual Studio は、解析された式を[評価するために、EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)または[EvaluateAsync](../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)を呼び出します。 どちらのメソッドも[EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)を`IDebugExpression2::EvaluateSync`呼び出し、メソッド`IDebugExpression2::EvaluateAsync`をバックグラウンド スレッドを通じてメソッドを呼び出す場合に、メソッドを呼び出して解析された式の値と型を表す[IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)インターフェイスを返します。 `IDebugParsedExpression::EvaluateSync`は、指定された SH、アドレス、およびバインダーを使用して、解析された式を、インターフェイスによって表`IDebugProperty2`される実際の値に変換します。

### <a name="for-example"></a>次に例を示します。
 実行中のプログラムでブレークポイントにヒットした後、ユーザーは **[クイック ウォッチ**] ダイアログ ボックスで変数を表示することを選択します。 このダイアログ ボックスには、変数の名前、値、および変数の型が表示されます。 通常、ユーザーは値を変更できます。

 [**クイック ウォッチ]** ダイアログ ボックスが表示されると、検査対象の変数の名前がテキストとして[ParseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)に送信されます。 これは、解析された式 (この場合は変数) を表す[IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md)オブジェクトを返します。 [次に EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)が呼`IDebugProperty2`び出され、変数の値と型、およびその名前を表すオブジェクトが生成されます。 表示されるのはこの情報です。

 ユーザーが変数の値を変更すると[、SetValueAsString](../../extensibility/debugger/reference/idebugproperty2-setvalueasstring.md)が新しい値で呼び出され、メモリ内の変数の値が変更され、プログラムの実行が再開されるときに使用されます。

 変数[の値を表示する](../../extensibility/debugger/displaying-locals.md)このプロセスの詳細については、「ローカルの表示」を参照してください。 変数[の値の変更](../../extensibility/debugger/changing-the-value-of-a-local.md)方法の詳細については、ローカルの値の変更を参照してください。

## <a name="in-this-section"></a>このセクションの内容
 [評価コンテキスト](../../extensibility/debugger/evaluation-context.md)DE が EE を呼び出すときに渡される引数を提供します。

 [キー式エバリュエーター インターフェイス](../../extensibility/debugger/key-expression-evaluator-interfaces.md)EE を記述するときに必要な重要なインターフェイスと評価コンテキストについて説明します。

## <a name="see-also"></a>関連項目
- [CLR 式エバリュエーターの記述](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
- [ローカルの表示](../../extensibility/debugger/displaying-locals.md)
- [ローカルの値の変更](../../extensibility/debugger/changing-the-value-of-a-local.md)
