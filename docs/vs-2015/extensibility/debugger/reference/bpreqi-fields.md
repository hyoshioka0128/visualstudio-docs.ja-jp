---
title: BPREQI_FIELDS |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- BPREQI_FIELDS
helpviewer_keywords:
- BPREQI_FIELDS enumeration
ms.assetid: 679e771e-4a79-484e-af37-f962ef4aa245
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a8ad9e4b6d83ebc05c78a8b84c0c06e00d7563bc
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68153227"
---
# <a name="bpreqi_fields"></a>BPREQI_FIELDS
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

ブレークポイント要求について取得する情報を指定します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
enum enum_BPREQI_FIELDS {   
   BPREQI_BPLOCATION   = 0x0001,  
   BPREQI_LANGUAGE     = 0x0002,  
   BPREQI_PROGRAM      = 0x0004,  
   BPREQI_PROGRAMNAME  = 0x0008,  
   BPREQI_THREAD       = 0x0010,  
   BPREQI_THREADNAME   = 0x0020,  
   BPREQI_PASSCOUNT    = 0x0040,  
   BPREQI_CONDITION    = 0x0080,  
   BPREQI_FLAGS        = 0x0100,  
   BPREQI_ALLOLDFIELDS = 0x01ff  
   BPREQI_VENDOR       = 0x0200,   // BP_REQUEST_INFO2 only  
   BPREQI_CONSTRAINT   = 0x0400,   // BP_REQUEST_INFO2 only  
   BPREQI_TRACEPOINT   = 0x0800,   // BP_REQUEST_INFO2 only  
   BPREQI_ALLFIELDS    = 0x0fff    // BP_REQUEST_INFO2 only  
};  
typedef DWORD BPREQI_FIELDS;  
```  
  
```csharp  
public enum enum_BPREQI_FIELDS {   
   BPREQI_BPLOCATION   = 0x0001,  
   BPREQI_LANGUAGE     = 0x0002,  
   BPREQI_PROGRAM      = 0x0004,  
   BPREQI_PROGRAMNAME  = 0x0008,  
   BPREQI_THREAD       = 0x0010,  
   BPREQI_THREADNAME   = 0x0020,  
   BPREQI_PASSCOUNT    = 0x0040,  
   BPREQI_CONDITION    = 0x0080,  
   BPREQI_FLAGS        = 0x0100,  
   BPREQI_ALLOLDFIELDS = 0x01ff  
   BPREQI_VENDOR       = 0x0200,   // BP_REQUEST_INFO2 only  
   BPREQI_CONSTRAINT   = 0x0400,   // BP_REQUEST_INFO2 only  
   BPREQI_TRACEPOINT   = 0x0800,   // BP_REQUEST_INFO2 only  
   BPREQI_ALLFIELDS    = 0x0fff    // BP_REQUEST_INFO2 only  
};  
```  
  
## <a name="members"></a>メンバー  
 BPREQI_BPLOCATION  
 `bpLocation` [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)または[BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)構造の (ブレークポイントの位置) フィールドを初期化/使用します。  
  
 BPREQI_LANGUAGE  
 `guidLanguage`または構造体のフィールドを初期化/使用し `BP_REQUEST_INFO` `BP_REQUEST_INFO2` ます。  
  
 BPREQI_PROGRAM  
 `pProgram`または構造体のフィールドを初期化/使用し `BP_REQUEST_INFO` `BP_REQUEST_INFO2` ます。  
  
 BPREQI_PROGRAMNAME  
 `bstrProgramName`または構造体のフィールドを初期化/使用し `BP_REQUEST_INFO` `BP_REQUEST_INFO2` ます。  
  
 BPREQI_THREAD  
 `pThread`または構造体のフィールドを初期化/使用し `BP_REQUEST_INFO` `BP_REQUEST_INFO2` ます。  
  
 BPREQI_THREADNAME  
 `bstrThreadName`または構造体のフィールドを初期化/使用し `BP_REQUEST_INFO` `BP_REQUEST_INFO2` ます。  
  
 BPREQI_PASSCOUNT  
 `bpPassCount`または構造体のフィールドを初期化/使用し `BP_REQUEST_INFO` `BP_REQUEST_INFO2` ます。  
  
 BPREQI_CONDITION  
 `bpCondition`または構造体の (ブレークポイント条件) フィールドを初期化または使用し `BP_REQUEST_INFO` `BP_REQUEST_INFO2` ます。  
  
 BPREQI_FLAGS  
 `dwFlags`または構造体のフィールドを初期化/使用し `BP_REQUEST_INFO` `BP_REQUEST_INFO2` ます。  
  
 BPREQI_ALLOLDFIELDS  
 構造体ののすべてのフィールドを初期化/使用し `BP_REQUEST_INFO` ます。  
  
 BPREQI_VENDOR  
 構造体のフィールドを初期化/使用し `guidVendor` `BP_REQUEST_INFO2` ます。  
  
 BPREQI_CONSTRAINT  
 構造体のフィールドを初期化/使用し `bstrConstraint` `BP_REQUEST_INFO2` ます。  
  
 BPREQI_TRACEPOINT  
 構造体のフィールドを初期化/使用し `bstrTracepoint` `BP_REQUEST_INFO2` ます。  
  
 BPREQI_ALLFIELDS  
 構造体のすべてのフィールドを指定し `BP_REQUEST_INFO2` ます。  
  
## <a name="remarks"></a>注釈  
 [Getrequestinfo](../../../extensibility/debugger/reference/idebugbreakpointrequest2-getrequestinfo.md)メソッドと[BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)メソッドに引数として渡され、 [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)および[BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)構造体のどのフィールドを初期化するかを指定します。  
  
 これらのフラグは、および構造体のどのフィールドが使用され、 `BP_REQUEST_INFO` `BP_REQUEST_INFO2` 各構造体が返されたときに有効であるかを示すためにも使用されます。  
  
 これらの値は、ビットごとのを使用して組み合わせることができ `OR` ます。  
  
## <a name="requirements"></a>要件  
 ヘッダー: msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [列挙](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [GetRequestInfo](../../../extensibility/debugger/reference/idebugbreakpointrequest2-getrequestinfo.md)   
 [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)   
 [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)
