---
title: ADDRESS_KIND |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- ADDRESS_KIND
helpviewer_keywords:
- ADDRESS_KIND enumeration
ms.assetid: 3a12fbec-7088-4cf9-8f6f-ad8ddec6009a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 1298df79bbe34b240d6e7b186f42e20b3d1a89de
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738150"
---
# <a name="address_kind"></a>ADDRESS_KIND
アドレスの種類を指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_ADDRESS_KIND {
    ADDRESS_KIND_NATIVE                  = 0x0001,
    ADDRESS_KIND_UNMANAGED_THIS_RELATIVE = 0x0002,
    ADDRESS_KIND_UNMANAGED_PHYSICAL      = 0x0005,
    ADDRESS_KIND_METADATA_METHOD         = 0x0010,
    ADDRESS_KIND_METADATA_FIELD          = 0x0011,
    ADDRESS_KIND_METADATA_LOCAL          = 0x0012,
    ADDRESS_KIND_METADATA_PARAM          = 0x0013,
    ADDRESS_KIND_METADATA_ARRAYELEM      = 0x0014,
    ADDRESS_KIND_METADATA_RETVAL         = 0x0015,
};
typedef DWORD ADDRESS_KIND;
```

```csharp
public enum enum_ADDRESS_KIND {
    ADDRESS_KIND_NATIVE                  = 0x0001,
    ADDRESS_KIND_UNMANAGED_THIS_RELATIVE = 0x0002,
    ADDRESS_KIND_UNMANAGED_PHYSICAL      = 0x0005,
    ADDRESS_KIND_METADATA_METHOD         = 0x0010,
    ADDRESS_KIND_METADATA_FIELD          = 0x0011,
    ADDRESS_KIND_METADATA_LOCAL          = 0x0012,
    ADDRESS_KIND_METADATA_PARAM          = 0x0013,
    ADDRESS_KIND_METADATA_ARRAYELEM      = 0x0014,
    ADDRESS_KIND_METADATA_RETVAL         = 0x0015,
};
```

## <a name="fields"></a>フィールド
`ADDRESS_KIND_NATIVE`\
[NATIVE_ADDRESS](../../../extensibility/debugger/reference/native-address.md)構造体で表されるネイティブ アドレス。

`ADDRESS_KIND_UNMANAGED_THIS_RELATIVE`\
`this` (Visual`Me` Basic では) ポインターを基準にして[、UNMANAGED_ADDRESS_THIS_RELATIVE](../../../extensibility/debugger/reference/unmanaged-address-this-relative.md)構造体で表されるアンマネージ アドレス。

`ADDRESS_KIND_UNMANAGED_PHYSICAL`\
[UNMANAGED_ADDRESS_PHYSICAL](../../../extensibility/debugger/reference/unmanaged-address-physical.md)構造体で表されるアンマネージ物理アドレス。

`ADDRESS_KIND_METHOD`\
[METADATA_ADDRESS_METHOD](../../../extensibility/debugger/reference/metadata-address-method.md)構造体で表されるクラスのメソッド。

`ADDRESS_KIND_FIELD`\
[METADATA_ADDRESS_FIELD](../../../extensibility/debugger/reference/metadata-address-field.md)構造体で表されるクラスのフィールド。

`ADDRESS_KIND_LOCAL`\
アドレスはローカル変数用で[、METADATA_ADDRESS_LOCAL](../../../extensibility/debugger/reference/metadata-address-local.md)構造で表されます。

`ADDRESS_KIND_PARAM`\
[METADATA_ADDRESS_PARAM](../../../extensibility/debugger/reference/metadata-address-param.md)構造体で表されるメソッドまたは関数パラメーター。

`ADDRESS_KIND_ARRAYELEM`\
[METADATA_ADDRESS_ARRAYELEM](../../../extensibility/debugger/reference/metadata-address-arrayelem.md)構造体で表される配列要素。

`ADDRESS_KIND_RETVAL`\
[METADATA_ADDRESS_RETVAL](../../../extensibility/debugger/reference/metadata-address-retval.md)構造体で表される戻り値。

## <a name="remarks"></a>Remarks
[GetAddress](../../../extensibility/debugger/reference/idebugaddress-getaddress.md)メソッドは、可能な構造体の和集合[、DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md)構造体を含む[DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md)構造体を返します。 構造体`dwKind`の`DEBUG_ADDRESS_UNION`フィールドは値を`ADDRESS_KIND`保持し、共用体フィールドの解釈方法を記述します。

## <a name="requirements"></a>必要条件
ヘッダー: sh.h

名前空間: を使用します。

アセンブリ:

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetAddress](../../../extensibility/debugger/reference/idebugaddress-getaddress.md)
- [DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md)
- [DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md)
