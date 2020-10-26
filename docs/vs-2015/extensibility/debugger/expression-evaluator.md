---
title: 式エバリュエーター |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- expressions [Debugging SDK]
- debugging [Debugging SDK], expression evaluation
- expression evaluation
ms.assetid: f9381b2f-99aa-426c-aea0-d9c15f3c859b
caps.latest.revision: 20
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 423df66e8bd6bc1257a32236aa4ffbb28b80d655
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68152745"
---
# <a name="expression-evaluator"></a>式エバリュエーター
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

式エバリュエーター (EE) は、言語の構文を調べて、実行時に変数と式を解析および評価します。これにより、IDE が中断モードのときにユーザーが表示できるようになります。  
  
## <a name="using-expression-evaluators"></a>式エバリュエーターの使用  
 式は、次のように [Parsetext](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) メソッドを使用して作成されます。  
  
1. デバッグエンジン (DE) は、 [IDebugExpressionContext2](../../extensibility/debugger/reference/idebugexpressioncontext2.md) インターフェイスを実装します。  
  
2. デバッグパッケージは、 `IDebugExpressionContext2` [IDebugStackFrame2](../../extensibility/debugger/reference/idebugstackframe2.md) インターフェイスからオブジェクトを取得し、そのオブジェクトに対してメソッドを呼び出して、 `IDebugStackFrame2::ParseText` [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) オブジェクトを取得します。  
  
3. デバッグパッケージは、 [EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) メソッドまたは [evaluateasync](../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md) メソッドを呼び出して、式の値を取得します。 `IDebugExpression2::EvaluateAsync` は、コマンド/イミディエイトウィンドウから呼び出されます。 他のすべての UI コンポーネントは `IDebugExpression2::EvaluateSync` を呼び出します。  
  
4. 式の評価結果は [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) オブジェクトになります。このオブジェクトには、式の評価結果の名前、型、および値が含まれています。  
  
   式の評価中に、EE はシンボルプロバイダーコンポーネントからの情報を必要とします。 シンボルプロバイダーは、解析された式を識別および理解するために使用するシンボリック情報を提供します。  
  
   非同期式の評価が完了すると、セッションデバッグマネージャー (SDM) を介して非同期イベントが送信され、式の評価が完了したことが IDE に通知されます。 同期式の評価が完了すると、メソッドの呼び出しから評価の結果が返され `IDebugExpression2::EvaluateSync` ます。  
  
## <a name="implementation-notes"></a>実装に関するメモ  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]デバッグエンジンは、共通言語ランタイム (CLR) インターフェイスを使用して式エバリュエーターと通信することを想定しています。 その結果、デバッグエンジンで動作する式エバリュエーターは [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] clr をサポートする必要があります (すべての clr デバッグインターフェイスの完全な一覧は、の一部である debugref.doc で参照でき [!INCLUDE[winsdklong](../../includes/winsdklong-md.md)] ます)。  
  
## <a name="see-also"></a>参照  
 [デバッガーのコンポーネント](../../extensibility/debugger/debugger-components.md)
