---
title: TYPE_INFO |マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
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
 共用体の解釈方法を決定する[dwTYPE_KIND](../../../extensibility/debugger/reference/dwtype-kind.md)列挙体の値。

 `type.typeMeta`\
 [C++のみ]METADATA_TYPEの[構造体](../../../extensibility/debugger/reference/metadata-type.md)`dwKind`が含まれています`TYPE_KIND_METADATA`。

 `type.typePdb`\
 [C++のみ]の`dwKind`場合[、PDB_TYPE](../../../extensibility/debugger/reference/pdb-type.md)構造体を`TYPE_KIND_PDB`格納します。

 `type.typeBuilt`\
 [C++のみ]の場合`dwKind`は[、BUILT_TYPE](../../../extensibility/debugger/reference/built-type.md)構造`TYPE_KIND_BUILT`を格納します。

 `type.unused`\
 未使用のパディング。

 `type`\
 ユニオンの名前。

 `unionmember`\
 [C#のみ]に基づいて、適切な構造体型に`dwKind`この型をマーシャリングします。

## <a name="remarks"></a>Remarks
 この構造体は[、GetTypeInfo](../../../extensibility/debugger/reference/idebugfield-gettypeinfo.md)メソッドに渡され、そこで値が入力されます。 構造体の内容の解釈方法は、フィールドに`dwKind`基づいています。

> [!NOTE]
> [C++のみ]等`dwKind`しい`TYPE_KIND_BUILT`場合は、構造体を破棄するときに、基になる[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)オブジェクトを解放`TYPE_INFO`する必要があります。 これは、`typeInfo.type.typeBuilt.pUnderlyingField->Release()` を呼び出すことによって行われます。

 [C#のみ]次の表は、型の種類`unionmember`ごとにメンバーを解釈する方法を示しています。 例は、ある種類の型に対してこれを行う方法を示しています。

|`dwKind`|`unionmember`として解釈される|
|--------------|----------------------------------|
|`TYPE_KIND_METADATA`|[METADATA_TYPE](../../../extensibility/debugger/reference/metadata-type.md)|
|`TYPE_KIND_PDB`|[PDB_TYPE](../../../extensibility/debugger/reference/pdb-type.md)|
|`TYPE_KIND_BUILT`|[BUILT_TYPE](../../../extensibility/debugger/reference/built-type.md)|

## <a name="example"></a>例
 この例では、C#`unionmember`で構造体の`TYPE_INFO`メンバーを解釈する方法を示します。 この例では、1 つの型`TYPE_KIND_METADATA`( ) のみを解釈していますが、他の型はまったく同じ方法で解釈されます。

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
 ヘッダー: sh.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [dwTYPE_KIND](../../../extensibility/debugger/reference/dwtype-kind.md)
- [ゲットタイプ情報](../../../extensibility/debugger/reference/idebugfield-gettypeinfo.md)
- [METADATA_TYPE](../../../extensibility/debugger/reference/metadata-type.md)
- [PDB_TYPE](../../../extensibility/debugger/reference/pdb-type.md)
- [BUILT_TYPE](../../../extensibility/debugger/reference/built-type.md)
