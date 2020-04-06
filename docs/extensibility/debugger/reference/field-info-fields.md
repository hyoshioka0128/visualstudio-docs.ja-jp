---
title: FIELD_INFO_FIELDS |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- FIELD_INFO_FIELDS
helpviewer_keywords:
- FIELD_INFO_FIELDS enumeration
ms.assetid: a69487d2-e701-4165-804a-8a011df9a3bd
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9a3d2e796d37606c51918d8e49db920161d63f55
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80736911"
---
# <a name="field_info_fields"></a>FIELD_INFO_FIELDS
[オブジェクトに](../../../extensibility/debugger/reference/idebugfield.md)関して取得する情報を指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_FIELD_INFO_FIELDS { 
    FIF_FULLNAME  = 0x0001,
    FIF_NAME      = 0x0002,
    FIF_TYPE      = 0x0004,
    FIF_MODIFIERS = 0x0008,
    FIF_ALL       = 0xffffffff,
    FIF_NONE      = 0x0000
};
typedef DWORD FIELD_INFO_FIELDS;
```

```csharp
public enum enum_FIELD_INFO_FIELDS {
    FIF_FULLNAME  = 0x0001,
    FIF_NAME      = 0x0002,
    FIF_TYPE      = 0x0004,
    FIF_MODIFIERS = 0x0008,
    FIF_ALL       = 0xffffffff,
    FIF_NONE      = 0x0000
};
```

## <a name="fields"></a>フィールド
`FIF_FULLNAME`\
FIELD_INFO構造体のフィールド`bstrFullName`を初期化/[FIELD_INFO](../../../extensibility/debugger/reference/field-info.md)使用します。

`FIF_NAME`\
構造体のフィールドを`bstrName`初期化/使用`FIELD_INFO`します。

`FIF_TYPE`\
構造体のフィールドを`bstrType`初期化/使用`FIELD_INFO`します。

`FIF_MODIFIERS`\
構造体のフィールドを`bstrModifiers`初期化/使用`FIELD_INFO`します。

## <a name="remarks"></a>Remarks
これらの値は、[初期化するFIELD_INFO](../../../extensibility/debugger/reference/field-info.md)構造体のフィールドを指定する引数として[GetInfo](../../../extensibility/debugger/reference/idebugfield-getinfo.md)メソッドにも渡されます。

これらの値は、`dwFields``FIELD_INFO`構造体のメンバーで使用され、どのフィールドが使用され、有効かを示すためにも使用されます。

これらのフラグはビット単位`OR`で組み合わせることができる。

## <a name="requirements"></a>必要条件
ヘッダー: sh.h

名前空間: を使用します。

アセンブリ:

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [FIELD_INFO](../../../extensibility/debugger/reference/field-info.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [GetInfo](../../../extensibility/debugger/reference/idebugfield-getinfo.md)
