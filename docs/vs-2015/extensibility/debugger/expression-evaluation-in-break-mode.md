---
title: 中断モードでの式の評価 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- break mode, expression evaluation
- debugging [Debugging SDK], expression evaluation
- expression evaluation, break mode
ms.assetid: 34fe5b58-15d5-4387-a266-72120f90a4b6
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 362e50e20519c358564d13ba169f706fe384ca5c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68152756"
---
# <a name="expression-evaluation-in-break-mode"></a>中断モードでの式の評価
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

ここでは、デバッガーが中断モードで、式の評価を行う必要がある場合に発生するプロセスについて説明します。  
  
## <a name="expression-evaluation-process"></a>式の評価プロセス  
 式の評価に関連する基本的な手順は次のとおりです。  
  
1. セッションデバッグマネージャー (SDM) は、 [IDebugStackFrame2:: Get式コンテキスト](../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md) を呼び出して、式コンテキストインターフェイス [IDebugExpressionContext2](../../extensibility/debugger/reference/idebugexpressioncontext2.md)を取得します。  
  
2. 次に、SDM は、解析する文字列を使用して [IDebugExpressionContext2::P arseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) を呼び出します。  
  
3. ParseText が S_OK を返さない場合は、エラーの原因が返されます。  
  
     それ以外  
  
     ParseText が S_OK を返す場合、SDM は [IDebugExpression2:: EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) または [IDebugExpression2:: evaluateasync](../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md) を呼び出して、解析された式から最終的な値を取得できます。  
  
    - を使用する場合は `IDebugExpression2::EvaluateSync` 、指定されたコールバックインターフェイスを使用して、評価の進行中のプロセスを通知します。 最終的な値は、 [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) インターフェイスで返されます。  
  
    - を使用する場合は `IDebugExpression2::EvaluateAsync` 、指定されたコールバックインターフェイスを使用して、評価の進行中のプロセスを通知します。 評価が完了すると、EvaluateAsync はコールバックを介して [IDebugExpressionEvaluationCompleteEvent2](../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md) インターフェイスを送信します。 このイベントインターフェイスでは、 [GetResult](../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2-getresult.md)を使用して最終的な値を取得できます。  
  
## <a name="see-also"></a>参照  
 [デバッガーのイベントの呼び出し](../../extensibility/debugger/calling-debugger-events.md)
