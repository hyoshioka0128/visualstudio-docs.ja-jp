---
title: 式を使用します。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugParsedExpression::EvaluateSync
helpviewer_keywords:
- IDebugParsedExpression::EvaluateSync method
ms.assetid: 0ea04cfa-de87-4b6c-897e-4572c1a28942
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 1f00b209ff5f91d160e89f5f55ad966fbe9e6414
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80726014"
---
# <a name="idebugparsedexpressionevaluatesync"></a>IDebugParsedExpression::EvaluateSync
このメソッドは、解析された式を評価し、必要に応じて結果を別のデータ型にキャストします。

## <a name="syntax"></a>構文

```cpp
HRESULT EvaluateSync( 
   DWORD                 dwEvalFlags,
   DWORD                 dwTimeout,
   IDebugSymbolProvider* pSymbolProvider,
   IDebugAddress*        pAddress,
   IDebugBinder*         pBinder,
   BSTR                  bstrResultType,
   IDebugProperty2**     ppResult
);
```

```csharp
int EvaluateSync(
   uint                 dwEvalFlags,
   uint                 dwTimeout,
   IDebugSymbolProvider pSymbolProvider,
   IDebugAddress        pAddress,
   IDebugBinder         pBinder,
   string               bstrResultType,
   out IDebugProperty2  ppResult
);
```

## <a name="parameters"></a>パラメーター
`dwEvalFlags`\
[in]式の評価方法を制御する[EVALFLAGS](../../../extensibility/debugger/reference/evalflags.md)定数の組み合わせ。

`dwTimeout`\
[in]このメソッドから戻るまでの最大待機時間をミリ秒単位で指定します。 無期限`INFINITE`に待機するために使用します。

`pSymbolProvider`\
[in]インターフェイスとして表現されるシンボル[プロバイダー](../../../extensibility/debugger/reference/idebugsymbolprovider.md) 。

`pAddress`\
[in][メソッド](../../../extensibility/debugger/reference/idebugaddress.md)内の現在の実行位置。

`pBinder`\
[in]バインダーは[、IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)インターフェイスとして表されます。

`bstrResultType`\
[in]結果をキャストする必要がある型。 この引数には、NULL 値を指定できます。

`ppResult`\
[アウト]評価結果を表す[IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)インターフェイスを返します。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 式の評価コンテキストは によって`pAddress`与えられ、それを含むメソッドを決定し、言語スコープの規則を使用して式内のシンボルの値を決定できます。

## <a name="see-also"></a>関連項目
- [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)
- [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)
- [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [IDebugParsedExpression](../../../extensibility/debugger/reference/idebugparsedexpression.md)
