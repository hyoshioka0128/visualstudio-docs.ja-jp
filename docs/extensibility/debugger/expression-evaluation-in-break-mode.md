---
title: 中断モードでの式の評価 |Microsoft Docs
description: デバッガーが中断モードで、式の評価を行う必要があるときに発生するプロセスについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- break mode, expression evaluation
- debugging [Debugging SDK], expression evaluation
- expression evaluation, break mode
ms.assetid: 34fe5b58-15d5-4387-a266-72120f90a4b6
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 041e499f4c670b5b31530c7fc0ecb74358a8087f
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99921496"
---
# <a name="expression-evaluation-in-break-mode"></a>中断モードでの式の評価
次のセクションでは、デバッガーが中断モードで、式の評価を行う必要がある場合に発生するプロセスについて説明します。

## <a name="expression-evaluation-process"></a>式の評価プロセス
 式の評価に関連する基本的な手順を次に示します。

1. セッションデバッグマネージャー (SDM) は、 [IDebugStackFrame2:: Get式コンテキスト](../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md) を呼び出して、式コンテキストインターフェイス [IDebugExpressionContext2](../../extensibility/debugger/reference/idebugexpressioncontext2.md)を取得します。

2. 次に、SDM は、解析する文字列を使用して [IDebugExpressionContext2::P arseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) を呼び出します。

3. ParseText が S_OK を返さない場合は、エラーの原因が返されます。

     それ以外

     ParseText が S_OK を返す場合、SDM は [IDebugExpression2:: EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) または [IDebugExpression2:: evaluateasync](../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md) を呼び出して、解析された式から最終的な値を取得できます。

    - を使用する場合 `IDebugExpression2::EvaluateSync` 、指定されたコールバックインターフェイスは、評価の進行中のプロセスを通信します。 最終的な値は、 [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) インターフェイスで返されます。

    - を使用する場合 `IDebugExpression2::EvaluateAsync` 、指定されたコールバックインターフェイスは、評価の進行中のプロセスを通信します。 評価が完了すると、EvaluateAsync はコールバックを介して [IDebugExpressionEvaluationCompleteEvent2](../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md) インターフェイスを送信します。 このイベントインターフェイスでは、最終的な値は [GetResult](../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2-getresult.md)になります。

## <a name="see-also"></a>関連項目
- [デバッガーイベントの呼び出し](../../extensibility/debugger/calling-debugger-events.md)
