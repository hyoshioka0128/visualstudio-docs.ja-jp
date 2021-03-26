---
description: このメソッドは、メソッドの場所とオフセットをメモリアドレスに変換します。
title: 'IDebugExpressionEvaluator:: GetMethodLocationProperty |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExpressionEvaluator::GetMethodLocationProperty
helpviewer_keywords:
- IDebugExpressionEvaluator::GetMethodLocationProperty method
ms.assetid: 52c42a2e-f144-476b-8bef-442464c8fe8e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ddc9c17b90be6d65786d58ff2bf585461c4fc69f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105092190"
---
# <a name="idebugexpressionevaluatorgetmethodlocationproperty"></a>IDebugExpressionEvaluator::GetMethodLocationProperty
このメソッドは、メソッドの場所とオフセットをメモリアドレスに変換します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetMethodLocationProperty( 
   LPCOLESTR             upstrFullyQualifiedMethodPlusOffset,
   IDebugSymbolProvider* pSymbolProvider,
   IDebugAddress*        pAddress,
   IDebugBinder*         pBinder,
   IDebugProperty2**     ppProperty
);
```

```csharp
int GetMethodLocationProperty(
   string               upstrFullyQualifiedMethodPlusOffset,
   IDebugSymbolProvider pSymbolProvider,
   IDebugAddress        pAddress,
   IDebugBinder         pBinder,
   out IDebugProperty2  ppProperty
);
```

## <a name="parameters"></a>パラメーター
`upstrFullyQualifiedMethodPlusOffset`\
から文字列として表現されるメソッドの場所とオフセット。

`pSymbolProvider`\
から [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md) オブジェクトとして表現されるシンボルプロバイダー。

`pAddress`\
から [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) オブジェクトとして表される、メソッド内のアドレス。

`pBinder`\
から [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md) オブジェクトとして表現されたバインダー。

`ppProperty`\
入出力メモリアドレスを表す [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) インターフェイスを返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>注釈
 返されたアドレスを使用して、ブレークポイントを設定できます。たとえば、のようになります。

 名前にかかわらず `upstrFullyQualifiedMethodPlusOffset` 、このパラメーターには部分的に修飾されたメソッド名を渡すことができます。 その場合は、選択されたメソッドが、を囲むメソッドです `pAddress` 。 このパラメーターがどのように解釈されるかは、式エバリュエーターとそれがサポートする言語の実装になります。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)
- [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [IDebugExpressionEvaluator](../../../extensibility/debugger/reference/idebugexpressionevaluator.md)
