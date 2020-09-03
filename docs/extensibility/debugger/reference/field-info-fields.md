---
title: FIELD_INFO_FIELDS |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80736911"
---
# <a name="field_info_fields"></a>FIELD_INFO_FIELDS
[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)オブジェクトについて取得する情報を指定します。

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
FIELD_INFO 構造体のフィールドを初期化/使用し `bstrFullName` ます。 [FIELD_INFO](../../../extensibility/debugger/reference/field-info.md)

`FIF_NAME`\
構造体のフィールドを初期化/使用し `bstrName` `FIELD_INFO` ます。

`FIF_TYPE`\
構造体のフィールドを初期化/使用し `bstrType` `FIELD_INFO` ます。

`FIF_MODIFIERS`\
構造体のフィールドを初期化/使用し `bstrModifiers` `FIELD_INFO` ます。

## <a name="remarks"></a>解説
また、これらの値は、 [FIELD_INFO](../../../extensibility/debugger/reference/field-info.md)構造体を初期化するフィールドを指定するために、 [GetInfo](../../../extensibility/debugger/reference/idebugfield-getinfo.md)メソッドに引数として渡されます。

これらの値は `dwFields` 、使用される `FIELD_INFO` フィールドと有効なフィールドを示すために、構造体のメンバーでも使用されます。

これらのフラグは、ビットごとのを使用して組み合わせることができ `OR` ます。

## <a name="requirements"></a>必要条件
ヘッダー: sh. h

名前空間: VisualStudio。

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [FIELD_INFO](../../../extensibility/debugger/reference/field-info.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [GetInfo](../../../extensibility/debugger/reference/idebugfield-getinfo.md)
