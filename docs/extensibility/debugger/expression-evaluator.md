---
title: 式エバリュエーター |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- expressions [Debugging SDK]
- debugging [Debugging SDK], expression evaluation
- expression evaluation
ms.assetid: f9381b2f-99aa-426c-aea0-d9c15f3c859b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a477aaceb57e6ccd2eb5125fcf9d8af9be59472b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738688"
---
# <a name="expression-evaluator"></a>式エバリュエーター
式エバリュエーター (EE) は、実行時に変数と式を解析および評価する言語の構文を調べ、IDE が中断モードのときにユーザーが表示できるようにします。

## <a name="use-expression-evaluators"></a>式エバリュエーターを使用する
 式は、次のように[ParseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)メソッドを使用して作成されます。

1. デバッグ エンジン (DE) は、[インターフェイス](../../extensibility/debugger/reference/idebugexpressioncontext2.md)を実装します。

2. デバッグ パッケージは`IDebugExpressionContext2`[、IDebugStackFrame2](../../extensibility/debugger/reference/idebugstackframe2.md)インターフェイスからオブジェクトを取得し、`IDebugStackFrame2::ParseText`そのメソッドを呼び出して[IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md)オブジェクトを取得します。

3. デバッグ パッケージは、式の値を取得する[EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)メソッドまたは[EvaluateAsync](../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)メソッドを呼び出します。 `IDebugExpression2::EvaluateAsync`はコマンド/イミディエイト ウィンドウから呼び出されます。 その他のすべての UI`IDebugExpression2::EvaluateSync`コンポーネントは、 を呼び出します。

4. 式の評価の結果は、式の評価結果の名前、型、および値を含む[IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)オブジェクトです。

   式の評価中、EE はシンボル プロバイダー コンポーネントからの情報を必要とします。 シンボル・プロバイダーは、構文解析された式を識別および理解するために使用される記号情報を提供します。

   非同期式の評価が完了すると、非同期イベントは、DE によってセッションのデバッグ マネージャー (SDM) を介して、式の評価が完了したことを IDE に通知するために送信されます。 そして、評価の結果は`IDebugExpression2::EvaluateSync`、メソッドの呼び出しから返されます。

## <a name="implementation-notes"></a>実装に関するメモ
 デバッグ[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]エンジンは、共通言語ランタイム (CLR) インターフェイスを使用して式エバリュエーターと対話することを期待します。 その結果、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]デバッグ エンジンと連携する式エバリュエーターが CLR をサポートする必要があります (すべての CLR デバッグ インターフェイスの完全な一覧は、[!INCLUDE[winsdklong](../../deployment/includes/winsdklong_md.md)]の一部である debugref.doc にあります)。

## <a name="see-also"></a>関連項目
- [デバッガー コンポーネント](../../extensibility/debugger/debugger-components.md)
