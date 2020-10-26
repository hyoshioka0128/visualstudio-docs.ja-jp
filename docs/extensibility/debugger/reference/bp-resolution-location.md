---
title: BP_RESOLUTION_LOCATION |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_RESOLUTION_LOCATION
helpviewer_keywords:
- BP_RESOLUTION_LOCATION structure
ms.assetid: 21dc5246-69c1-43e3-855c-9cd4e596c0e6
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 4b11d80e90daec19a14ca509e5a4b9bdb2d1ced4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80737813"
---
# <a name="bp_resolution_location"></a>BP_RESOLUTION_LOCATION
ブレークポイントの解決場所の構造を指定します。

## <a name="syntax"></a>構文

```cpp
struct _BP_RESOLUTION_LOCATION {
    BP_TYPE bpType;
    union {
        BP_RESOLUTION_CODE bpresCode;
        BP_RESOLUTION_DATA bpresData;
        int                unused;
    } bpResLocation;
} BP_RESOLUTION_LOCATION;
```

```csharp
public struct BP_RESOLUTION_LOCATION {
    public uint   bpType;
    public IntPtr unionmember1;
    public IntPtr unionmember2;
    public IntPtr unionmember3;
    public uint   unionmember4;
};
```

## <a name="members"></a>メンバー
`bpType`\
[BP_TYPE](../../../extensibility/debugger/reference/bp-type.md) `bpResLocation` 共用体またはメンバーを解釈する方法を指定する BP_TYPE 列挙の値 `unionmemberX` 。

`bpResLocation.bpresCode`\
[C++ のみ]の場合、 [BP_RESOLUTION_CODE](../../../extensibility/debugger/reference/bp-resolution-code.md)構造体が含まれ `bpType`  =  `BPT_CODE` ます。

`bpResLocation.bpresData`\
[C++ のみ]の場合、 [BP_RESOLUTION_DATA](../../../extensibility/debugger/reference/bp-resolution-data.md)構造体が含まれ `bpType`  =  `BPT_DATA` ます。

`bpResLocation.unused`\
[C++ のみ]プレースホルダー。

`unionmember1`\
[C# のみ]解釈方法については、「解説」を参照してください。

`unionmember2`\
[C# のみ]解釈方法については、「解説」を参照してください。

`unionmember3`\
[C# のみ]解釈方法については、「解説」を参照してください。

`unionmember4`\
[C# のみ]解釈方法については、「解説」を参照してください。

## <a name="remarks"></a>解説
この構造体は、 [BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md) および [BP_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-resolution-info.md) 構造体のメンバーです。

 [C# のみ] `unionmemberX` メンバーは、次の表に従って解釈されます。 左の列で値を調べ `bpType` て、各メンバーが表すものを特定し `unionmemberX` 、それに応じてをマーシャリングし `unionmemberX` ます。 この構造体を C# で解釈する方法については、例を参照してください。

|`bpLocationType`|`unionmember1`|`unionmember2`|`unionmember3`|`unionmember4`|
|----------------------|--------------------|--------------------|--------------------|--------------------|
|`BPT_CODE`|[IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)|-|-|-|
|`BPT_DATA`|`string` (データ式)|`string` (関数名)|`string` (イメージ名)|`enum_BP_RES_DATA_FLAGS`|

## <a name="example"></a>例
この例では、C# で構造体を解釈する方法を示し `BP_RESOLUTION_LOCATION` ます。

```csharp
using System;
using System.Runtime.Interop.Services;
using Microsoft.VisualStudio.Debugger.Interop;

namespace MyPackage
{
    public class MyClass
    {
        public void Interpret(BP_RESOLUTION_LOCATION bprl)
        {
            if (bprl.bpType == (uint)enum_BP_TYPE.BPT_CODE)
            {
                IDebugCodeContext2 pContext = (IDebugCodeContext2)Marshal.GetObjectForIUnknown(bp.unionmember1);
            }
            else if (bprl.bpType == (uint)enum_BP_TYPE.BPT_DATA)
            {
                string dataExpression = Marshal.PtrToStringBSTR(bp.unionmember3);
                string functionName = Marshal.PtrToStringBSTR(bp.unionmember2);
                string imageName = Marshal.PtrToStringBSTR(bp.unionmember3);
                enum_BP_RES_DATA_FLAGS numElements = (enum_BP_RES_DATA_FLAGS)bp.unionmember4;
            }
        }
    }
}
```

## <a name="requirements"></a>必要条件
ヘッダー: msdbg. h

名前空間: VisualStudio。

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [BP_TYPE](../../../extensibility/debugger/reference/bp-type.md)
- [BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md)
- [BP_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-resolution-info.md)
- [BP_RESOLUTION_CODE](../../../extensibility/debugger/reference/bp-resolution-code.md)
- [BP_RESOLUTION_DATA](../../../extensibility/debugger/reference/bp-resolution-data.md)
- [BP_RES_DATA_FLAGS](../../../extensibility/debugger/reference/bp-res-data-flags.md)
