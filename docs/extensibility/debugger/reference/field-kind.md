---
title: FIELD_KIND |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- FIELD_KIND
helpviewer_keywords:
- FIELD_KIND enumeration
ms.assetid: fd522b9c-52e2-42fa-939d-343347d5c3b1
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: cafe4a34745f3b34070f7d8fed1a246c806375a4
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80736860"
---
# <a name="field_kind"></a>FIELD_KIND
[オブジェクトに](../../../extensibility/debugger/reference/idebugfield.md)含まれるフィールドの種類を指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_FIELD_KIND {
    FIELD_KIND_NONE       = 0x00000000,

    // Type of field
    FIELD_KIND_TYPE       = 0x00000001,
    FIELD_KIND_SYMBOL     = 0x00000002,

    // Storage type of the field
    FIELD_TYPE_PRIMITIVE  = 0x00000010,
    FIELD_TYPE_STRUCT     = 0x00000020,
    FIELD_TYPE_CLASS      = 0x00000040,
    FIELD_TYPE_INTERFACE  = 0x00000080,
    FIELD_TYPE_UNION      = 0x00000100,
    FIELD_TYPE_ARRAY      = 0x00000200,
    FIELD_TYPE_METHOD     = 0x00000400,
    FIELD_TYPE_BLOCK      = 0x00000800,
    FIELD_TYPE_POINTER    = 0x00001000,
    FIELD_TYPE_ENUM       = 0x00002000,
    FIELD_TYPE_LABEL      = 0x00004000,
    FIELD_TYPE_TYPEDEF    = 0x00008000,
    FIELD_TYPE_BITFIELD   = 0x00010000,
    FIELD_TYPE_NAMESPACE  = 0x00020000,
    FIELD_TYPE_MODULE     = 0x00040000,
    FIELD_TYPE_DYNAMIC    = 0x00080000,
    FIELD_TYPE_PROP       = 0x00100000,
    FIELD_TYPE_INNERCLASS = 0x00200000,
    FIELD_TYPE_REFERENCE  = 0x00400000,
    FIELD_TYPE_EXTENDED   = 0x00800000,

    // Specific information about symbols
    FIELD_SYM_MEMBER      = 0x01000000,
    FIELD_SYM_LOCAL       = 0x02000000,
    FIELD_SYM_PARAM       = 0x04000000,
    FIELD_SYM_THIS        = 0x08000000,
    FIELD_SYM_GLOBAL      = 0x10000000,
    FIELD_SYM_PROP_GETTER = 0x20000000,
    FIELD_SYM_PROP_SETTER = 0x40000000,
    FIELD_SYM_EXTENDED    = 0x80000000,

    FIELD_KIND_MASK       = 0x0000000f,
    FIELD_TYPE_MASK       = 0x00fffff0,
    FIELD_SYM_MASK        = 0xff000000,

    FIELD_KIND_ALL        = 0xffffffff
};
typedef DWORD FIELD_KIND;
```

```csharp
public enum enum_FIELD_KIND {
    FIELD_KIND_NONE       = 0x00000000,

    // Type of field
    FIELD_KIND_TYPE       = 0x00000001,
    FIELD_KIND_SYMBOL     = 0x00000002,

    // Storage type of the field
    FIELD_TYPE_PRIMITIVE  = 0x00000010,
    FIELD_TYPE_STRUCT     = 0x00000020,
    FIELD_TYPE_CLASS      = 0x00000040,
    FIELD_TYPE_INTERFACE  = 0x00000080,
    FIELD_TYPE_UNION      = 0x00000100,
    FIELD_TYPE_ARRAY      = 0x00000200,
    FIELD_TYPE_METHOD     = 0x00000400,
    FIELD_TYPE_BLOCK      = 0x00000800,
    FIELD_TYPE_POINTER    = 0x00001000,
    FIELD_TYPE_ENUM       = 0x00002000,
    FIELD_TYPE_LABEL      = 0x00004000,
    FIELD_TYPE_TYPEDEF    = 0x00008000,
    FIELD_TYPE_BITFIELD   = 0x00010000,
    FIELD_TYPE_NAMESPACE  = 0x00020000,
    FIELD_TYPE_MODULE     = 0x00040000,
    FIELD_TYPE_DYNAMIC    = 0x00080000,
    FIELD_TYPE_PROP       = 0x00100000,
    FIELD_TYPE_INNERCLASS = 0x00200000,
    FIELD_TYPE_REFERENCE  = 0x00400000,
    FIELD_TYPE_EXTENDED   = 0x00800000,

