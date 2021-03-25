---
description: この構造体は、スコープ内のローカル変数のアドレス (通常は関数またはメソッド) を表します。
title: METADATA_ADDRESS_LOCAL |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- METADATA_ADDRESS_LOCAL
helpviewer_keywords:
- METADATA_ADDRESS_LOCAL structure
ms.assetid: 635f6bc5-c486-4e0e-83db-36f15e543843
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c265f8312b9a23b3b10f06595240dae20894f001
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105061551"
---
# <a name="metadata_address_local"></a>METADATA_ADDRESS_LOCAL

この構造体は、スコープ内のローカル変数のアドレス (通常は関数またはメソッド) を表します。

## <a name="syntax"></a>構文

```cpp
typedef struct _tagMETADATA_ADDRESS_LOCAL {
    _mdToken  tokMethod;
    IUnknown* pLocal;
    DWORD     dwIndex;
} METADATA_ADDRESS_LOCAL;
```

```csharp
public struct METADATA_ADDRESS_LOCAL {
    public int    tokMethod;
    public object pLocal;
    public uint   dwIndex;
}
```

## <a name="members"></a>メンバー

`tokMethod`\
ローカル変数が含まれているメソッドまたは関数の ID。

[C++] `_mdToken` は、 `typedef` 32 ビットのです `int` 。

`pLocal`\
この構造体が表すアドレスを持つトークン。

`dwIndex`\
には、メソッドまたは関数内のこのローカル変数のインデックス、またはその他の値 (言語固有) を指定できます。

## <a name="remarks"></a>注釈

この構造体は、構造体のフィールドがに設定されている場合に、 [DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md) 構造体の和集合の一部になり `dwKind` `DEBUG_ADDRESS_UNION` `ADDRESS_KIND_LOCAL` ます ( [ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md) 列挙型の値)。

> [!WARNING]
> [C++ のみ] `pLocal` が null でない場合は、トークンポインターでを呼び出す必要があり `Release` `addr` ます (は [DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md) 構造のフィールドです)。
>
> ```cpp
> if (addr.dwKind == ADDRESS_KIND_METADATA_LOCAL && addr.addr.addrLocal.pLocal != NULL)
> {
>     addr.addr.addrLocal.pLocal->Release();
> }
> ```

## <a name="requirements"></a>要件

ヘッダー: sh. h

名前空間: VisualStudio。

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>こちらもご覧ください

- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md)
- [DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md)
- [ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md)
