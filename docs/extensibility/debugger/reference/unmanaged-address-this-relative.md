---
description: この構造体は、このポインター (Visual Basic) に対して相対的なアドレスを表します。
title: UNMANAGED_ADDRESS_THIS_RELATIVE |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- UNMANAGED_ADDRESS_THIS_RELATIVE
helpviewer_keywords:
- UNMANAGED_ADDRESS_THIS_RELATIVE structure
ms.assetid: e6a91ace-2d47-4ff9-aefb-8d8b68eab0b2
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: cc3e72a536af25c3c62d953a0e5cfb75b5200c69
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102223368"
---
# <a name="unmanaged_address_this_relative"></a>UNMANAGED_ADDRESS_THIS_RELATIVE
この構造体は、ポインターに対して相対的なアドレス `this` ( `Me` Visual Basic) を表します。

## <a name="syntax"></a>構文

```cpp
typedef struct _tagUNMANAGED_THIS_RELATIVE {
   DWORD dwOffset;
   DWORD dwBitOffset;
   DWORD dwBitLength;
} UNMANAGED_ADDRESS_THIS_RELATIVE;
```

```csharp
public struct UNMANAGED_THIS_RELATIVE {
   public uint dwOffset;
   public uint dwBitOffset;
   public uint dwBitLength;
}
```

## <a name="members"></a>メンバー
 `dwOffset`\
 基本位置からのバイトオフセット (たとえば、クラス vtable の開始)。

 `dwBitOffset`\
 基本位置からのビット単位のオフセット (ビットフィールドを参照する場合を除き、常に0です)。

 `dwBitLength`\
 アドレスを表すビット数 (ビットフィールドを参照している場合を除き、常に0です)。

## <a name="remarks"></a>解説
 この構造体は、構造体のフィールドがに設定されている場合に、 [DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md) 構造体の和集合の一部になり `dwKind` `DEBUG_ADDRESS_UNION` `ADDRESS_KIND_UNMANAGED_THIS_RELATIVE` ます ( [ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md) 列挙型の値)。

## <a name="requirements"></a>必要条件
 ヘッダー: sh. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md)
