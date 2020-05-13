---
title: IDebug ジェネリックパラムフィールド::形式パラムの取得 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugGenericParamField::GetNameOfFormalParam
- GetNameOfFormalParam
ms.assetid: 05032a83-49ce-4007-b5d6-7b56945b956c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 03fb76b96804df900e21b0f91b9c5ba599449cf5
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80727960"
---
# <a name="idebuggenericparamfieldgetnameofformalparam"></a>IDebugGenericParamField::GetNameOfFormalParam
このジェネリック パラメーターの名前を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetNameOfFormalParam (
    BSTR* pbstrName
);
```

```csharp
int GetNameOfFormalParam (
    string pbstrName
);
```

## <a name="parameters"></a>パラメーター
`pbstrName`\
[アウト]このジェネリック パラメーターの名前。

## <a name="return-value"></a>戻り値
成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="example"></a>例
インターフェイスを公開する**オブジェクト**に対してこの[メソッドを実装](../../../extensibility/debugger/reference/idebuggenericparamfield.md)する方法を次の例に示します。

```cpp
HRESULT CDebugGenericParamFieldType::GetNameOfFormalParam(BSTR *pbstrName)
{
    HRESULT hr = S_OK;
    CComBSTR bstrName;

    METHOD_ENTRY( CDebugGenericParamFieldType::GetNameOfFormalParam );

    IfFalseGo( pbstrName, E_INVALIDARG );
    IfFailGo( this->LoadProps() );
    IfNullGo( *pbstrName = SysAllocString(m_bstrName), E_OUTOFMEMORY );

Error:

    METHOD_EXIT( CDebugGenericParamFieldType::GetNameOfFormalParam, hr );
    return hr;
}
```

## <a name="see-also"></a>関連項目
- [IDebugGenericParamField](../../../extensibility/debugger/reference/idebuggenericparamfield.md)
