---
title: IDebugSymbolProvider |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80719171"
---
# <a name="idebugsymbolprovider"></a>IDebugSymbolProvider
このインターフェイスは、シンボルと型を提供し、それらをフィールドとして返すシンボルプロバイダーを表します。

## <a name="syntax"></a>構文

```
IDebugSymbolProvider : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
シンボルプロバイダーは、このインターフェイスを実装して、シンボルと型の情報を式エバリュエーターに提供する必要があります。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
このインターフェイスは、COM の `CoCreateInstance` 関数 (アンマネージシンボルプロバイダーの場合) を使用するか、適切なマネージコードアセンブリを読み込んで、そのアセンブリ内の情報に基づいてシンボルプロバイダーをインスタンス化することによって取得されます。 デバッグエンジンは、式エバリュエーターと連携して動作するようにシンボルプロバイダーをインスタンス化します。 このインターフェイスをインスタンス化する方法の例を参照してください。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
次の表に、のメソッドを示し `IDebugSymbolProvider` ます。

|メソッド|説明|
|------------|-----------------|
|`Initialize`|非推奨。 使用しないでください。|
|`Uninitialize`|使用は推奨されていません。 使用しないでください。|
|[GetContainerField](../../../extensibility/debugger/reference/idebugsymbolprovider-getcontainerfield.md)|デバッグアドレスを格納しているフィールドを取得します。|
|`GetField`|非推奨。 使用しないでください。|
|[GetAddressesFromPosition](../../../extensibility/debugger/reference/idebugsymbolprovider-getaddressesfromposition.md)|ドキュメントの位置をデバッグアドレスの配列にマップします。|
|[GetAddressesFromContext](../../../extensibility/debugger/reference/idebugsymbolprovider-getaddressesfromcontext.md)|ドキュメントコンテキストをデバッグアドレスの配列にマップします。|
|[GetContextFromAddress](../../../extensibility/debugger/reference/idebugsymbolprovider-getcontextfromaddress.md)|デバッグアドレスをドキュメントコンテキストにマップします。|
|[GetLanguage](../../../extensibility/debugger/reference/idebugsymbolprovider-getlanguage.md)|デバッグアドレスでコードをコンパイルするために使用される言語を取得します。|
|`GetGlobalContainer`|非推奨。 使用しないでください。|
|[GetMethodFieldsByName](../../../extensibility/debugger/reference/idebugsymbolprovider-getmethodfieldsbyname.md)|完全修飾メソッド名を表すフィールドを取得します。|
|[GetClassTypeByName](../../../extensibility/debugger/reference/idebugsymbolprovider-getclasstypebyname.md)|完全修飾クラス名を表すクラスフィールド型を取得します。|
|[GetNamespacesUsedAtAddress](../../../extensibility/debugger/reference/idebugsymbolprovider-getnamespacesusedataddress.md)|デバッグアドレスに関連付けられた名前空間の列挙子を作成します。|
|[GetTypeByName](../../../extensibility/debugger/reference/idebugsymbolprovider-gettypebyname.md)|シンボル名をシンボルの種類にマップします。|
|[GetNextAddress](../../../extensibility/debugger/reference/idebugsymbolprovider-getnextaddress.md)|メソッド内の指定されたデバッグアドレスの後に続くデバッグアドレスを取得します。|

## <a name="remarks"></a>注釈
このインターフェイスは、ドキュメントの位置をデバッグアドレスに、またはその逆にマップします。

## <a name="requirements"></a>必要条件
ヘッダー: sh. h

名前空間: VisualStudio。

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="example"></a>例
この例では、GUID (デバッグエンジンがこの値を認識している必要があります) を指定して、シンボルプロバイダーをインスタンス化する方法を示します。

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
