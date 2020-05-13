---
title: DEBUGREF_INFO_FLAGS |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DEBUGREF_INFO_FLAGS
helpviewer_keywords:
- DEBUGREF_INFO_FLAGS enumeration
ms.assetid: 1b043327-302a-4f6d-b51d-f94f9d7c7f9d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: cb10ae5d3b4ce9f8aa777f643d412e075bd5293f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737391"
---
# <a name="debugref_info_flags"></a>DEBUGREF_INFO_FLAGS
デバッグ参照オブジェクトについて取得する情報を指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_DEBUGREF_INFO_FLAGS {
    DEBUGREF_INFO_NAME             = 0x00000001,
    DEBUGREF_INFO_TYPE             = 0x00000002,
    DEBUGREF_INFO_VALUE            = 0x00000004,
    DEBUGREF_INFO_ATTRIB           = 0x00000008,
    DEBUGREF_INFO_REFTYPE          = 0x00000010,
    DEBUGREF_INFO_REF              = 0x00000020,
    DEBUGREF_INFO_VALUE_AUTOEXPAND = 0x00010000,
    DEBUGREF_INFO_NONE             = 0x00000000,
    DEBUGREF_INFO_ALL              = 0xffffffff
};
typedef DWORD DEBUGREF_INFO_FLAGS;
```

```csharp
public enum enum_DEBUGREF_INFO_FLAGS {
    DEBUGREF_INFO_NAME             = 0x00000001,
    DEBUGREF_INFO_TYPE             = 0x00000002,
    DEBUGREF_INFO_VALUE            = 0x00000004,
    DEBUGREF_INFO_ATTRIB           = 0x00000008,
    DEBUGREF_INFO_REFTYPE          = 0x00000010,
    DEBUGREF_INFO_REF              = 0x00000020,
    DEBUGREF_INFO_VALUE_AUTOEXPAND = 0x00010000,
    DEBUGREF_INFO_NONE             = 0x00000000,
    DEBUGREF_INFO_ALL              = 0xffffffff
};
```

## <a name="fields"></a>フィールド
`DEBUGREF_INFO_NAME`\
構造体のフィールドを`bstrName`初期化/使用します。

`DEBUGREF_INFO_TYPE`\
構造体のフィールドを`bstrType`初期化/使用します。

`DEBUGREF_INFO_VALUE`\
構造体のフィールドを`bstrValue`初期化/使用します。

`DEBUGREF_INFO_ATTRIB`\
構造体のフィールドを`dwAttrib`初期化/使用します。

`DEBUGREF_INFO_REFTYPE`\
構造体のフィールドを`dwRefType`初期化/使用します。

`DEBUGREF_INFO_REF`\
構造体のフィールドを`pReference`初期化/使用します。

`DEBUGREF_INFO_VALUE_AUTOEXPAND`\
値フィールドには、このタイプのオブジェクトの自動拡張値 (使用可能な場合) が含まれている必要があります。

`DEBUGREF_INFO_NONE`\
フラグが設定されていない状態を示します。

`DEBUGREF_INFO_ALL`\
フラグのマスクを示します。

## <a name="remarks"></a>Remarks
これらのフラグは[EnumChildren](../../../extensibility/debugger/reference/idebugreference2-enumchildren.md)メソッドと[GetReferenceInfo](../../../extensibility/debugger/reference/idebugreference2-getreferenceinfo.md)メソッドに渡され、[初期化するDEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md)構造体のフィールドを示します。

構造体の`dwFields`メンバーに対して`DEBUG_REFERENCE_INFO`、構造体が返されるときに使用され、有効なフィールドを示すために使用されます。

これらの値はビット単位`OR`で組み合わせることができる。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: を使用します。

アセンブリ:

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md)
- [EnumChildren](../../../extensibility/debugger/reference/idebugreference2-enumchildren.md)
- [GetReferenceInfo](../../../extensibility/debugger/reference/idebugreference2-getreferenceinfo.md)
