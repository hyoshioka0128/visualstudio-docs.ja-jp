---
title: BP_REQUEST_INFO2 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- BP_REQUEST_INFO2
helpviewer_keywords:
- BP_REQUEST_INFO2 structure
ms.assetid: 008c87f7-a76e-43d3-8904-11b225d6a9a5
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 65edef6585fd8367c6fb23c291bf4e8376de8861
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68153360"
---
# <a name="bp_request_info2"></a>BP_REQUEST_INFO2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

ベンダー GUID、制約、およびトレースポイントを含む、ブレークポイントを実装するために必要な情報が含まれています。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
typedef struct _BP_REQUEST_INFO2 {  
   BPREQI_FIELDS   dwFields;  
   GUID            guidLanguage;  
   BP_LOCATION     bpLocation;  
   IDebugProgram2* pProgram;  
   BSTR            bstrProgramName;  
   IDebugThread2*  pThread;  
   BSTR            bstrThreadName;  
   BP_CONDITION    bpCondition;  
   BP_PASSCOUNT    bpPassCount;  
   BP_FLAGS        dwFlags;  
   GUID            guidVendor;  
   BSTR            bstrConstraint;  
   BSTR            bstrTracepoint;  
} BP_REQUEST_INFO2;  
```  
  
```csharp  
public struct BP_REQUEST_INFO2 {  
   public uint           dwFields;  
   public Guid           guidLanguage;  
   public BP_LOCATION    bpLocation;  
   public IDebugProgram2 pProgram;  
   public string         bstrProgramName;  
   public IDebugThread2  pThread;  
   public string         bstrThreadName;  
   public BP_CONDITION   bpCondition;  
   public BP_PASSCOUNT   bpPassCount;  
   public uint           dwFlags;  
   public Guid           guidVendor;  
   public string         bstrConstraint;  
   public string         bstrTracepoint;  
};  
```  
  
## <a name="members"></a>メンバー  
 `dwFields`  
 入力するフィールドを指定する、 [BPREQI_FIELDS](../../../extensibility/debugger/reference/bpreqi-fields.md) 列挙のフラグの組み合わせ。  
  
 `guidLanguage`  
 言語の GUID です。  
  
 `bpLocation`  
 ブレークポイントの位置の種類を指定する [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md) 構造体。  
  
 `pProgram`  
 ブレークポイントが発生するアプリケーションを表す [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) オブジェクト。  
  
 `bstrProgramName`  
 ブレークポイントが発生するアプリケーションの名前。  
  
 `pThread`  
 ブレークポイントが発生するスレッドを表す [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md) オブジェクト。  
  
 `bstrThreadName`  
 ブレークポイントが発生するスレッドの名前。  
  
 `bpCondition`  
 ブレークポイントが発生する条件を記述する [BP_CONDITION](../../../extensibility/debugger/reference/bp-condition.md) 構造体。  
  
 `bpPassCount`  
 ブレークポイントのパスカウント情報を格納する [BP_PASSCOUNT](../../../extensibility/debugger/reference/bp-passcount.md) 構造体。  
  
 `dwFlags`  
 要求されたブレークポイントのフラグを指定する、 [BP_FLAGS](../../../extensibility/debugger/reference/bp-flags.md) 列挙のフラグの組み合わせ。  
  
 `guidVendor`  
 ベンダの GUID。 Null 値を指定できます。  
  
 `bstrConstraint`  
 ブレークポイント制約の名前。 Null 値を指定できます。  
  
 `bstrTracepoint`  
 トレースポイントの名前。 Null 値を指定できます。  
  
## <a name="remarks"></a>注釈  
 この構造体は、 [GetRequestInfo2](../../../extensibility/debugger/reference/idebugbreakpointrequest3-getrequestinfo2.md) メソッドによって返されます。  
  
## <a name="requirements"></a>要件  
 ヘッダー: msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)   
 [GetRequestInfo2](../../../extensibility/debugger/reference/idebugbreakpointrequest3-getrequestinfo2.md)   
 [BPREQI_FIELDS](../../../extensibility/debugger/reference/bpreqi-fields.md)   
 [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)   
 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)   
 [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)   
 [BP_CONDITION](../../../extensibility/debugger/reference/bp-condition.md)   
 [BP_PASSCOUNT](../../../extensibility/debugger/reference/bp-passcount.md)   
 [BP_FLAGS](../../../extensibility/debugger/reference/bp-flags.md)
