---
title: BP_LOCATION |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- BP_LOCATION
helpviewer_keywords:
- BP_LOCATION union
ms.assetid: ed1e874c-f289-4c31-8b6c-04dde03ad0f5
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2a3e5f690a679118c7bb02c110d6e5d066a2bd0d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68153394"
---
# <a name="bp_location"></a>BP_LOCATION
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

ブレークポイントの位置を示すために使用される構造体の種類を指定します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
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
 `bpLocationType`  
 共用体またはメンバーを解釈するために使用される [BP_LOCATION_TYPE](../../../extensibility/debugger/reference/bp-location-type.md) 列挙の値 `bpLocation` `unionmemberX` 。  
  
 `bpLocation`.`bplocCodeFileLine`  
 [C++ のみ]の場合、 [BP_LOCATION_CODE_FILE_LINE](../../../extensibility/debugger/reference/bp-location-code-file-line.md)構造体が含まれ `bpLocationType`  =  `BPLT_CODE_FILE_LINE` ます。  
  
 `bpLocation.bplocCodeFuncOffset`  
 [C++ のみ]の場合、 [BP_LOCATION_CODE_FUNC_OFFSET](../../../extensibility/debugger/reference/bp-location-code-func-offset.md)構造体が含まれ `bpLocationType`  =  `BPLT_CODE_FUNC_OFFSET` ます。  
  
 `bpLocation.bplocCodeContext`  
 [C++ のみ]の場合、 [BP_LOCATION_CODE_CONTEXT](../../../extensibility/debugger/reference/bp-location-code-context.md)構造体が含まれ `bpLocationType`  =  `BPLT_CODE_CONTEXT` ます。  
  
 `bpLocation.bplocCodeString`  
 [C++ のみ]の場合、 [BP_LOCATION_CODE_STRING](../../../extensibility/debugger/reference/bp-location-code-string.md)構造体が含まれ `bpLocationType`  =  `BPLT_CODE_STRING` ます。  
  
 `bpLocation.bplocCodeAddress`  
 [C++ のみ]の場合、 [BP_LOCATION_CODE_ADDRESS](../../../extensibility/debugger/reference/bp-location-code-address.md)構造体が含まれ `bpLocationType`  =  `BPLT_CODE_ADDRESS` ます。  
  
 `bpLocation.bplocDataString`  
 [C++ のみ]の場合、 [BP_LOCATION_DATA_STRING](../../../extensibility/debugger/reference/bp-location-data-string.md)構造体が含まれ `bpLocationType`  =  `BPLT_DATA_STRING` ます。  
  
 `bpLocation.bplocResolution`  
 [C++ のみ]の場合、 [BP_LOCATION_RESOLUTION](../../../extensibility/debugger/reference/bp-location-resolution.md)構造体が含まれ `bpLocationType`  =  `BPLT_RESOLUTION` ます。  
  
 `unionmember1`  
 [C# のみ]解釈方法については、「解説」を参照してください。  
  
 `unionmember2`  
 [C# のみ]解釈方法については、「解説」を参照してください。  
  
 `unionmember3`  
 [C# のみ]解釈方法については、「解説」を参照してください。  
  
 `unionmember4`  
 [C# のみ]解釈方法については、「解説」を参照してください。  
  
## <a name="remarks"></a>注釈  
 この構造体は、 [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md) および [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md) 構造体のメンバーです。  
  
 [C# のみ] `unionmemberX` メンバーは、次の表に従って解釈されます。 左側の列で値を確認 `bpLocationType` し、他の列を参照して各メンバーが表すものを特定し `unionmemberX` 、それに応じてをマーシャリングし `unionmemberX` ます。 C# でこの構造体の一部を解釈する方法については、例を参照してください。  
  
|`bpLocationType`|`unionmember1`|`unionmember2`|`unionmember3`|`unionmember4`|  
|----------------------|--------------------|--------------------|--------------------|--------------------|  
|`BPLT_CODE_FILE_LINE`|`string` (コンテキスト)|[IDebugDocumentPosition2](../../../extensibility/debugger/reference/idebugdocumentposition2.md)|-|-|  
|`BPLT_CODE_FUNC_OFFSET`|`string` (コンテキスト)|[IDebugFunctionPosition2](../../../extensibility/debugger/reference/idebugfunctionposition2.md)|-|-|  
|`BPLT_CODE_CONTEXT`|[IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)|-|-|-|  
|`BPLT_CODE_STRING`|`string` (コンテキスト)|`string` (条件式)|-|-|  
|`BPLT_CODE_ADDRESS`|`string` (コンテキスト)|`string` (モジュールの URL)|`string` (関数名)|`string` 先|  
|`BPLT_DATA_STRING`|[IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)|`string` (コンテキスト)|`string` (データ式)|`uint` (要素の数)|  
|`BPLT_RESOLUTION`|[IDebugBreakpointResolution2](../../../extensibility/debugger/reference/idebugbreakpointresolution2.md)|-|-|-|  
  
## <a name="example"></a>例  
 この例 `BP_LOCATION` では、型の C# で構造体を解釈する方法を示し `BPLT_DATA_STRING` ます。 この特定の型は、 `unionmemberX` すべての可能な形式 (オブジェクト、文字列、および数値) の4つのメンバーすべてを解釈する方法を示しています。  
  
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
  
## <a name="requirements"></a>要件  
 ヘッダー: msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)   
 [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)   
 [BP_LOCATION_CODE_FILE_LINE](../../../extensibility/debugger/reference/bp-location-code-file-line.md)   
 [BP_LOCATION_CODE_FUNC_OFFSET](../../../extensibility/debugger/reference/bp-location-code-func-offset.md)   
 [BP_LOCATION_CODE_CONTEXT](../../../extensibility/debugger/reference/bp-location-code-context.md)   
 [BP_LOCATION_CODE_STRING](../../../extensibility/debugger/reference/bp-location-code-string.md)   
 [BP_LOCATION_CODE_ADDRESS](../../../extensibility/debugger/reference/bp-location-code-address.md)   
 [BP_LOCATION_DATA_STRING](../../../extensibility/debugger/reference/bp-location-data-string.md)   
 [BP_LOCATION_RESOLUTION](../../../extensibility/debugger/reference/bp-location-resolution.md)
