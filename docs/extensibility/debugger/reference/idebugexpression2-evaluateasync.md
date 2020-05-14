---
title: 表現2::評価非同期 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExpression2::EvaluateAsync
helpviewer_keywords:
- IDebugExpression2::EvaluateAsync
ms.assetid: 848fe6cb-0759-42f2-890b-d2b551c527d6
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 2cd1eba56f8e3c5a1a779acc3330790e9ba2bc96
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80729753"
---
# <a name="idebugexpression2evaluateasync"></a>IDebugExpression2::EvaluateAsync
このメソッドは、式を非同期的に評価します。

## <a name="syntax"></a>構文

```cpp
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

## <a name="parameters"></a>パラメーター
`dwFlags`\
[in]式の評価を制御する[EVALFLAGS](../../../extensibility/debugger/reference/evalflags.md)列挙体のフラグの組み合わせ。

`pExprCallback`\
[in]このパラメーターは常に NULL 値です。

## <a name="return-value"></a>戻り値
成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。 一般的なエラー コードは次のとおりです。

|エラー|説明|
|-----------|-----------------|
|E_EVALUATE_BUSY_WITH_EVALUATION|別の式が現在評価中であり、同時式の評価はサポートされていません。|

## <a name="remarks"></a>Remarks
このメソッドは、式の評価を開始した直後に返す必要があります。 式が正常に評価されると[、IDebugExpression 評価完了イベント2](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md)を[、アタッチまたはアタッチ](../../../extensibility/debugger/reference/idebugprogram2-attach.md)を通じて指定[されたイベント](../../../extensibility/debugger/reference/idebugeventcallback2.md)コールバックに送信する必要[Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md)があります。

## <a name="example"></a>例
`CExpression` [IDebugExpression2](../../../extensibility/debugger/reference/idebugexpression2.md)インターフェイスを実装する単純なオブジェクトに対してこのメソッドを実装する方法を次の例に示します。

```cpp
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

## <a name="see-also"></a>関連項目
- [IDebugExpression2](../../../extensibility/debugger/reference/idebugexpression2.md)
- [IDebugExpressionEvaluationCompleteEvent2](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md)
- [EVALFLAGS](../../../extensibility/debugger/reference/evalflags.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
