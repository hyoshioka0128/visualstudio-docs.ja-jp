---
title: TYPE_INFO |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- TYPE_INFO
helpviewer_keywords:
- TYPE_INFO structure
ms.assetid: d725cb68-a565-49d1-a16f-ff0445c587a0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 82796c1d82dc3ca77151abcec3e1dd6ce13ac59d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80713326"
---
# <a name="type_info"></a>TYPE_INFO
この構造体は、フィールドの型に関するさまざまな種類の情報を指定します。

## <a name="syntax"></a>構文

```cpp
struct _tagTYPE_INFO_UNION {
   dwTYPE_KIND dwKind;
   union {
      METADATA_TYPE typeMeta;
      PDB_TYPE      typePdb;
      BUILT_TYPE    typeBuilt;
      DWORD         unused;
   } type;
} TYPE_INFO;
```

```csharp
public struct TYPE_INFO {
   public uint   dwKind;
   public IntPtr unionmember;
};
```

## <a name="members"></a>メンバー
 `dwKind`\
 共用体を解釈する方法を決定する [dwTYPE_KIND](../../../extensibility/debugger/reference/dwtype-kind.md) 列挙の値。

 `type.typeMeta`\
 [C++ のみ]がの場合は、 [METADATA_TYPE](../../../extensibility/debugger/reference/metadata-type.md) 構造体を格納し `dwKind` `TYPE_KIND_METADATA` ます。

 `type.typePdb`\
 [C++ のみ]がの場合は、 [PDB_TYPE](../../../extensibility/debugger/reference/pdb-type.md) 構造体を格納し `dwKind` `TYPE_KIND_PDB` ます。

 `type.typeBuilt`\
 [C++ のみ]がの場合は、 [BUILT_TYPE](../../../extensibility/debugger/reference/built-type.md) 構造体を格納し `dwKind` `TYPE_KIND_BUILT` ます。

 `type.unused`\
 未使用の埋め込み。

 `type`\
 共用体の名前。

 `unionmember`\
 [C# のみ]このをに基づいて適切な構造体型にマーシャリングし `dwKind` ます。

## <a name="remarks"></a>注釈
 この構造体は、 [GetTypeInfo](../../../extensibility/debugger/reference/idebugfield-gettypeinfo.md) メソッドに渡され、そこに格納されます。 構造体の内容がどのように解釈されるかは、フィールドに基づいて決まり `dwKind` ます。

> [!NOTE]
> [C++ のみ]が `dwKind` に等しい場合 `TYPE_KIND_BUILT` は、構造体を破棄するときに、基になる [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) オブジェクトを解放する必要があり `TYPE_INFO` ます。 これは、`typeInfo.type.typeBuilt.pUnderlyingField->Release()` を呼び出すことによって行われます。

 [C# のみ]次の表は、型の種類ごとにメンバーを解釈する方法を示して `unionmember` います。 この例では、1種類の型に対してこれがどのように行われるかを示します。

|`dwKind`|`unionmember` 解釈される|
|--------------|----------------------------------|
|`TYPE_KIND_METADATA`|[METADATA_TYPE](../../../extensibility/debugger/reference/metadata-type.md)|
|`TYPE_KIND_PDB`|[PDB_TYPE](../../../extensibility/debugger/reference/pdb-type.md)|
|`TYPE_KIND_BUILT`|[BUILT_TYPE](../../../extensibility/debugger/reference/built-type.md)|

## <a name="example"></a>例
 この例は、 `unionmember` C# で構造体のメンバーを解釈する方法を示して `TYPE_INFO` います。 この例では、1つの型 () のみを解釈し `TYPE_KIND_METADATA` ますが、他の型はまったく同じように解釈されます。

```csharp
using System;
using System.Runtime.Interop.Services;
using Microsoft.VisualStudio.Debugger.Interop;

namespace MyPackage
{
    public class MyClass
    {
        public void Interpret(TYPE_INFO ti)
        {
            if (ti.dwKind == (uint)enum_dwTypeKind.TYPE_KIND_METADATA)
            {
                 METADATA_TYPE dataType = (METADATA_TYPE)Marshal.PtrToStructure(ti.unionmember,
                                               typeof(METADATA_TYPE));
            }
        }
    }
}
```

## <a name="requirements"></a>必要条件
 ヘッダー: sh. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [dwTYPE_KIND](../../../extensibility/debugger/reference/dwtype-kind.md)
- [GetTypeInfo](../../../extensibility/debugger/reference/idebugfield-gettypeinfo.md)
- [METADATA_TYPE](../../../extensibility/debugger/reference/metadata-type.md)
- [PDB_TYPE](../../../extensibility/debugger/reference/pdb-type.md)
- [BUILT_TYPE](../../../extensibility/debugger/reference/built-type.md)
