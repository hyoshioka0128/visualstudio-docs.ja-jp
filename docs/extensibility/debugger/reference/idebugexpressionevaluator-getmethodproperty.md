---
description: このメソッドは、メソッドのローカル、引数、およびその他のプロパティを格納しているプロパティオブジェクトを取得します。
title: 'IDebugExpressionEvaluator:: GetMethodProperty |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExpressionEvaluator::GetMethodProperty
helpviewer_keywords:
- IDebugExpressionEvaluator::GetMethodProperty method
ms.assetid: c394fe4d-eeb6-4feb-828c-098d84a6f1ba
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e4a82ce250b47f2f199d9e8e8fcf3a2ca7ec5777
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105092177"
---
# <a name="idebugexpressionevaluatorgetmethodproperty"></a>IDebugExpressionEvaluator::GetMethodProperty
このメソッドは、メソッドのローカル、引数、およびその他のプロパティを格納しているプロパティオブジェクトを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetMethodProperty( 
   IDebugSymbolProvider* pSymbolProvider,
   IDebugAddress*        pAddress,
   IDebugBinder*         pBinder,
   BOOL                  fIncludeHiddenLocals,
   IDebugProperty2**     ppProperty
);
```

```csharp
int GetMethodProperty(
   IDebugSymbolProvider pSymbolProvider,
   IDebugAddress        pAddress,
   IDebugBinder         pBinder,
   int                  fIncludeHiddenLocals,
   out IDebugProperty2  ppProperty
);
```

## <a name="parameters"></a>パラメーター
`pSymbolProvider`\
から使用するシンボルプロバイダー。 [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md) オブジェクトとして表現されます。

`pAddress`\
から [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) オブジェクトとして表される、最も近い関数に解決される必要がある、コード内のアドレス。

`pBinder`\
から使用するバインダー。 [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md) オブジェクトとして表現されます。

`fIncludeHiddenLocals`\
から0以外 () は、 `TRUE` 非表示のローカルを含めることを意味します。ゼロ ( `FALSE` ) は、隠しローカルを除外することを意味します。

`ppProperty`\
入出力メソッドを表す [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>注釈
 非表示のローカルは、通常、コンパイラによって生成される変数です。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugExpressionEvaluator](../../../extensibility/debugger/reference/idebugexpressionevaluator.md)
- [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)
- [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)
- [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
