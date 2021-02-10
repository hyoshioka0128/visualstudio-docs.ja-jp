---
title: FIELD_INFO |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- FIELD_INFO
helpviewer_keywords:
- FIELD_INFO structure
ms.assetid: bfafef6d-0c83-43d7-a779-1f0d24b166a1
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f358c6c9a192ddd4d71f26a0f2f795ae012bc2c7
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99941841"
---
# <a name="field_info"></a>FIELD_INFO
この構造体は、ローカル変数、パラメーター、またはその他のフィールドを記述します。

## <a name="syntax"></a>構文

```cpp
typedef struct _tagFieldInfo {
    FIELD_INFO_FIELDS dwFields;
    BSTR              bstrFullName;
    BSTR              bstrName;
    BSTR              bstrType;
    FIELD_MODIFIERS   dwModifiers;
} FIELD_INFO;
```

```csharp
public struct FIELD_INFO {
    public uint   dwFields;
    public string bstrFullName;
    public string bstrName;
    public string bstrType;
    public uint   dwModifiers;
};
```

## <a name="members"></a>メンバー
`dwFields`\
入力されるメンバーを指定する、 [FIELD_INFO_FIELDS](../../../extensibility/debugger/reference/field-info-fields.md) 列挙のフラグの組み合わせ。

`bstrFullName`\
フィールドの完全な名前。

`bstrName`\
フィールドの短い名前。

`bstrType`\
フィールドの型。

`dwModifiers`\
フィールドを説明する [FIELD_MODIFIERS](../../../extensibility/debugger/reference/field-modifiers.md) 列挙のフラグの組み合わせ。

## <a name="remarks"></a>解説
この構造体は、入力されている [GetInfo](../../../extensibility/debugger/reference/idebugfield-getinfo.md) メソッドに渡されます。

## <a name="requirements"></a>要件
ヘッダー: sh. h

名前空間: VisualStudio。

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [FIELD_INFO_FIELDS](../../../extensibility/debugger/reference/field-info-fields.md)
- [FIELD_MODIFIERS](../../../extensibility/debugger/reference/field-modifiers.md)
- [GetInfo](../../../extensibility/debugger/reference/idebugfield-getinfo.md)
