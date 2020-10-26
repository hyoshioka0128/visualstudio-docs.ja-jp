---
title: BPREQI_FIELDS90 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- BPREQI_FIELDS90 enumeration
ms.assetid: bf6f7efc-39f2-46a2-906d-c3647bf89995
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 97a38b4296668cb287f34e5b1afcbd7c90477011
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68153216"
---
# <a name="bpreqi_fields90"></a>BPREQI_FIELDS90
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

ブレークポイント要求について取得する情報を指定する有効な値を列挙します。 この列挙体は [BPREQI_FIELDS](../../../extensibility/debugger/reference/bpreqi-fields.md) 列挙体を拡張します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
enum enum_BPREQI_FIELDS90  
{  
   // VS 8.0 values  
   BPREQI90_BPLOCATION                = 0x0001,  
   BPREQI90_LANGUAGE                  = 0x0002,  
   BPREQI90_PROGRAM                   = 0x0004,  
   BPREQI90_PROGRAMNAME               = 0x0008,  
   BPREQI90_THREAD                    = 0x0010,  
   BPREQI90_THREADNAME                = 0x0020,  
   BPREQI90_PASSCOUNT                 = 0x0040,  
   BPREQI90_CONDITION                 = 0x0080,  
   BPREQI90_FLAGS                     = 0x0100,  
   BPREQI90_ALLOLDFIELDS              = 0x01ff,  
   BPREQI90_VENDOR                    = 0x0200,  
   BPREQI90_CONSTRAINT                = 0x0400,  
   BPREQI90_TRACEPOINT                = 0x0800,  
  
   // Values added in VS 9.0  
   BPREQI90_MACROTRACEPOINT           = 0x1000,  
  
   BPREQI90_ALLFIELDS                 = 0xffff  
};  
typedef DWORD BPREQI_FIELDS90;  
```  
  
```csharp  
public enum enum_BPREQI_FIELDS90  
{  
    // VS 8.0 values  
    BPREQI90_BPLOCATION                = 0x0001,  
    BPREQI90_LANGUAGE                  = 0x0002,  
    BPREQI90_PROGRAM                   = 0x0004,  
    BPREQI90_PROGRAMNAME               = 0x0008,  
    BPREQI90_THREAD                    = 0x0010,  
    BPREQI90_THREADNAME                = 0x0020,  
    BPREQI90_PASSCOUNT                 = 0x0040,  
    BPREQI90_CONDITION                 = 0x0080,  
    BPREQI90_FLAGS                     = 0x0100,  
    BPREQI90_ALLOLDFIELDS              = 0x01ff,  
    BPREQI90_VENDOR                    = 0x0200,  
    BPREQI90_CONSTRAINT                = 0x0400,  
    BPREQI90_TRACEPOINT                = 0x0800,  
  
    // Values added in VS 9.0  
    BPREQI90_MACROTRACEPOINT           = 0x1000,  
  
    BPREQI90_ALLFIELDS                 = 0xffff  
};  
```  
  
#### <a name="parameters"></a>パラメーター  
 BPREQI90_BPLOCATION  
 `bpLocation` [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)または[BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)構造の (ブレークポイントの場所) フィールドを初期化または使用します。  
  
 BPREQI90_LANGUAGE  
 `guidLanguage`または構造体のフィールドを初期化または使用し `BP_REQUEST_INFO` `BP_REQUEST_INFO2` ます。  
  
 BPREQI90_PROGRAM  
 `pProgram`または構造体のフィールドを初期化または使用し `BP_REQUEST_INFO` `BP_REQUEST_INFO2` ます。  
  
 BPREQI90_PROGRAMNAME  
 `bstrProgramName`または構造体のフィールドを初期化または使用し `BP_REQUEST_INFO` `BP_REQUEST_INFO2` ます。  
  
 BPREQI90_THREAD  
 `pThread`または構造体のフィールドを初期化または使用し `BP_REQUEST_INFO` `BP_REQUEST_INFO2` ます。  
  
 BPREQI90_THREADNAME  
 `bstrThreadName`または構造体のフィールドを初期化または使用し `BP_REQUEST_INFO` `BP_REQUEST_INFO2` ます。  
  
 BPREQI90_PASSCOUNT  
 `bpPassCount`または構造体のフィールドを初期化または使用し `BP_REQUEST_INFO` `BP_REQUEST_INFO2` ます。  
  
 BPREQI90_CONDITION  
 `bpCondition`または構造体の (ブレークポイント条件) フィールドを初期化または使用し `BP_REQUEST_INFO` `BP_REQUEST_INFO2` ます。  
  
 BPREQI90_FLAGS  
 `dwFlags`または構造体のフィールドを初期化または使用し `BP_REQUEST_INFO` `BP_REQUEST_INFO2` ます。  
  
 BPREQI90_ALLOLDFIELDS  
 構造体ののすべてのフィールドを初期化または使用し `BP_REQUEST_INFO` ます。  
  
 BPREQI90_VENDOR  
 構造体のフィールドを初期化または使用し `guidVendor` `BP_REQUEST_INFO2` ます。  
  
 BPREQI90_CONSTRAINT  
 構造体のフィールドを初期化または使用し `bstrConstraint` `BP_REQUEST_INFO2` ます。  
  
 BPREQI90_TRACEPOINT  
 構造体のフィールドを初期化または使用し `bstrTracepoint` `BP_REQUEST_INFO2` ます。  
  
 BPREQI90_MACROTRACEPOINT  
 構造体のフィールドを初期化または使用し `bstrMacroTracepoint` `BP_REQUEST_INFO2` ます。 BPREQI_ALLFIELDS には、このフィールドは含まれません。  
  
 BPREQI90_ALLFIELDS  
 構造体のすべてのフィールドを指定し `BP_REQUEST_INFO2` ます。  
  
## <a name="requirements"></a>要件  
 ヘッダー: Msdbg90  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
