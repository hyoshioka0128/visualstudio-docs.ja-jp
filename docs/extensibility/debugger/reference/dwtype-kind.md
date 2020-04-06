---
title: dwTYPE_KIND |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- dwTYPE_KIND
helpviewer_keywords:
- dwTYPE_KIND enumeration
ms.assetid: 6ff56b0f-c502-4e6c-9829-bfa05361b783
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a9d790f12d3fc21bbae7373470746af2ebfe6dc9
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737193"
---
# <a name="dwtype_kind"></a>dwTYPE_KIND
[オブジェクトの](../../../extensibility/debugger/reference/idebugfield.md)型を解釈する方法を指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_dwTYPE_KIND {
    TYPE_KIND_METADATA = 0x0001,
    TYPE_KIND_PDB      = 0x0002,
    TYPE_KIND_BUILT    = 0x0003,
};

typedef DWORD dwTYPE_KIND;
```

```csharp
public enum enum_dwTYPE_KIND {
    TYPE_KIND_METADATA = 0x0001,
    TYPE_KIND_PDB      = 0x0002,
    TYPE_KIND_BUILT    = 0x0003,
};
```

## <a name="fields"></a>フィールド
`TYPE_KIND_METADATA`\
[TYPE_INFO](../../../extensibility/debugger/reference/type-info.md)共用体は[、METADATA_TYPE](../../../extensibility/debugger/reference/metadata-type.md)構造として解釈されるべきです。

`TYPE_KIND_PDB`\
共用`TYPE_INFO`体は[PDB_TYPE](../../../extensibility/debugger/reference/pdb-type.md)構造として解釈されるべきです。

`TYPE_KIND_BUILT`\
共用`TYPE_INFO`体は[BUILT_TYPE](../../../extensibility/debugger/reference/built-type.md)構造として解釈されるべきです。

## <a name="remarks"></a>Remarks
この列挙体の値は`dwKind`[、TYPE_INFO](../../../extensibility/debugger/reference/type-info.md)構造体のフィールドに表示され、共用体メンバーの解釈方法を`type`決定するために使用されます。 構造体`TYPE_INFO`は[、GetTypeInfo](../../../extensibility/debugger/reference/idebugfield-gettypeinfo.md)メソッドの呼び出しによって返されます。

## <a name="requirements"></a>必要条件
ヘッダー: sh.h

名前空間: を使用します。

アセンブリ:

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [TYPE_INFO](../../../extensibility/debugger/reference/type-info.md)
- [ゲットタイプ情報](../../../extensibility/debugger/reference/idebugfield-gettypeinfo.md)
- [METADATA_TYPE](../../../extensibility/debugger/reference/metadata-type.md)
- [PDB_TYPE](../../../extensibility/debugger/reference/pdb-type.md)
- [BUILT_TYPE](../../../extensibility/debugger/reference/built-type.md)
