---
title: METADATA_ADDRESS_RETVAL |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
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
 この戻り値の対象となるメソッドの ID。

 `dwCorType`\
 戻り値の基本型。 これは `CorElementType` .NET FRAMEWORK SDK corhdr .h ファイルで定義されている列挙体の値です。

 `dwSigSize`\
 戻り値のシグネチャのサイズ (に格納されている `rgSig` )。

 `rgSig`\
 戻り値の署名を形成するバイト配列。

## <a name="remarks"></a>解説
 この構造体は、構造体のフィールドがに設定されている場合に、 [DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md) 構造体の和集合の一部になり `dwKind` `DEBUG_ADDRESS_UNION` `ADDRESS_KIND_RETVAL` ます ( [ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md) 列挙型の値)。

## <a name="requirements"></a>必要条件
 ヘッダー: sh. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md)
- [ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md)
