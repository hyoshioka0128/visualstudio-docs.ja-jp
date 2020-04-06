---
title: METADATA_ADDRESS_RETVAL |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- METADATA_ADDRESS_RETVAL
helpviewer_keywords:
- METADATA_ADDRESS_RETVAL structure
ms.assetid: 5b0ec0fb-84b3-4ce7-8e24-becf3d881d7d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f2437d10078eb623e063b3292d96ef9bb4a9cf64
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80714272"
---
# <a name="metadata_address_retval"></a>METADATA_ADDRESS_RETVAL
この構造体は、メソッドまたは関数からの戻り値を表します。

## <a name="syntax"></a>構文

```cpp
typedef struct _tagMETADATA_ADDRESS_RETVAL {
   _mdToken tokMethod;
   DWORD    dwCorType;
   DWORD    dwSigSize;
   BYTE     rgSig[10];
} METADATA_ADDRESS_RETVAL;
```

```csharp
public struct METADATA_ADDRESS_RETVAL {
   public int    tokMethod;
   public uint   dwCorType;
   public uint   dwSigSize;
   public byte[] rgSig;
}
```

## <a name="members"></a>メンバー
 `tokMethod`\
 この戻り値のメソッドの ID。

 `dwCorType`\
 戻り値の基本型。 これは、.NET Framework `CorElementType` SDK の corhdr.h ファイルで定義されている列挙型の値です。

 `dwSigSize`\
 戻り値シグネチャのサイズ ( に`rgSig`格納されている)

 `rgSig`\
 戻り値のシグネチャを形成するバイト配列。

## <a name="remarks"></a>Remarks
 構造体`dwKind`のフィールドが[(ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md)列挙体の値) に`ADDRESS_KIND_RETVAL`設定されている`DEBUG_ADDRESS_UNION`場合、この構造体は[DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md)構造体の共用体の一部です。

## <a name="requirements"></a>必要条件
 ヘッダー: sh.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md)
- [ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md)
