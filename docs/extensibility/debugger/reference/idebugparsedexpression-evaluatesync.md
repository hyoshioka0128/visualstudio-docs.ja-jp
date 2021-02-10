---
title: 'IDebugParsedExpression:: EvaluateSync |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugParsedExpression::EvaluateSync
helpviewer_keywords:
- IDebugParsedExpression::EvaluateSync method
ms.assetid: 0ea04cfa-de87-4b6c-897e-4572c1a28942
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ff14c10f5563053ce704982455eee6d9dc81b742
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99953254"
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
から式の評価方法を制御する [Evalflags](../../../extensibility/debugger/reference/evalflags.md) 定数の組み合わせ。

`dwTimeout`\
からこのメソッドから制御が戻るまでに待機する最大時間をミリ秒単位で指定します。 `INFINITE`無期限に待機するには、を使用します。

`pSymbolProvider`\
からシンボルプロバイダー。 [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md) インターフェイスとして表現されます。

`pAddress`\
から [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) インターフェイスとして表される、メソッド内の現在の実行位置。

`pBinder`\
からバインダーは、 [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md) インターフェイスとして表現されます。

`bstrResultType`\
から結果のキャスト先の型。 この引数には null 値を指定できます。

`ppResult`\
入出力評価の結果を表す [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) インターフェイスを返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
 式の評価コンテキストは、によって指定されます。これにより、含まれている `pAddress` メソッドを決定し、言語のスコープルールを使用して、式のシンボルの値を決定できます。

## <a name="see-also"></a>関連項目
- [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)
- [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)
- [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [IDebugParsedExpression](../../../extensibility/debugger/reference/idebugparsedexpression.md)
