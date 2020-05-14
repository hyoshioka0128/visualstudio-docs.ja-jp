---
title: DEBUG_ADDRESS_UNION |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DEBUG_ADDRESS_UNION
helpviewer_keywords:
- DEBUG_ADDRESS_UNION union
ms.assetid: e3d11aab-de0d-4109-b5dc-11e07e64382d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ad531ee10914e404459632c98aae4a9bbda8e437
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737532"
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
ADDRESS_KIND[列挙体](../../../extensibility/debugger/reference/address-kind.md)の値。

`addr.addrNative`\
[C++のみ]= ADDRESS_KIND_NATIVEの場合`dwKind`[、NATIVE_ADDRESS](../../../extensibility/debugger/reference/native-address.md)構造を格納します。

`addr.addrThisRel`\
[C++のみ]= ADDRESS_KIND_UNMANAGED_THIS_RELATIVEの`dwKind`[場合、UNMANAGED_ADDRESS_THIS_RELATIVE](../../../extensibility/debugger/reference/unmanaged-address-this-relative.md)構造を格納します。

`addr.addUPhysical`\
[C++のみ]= ADDRESS_KIND_UNMANAGED_PHYSICALの`dwKind`[場合、UNMANAGED_ADDRESS_PHYSICAL](../../../extensibility/debugger/reference/unmanaged-address-physical.md)構造体を格納します。

`addr.addrMethod`\
[C++のみ]= ADDRESS_KIND_METHODの場合`dwKind`[、METADATA_ADDRESS_METHOD](../../../extensibility/debugger/reference/metadata-address-method.md)構造を格納します。

`addr.addrField`\
[C++のみ]= ADDRESS_KIND_FIELDの`dwKind`[場合、METADATA_ADDRESS_FIELD](../../../extensibility/debugger/reference/metadata-address-field.md)構造を格納します。

`addr.addrLocal`\
[C++のみ]= ADDRESS_KIND_LOCALの場合`dwKind`[、METADATA_ADDRESS_LOCAL](../../../extensibility/debugger/reference/metadata-address-local.md)構造を格納します。

`addr.addrParam`\
[C++のみ]= ADDRESS_KIND_PARAMの場合`dwKind`[、METADATA_ADDRESS_PARAM](../../../extensibility/debugger/reference/metadata-address-param.md)構造を格納します。

`addr.addrArrayElem`\
[C++のみ]= ADDRESS_KIND_ARRAYELEMの`dwKind`[場合、METADATA_ADDRESS_ARRAYELEM](../../../extensibility/debugger/reference/metadata-address-arrayelem.md)構造を格納します。

`addr.addrRetVal`\
[C++のみ]= ADDRESS_KIND_RETVALの`dwKind`[場合、METADATA_ADDRESS_RETVAL](../../../extensibility/debugger/reference/metadata-address-retval.md)構造を格納します。

`addr.unused`\
[C++のみ]パディング。

`addr`\
[C++のみ]共用体の名前。

`unionmember`\
[C#のみ]この値は、 に基づいて適切な構造体型にマーシャリング`dwKind`する必要があります。 共用体の関連`dwKind`付けと解釈については、「解説」を参照してください。

## <a name="remarks"></a>Remarks
この構造体は[、DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md)構造の一部であり、さまざまな種類のアドレスの 1 つを表`DEBUG_ADDRESS`します (構造体は[GetAddress](../../../extensibility/debugger/reference/idebugaddress-getaddress.md)メソッドの呼び出しによって埋められます)。

 [C#のみ]次の表は、アドレスの種類`unionmember`ごとにメンバーを解釈する方法を示しています。 例は、ある種類のアドレスに対してこれを行う方法を示しています。

|`dwKind`|`unionmember`として解釈される|
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
この例では、C# の構造体のアドレス`METADATA_ADDRESS_ARRAYELEM`( `DEBUG_ADDRESS_UNION` ) の種類を解釈する方法を示します。 残りの要素は、まったく同じ方法で解釈できます。

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

## <a name="requirements"></a>必要条件
ヘッダー: sh.h

名前空間: を使用します。

アセンブリ:

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md)
- [ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md)
- [GetAddress](../../../extensibility/debugger/reference/idebugaddress-getaddress.md)
