---
title: METADATA_ADDRESS_LOCAL |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- METADATA_ADDRESS_LOCAL
helpviewer_keywords:
- METADATA_ADDRESS_LOCAL structure
ms.assetid: 635f6bc5-c486-4e0e-83db-36f15e543843
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e3adf9ca5f679c7a526f10b1ee6c91d50dac52d2
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80714485"
---
# <a name="metadata_address_local"></a>METADATA_ADDRESS_LOCAL

この構造体は、スコープ内のローカル変数のアドレスを表します (通常は関数またはメソッド)。

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
ローカル変数が属するメソッドまたは関数の ID。

[C++]`_mdToken`は`typedef`32 ビット`int`用です。

`pLocal`\
この構造体が表すアドレスを持つトークン。

`dwIndex`\
メソッドまたは関数内のこのローカル変数のインデックス、またはその他の値 (言語固有) を指定できます。

## <a name="remarks"></a>Remarks

構造体`dwKind`のフィールドが[(ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md)列挙体の値) に`ADDRESS_KIND_LOCAL`設定されている`DEBUG_ADDRESS_UNION`場合、この構造体は[DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md)構造体の共用体の一部です。

> [!WARNING]
> [C++のみ]null`pLocal`でない場合は、トークン ポインタ`Release` [(DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md)構造体の`addr`フィールド) を呼び出す必要があります。
>
> ```cpp
> if (addr.dwKind == ADDRESS_KIND_METADATA_LOCAL && addr.addr.addrLocal.pLocal != NULL)
> {
>     addr.addr.addrLocal.pLocal->Release();
> }
> ```

## <a name="requirements"></a>必要条件

ヘッダー: sh.h

名前空間: を使用します。

アセンブリ:

## <a name="see-also"></a>関連項目

- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md)
- [DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md)
- [ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md)
