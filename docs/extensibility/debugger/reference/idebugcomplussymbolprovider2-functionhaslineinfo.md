---
title: を提供します。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- FunctionHasLineInfo
- IDebugComPlusSymbolProvider2::FunctionHasLineInfo
ms.assetid: e1b508f1-6521-492f-b110-ab957744a037
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3a574766b884bf1aeed253754534fee66967e9ef
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80733461"
---
# <a name="idebugcomplussymbolprovider2functionhaslineinfo"></a>IDebugComPlusSymbolProvider2::FunctionHasLineInfo
指定したメソッドに行情報があるかどうかを判断します。

## <a name="syntax"></a>構文

```cpp
HRESULT FunctionHasLineInfo(
    IDebugAddress* pAddress
);
```

```csharp
int FunctionHasLineInfo(
    IDebugAddress pAddress
);
```

## <a name="parameters"></a>パラメーター
`pAddress`\
[in]インターフェイスによって表されるデバッグ[アドレス](../../../extensibility/debugger/reference/idebugaddress.md)。 このアドレスはMETHOD_ADDRESSでなければなりません。

## <a name="return-value"></a>戻り値
成功した場合は`S_OK`、 を返します。それ以外の`S_FALSE`場合は、 を返します。

## <a name="example"></a>例
インターフェイスを公開する**CDebugSymbolProvider**オブジェクトに対してこのメソッドを実装する方法を次の例[に](../../../extensibility/debugger/reference/idebugcomplussymbolprovider2.md)示します。

```cpp
HRESULT CDebugSymbolProvider::FunctionHasLineInfo(
    IDebugAddress* pAddress
)
{
    HRESULT hr = S_OK;
    CDEBUG_ADDRESS address;
    CComPtr<CModule> pModule;

    METHOD_ENTRY( CDebugSymbolProvider::LoadSymbol );

    IfFalseGo( pAddress, E_INVALIDARG );

    IfFailGo( pAddress->GetAddress( &address ) );

    ASSERT(address.addr.dwKind == ADDRESS_KIND_METADATA_METHOD);
    IfFalseGo( address.addr.dwKind == ADDRESS_KIND_METADATA_METHOD, S_FALSE );

    IfFailGo( GetModule( address.GetModule(), &pModule) );

    if (!pModule->FunctionHasLineInfo( address.addr.addr.addrMethod.tokMethod,
                                       address.addr.addr.addrMethod.dwVersion))
    {

        // S_FALSE indicates this method does not have line info

        hr = S_FALSE;
    }

Error:

    METHOD_EXIT( CDebugSymbolProvider::LoadSymbol, hr );

    return hr;
}
```

## <a name="see-also"></a>関連項目
- [IDebugComPlusSymbolProvider2](../../../extensibility/debugger/reference/idebugcomplussymbolprovider2.md)
