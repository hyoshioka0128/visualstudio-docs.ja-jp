---
title: 'IPropertyProxyEESide:: ResolveAssemblyRef |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IPropertyProxyEESide::ResolveAssemblyRef
helpviewer_keywords:
- IPropertyProxyEESide::ResolveAssemblyRef
ms.assetid: 662ca0a6-dad0-4c00-a718-bb3bbc5bd9da
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: fc14d3aff5116f7bfb18244f39d14ec2dbbd37f1
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99895961"
---
# <a name="ipropertyproxyeesideresolveassemblyref"></a>IPropertyProxyEESide::ResolveAssemblyRef
指定したマネージアセンブリ参照の場所を決定します。

## <a name="syntax"></a>構文

```cpp
HRESULT ResolveAssemblyRef(
   BSTR*                  assemName,
   IEEDataStorage**       assemBytes,
   IEEDataStorage**       assemPdb,
   BSTR*                  assemLocation,
   ASSEMBLYLOCRESOLUTION* alr
);
```

```csharp
int ResolveAssemblyRef(
   ref string                     assemName,
   out IEEDataStorage             assemBytes,
   out IEEDataStorage             assemPdb,
   out string                     assemLocation,
   out enum_ASSEMBLYLOCRESOLUTION alr
);
```

## <a name="parameters"></a>パラメーター
`assemName`\
から解決するアセンブリの名前。

`assemBytes`\
入出力参照に関連付けられているアセンブリのバイト数を含む [Ieedatastorage](../../../extensibility/debugger/reference/ieedatastorage.md) オブジェクトを返します。

`assemPdb`\
入出力 `IEEDataStorage` この参照に関連付けられているシンボルストアデータを格納しているオブジェクトを返します。

`assemLocation`\
入出力この参照のパスの場所を返します。

`alr`\
入出力この参照のアセンブリの場所を示す値を [Assemblylocresolution](../../../extensibility/debugger/reference/assemblylocresolution.md) 列挙から返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
 このメソッドは、通常、カスタム式エバリュエーターによって実装されていません。

## <a name="see-also"></a>関連項目
- [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)
- [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)
- [ASSEMBLYLOCRESOLUTION](../../../extensibility/debugger/reference/assemblylocresolution.md)
