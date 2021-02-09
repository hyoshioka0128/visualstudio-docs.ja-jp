---
title: 'IDebugComPlusSymbolProvider:: Loadシンボル Fromstream |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugComPlusSymbolProvider::LoadSymbolsFromStream
- LoadSymbolsFromStream
ms.assetid: 1de272f0-24f4-4548-8b70-a205cddd4727
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9c3c4c5cbaea8328f0240b5bf41fde3ea7042635
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99842512"
---
# <a name="idebugcomplussymbolproviderloadsymbolsfromstream"></a>IDebugComPlusSymbolProvider::LoadSymbolsFromStream
データストリームを指定してデバッグシンボルを読み込みます。

## <a name="syntax"></a>構文

```cpp
HRESULT LoadSymbolsFromStream(
    ULONG32   ulAppDomainID,
    GUID      guidModule,
    ULONGLONG baseAddress,
    IUnknown* pUnkMetadataImport,
    IStream*  pStream
);
```

```csharp
int LoadSymbolsFromStream(
    uint    ulAppDomainID,
    Guid    guidModule,
    ulong   baseAddress,
    object  pUnkMetadataImport,
    IStream pStream
);
```

## <a name="parameters"></a>パラメーター
`ulAppDomainID`\
からアプリケーションドメインの識別子。

`guidModule`\
からモジュールの一意識別子。

`baseAddress`\
からベースメモリアドレス。

`pUnkMetadataImport`\
からシンボルメタデータを格納しているオブジェクト。

`pStream`\
からシンボルを格納しているデータストリーム。

## <a name="return-value"></a>戻り値
成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="example"></a>例
次の例は、 [IDebugComPlusSymbolProvider](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md)インターフェイスを公開する **Cdebugシンボルプロバイダー** オブジェクトに対してこのメソッドを実装する方法を示しています。 メソッドは、 [Loadシンボル Fromstreamwithcormodule](../../../extensibility/debugger/reference/idebugcomplussymbolprovider2-loadsymbolsfromstreamwithcormodule.md) メソッドを呼び出します。

```cpp
HRESULT CDebugSymbolProvider::LoadSymbolsFromStream(
    ULONG32 ulAppDomainID,
    GUID guidModule,
    ULONGLONG baseOffset,
    IUnknown* pUnkMetadataImport,
    IStream* pStream
)
{
    return LoadSymbolsFromStreamWithCorModule (ulAppDomainID, guidModule, baseOffset, pUnkMetadataImport, NULL, pStream);
}
```

## <a name="see-also"></a>関連項目
- [IDebugComPlusSymbolProvider](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md)
