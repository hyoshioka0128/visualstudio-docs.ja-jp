---
title: BP_RESOLUTION_LOCATION |マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737813"
---
# <a name="bp_resolution_location"></a>BP_RESOLUTION_LOCATION
ブレークポイントの解像度の場所の構造を指定します。

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
共用体または`unionmemberX`メンバーの解釈方法を指定する[BP_TYPE](../../../extensibility/debugger/reference/bp-type.md)列挙`bpResLocation`体の値。

`bpResLocation.bpresCode`\
[C++のみ]BP_RESOLUTION_CODE構造体[を](../../../extensibility/debugger/reference/bp-resolution-code.md)格納します`bpType` = `BPT_CODE`。

`bpResLocation.bpresData`\
[C++のみ]BP_RESOLUTION_DATA構造[を](../../../extensibility/debugger/reference/bp-resolution-data.md)格納します`bpType` = `BPT_DATA`。

`bpResLocation.unused`\
[C++のみ]プレースホルダ。

`unionmember1`\
[C#のみ]解釈方法については、「解説」を参照してください。

`unionmember2`\
[C#のみ]解釈方法については、「解説」を参照してください。

`unionmember3`\
[C#のみ]解釈方法については、「解説」を参照してください。

`unionmember4`\
[C#のみ]解釈方法については、「解説」を参照してください。

## <a name="remarks"></a>Remarks
この構造体は[、BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md)と[BP_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-resolution-info.md)構造のメンバーです。

 [C#のみ]メンバー`unionmemberX`は、次の表に従って解釈されます。 左の列を見下ろし`bpType`、その後、各`unionmemberX`メンバーが何を表しているかを判断`unionmemberX`し、それに応じてマーシャリングします。 C# でこの構造体を解釈する方法については、例を参照してください。

|`bpLocationType`|`unionmember1`|`unionmember2`|`unionmember3`|`unionmember4`|
|----------------------|--------------------|--------------------|--------------------|--------------------|
|`BPT_CODE`|[IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)|-|-|-|
|`BPT_DATA`|`string`(データ式)|`string`(関数名)|`string`(画像名)|`enum_BP_RES_DATA_FLAGS`|

## <a name="example"></a>例
この例では、C#`BP_RESOLUTION_LOCATION`で構造体を解釈する方法を示します。

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
ヘッダー: msdbg.h

名前空間: を使用します。

アセンブリ:

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [BP_TYPE](../../../extensibility/debugger/reference/bp-type.md)
- [BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md)
- [BP_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-resolution-info.md)
- [BP_RESOLUTION_CODE](../../../extensibility/debugger/reference/bp-resolution-code.md)
- [BP_RESOLUTION_DATA](../../../extensibility/debugger/reference/bp-resolution-data.md)
- [BP_RES_DATA_FLAGS](../../../extensibility/debugger/reference/bp-res-data-flags.md)
