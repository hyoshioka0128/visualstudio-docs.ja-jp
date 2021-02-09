---
title: DEBUG_ADDRESS_UNION |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DEBUG_ADDRESS_UNION
helpviewer_keywords:
- DEBUG_ADDRESS_UNION union
ms.assetid: e3d11aab-de0d-4109-b5dc-11e07e64382d
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 76fc15389242de1011851492e3a68dc001534582
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99899128"
---
# <a name="debug_address_union"></a>DEBUG_ADDRESS_UNION
さまざまな種類のアドレスについて説明します。

## <a name="syntax"></a>構文

```cpp
typedef struct _tagDEBUG_ADDRESS_UNION {
   ADDRESS_KIND dwKind;
   union {
      NATIVE_ADDRESS                  addrNative;
      UNMANAGED_ADDRESS_THIS_RELATIVE addrThisRel;
      UNMANAGED_ADDRESS_PHYSICAL      addrUPhysical;
      METADATA_ADDRESS_METHOD         addrMethod;
      METADATA_ADDRESS_FIELD          addrField;
      METADATA_ADDRESS_LOCAL          addrLocal;
      METADATA_ADDRESS_PARAM          addrParam;
      METADATA_ADDRESS_ARRAYELEM      addrArrayElem;
      METADATA_ADDRESS_RETVAL         addrRetVal;
      DWORD                           unused;
   } addr;
} DEBUG_ADDRESS_UNION;
```

```csharp
public struct DEBUG_ADDRESS_UNION {
   public ADDRESS_KIND dwKind;
   public IntPtr       unionmember;
}
```

## <a name="members"></a>メンバー
`dwKind`\
共用体の解釈方法を指定する [ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md) 列挙の値。

`addr.addrNative`\
[C++ のみ]= ADDRESS_KIND_NATIVE の場合は、 [NATIVE_ADDRESS](../../../extensibility/debugger/reference/native-address.md) 構造体が含まれ `dwKind` ます。

`addr.addrThisRel`\
[C++ のみ]= ADDRESS_KIND_UNMANAGED_THIS_RELATIVE の場合は、[UNMANAGED_ADDRESS_THIS_RELATIVE](../../../extensibility/debugger/reference/unmanaged-address-this-relative.md) 構造体が含まれ `dwKind` ます。

`addr.addUPhysical`\
[C++ のみ]= ADDRESS_KIND_UNMANAGED_PHYSICAL の場合は、[UNMANAGED_ADDRESS_PHYSICAL](../../../extensibility/debugger/reference/unmanaged-address-physical.md) 構造体が含まれ `dwKind` ます。

`addr.addrMethod`\
[C++ のみ]= ADDRESS_KIND_METHOD の場合は、[METADATA_ADDRESS_METHOD](../../../extensibility/debugger/reference/metadata-address-method.md) 構造体が含まれ `dwKind` ます。

`addr.addrField`\
[C++ のみ]= ADDRESS_KIND_FIELD の場合は、[METADATA_ADDRESS_FIELD](../../../extensibility/debugger/reference/metadata-address-field.md) 構造体が含まれ `dwKind` ます。

`addr.addrLocal`\
[C++ のみ]= ADDRESS_KIND_LOCAL の場合は、[METADATA_ADDRESS_LOCAL](../../../extensibility/debugger/reference/metadata-address-local.md) 構造体が含まれ `dwKind` ます。

`addr.addrParam`\
[C++ のみ]= ADDRESS_KIND_PARAM の場合は、[METADATA_ADDRESS_PARAM](../../../extensibility/debugger/reference/metadata-address-param.md) 構造体が含まれ `dwKind` ます。

`addr.addrArrayElem`\
[C++ のみ]= ADDRESS_KIND_ARRAYELEM の場合は、[METADATA_ADDRESS_ARRAYELEM](../../../extensibility/debugger/reference/metadata-address-arrayelem.md) 構造体が含まれ `dwKind` ます。

