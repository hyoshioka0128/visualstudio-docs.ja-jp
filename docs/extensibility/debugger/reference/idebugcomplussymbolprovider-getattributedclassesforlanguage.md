---
title: IDebugComPlusSymbolProvider::GetAttributedClassesForLanguage
titleSuffix: ''
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- GetAttributedClassesForLanguage
- IDebugComPlusSymbolProvider::GetAttributedClassesForLanguage
ms.assetid: e5b1b8b6-52a6-4ade-9a36-644abfa9f4b2
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 2c82357a79a1921986b6d7acc2cb1fcde208d9c0
ms.sourcegitcommit: 2a201c93ed526b0f7e5848657500f1111b08ac2a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2020
ms.locfileid: "89741491"
---
# <a name="idebugcomplussymbolprovidergetattributedclassesforlanguage"></a>IDebugComPlusSymbolProvider::GetAttributedClassesForLanguage
指定したプログラミング言語で実装されている、指定した属性を持つクラスを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetAttributedClassesForLanguage (
    GUID               guidLanguage,
    LPOLESTR           pstrAttribute,
    IEnumDebugFields** ppEnum
);
```

```csharp
int GetAttributedClassesForLanguage (
    Guid                 guidLanguage,
    string               pstrAttribute,
    out IEnumDebugFields ppEnum
);
```

## <a name="parameters"></a>パラメーター
`guidLanguage`\
から言語の一意の識別子。

`pstrAttribute`\
から属性文字列。

`ppEnum`\
入出力属性クラスの列挙体を返します。

## <a name="return-value"></a>戻り値
成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="example"></a>例
次の例は、 [IDebugComPlusSymbolProvider](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md)インターフェイスを公開する**Cdebugシンボルプロバイダー**オブジェクトに対してこのメソッドを実装する方法を示しています。

```cpp
HRESULT CDebugSymbolProvider::GetAttributedClassesForLanguage(
    GUID guidLanguage,
    __in_z LPOLESTR pstrAttribute,
    IEnumDebugFields** ppEnum
)
{
    HRESULT hr = S_OK;
    CFieldList listFields;
    CModIter ModIter;
    CModule* pModule; // the iterator owns the reference
    ULONG cClasses = 0;
    DWORD iTypeDef = 0;
    mdTypeDef* rgTypeDefs = NULL;
    IDebugField** rgFields = NULL;
    DWORD ctField = 0;
    CEnumDebugFields* pEnumFields = NULL;

    ASSERT(IsValidObjectPtr(this, CDebugSymbolProvider));
    ASSERT(IsValidWritePtr(ppEnum, IEnumDebugFields*));

    METHOD_ENTRY( CDebugSymbolProvider::GetAttributedClassesForLanguage );

    IfFalseGo( ppEnum, E_INVALIDARG );
    *ppEnum = NULL;

    // For Each Module - call EnumFields
    IfFailGo( GetModuleIter(&ModIter) );

    // Find the Max number of classes
    while (ModIter.GetNext(&pModule))
    {
        CComPtr<IMetaDataImport> pMetaData;
        HCORENUM hEnum = 0;
        ULONG cTypeDefs;
        ULONG cEnum;

        pModule->GetMetaData( &pMetaData );

        IfFailGo( pMetaData->EnumTypeDefs( &hEnum,
                                           NULL,
                                           0,
                                           &cTypeDefs ) );
        IfFailGo( pMetaData->CountEnum( hEnum, &cEnum ) );
        cClasses += cEnum;
    }

    IfNullGo( rgTypeDefs = new mdTypeDef[cClasses], E_OUTOFMEMORY );
    IfNullGo( rgFields = new IDebugField * [cClasses], E_OUTOFMEMORY );

    ModIter.Reset();

    // Create the classes
    while (ModIter.GetNext(&pModule))
    {
        CComPtr<IMetaDataImport> pMetaData;
        HCORENUM hEnum = 0;
        ULONG cTypeDefs;
        ULONG cEnum;
        const void* pUnused;
        ULONG cbUnused;

        pModule->GetMetaData( &pMetaData );

        IfFailGo( pMetaData->EnumTypeDefs( &hEnum,
                                           NULL,
                                           0,
                                           &cTypeDefs ) );
        IfFailGo( pMetaData->CountEnum( hEnum, &cEnum ) );
        IfFailGo( pMetaData->EnumTypeDefs( &hEnum,
                                           rgTypeDefs,
                                           cEnum,
                                           &cTypeDefs ) );

        pMetaData->CloseEnum(hEnum);
        hEnum = NULL;

        for ( iTypeDef = 0; iTypeDef < cTypeDefs; iTypeDef++)
        {

            if (pMetaData->GetCustomAttributeByName( rgTypeDefs[iTypeDef],
                    pstrAttribute,
                    &pUnused,
                    &cbUnused ) == S_OK)
            {
                // Only return classes implemeted in the correct language

                if (pModule->ClassImplementedInLanguage( rgTypeDefs[iTypeDef],
                        guidLanguage) )
                {
                    if (CreateClassType( pModule->GetID(),
                                         rgTypeDefs[iTypeDef],
                                         rgFields + ctField) == S_OK)
                    {
                        ctField++;
                    }
                    else
                    {
                        ASSERT(!"Failed to Create Attributed Class");
                    }
                }
            }
        }
    }

    IfNullGo( pEnumFields = new CEnumDebugFields, E_OUTOFMEMORY );
    IfFailGo( pEnumFields->Initialize(rgFields, ctField) );
    IfFailGo( pEnumFields->QueryInterface( __uuidof(IEnumDebugFields),
                                           (void**) ppEnum ) );

Error:

    METHOD_EXIT( CDebugSymbolProvider::GetAttributedClassesForLanguage, hr );

    DELETERG( rgTypeDefs );

    for ( iTypeDef = 0; iTypeDef < ctField; iTypeDef++)
    {
        RELEASE( rgFields[iTypeDef] );
    }

    DELETERG( rgFields );
    RELEASE( pEnumFields );

    return hr;
}
```

## <a name="see-also"></a>関連項目
- [IDebugComPlusSymbolProvider](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md)
