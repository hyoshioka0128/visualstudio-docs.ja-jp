---
title: DEBUGPROP_INFO_FLAGS |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DEBUGPROP_INFO_FLAGS
helpviewer_keywords:
- DBGPROP_INFO_FLAGS enumeration
ms.assetid: 1c7fe777-615e-4929-9ed4-970d9fe0eb81
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: fa7e4a498188dc91f2a47b3ccf27f367f15ec77b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737395"
---
# <a name="debugprop_info_flags"></a>DEBUGPROP_INFO_FLAGS
デバッグ プロパティ オブジェクトについて取得する情報を指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_DEBUGPROP_INFO_FLAGS {
    DEBUGPROP_INFO_FULLNAME          = 0x00000001,
    DEBUGPROP_INFO_NAME              = 0x00000002,
    DEBUGPROP_INFO_TYPE              = 0x00000004,
    DEBUGPROP_INFO_VALUE             = 0x00000008,
    DEBUGPROP_INFO_ATTRIB            = 0x00000010,
    DEBUGPROP_INFO_PROP              = 0x00000020,
    DEBUGPROP_INFO_VALUE_AUTOEXPAND  = 0x00010000,
    DEBUGPROP_INFO_VALUE_NOFUNCEVAL  = 0x00020000,
    DEBUGPROP_INFO_VALUE_RAW         = 0x00040000,
    DEBUGPROP_INFO_VALUE_NO_TOSTRING = 0x00080000
    DEBUGPROP_INFO_NONE              = 0x00000000,
    DEBUGPROP_INFO_STANDARD          = DEBUGPROP_INFO_ATTRIB |
                                        DEBUGPROP_INFO_NAME |
                                        DEBUGPROP_INFO_TYPE |
                                        DEBUGPROP_INFO_VALUE,
    DEBUGPROP_INFO_ALL               = 0xffffffff
};
typedef DWORD DEBUGPROP_INFO_FLAGS;
```

```csharp
public enum enum_DEBUGPROP_INFO_FLAGS {
    DEBUGPROP_INFO_FULLNAME          = 0x00000001,
    DEBUGPROP_INFO_NAME              = 0x00000002,
    DEBUGPROP_INFO_TYPE              = 0x00000004,
    DEBUGPROP_INFO_VALUE             = 0x00000008,
    DEBUGPROP_INFO_ATTRIB            = 0x00000010,
    DEBUGPROP_INFO_PROP              = 0x00000020,
    DEBUGPROP_INFO_VALUE_AUTOEXPAND  = 0x00010000,
    DEBUGPROP_INFO_VALUE_NOFUNCEVAL  = 0x00020000,
    DEBUGPROP_INFO_VALUE_RAW         = 0x00040000,
    DEBUGPROP_INFO_VALUE_NO_TOSTRING = 0x00080000
    DEBUGPROP_INFO_NONE              = 0x00000000,
    DEBUGPROP_INFO_STANDARD          = DEBUGPROP_INFO_ATTRIB |
                                        DEBUGPROP_INFO_NAME |
                                        DEBUGPROP_INFO_TYPE |
                                        DEBUGPROP_INFO_VALUE,
    DEBUGPROP_INFO_ALL               = 0xffffffff
};
```

## <a name="fields"></a>フィールド
`DEBUGPROP_INFO_FULLNAME`\
フィールドを初期化/`bstrFullName`使用します。

`DEBUGPROP_INFO_NAME`\
フィールドを初期化/`bstrName`使用します。

`DEBUGPROP_INFO_TYPE`\
フィールドを初期化/`bstrType`使用します。

`DEBUGPROP_INFO_VALUE`\
フィールドを初期化/`bstrValue`使用します。

`DEBUGPROP_INFO_ATTRIB`\
フィールドを初期化/`dwAttrib`使用します。

`DEBUGPROP_INFO_PROP`\
`pProperty` [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)インターフェイスを含むフィールドを初期化/使用します。

`DEBUGPROP_INFO_VALUE_AUTOEXPAND`\
値フィールドに、このタイプのオブジェクトの自動拡張値 (使用可能な場合) が含まれる必要があることを指定します。

`DEBUGPROP_INFO_VALUE_NOFUNCEVAL`\
非推奨になりました。

`DEBUGPROP_INFO_VALUE_RAW`\
美しい値やメンバーを返しません (つまり、値の書式は設定しないでください)。

`DEBUGPROP_INFO_VALUE_NO_TOSTRING`\
特殊な合成値を返しません (たとえば、値を生成するために`ToString()`オブジェクトを呼び出さない)。

`DEBUGPROP_INFO_NONE`\
フラグが設定されていない場合に指定します。

`DEBUGPROP_INFO_STANDARD`\
`dwAttrib`、 、、`bstrName``bstrType`および`bstrValue`の各フィールドを初期化/使用します。

`DEBUGPROP_INFO_All`\
すべてのフラグのマスクを示します。

## <a name="remarks"></a>Remarks
これらの値は[、DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)構造体を初期化するフィールドを示すために[GetPropertyInfo、](../../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md)[列挙子](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)、および[列挙プロパティ](../../../extensibility/debugger/reference/idebugstackframe2-enumproperties.md)の各メソッドに渡されます。

これらの値は、`dwFields``DEBUG_PROPERTY_INFO`構造体のメンバーに対しても使用され、構造体のどのフィールドが使用され、構造体が返されるときに有効かを示します。

これらの値はビット単位`OR`で組み合わせることができる。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: を使用します。

アセンブリ:

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [プロパティ情報を取得します。](../../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md)
- [EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)
- [EnumProperties](../../../extensibility/debugger/reference/idebugstackframe2-enumproperties.md)
- [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)
