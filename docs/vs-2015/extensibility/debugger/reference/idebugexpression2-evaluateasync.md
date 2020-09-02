---
title: 'IDebugExpression2:: EvaluateAsync |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugExpression2::EvaluateAsync
helpviewer_keywords:
- IDebugExpression2::EvaluateAsync
ms.assetid: 848fe6cb-0759-42f2-890b-d2b551c527d6
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2e084152f6215878816739f46dc91fa322cf9c94
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68158438"
---
# <a name="idebugexpression2evaluateasync"></a>IDebugExpression2::EvaluateAsync
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このメソッドは、式を非同期的に評価します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT EvaluateAsync (   
   EVALFLAGS             dwFlags,  
   IDebugEventCallback2* pExprCallback  
);  
```  
  
```csharp  
int EvaluateAsync(  
   enum_EVALFLAGS       dwFlags,   
   IDebugEventCallback2 pExprCallback  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `dwFlags`  
 から式の評価を制御する [Evalflags](../../../extensibility/debugger/reference/evalflags.md) 列挙のフラグの組み合わせ。  
  
 `pExprCallback`  
 からこのパラメーターは常に null 値です。  
  
## <a name="return-value"></a>戻り値  
 成功した場合は、を返します。それ以外の場合は `S_OK` エラーコードを返します。 一般的なエラーコードは次のとおりです。  
  
|エラー|説明|  
|-----------|-----------------|  
|E_EVALUATE_BUSY_WITH_EVALUATION|現在、別の式が評価されていますが、同時式の評価はサポートされていません。|  
  
## <a name="remarks"></a>注釈  
 このメソッドは、式の評価を開始した直後にを返します。 式が正常に評価された場合は、 [attach](../../../extensibility/debugger/reference/idebugprogram2-attach.md)または[attach](../../../extensibility/debugger/reference/idebugengine2-attach.md)によって提供される[IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)イベントコールバックに[IDebugExpressionEvaluationCompleteEvent2](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md)を送信する必要があります。  
  
## <a name="example"></a>例  
 次の例は、IDebugExpression2 インターフェイスを実装する単純なオブジェクトに対してこのメソッドを実装する方法を示して `CExpression` います。 [IDebugExpression2](../../../extensibility/debugger/reference/idebugexpression2.md)  
  
```cpp#  
HRESULT CExpression::EvaluateAsync(EVALFLAGS dwFlags,  
                                   IDebugEventCallback2* pExprCallback)  
{  
    // Set the aborted state to FALSE  
    // in case the user tries to redo the evaluation after aborting.  
    m_bAborted = FALSE;  
    // Post the WM_EVAL_EXPR message in the message queue of the current thread.  
    // This starts the expression evaluation on a background thread.  
    PostThreadMessage(GetCurrentThreadId(), WM_EVAL_EXPR, 0, (LPARAM) this);  
    return S_OK;  
}  
```  
  
## <a name="see-also"></a>参照  
 [IDebugExpression2](../../../extensibility/debugger/reference/idebugexpression2.md)   
 [IDebugExpressionEvaluationCompleteEvent2](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md)   
 [EVALFLAGS](../../../extensibility/debugger/reference/evalflags.md)   
 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
