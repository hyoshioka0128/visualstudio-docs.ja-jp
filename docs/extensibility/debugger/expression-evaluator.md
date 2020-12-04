---
title: 式エバリュエーター |Microsoft Docs
description: 式エバリュエーターについて説明します。式エバリュエーターは、中断モードで実行時に変数と式を解析して評価するために言語の構文を確認します。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: a8223e39eb804684fede50ceb2f7c859e198a272
ms.sourcegitcommit: bbed6a0b41ac4c4a24e8581ff3b34d96345ddb00
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2020
ms.locfileid: "96560136"
---
# <a name="expression-evaluator"></a>式エバリュエーター
式エバリュエーター (EE) は、言語の構文を調べて、実行時に変数と式を解析および評価します。これにより、IDE が中断モードのときにユーザーが表示できるようになります。

## <a name="use-expression-evaluators"></a>式エバリュエーターを使用する
 式は、次のように [Parsetext](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) メソッドを使用して作成されます。

1. デバッグエンジン (DE) は、 [IDebugExpressionContext2](../../extensibility/debugger/reference/idebugexpressioncontext2.md) インターフェイスを実装します。

2. デバッグパッケージは、 `IDebugExpressionContext2` [IDebugStackFrame2](../../extensibility/debugger/reference/idebugstackframe2.md) インターフェイスからオブジェクトを取得し、そのオブジェクトに対してメソッドを呼び出して、 `IDebugStackFrame2::ParseText` [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) オブジェクトを取得します。

3. デバッグパッケージは、 [EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) メソッドまたは [evaluateasync](../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md) メソッドを呼び出して、式の値を取得します。 `IDebugExpression2::EvaluateAsync` は、コマンド/イミディエイトウィンドウから呼び出されます。 他のすべての UI コンポーネントは `IDebugExpression2::EvaluateSync` を呼び出します。

4. 式の評価結果は [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) オブジェクトになります。このオブジェクトには、式の評価結果の名前、型、および値が含まれています。

   式の評価中に、EE はシンボルプロバイダーコンポーネントからの情報を必要とします。 シンボルプロバイダーは、解析された式を識別および理解するために使用するシンボリック情報を提供します。

   非同期式の評価が完了すると、セッションデバッグマネージャー (SDM) を介して非同期イベントが送信され、式の評価が完了したことが IDE に通知されます。 次に、評価の結果がメソッドの呼び出しから返され `IDebugExpression2::EvaluateSync` ます。

## <a name="implementation-notes"></a>実装に関するメモ
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]デバッグエンジンは、共通言語ランタイム (CLR) インターフェイスを使用して式エバリュエーターと通信することを想定しています。 その結果、デバッグエンジンで動作する式エバリュエーターは [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] clr をサポートする必要があります (すべての clr デバッグインターフェイスの完全な一覧は、の一部である debugref.doc で参照でき [!INCLUDE[winsdklong](../../deployment/includes/winsdklong_md.md)] ます)。

## <a name="see-also"></a>関連項目
- [デバッガーコンポーネント](../../extensibility/debugger/debugger-components.md)
