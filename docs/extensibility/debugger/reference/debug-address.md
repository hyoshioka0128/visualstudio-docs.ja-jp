---
title: DEBUG_ADDRESS |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DEBUG_ADDRESS
helpviewer_keywords:
- DEBUG_ADDRESS structure
ms.assetid: 79f5e765-9aac-4b6e-82ef-bed88095e9ba
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: fe778ba3ed80930a4cd7b4fa1170f286b3ccf6ec
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737512"
---
# <a name="debug_address"></a>DEBUG_ADDRESS
この構造体はアドレスを表します。

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
> この値はシンボル プロバイダーに固有であるため、クラス型の識別子以外の一般的な意味はありません。

`addr`\
DEBUG_ADDRESS_UNION[構造体で](../../../extensibility/debugger/reference/debug-address-union.md)、個々の住所タイプを記述する構造体の和集合を含みます。 値`addr`。`dwKind` 共用体の解釈方法を説明する[ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md)列挙体から取得されます。

## <a name="remarks"></a>Remarks
この構造体は[、GetAddress](../../../extensibility/debugger/reference/idebugaddress-getaddress.md)メソッドに渡され、値が入力されます。

**警告 [C++ のみ]**

が`addr.dwKind` `ADDRESS_KIND_METADATA_LOCAL` null`addr.addr.addrLocal.pLocal`値でない場合は、トークン ポインターを呼`Release`び出す必要があります。

```
if (addr.dwKind == ADDRESS_KIND_METADATA_LOCAL && addr.addr.addrLocal.pLocal != NULL)
{
    addr.addr.addrLocal.pLocal->Release();
}
```

## <a name="requirements"></a>必要条件
ヘッダー: sh.h

名前空間: を使用します。

アセンブリ:

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [GetAddress](../../../extensibility/debugger/reference/idebugaddress-getaddress.md)
- [DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md)
- [ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md)
