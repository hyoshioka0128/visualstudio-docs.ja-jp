---
description: スタックフレームとスレッドの現在のコンテキスト内での式の評価の評価コンテキストを取得します。
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
ms.openlocfilehash: 4780b979102ee2ada499e2cd2e0f8ca728cadd91
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102145938"
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
