---
title: をクリックします。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugSymbolProvider
helpviewer_keywords:
- IDebugSymbolProvider interface
ms.assetid: df5f095f-1dee-46f9-84cf-92417c71d5fb
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 11e180288a9312d9af5a3d3b1bd63d8f2266f581
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80719171"
---
# <a name="idebugsymbolprovider"></a>IDebugSymbolProvider
このインターフェイスは、シンボルと型を提供するシンボル プロバイダーを表し、それらをフィールドとして返します。

## <a name="syntax"></a>構文

```
IDebugSymbolProvider : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
シンボル プロバイダーは、シンボルと型の情報を式エバリュエーターに提供するために、このインターフェイスを実装する必要があります。

## <a name="notes-for-callers"></a>発信者向けのメモ
このインターフェイスは、COM の`CoCreateInstance`関数 (アンマネージ シンボル プロバイダーの場合) を使用するか、適切なマネージ コード アセンブリを読み込み、そのアセンブリ内の情報に基づいてシンボル プロバイダーをインスタンス化することによって取得されます。 デバッグ エンジンは、式エバリュエーターと連携して動作するシンボル プロバイダーをインスタンス化します。 このインターフェイスをインスタンス化する 1 つの方法については、例を参照してください。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
次の表に`IDebugSymbolProvider`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|`Initialize`|非推奨になりました。 使用しないでください。|
|`Uninitialize`|非推奨になりました。 使用しないでください。|
|[GetContainerField](../../../extensibility/debugger/reference/idebugsymbolprovider-getcontainerfield.md)|デバッグ アドレスを含むフィールドを取得します。|
|`GetField`|非推奨になりました。 使用しないでください。|
|[GetAddressesFromPosition](../../../extensibility/debugger/reference/idebugsymbolprovider-getaddressesfromposition.md)|ドキュメントの位置をデバッグ アドレスの配列にマップします。|
|[GetAddressesFromContext](../../../extensibility/debugger/reference/idebugsymbolprovider-getaddressesfromcontext.md)|ドキュメント コンテキストをデバッグ アドレスの配列にマップします。|
|[GetContextFromAddress](../../../extensibility/debugger/reference/idebugsymbolprovider-getcontextfromaddress.md)|デバッグ アドレスをドキュメント コンテキストにマップします。|
|[GetLanguage](../../../extensibility/debugger/reference/idebugsymbolprovider-getlanguage.md)|デバッグ アドレスでコードをコンパイルするために使用する言語を取得します。|
|`GetGlobalContainer`|非推奨になりました。 使用しないでください。|
|[GetMethodFieldsByName](../../../extensibility/debugger/reference/idebugsymbolprovider-getmethodfieldsbyname.md)|完全修飾メソッド名を表すフィールドを取得します。|
|[GetClassTypeByName](../../../extensibility/debugger/reference/idebugsymbolprovider-getclasstypebyname.md)|完全修飾クラス名を表すクラス フィールド型を取得します。|
|[GetNamespacesUsedAtAddress](../../../extensibility/debugger/reference/idebugsymbolprovider-getnamespacesusedataddress.md)|デバッグ アドレスに関連付けられている名前空間の列挙子を作成します。|
|[GetTypeByName](../../../extensibility/debugger/reference/idebugsymbolprovider-gettypebyname.md)|シンボル名をシンボル タイプにマップします。|
|[GetNextAddress](../../../extensibility/debugger/reference/idebugsymbolprovider-getnextaddress.md)|メソッド内の特定のデバッグ アドレスの後に続くデバッグ アドレスを取得します。|

## <a name="remarks"></a>Remarks
このインターフェイスは、ドキュメントの位置をデバッグ アドレスにマップし、その逆も同様です。

## <a name="requirements"></a>必要条件
ヘッダー: sh.h

名前空間: を使用します。

アセンブリ:

## <a name="example"></a>例
この例では、GUID を指定してシンボル プロバイダーをインスタンス化する方法を示します (デバッグ エンジンはこの値を知っている必要があります)。

```cpp
// A debug engine uses its own symbol provider and would know the GUID
// of that provider.
IDebugSymbolProvider *GetSymbolProvider(GUID *pSymbolProviderGuid)
{
    // This is typically defined globally. For this example, it is
    // defined here.
    static const WCHAR strRegistrationRoot[] = L"Software\\Microsoft\\VisualStudio\\8.0Exp";
    IDebugSymbolProvider *pProvider = NULL;
    if (pSymbolProviderGuid != NULL) {
        CLSID clsidProvider = { 0 };
        ::GetSPMetric(*pSymbolProviderGuid,
                      storetypeFile,
                      metricCLSID,
                      &clsidProvider,
                      strRegistrationRoot);
        if (IsEqualGUID(clsidProvider,GUID_NULL)) {
            // No file type provider, try metadata provider.
            ::GetSPMetric(*pSymbolProviderGuid,
                          ::storetypeMetadata,
                          metricCLSID,
                          &clsidProvider,
                          strRegistrationRoot);
        }
        if (!IsEqualGUID(clsidProvider,GUID_NULL)) {
            CComPtr<IDebugSymbolProvider> spSymbolProvider;
            spSymbolProvider.CoCreateInstance(clsidProvider);
            if (spSymbolProvider != NULL) {
                pProvider = spSymbolProvider.Detach();
            }
        }
    }
    return(pProvider);
}
```

## <a name="see-also"></a>関連項目
- [シンボル プロバイダーのインターフェイス](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
