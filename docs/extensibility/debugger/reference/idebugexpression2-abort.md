---
title: Iデバッグ式2::中止 |マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80729764"
---
# <a name="idebugexpression2abort"></a>IDebugExpression2::Abort
このメソッドは[、EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)メソッドの呼び出しによって開始された非同期式の評価をキャンセルします。

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
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 非同期式の評価が取り消された場合は、[アタッチ](../../../extensibility/debugger/reference/idebugprogram2-attach.md)メソッドまたは[アタッチ](../../../extensibility/debugger/reference/idebugengine2-attach.md)メソッドに渡されたイベント コールバックに[IDebugExpression 評価完了イベント2](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md)イベントを送信しないでください。

## <a name="see-also"></a>関連項目
- [IDebugExpression2](../../../extensibility/debugger/reference/idebugexpression2.md)
- [IDebugExpressionEvaluationCompleteEvent2](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md)
- [EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)
