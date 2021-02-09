---
title: IDebugExpressionEvaluator::P arse |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExpressionEvaluator::Parse
helpviewer_keywords:
- IDebugExpressionEvaluator::Parse method
ms.assetid: e6e31b3a-63a7-4293-bcda-267eb78dffb6
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: abcc66eb8a0f1419d447dfbd0081b39583e2941e
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99930292"
---
# <a name="idebugexpressionevaluatorparse"></a>IDebugExpressionEvaluator::Parse
このメソッドは、式文字列を解析された式に変換します。

## <a name="syntax"></a>構文

```cpp
HRESULT Parse( 
   LPCOLESTR                upstrExpression,
   PARSEFLAGS               dwFlags,
   UINT                     nRadix,
   BSTR*                    pbstrError,
   UINT*                    pichError,
   IDebugParsedExpression** ppParsedExpression
);
```

```csharp
int Parse(
   string                     upstrExpression,
   enum_PARSEFLAGS            dwFlags,
   uint                       nRadix,
   out string                 pbstrError,
   out uint                   pichError,
   out IDebugParsedExpression ppParsedExpression
);
```

## <a name="parameters"></a>パラメーター
`upstrExpression`\
から解析する式文字列。

`dwFlags`\
から式の解析方法を決定する [Parseflags](../../../extensibility/debugger/reference/parseflags.md) 定数のコレクション。

`nRadix`\
から数値情報を解釈するために使用される基数。

`pbstrError`\
入出力エラーを人間が判読できるテキストとして返します。

`pichError`\
入出力式文字列内のエラーの先頭の文字位置を返します。

`ppParsedExpression`\
入出力 [IDebugParsedExpression](../../../extensibility/debugger/reference/idebugparsedexpression.md) オブジェクト内の解析された式を返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
 このメソッドは、実際の値ではなく、解析された式を生成します。 解析された式を評価する準備ができました。つまり、値に変換されます。

## <a name="see-also"></a>関連項目
- [IDebugExpressionEvaluator](../../../extensibility/debugger/reference/idebugexpressionevaluator.md)
- [IDebugParsedExpression](../../../extensibility/debugger/reference/idebugparsedexpression.md)
- [PARSEFLAGS](../../../extensibility/debugger/reference/parseflags.md)
