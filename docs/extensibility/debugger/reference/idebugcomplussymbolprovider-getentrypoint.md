---
title: を提供します。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugComPlusSymbolProvider::GetEntryPoint
- GetEntryPoint
ms.assetid: 9640e121-1da1-41f9-8e66-76efca36baf2
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c686659d2a3d5e81e8e466bf1707337842cf8317
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80733903"
---
# <a name="idebugcomplussymbolprovidergetentrypoint"></a>IDebugComPlusSymbolProvider::GetEntryPoint
アプリケーションのエントリ ポイントを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetEntryPoint(
    ULONG32         ulAppDomainID,
    GUID            guidModule,
    IDebugAddress** ppAddress
);
```

```csharp
int GetEntryPoint(
    uint              ulAppDomainID,
    Guid              guidModule,
    out IDebugAddress ppAddress
);
```

## <a name="parameters"></a>パラメーター
`ulAppDomainID`\
[in]アプリケーション ドメインの識別子。

`guidModule`\
[in]モジュールの一意の識別子です。

`ppAddress`\
[アウト][インターフェイス](../../../extensibility/debugger/reference/idebugaddress.md)によって表されるエントリ ポイントを返します。

## <a name="return-value"></a>戻り値
成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="example"></a>例
インターフェイスを公開する**CDebugSymbolProvider**オブジェクトに対してこのメソッドを実装する方法を次の例[に](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md)示します。

```cpp
HRESULT CDebugSymbolProvider::GetEntryPoint(
    ULONG32 ulAppDomainID,
    GUID guidModule,
    IDebugAddress **ppAddress
)
{
    HRESULT hr = S_OK;
    CComPtr<CModule> pModule;
    Module_ID idModule(ulAppDomainID, guidModule);

    ASSERT(IsValidObjectPtr(this, CDebugSymbolProvider));
    ASSERT(IsValidWritePtr(ppAddress, IDebugAddress *));

    METHOD_ENTRY( CDebugSymbolProvider::GetEntryPoint );

    IfFalseGo( ppAddress, E_INVALIDARG );

    *ppAddress = NULL;

    IfFailGo( GetModule( idModule, &pModule) );

    IfFailGo( pModule->GetEntryPoint( ppAddress ) );

Error:

    METHOD_EXIT( CDebugSymbolProvider::GetEntryPoint, hr );

    return hr;
}
```

## <a name="see-also"></a>関連項目
- [IDebugComPlusSymbolProvider](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md)
