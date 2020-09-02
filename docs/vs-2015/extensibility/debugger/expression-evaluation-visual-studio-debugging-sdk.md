---
title: 式の評価 (Visual Studio デバッグ SDK) |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], expression evaluation
- expression evaluation
ms.assetid: 5044ced5-c18c-4534-b0bf-cc3e50cd57ac
caps.latest.revision: 8
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 0f2a84f01168dd01921d933a80fe052c1a6c6447
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62562212"
---
# <a name="expression-evaluation-visual-studio-debugging-sdk"></a>式の評価 (Visual Studio Debugging SDK)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

中断モードでは、IDE は、プログラムの複数の変数を含む単純な式を評価できる必要があります。 これを実現するには、デバッグエンジン (DE) が、IDE のいずれかのウィンドウに入力された式を解析して評価できる必要があります。  
  
 式は、 [IDebugExpressionContext2::P arseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) メソッドを使用して作成され、結果の [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) インターフェイスによって表されます。  
  
 **IDebugExpression2**インターフェイスは DE によって実装され、式の評価結果を ide に表示するために、 [IDEBUGPROPERTY2](../../extensibility/debugger/reference/idebugproperty2.md)インターフェイスを ide に返すために**evalasync**メソッドを呼び出します。 [IDebugProperty2:: GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md) は、式の値をウォッチウィンドウまたは [ローカル] ウィンドウに配置するために使用できる構造体を返します。  
  
 デバッグパッケージまたはセッションデバッグマネージャー (SDM) は、 [IDebugExpression2:: EvaluateAsync](../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md) または [EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) を呼び出して、評価の結果を表す [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) インターフェイスを取得します。 `IDebugProperty2` には、式の名前、型、および値を返すメソッドがあります。 この情報は、さまざまなデバッガーウィンドウに表示されます。  
  
## <a name="using-expression-evaluation"></a>式の評価の使用  
 式の評価を使用するには、次の表に示すように、 [IDebugExpressionContext2::P arseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) メソッドと [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) インターフェイスのすべてのメソッドを実装する必要があります。  
  
|メソッド|説明|  
|------------|-----------------|  
|[EvaluateAsync](../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)|式を非同期的に評価します。|  
|[中止](../../extensibility/debugger/reference/idebugexpression2-abort.md)|非同期式の評価を終了します。|  
|[EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)|式を同期的に評価します。|  
  
 同期および非同期評価を行うには、 [IDebugProperty2:: GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md) メソッドの実装が必要です。 非同期式の評価には、 [IDebugExpressionEvaluationCompleteEvent2](../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md)の実装が必要です。  
  
## <a name="see-also"></a>参照  
 [実行の制御と状態の評価](../../extensibility/debugger/execution-control-and-state-evaluation.md)
