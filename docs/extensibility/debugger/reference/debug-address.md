---
title: DEBUG_ADDRESS |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DEBUG_ADDRESS
helpviewer_keywords:
- DEBUG_ADDRESS structure
ms.assetid: 79f5e765-9aac-4b6e-82ef-bed88095e9ba
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e02f78e82c87bceb10b71bcb303a78f25a9a623e
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99899117"
---
# <a name="debug_address"></a>DEBUG_ADDRESS
この構造体は、アドレスを表します。

## <a name="syntax"></a>構文

```cpp
typedef struct _tagDEBUG_ADDRESS {
    ULONG32             ulAppDomainID;
    GUID                guidModule;
    _mdToken            tokClass;
    DEBUG_ADDRESS_UNION addr;
} DEBUG_ADDRESS;
```

```csharp
public struct DEBUG_ADDRESS {
    public uint                ulAppDomainID;
    public Guid                guidModule;
    public int                 tokClass;
    public DEBUG_ADDRESS_UNION addr;
}
```

## <a name="members"></a>メンバー
`ulAppDomainID`\
プロセス ID。

`guidModule`\
このアドレスを含むモジュールの GUID。

`tokClass`\
このアドレスのクラスまたは型を識別するトークン。

> [!NOTE]
> この値はシンボルプロバイダーに固有であるため、クラス型の識別子としてではなく、一般的な意味を持ちません。

`addr`\
[DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md)構造体。個々のアドレスの種類を記述する構造体の和集合を格納します。 値 `addr` 。`dwKind` は、 [ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md) 列挙体から取得します。これは、共用体を解釈する方法を説明します。

## <a name="remarks"></a>解説
この構造体は、入力される [Getaddress](../../../extensibility/debugger/reference/idebugaddress-getaddress.md) メソッドに渡されます。

**警告 [C++ のみ]**

がで、 `addr.dwKind` `ADDRESS_KIND_METADATA_LOCAL` `addr.addr.addrLocal.pLocal` が null 値でない場合は、トークンポインターでを呼び出す必要があり `Release` ます。

```
if (addr.dwKind == ADDRESS_KIND_METADATA_LOCAL && addr.addr.addrLocal.pLocal != NULL)
{
    addr.addr.addrLocal.pLocal->Release();
}
```

## <a name="requirements"></a>要件
ヘッダー: sh. h

名前空間: VisualStudio。

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [GetAddress](../../../extensibility/debugger/reference/idebugaddress-getaddress.md)
- [DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md)
- [ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md)
