---
title: 'IDebugGenericParamField:: GetFlags |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- GetFlags
- IDebugGenericParamField::GetFlags
ms.assetid: adcbbca1-8960-4c88-86b0-8b9467056c97
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 8d131a5dc4a1fd64f2a82bff4f51f7cbc4a905a8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80728004"
---
# <a name="idebuggenericparamfieldgetflags"></a>IDebugGenericParamField::GetFlags
このジェネリックパラメーターのフラグを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetFlags(
    DWORD* pdwFlags
);
```

```csharp
int GetFlags(
    ref uint pdwFlags
);
```

## <a name="parameters"></a>パラメーター
`pdwFlags`\
入出力このジェネリックパラメーターのフラグを返します。

## <a name="return-value"></a>戻り値
成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
これらのフラグには、さまざまな特殊な制約に関する情報が含まれています。

## <a name="example"></a>例
次の例は、 [IDebugGenericParamField](../../../extensibility/debugger/reference/idebuggenericparamfield.md)インターフェイスを公開する**CDebugGenericParamFieldType**オブジェクトに対してこのメソッドを実装する方法を示しています。

```cpp
HRESULT CDebugGenericParamFieldType::GetFlags(DWORD *pdwFlags)
{
    HRESULT hr = S_OK;

    METHOD_ENTRY( CDebugGenericParamFieldType::GetFlags );

    IfFalseGo( pdwFlags, E_INVALIDARG );
    IfFailGo( this->LoadProps() );
    *pdwFlags = m_dwFlags;

Error:

    METHOD_EXIT( CDebugGenericParamFieldType::GetFlags, hr );
    return hr;
}
```

## <a name="see-also"></a>関連項目
- [IDebugGenericParamField](../../../extensibility/debugger/reference/idebuggenericparamfield.md)
