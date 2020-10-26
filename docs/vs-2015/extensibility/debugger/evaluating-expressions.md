---
title: 式の評価 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- expressions [Debugging SDK], evaluating
- debugging [Debugging SDK], expression evaluation
- expression evaluation
ms.assetid: 5ccfcc80-dea5-48a1-8bae-6a26f8d3bc56
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: caff42c2e203151c6bab7d50b41744c2469ab3c2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68151624"
---
# <a name="evaluating-expressions"></a>式の評価
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

式は、[自動変数]、[ウォッチ]、[クイックウォッチ]、または [イミディエイト] ウィンドウから渡された文字列から作成されます。 式が評価されると、変数または引数の名前と型、およびその値を含む、印刷可能な文字列が生成されます。 この文字列は、対応する IDE ウィンドウに表示されます。  
  
## <a name="implementation"></a>実装  
 式は、ブレークポイントでプログラムが停止したときに評価されます。 式自体は、 [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) インターフェイスによって表されます。これは、指定された式の評価コンテキスト内で、バインドおよび評価の準備ができている解析済みの式を表します。 スタックフレームは、 [IDebugExpressionContext2](../../extensibility/debugger/reference/idebugexpressioncontext2.md) インターフェイスを実装することによってデバッグエンジン (DE) が提供する式の評価コンテキストを決定します。  
  
 ユーザー文字列と[IDebugExpressionContext2](../../extensibility/debugger/reference/idebugexpressioncontext2.md)インターフェイスが指定されている場合、デバッグエンジン (DE) は、ユーザー文字列を[IDebugExpressionContext2::P arsetext](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)メソッドに渡すことによって[IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md)インターフェイスを取得できます。 返される IDebugExpression2 インターフェイスには、評価のために準備された解析済みの式が含まれます。  
  
 インターフェイスを使用して `IDebugExpression2` 、DE は、 [IDebugExpression2:: EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) または [IDebugExpression2:: evaluateasync](../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)を使用して、同期または非同期の式の評価によって式の値を取得できます。 この値は、変数または引数の名前および型と共に IDE に送信され、表示されます。 値、名前、および型は、 [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) インターフェイスによって表されます。  
  
 式の評価を有効にするには、DE で [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) インターフェイスと [IDebugExpressionContext2](../../extensibility/debugger/reference/idebugexpressioncontext2.md) インターフェイスを実装する必要があります。 同期と非同期のどちらの評価でも、 [IDebugProperty2:: GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md) メソッドの実装が必要です。  
  
## <a name="see-also"></a>参照  
 [スタックフレーム](../../extensibility/debugger/stack-frames.md)   
 [式の評価コンテキスト](../../extensibility/debugger/expression-evaluation-context.md)   
 [タスクのデバッグ](../../extensibility/debugger/debugging-tasks.md)
