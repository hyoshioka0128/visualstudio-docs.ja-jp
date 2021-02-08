---
title: 'IDebugStackFrame2:: Get式 Context |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugStackFrame2::GetExpressionContext
helpviewer_keywords:
- IDebugStackFrame2::GetExpressionContext
ms.assetid: a2604e6a-502d-473b-868f-b11ac64c7a35
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f82d76bb47c22ef77ba14e0a1ad64fa0404a6585
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99837511"
---
# <a name="idebugstackframe2getexpressioncontext"></a>IDebugStackFrame2::GetExpressionContext
スタックフレームとスレッドの現在のコンテキスト内での式の評価の評価コンテキストを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetExpressionContext ( 
   IDebugExpressionContext2** ppExprCxt
);
```

```csharp
int GetExpressionContext ( 
   out IDebugExpressionContext2 ppExprCxt
);
```

## <a name="parameters"></a>パラメーター
`ppExprCxt`\
入出力式の評価のコンテキストを表す [IDebugExpressionContext2](../../../extensibility/debugger/reference/idebugexpressioncontext2.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
 一般に、式の評価コンテキストは、式の評価を実行するためのスコープと考えることができます。 [Parsetext](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)メソッドを呼び出して式を解析し、結果の[EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)または[evaluateasync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)メソッドを呼び出して、解析された式を評価します。

## <a name="see-also"></a>関連項目
- [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)
- [IDebugExpressionContext2](../../../extensibility/debugger/reference/idebugexpressioncontext2.md)
- [ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)
- [EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)
- [EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)
