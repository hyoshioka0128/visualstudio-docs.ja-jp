---
title: NATIVE_ADDRESS |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- NATIVE_ADDRESS
helpviewer_keywords:
- NATIVE_ADDRESS structure
ms.assetid: 7a0cd085-bfc8-45cc-a3d4-4459070e207a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 7c62bbea846f3d486ead8add4dfab2182df1e1bb
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80714339"
---
# <a name="native_address"></a>NATIVE_ADDRESS

この構造体は、ネイティブ アドレスを表します。

## <a name="syntax"></a>構文

```cpp
typedef struct _tagNATIVE_ADDRESS {
    DWORD unknown;
} NATIVE_ADDRESS;
```

```csharp
public struct NATIVE_ADDRESS {
    public uint unknown;
}
```

## <a name="members"></a>メンバー

`unknown`\
ネイティブ アドレス (この意味は、ランタイムとオペレーティング システムによって異なります)。

## <a name="remarks"></a>Remarks

構造体`dwKind`のフィールドが[(ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md)列挙体の値) に`ADDRESS_KIND_NATIVE`設定されている`DEBUG_ADDRESS_UNION`場合、この構造体は[DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md)構造体の共用体の一部です。

## <a name="requirements"></a>必要条件

ヘッダー: sh.h

名前空間: を使用します。

アセンブリ:

## <a name="see-also"></a>関連項目

- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md)