`addr.addrRetVal`\
[C++ のみ]= ADDRESS_KIND_RETVAL の場合は、[METADATA_ADDRESS_RETVAL](../../../extensibility/debugger/reference/metadata-address-retval.md) 構造体が含まれ `dwKind` ます。

`addr.unused`\
[C++ のみ] 埋め込み。

`addr`\
[C++ のみ]共用体の名前。

`unionmember`\
[C# のみ]この値は、に基づいて適切な構造体の型にマーシャリングする必要があり `dwKind` ます。 共用体のとの間の関連付けについては、「解説」を参照してください `dwKind` 。

## <a name="remarks"></a>解説
この構造体は [DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md) 構造体に含まれており、さまざまな種類のアドレスのうちの1つを表し `DEBUG_ADDRESS` ます (構造体は、 [getaddress](../../../extensibility/debugger/reference/idebugaddress-getaddress.md) メソッドの呼び出しによって入力されます)。

 [C# のみ]次の表は、 `unionmember` アドレスの種類ごとにメンバーを解釈する方法を示しています。 この例では、1つのアドレスに対してこれがどのように行われるかを示します。

|`dwKind`|`unionmember` 解釈される|
|--------------|----------------------------------|
|`ADDRESS_KIND_NATIVE`|[NATIVE_ADDRESS](../../../extensibility/debugger/reference/native-address.md)|
|`ADDRESS_KIND_UNMANAGED_THIS_RELATIVE`|[UNMANAGED_ADDRESS_THIS_RELATIVE](../../../extensibility/debugger/reference/unmanaged-address-this-relative.md)|
|`ADDRESS_KIND_UNMANAGED_PHYSICAL`|[UNMANAGED_ADDRESS_PHYSICAL](../../../extensibility/debugger/reference/unmanaged-address-physical.md)|
|`ADDRESS_KIND_METHOD`|[METADATA_ADDRESS_METHOD](../../../extensibility/debugger/reference/metadata-address-method.md)|
|`ADDRESS_KIND_FIELD`|[METADATA_ADDRESS_FIELD](../../../extensibility/debugger/reference/metadata-address-field.md)|
|`ADDRESS_KIND_LOCAL`|[METADATA_ADDRESS_LOCAL](../../../extensibility/debugger/reference/metadata-address-local.md)|
|`ADDRESS_KIND_PARAM`|[METADATA_ADDRESS_PARAM](../../../extensibility/debugger/reference/metadata-address-param.md)|
|`ADDRESS_KIND_ARRAYELEM`|[METADATA_ADDRESS_ARRAYELEM](../../../extensibility/debugger/reference/metadata-address-arrayelem.md)|
|`ADDRESS_KIND_RETVAL`|[METADATA_ADDRESS_RETVAL](../../../extensibility/debugger/reference/metadata-address-retval.md)|

## <a name="example"></a>例
この例 `METADATA_ADDRESS_ARRAYELEM` では、 `DEBUG_ADDRESS_UNION` C# で構造体の1つの種類のアドレス () を解釈する方法を示します。 残りの要素は、まったく同じ方法で解釈できます。

```csharp
using System;
using System.Runtime.Interop.Services;
using Microsoft.VisualStudio.Debugger.Interop;

namespace MyPackage
{
    public class MyClass
    {
        public void Interpret(DEBUG_ADDRESS_UNION dau)
        {
            if (dau.dwKind == (uint)enum_ADDRESS_KIND.ADDRESS_KIND_METADATA_ARRAYELEM)
            {
                 METADATA_ADDRESS_ARRAYELEM arrayElem =
                     (METADATA_ADDRESS_ARRAYELEM)Marshal.PtrToStructure(dau.unionmember,
                                 typeof(METADATA_ADDRESS_ARRAYELEM));
            }
        }
    }
}
```

## <a name="requirements"></a>要件
ヘッダー: sh. h

名前空間: VisualStudio。

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md)
- [ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md)
- [GetAddress](../../../extensibility/debugger/reference/idebugaddress-getaddress.md)
