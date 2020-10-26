---
title: 'IDebugExpression2:: Abort |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExpression2::Abort
helpviewer_keywords:
- IDebugExpression2::Abort
ms.assetid: 4fcb712e-1bdb-4b75-a440-35cc79ee147e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 5de2e34a8ae1e038c2109627099dacc5bd03a1ac
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80729764"
---
# <a name="idebugexpression2abort"></a>IDebugExpression2::Abort
このメソッドは、 [Evaluateasync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md) メソッドの呼び出しによって開始された非同期式の評価をキャンセルします。

## <a name="syntax"></a>構文

```cpp
HRESULT Abort(
   void
);
```

```csharp
int Abort();
```

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
 非同期式の評価が取り消された場合、 [attach](../../../extensibility/debugger/reference/idebugprogram2-attach.md)メソッドまたは[attach](../../../extensibility/debugger/reference/idebugengine2-attach.md)メソッドに渡されたイベントコールバックに[IDebugExpressionEvaluationCompleteEvent2](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md)イベントを送信しません。

## <a name="see-also"></a>関連項目
- [IDebugExpression2](../../../extensibility/debugger/reference/idebugexpression2.md)
- [IDebugExpressionEvaluationCompleteEvent2](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md)
- [EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)
