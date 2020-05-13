---
title: METADATA_ADDRESS_ARRAYELEM |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- METADATA_ADDRESS_ARRAYELEM
helpviewer_keywords:
- METADATA_ADDRESS_ARRAYELEM structure
ms.assetid: 24321be5-7c17-4038-82a1-c20a2b68ff3c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 67e39eb8b03dd6f75ac39155bd744e03084beb0b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80714546"
---
# <a name="metadata_address_arrayelem"></a>METADATA_ADDRESS_ARRAYELEM

この構造体は、配列内の配列要素を表します。

## <a name="syntax"></a>構文

```cpp
typedef struct _tagMETADATA_ADDRESS_ARRAYELEM {
    _mdToken tokMethod;
    DWORD    dwIndex;
} METADATA_ADDRESS_ARRAYELEM;
```

```csharp
public struct METADATA_ADDRESS_ARRAYELEM {
    public int  tokMethod;
    public uint dwIndex;
}
```

## <a name="members"></a>メンバー

`tokMethod`\
この要素の一部である配列の ID。

[C++]`_mdToken`は`typedef`32 ビット`int`用です。

`dwIndex`\
配列内のこの要素のインデックス。

## <a name="remarks"></a>Remarks
構造体`dwKind`のフィールドが[(ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md)列挙体の値) に`ADDRESS_KIND_ARRAYELEM`設定されている`DEBUG_ADDRESS_UNION`場合、この構造体は[DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md)構造体の共用体の一部です。

## <a name="requirements"></a>必要条件
ヘッダー: sh.h

名前空間: を使用します。

アセンブリ:

## <a name="see-also"></a>関連項目

- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md)
- [ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md)
