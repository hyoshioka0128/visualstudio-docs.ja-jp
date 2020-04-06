---
title: METADATA_ADDRESS_METHOD |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- METADATA_ADDRESS_METHOD
helpviewer_keywords:
- METADATA_ADDRESS_METHOD structure
ms.assetid: fc0e5370-1b4f-4867-837f-0d63c4b9dd09
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: bc3dd7a34e4f9a3e1b933781aeaf4e18cad7ec17
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80714453"
---
# <a name="metadata_address_method"></a>METADATA_ADDRESS_METHOD
この構造体は、クラスのメソッドのアドレスを表します。

## <a name="syntax"></a>構文

```cpp
typedef struct _tagMETADATA_ADDRESS_METHOD {
   _mdToken tokMethod;
   DWORD    dwOffset;
   DWORD    dwVersion;
} METADATA_ADDRESS_METHOD;
```

```csharp
public struct METADATA_ADDRESS_METHOD {
   public int  tokMethod;
   public uint dwOffset;
   public uint dwVersion;
}
```

## <a name="members"></a>メンバー
 `tokMethod`\
 メソッドの ID。

 [C++]`_mdToken`は`typedef`32 ビット`int`用です。

 `dwOffset`\
 クラス開始からこのメソッドへのオフセット (vtable へのオフセットを表すことができます)。

 `dwVersion`\
 メソッドのバージョン (この値は、シンボル プロバイダーに固有です)。

## <a name="remarks"></a>Remarks
 構造体`dwKind`のフィールドが[(ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md)列挙体の値) に`ADDRESS_KIND_METHOD`設定されている`DEBUG_ADDRESS_UNION`場合、この構造体は[DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md)構造体の共用体の一部です。

## <a name="requirements"></a>必要条件
 ヘッダー: sh.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md)
- [ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md)
