---
title: メソッドの評価メソッド::プロパティ |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExpressionEvaluator::GetMethodLocationProperty
helpviewer_keywords:
- IDebugExpressionEvaluator::GetMethodLocationProperty method
ms.assetid: 52c42a2e-f144-476b-8bef-442464c8fe8e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a6ba87d6c1a1f7370ce5e209440589f362b87035
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80729527"
---
# <a name="idebugexpressionevaluatorgetmethodlocationproperty"></a>IDebugExpressionEvaluator::GetMethodLocationProperty
このメソッドは、メソッドの場所とオフセットをメモリ アドレスに変換します。

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
[in]文字列で表されるメソッドの位置とオフセット。

`pSymbolProvider`\
[in]として表されるシンボル プロバイダー、 [IDebug シンボル プロバイダーオブジェクト](../../../extensibility/debugger/reference/idebugsymbolprovider.md)。

`pAddress`\
[in][メソッド](../../../extensibility/debugger/reference/idebugaddress.md)内のアドレス。

`pBinder`\
[in][IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)オブジェクトとして表されるバインダー。

`ppProperty`\
[アウト]メモリ アドレスを表す[IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)インターフェイスを返します。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 返されたアドレスは、たとえば、ブレークポイントを設定するために使用できます。

 名前`upstrFullyQualifiedMethodPlusOffset`に関わらず、このパラメータには部分的に修飾されたメソッド名を渡すことができます。 その場合、選択されたメソッドは を囲むメソッドです`pAddress`。 このパラメーターの解釈方法は、式エバリュエーターの実装と、それがサポートする言語によって行われます。

## <a name="see-also"></a>関連項目
- [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)
- [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [IDebugExpressionEvaluator](../../../extensibility/debugger/reference/idebugexpressionevaluator.md)
