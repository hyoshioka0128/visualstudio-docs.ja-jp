---
description: 'IDebugComPlusSymbolProvider2:: GetTypeFromToken は、そのトークンを指定して型を取得します。'
title: 'IDebugComPlusSymbolProvider2:: GetTypeFromToken |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugComPlusSymbolProvider2::GetTypeFromToken
- GetTypeFromToken
ms.assetid: 4452bc5d-0225-40e0-a467-c472a5c7c4ee
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3f4bcc8d92cc58a719e9b450ec79e8376de554ab
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105077981"
---
# <a name="idebugcomplussymbolprovider2gettypefromtoken"></a>IDebugComPlusSymbolProvider2::GetTypeFromToken
トークンを指定して型を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetTypeFromToken(
    ULONG32       appDomain,
    GUID          guidModule,
    DWORD         tdToken,
    IDebugField** ppField
);
```

```csharp
int GetTypeFromToken(
    uint            appDomain,
    Guid            guidModule,
    uint            tdToken,
    out IDebugField ppField
);
```

## <a name="parameters"></a>パラメーター
`appDomain`\
からアプリケーションドメインの識別子。

`guidModule`\
からモジュールの一意識別子。

`tdToken`\
から取得する型のトークン。

`ppField`\
入出力 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)によって表される型を返します。

## <a name="return-value"></a>戻り値
成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="example"></a>例
次の例は、 [IDebugComPlusSymbolProvider2](../../../extensibility/debugger/reference/idebugcomplussymbolprovider2.md)インターフェイスを公開する **Cdebugシンボルプロバイダー** オブジェクトに対してこのメソッドを実装する方法を示しています。

```cpp
HRESULT CDebugSymbolProvider::GetTypeFromToken(
    ULONG32 ulAppDomainID,
    GUID guidModule,
    DWORD tdToken,
    IDebugField **ppField)
{
    HRESULT hr = E_FAIL;

    METHOD_ENTRY( CDebugDynamicFieldSymbol::GetTypeFromToken );

    ASSERT(IsValidObjectPtr(this, CDebugSymbolProvider));
    ASSERT(IsValidWritePtr(ppField, IDebugField*));

    Module_ID idModule(ulAppDomainID, guidModule);

    IfFailGo( this->CreateClassType(idModule, tdToken, ppField) );

Error:

    METHOD_EXIT( CDebugDynamicFieldSymbol::GetTypeFromToken, hr );

    return hr;
}
```

## <a name="see-also"></a>こちらもご覧ください
- [IDebugComPlusSymbolProvider2](../../../extensibility/debugger/reference/idebugcomplussymbolprovider2.md)
