---
title: ブレークモードでの式評価 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- break mode, expression evaluation
- debugging [Debugging SDK], expression evaluation
- expression evaluation, break mode
ms.assetid: 34fe5b58-15d5-4387-a266-72120f90a4b6
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: bc09fc43bd9f0edea4f6dc32e5f37c387c045796
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738720"
---
# <a name="expression-evaluation-in-break-mode"></a>ブレークモードでの式評価
次のセクションでは、デバッガーが中断モードで、式の評価を行う必要がある場合に発生するプロセスについて説明します。

## <a name="expression-evaluation-process"></a>式の評価プロセス
 式の評価に関する基本的な手順を次に示します。

1. セッション デバッグ マネージャー (SDM) は、式コンテキスト インターフェイスを取得するために[IDebugStackFrame2::GetExpressionContext](../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md)を呼び出します。 [IDebugExpressionContext2](../../extensibility/debugger/reference/idebugexpressioncontext2.md)

2. その後、SDM は、解析する文字列を使用して[IDebugExpressionContext2::Pを](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)呼び出します。

3. ParseText がS_OKを返さない場合は、エラーの理由が返されます。

     -それ以外の場合-

     ParseText がS_OKを返す場合、SDM は[IDebugExpression2:::評価同期](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)または[IDebugExpression2::評価非同期](../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)を呼び出して、解析された式から最終的な値を取得できます。

    - を使用`IDebugExpression2::EvaluateSync`する場合、指定されたコールバック インターフェイスは、評価の進行中のプロセスを通信します。 最終的な値は[、IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)インターフェイスで返されます。

    - を使用`IDebugExpression2::EvaluateAsync`する場合、指定されたコールバック インターフェイスは、評価の進行中のプロセスを通信します。 評価が完了すると、コールバックを介して[IDebug 式評価コンプリート イベント 2](../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md)インターフェイスが送信されます。 このイベント インターフェイスでは[、GetResult](../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2-getresult.md)を使用して最終的な値が返されます。

## <a name="see-also"></a>関連項目
- [デバッガー イベントの呼び出し](../../extensibility/debugger/calling-debugger-events.md)
