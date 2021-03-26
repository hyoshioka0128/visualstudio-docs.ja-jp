---
description: このメソッドは、EvaluateAsync) メソッドの呼び出しによって開始された非同期式の評価をキャンセルします。
title: 'IDebugExpression2:: Abort |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExpression2::Abort
helpviewer_keywords:
- IDebugExpression2::Abort
ms.assetid: 4fcb712e-1bdb-4b75-a440-35cc79ee147e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d6c355d2c4ee3cf63551f54b050b0ea42f4fdddc
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105092450"
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

## <a name="remarks"></a>注釈
 非同期式の評価が取り消された場合、 [attach](../../../extensibility/debugger/reference/idebugprogram2-attach.md)メソッドまたは[attach](../../../extensibility/debugger/reference/idebugengine2-attach.md)メソッドに渡されたイベントコールバックに[IDebugExpressionEvaluationCompleteEvent2](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md)イベントを送信しません。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugExpression2](../../../extensibility/debugger/reference/idebugexpression2.md)
- [IDebugExpressionEvaluationCompleteEvent2](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md)
- [EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)