    // Specific information about symbols
    FIELD_SYM_MEMBER      = 0x01000000,
    FIELD_SYM_LOCAL       = 0x02000000,
    FIELD_SYM_PARAM       = 0x04000000,
    FIELD_SYM_THIS        = 0x08000000,
    FIELD_SYM_GLOBAL      = 0x10000000,
    FIELD_SYM_PROP_GETTER = 0x20000000,
    FIELD_SYM_PROP_SETTER = 0x40000000,
    FIELD_SYM_EXTENDED    = 0x80000000,

    FIELD_KIND_MASK       = 0x0000000f,
    FIELD_TYPE_MASK       = 0x00fffff0,
    FIELD_SYM_MASK        = 0xff000000,

    FIELD_KIND_ALL        = 0xffffffff
};
```

## <a name="fields"></a>フィールド
`FIELD_KIND_TYPE`\
フィールドが型だけであることを示します。

`FIELD_KIND_SYMBOL`\
フィールドが、型、名前、およびその他の情報を含むシンボルであることを示します。

`FIELD_TYPE_PRIMITIVE`\
フィールドがプリミティブ データ型であることを示します。

`FIELD_TYPE_STRUCT`\
フィールドが構造体であることを示します。

`FIELD_TYPE_CLASS`\
フィールドがクラスであることを示します。

`FIELD_TYPE_INTERFACE`\
フィールドがインターフェイスであることを示します。

`FIELD_TYPE_UNION`\
フィールドが共用体であることを示します。

`FIELD_TYPE_ARRAY`\
フィールドが配列であることを示します。

`FIELD_TYPE_METHOD`\
フィールドがメソッドであることを示します。

`FIELD_TYPE_BLOCK`\
フィールドがブロックであることを示します。

`FIELD_TYPE_POINTER`\
フィールドがポインターであることを示します。

`FIELD_TYPE_ENUM`\
フィールドが列挙型であることを示します。

`FIELD_TYPE_LABEL`\
フィールドがラベルであることを示します。

`FIELD_TYPE_TYPEDEF`\
フィールドが型定義であることを示します。

`FIELD_TYPE_BITFIELD`\
フィールドがビット フィールドであることを示します。

`FIELD_TYPE_NAMESPACE`\
フィールドが名前空間であることを示します。

`FIELD_TYPE_MODULE`\
フィールドがモジュールであることを示します。

`FIELD_TYPE_DYNAMIC`\
フィールドが動的であることを示します。

`FIELD_TYPE_PROP`\
フィールドがプロパティであることを示します。

`FIELD_TYPE_INNERCLASS`\
フィールドが内部クラスであることを示します。

`FIELD_TYPE_REFERENCE`\
フィールドが参照であることを示します。

`FIELD_TYPE_EXTENDED`\
将来利用するために予約されています。

`FIELD_SYM_MEMBER`\
フィールドがメンバーであることを示します。

`FIELD_SYM_LOCAL`\
フィールドがローカルであることを示します。

`FIELD_SYM_PARAMETER`\
フィールドがパラメーターであることを示します。

`FIELD_SYM_THIS`\
フィールドが "this" ポインターであることを示します。

`FIELD_SYM_GLOBAL`\
フィールドがグローバルであることを示します。

`FIELD_SYM_PROP_GETTER`\
フィールドがプロパティを取得することを示します。

`FIELD_SYM_PROP_SETTER`\
フィールドがプロパティを設定することを示します。

`FIELD_SYM_EXTENDED`\
将来利用するために予約されています。

`FIELD_KIND_MASK`\
フィールドの種類のマスクを示します。

`FIELD_TYPE_MASK`\
フィールド型のマスクを示します。

`FIELD_SYM_MASK`\
シンボル情報のマスクを示します。

## <a name="remarks"></a>Remarks
[GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md)メソッドの呼び出しから返されます。

フィールドの種類に応じて、[より](/cpp/atl/queryinterface)具体的な形式のインターフェイスの[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)インターフェイスでクエリ インターフェイスを呼び出すことができます。 たとえば[、GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md)が戻`FIELD_TYPE_METHOD`った場合は、I`QueryInterface``DebugField`を呼び出して[IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)インターフェイスを取得できます。

## <a name="requirements"></a>必要条件
ヘッダー: sh.h

名前空間: を使用します。

アセンブリ:

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [FIELD_MODIFIERS](../../../extensibility/debugger/reference/field-modifiers.md)
- [GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
