---
title: TYPE_INFO |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- TYPE_INFO
helpviewer_keywords:
- TYPE_INFO structure
ms.assetid: d725cb68-a565-49d1-a16f-ff0445c587a0
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 12102c297c34649c753cf1c811994f9e750b9605
ms.sourcegitcommit: 4ae5e9817ad13edd05425febb322b5be6d3c3425
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/11/2020
ms.locfileid: "91838478"
---
# <a name="type_info"></a>TYPE_INFO
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

この構造体は、フィールドの型に関するさまざまな種類の情報を指定します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
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
  
#### <a name="parameters"></a>パラメーター  
 dwKind  
 共用体を解釈する方法を決定する [dwTYPE_KIND](../../../extensibility/debugger/reference/dwtype-kind.md) 列挙の値。  
  
 typeMeta  
 [C++ のみ]がの場合は、 [METADATA_TYPE](../../../extensibility/debugger/reference/metadata-type.md) 構造体を格納し `dwKind` `TYPE_KIND_METADATA` ます。  
  
 「typePdb」と入力します。  
 [C++ のみ]がの場合は、 [PDB_TYPE](../../../extensibility/debugger/reference/pdb-type.md) 構造体を格納し `dwKind` `TYPE_KIND_PDB` ます。  
  
 「typeBuilt」と入力します。  
 [C++ のみ]がの場合は、 [BUILT_TYPE](../../../extensibility/debugger/reference/built-type.md) 構造体を格納し `dwKind` `TYPE_KIND_BUILT` ます。  
  
 型。使用しない  
 未使用の埋め込み。  
  
 type  
 共用体の名前。  
  
 unionmember  
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
  
## <a name="requirements"></a>要件  
 ヘッダー: sh. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)   
 [dwTYPE_KIND](../../../extensibility/debugger/reference/dwtype-kind.md)   
 [GetTypeInfo](../../../extensibility/debugger/reference/idebugfield-gettypeinfo.md)   
 [METADATA_TYPE](../../../extensibility/debugger/reference/metadata-type.md)   
 [PDB_TYPE](../../../extensibility/debugger/reference/pdb-type.md)   
 [BUILT_TYPE](../../../extensibility/debugger/reference/built-type.md)
