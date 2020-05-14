---
title: BP_LOCATION |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_LOCATION
helpviewer_keywords:
- BP_LOCATION union
ms.assetid: ed1e874c-f289-4c31-8b6c-04dde03ad0f5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c98fde516a3e836302cd7eb2c73abd730d5cc8c5
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737932"
---
# <a name="bp_location"></a>BP_LOCATION
ブレークポイントの場所を記述するために使用する構造体の種類を指定します。

## <a name="syntax"></a>構文

```cpp
typedef struct _BP_LOCATION {
    BP_LOCATION_TYPE bpLocationType;
    union {
        BP_LOCATION_CODE_FILE_LINE   bplocCodeFileLine;
        BP_LOCATION_CODE_FUNC_OFFSET bplocCodeFuncOffset;
        BP_LOCATION_CODE_CONTEXT     bplocCodeContext;
        BP_LOCATION_CODE_STRING      bplocCodeString;
        BP_LOCATION_CODE_ADDRESS     bplocCodeAddress;
        BP_LOCATION_DATA_STRING      bplocDataString;
        BP_LOCATION_RESOLUTION       bplocResolution;
        DWORD                        unused;
    } bpLocation;
} BP_LOCATION;
```

```csharp
public struct BP_LOCATION {
    public uint   bpLocationType;
    public IntPtr unionmember1;
    public IntPtr unionmember2;
    public IntPtr unionmember3;
    public IntPtr unionmember4;
};
```

## <a name="members"></a>メンバー
`bpLocationType`\
共用体または`unionmemberX`メンバーの解釈に使用される[BP_LOCATION_TYPE](../../../extensibility/debugger/reference/bp-location-type.md)列挙体の`bpLocation`値。

`bpLocation`.`bplocCodeFileLine`\
[C++のみ]BP_LOCATION_CODE_FILE_LINEの[構造体](../../../extensibility/debugger/reference/bp-location-code-file-line.md)を`bpLocationType` = `BPLT_CODE_FILE_LINE`格納します 。

`bpLocation.bplocCodeFuncOffset`\
[C++のみ]BP_LOCATION_CODE_FUNC_OFFSETの[構造体](../../../extensibility/debugger/reference/bp-location-code-func-offset.md)を`bpLocationType` = `BPLT_CODE_FUNC_OFFSET`格納します 。

`bpLocation.bplocCodeContext`\
[C++のみ]BP_LOCATION_CODE_CONTEXTの[構造体](../../../extensibility/debugger/reference/bp-location-code-context.md)を`bpLocationType` = `BPLT_CODE_CONTEXT`格納します 。

`bpLocation.bplocCodeString`\
[C++のみ]BP_LOCATION_CODE_STRING構造[を](../../../extensibility/debugger/reference/bp-location-code-string.md)格納します`bpLocationType` = `BPLT_CODE_STRING`。

`bpLocation.bplocCodeAddress`\
[C++のみ]BP_LOCATION_CODE_ADDRESS構造[が](../../../extensibility/debugger/reference/bp-location-code-address.md)含`bpLocationType` = `BPLT_CODE_ADDRESS`まれています 。

`bpLocation.bplocDataString`\
[C++のみ]BP_LOCATION_DATA_STRING構造[を](../../../extensibility/debugger/reference/bp-location-data-string.md)格納します`bpLocationType` = `BPLT_DATA_STRING`。

`bpLocation.bplocResolution`\
[C++のみ]BP_LOCATION_RESOLUTIONの[構造体](../../../extensibility/debugger/reference/bp-location-resolution.md)を`bpLocationType` = `BPLT_RESOLUTION`格納します 。

`unionmember1`\
[C#のみ]解釈方法については、「解説」を参照してください。

`unionmember2`\
[C#のみ]解釈方法については、「解説」を参照してください。

`unionmember3`\
[C#のみ]解釈方法については、「解説」を参照してください。

`unionmember4`\
[C#のみ]解釈方法については、「解説」を参照してください。

## <a name="remarks"></a>Remarks
この構造体は[、BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)および[BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)構造のメンバーです。

 [C#のみ]メンバー`unionmemberX`は、次の表に従って解釈されます。 左の列で値を`bpLocationType`見てから、他の列を見て、各`unionmemberX`メンバーが何を表`unionmemberX`しているかを判断し、それに応じてマーシャリングします。 C# でこの構造体の一部を解釈する方法については、例を参照してください。

|`bpLocationType`|`unionmember1`|`unionmember2`|`unionmember3`|`unionmember4`|
|----------------------|--------------------|--------------------|--------------------|--------------------|
|`BPLT_CODE_FILE_LINE`|`string`(コンテキスト)|[IDebugDocumentPosition2](../../../extensibility/debugger/reference/idebugdocumentposition2.md)|-|-|
|`BPLT_CODE_FUNC_OFFSET`|`string`(コンテキスト)|[IDebugFunctionPosition2](../../../extensibility/debugger/reference/idebugfunctionposition2.md)|-|-|
|`BPLT_CODE_CONTEXT`|[IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)|-|-|-|
|`BPLT_CODE_STRING`|`string`(コンテキスト)|`string`(条件式)|-|-|
|`BPLT_CODE_ADDRESS`|`string`(コンテキスト)|`string`(モジュール URL)|`string`(関数名)|`string`(住所)|
|`BPLT_DATA_STRING`|[IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)|`string`(コンテキスト)|`string`(データ式)|`uint`(要素数)|
|`BPLT_RESOLUTION`|[IDebugBreakpointResolution2](../../../extensibility/debugger/reference/idebugbreakpointresolution2.md)|-|-|-|

## <a name="example"></a>例
この例では、型の`BP_LOCATION`C# の構造体を`BPLT_DATA_STRING`解釈する方法を示します。 この特定の型は、4 つの`unionmemberX`メンバーすべてを、すべての可能な形式 (オブジェクト、文字列、および数値) で解釈する方法を示しています。

```csharp
using System;
using System.Runtime.Interop.Services;
using Microsoft.VisualStudio.Debugger.Interop;

namespace MyPackage
{
    public class MyClass
    {
        public void Interpret(BP_LOCATION bp)
        {
            if (bp.bpLocationType == (uint)enum_BP_LOCATION_TYPE.BPLT_DATA_STRING)
            {
                IDebugThread2 pThread = (IDebugThread2)Marshal.GetObjectForIUnknown(bp.unionmember1);
                string context = Marshal.PtrToStringBSTR(bp.unionmember2);
                string dataExpression = Marshal.PtrToStringBSTR(bp.unionmember3);
                uint numElements = (uint)Marshal.ReadInt32(bp.unionmember4);
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
- [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)
- [BP_LOCATION_CODE_FILE_LINE](../../../extensibility/debugger/reference/bp-location-code-file-line.md)
- [BP_LOCATION_CODE_FUNC_OFFSET](../../../extensibility/debugger/reference/bp-location-code-func-offset.md)
- [BP_LOCATION_CODE_CONTEXT](../../../extensibility/debugger/reference/bp-location-code-context.md)
- [BP_LOCATION_CODE_STRING](../../../extensibility/debugger/reference/bp-location-code-string.md)
- [BP_LOCATION_CODE_ADDRESS](../../../extensibility/debugger/reference/bp-location-code-address.md)
- [BP_LOCATION_DATA_STRING](../../../extensibility/debugger/reference/bp-location-data-string.md)
- [BP_LOCATION_RESOLUTION](../../../extensibility/debugger/reference/bp-location-resolution.md)
