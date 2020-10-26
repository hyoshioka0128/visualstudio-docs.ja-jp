---
title: BP_REQUEST_INFO |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- BP_REQUEST_INFO
helpviewer_keywords:
- BP_REQUEST_INFO structure
ms.assetid: 42a31412-5b6b-47fe-a762-0c2bc769e1cc
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: c514f43f39f0b002da0f01b1804120b98530990b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68182949"
---
# <a name="bp_request_info"></a>BP_REQUEST_INFO
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

ブレークポイントを実装するために必要な情報が含まれています。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
typedef struct _BP_REQUEST_INFO {  
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
} BP_REQUEST_INFO;  
```  
  
```csharp  
public struct BP_REQUEST_INFO {  
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
  
## <a name="remarks"></a>注釈  
 この構造体は、 [Getrequestinfo](../../../extensibility/debugger/reference/idebugbreakpointrequest2-getrequestinfo.md) メソッドによって返されます。  
  
 デバッグエンジンのベンダ GUID、ブレークポイントの制約、またはトレースポイントを取得する必要がある場合は、 [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md) 構造を参照してください。  
  
## <a name="requirements"></a>要件  
 ヘッダー: msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)   
 [GetRequestInfo](../../../extensibility/debugger/reference/idebugbreakpointrequest2-getrequestinfo.md)   
 [BPREQI_FIELDS](../../../extensibility/debugger/reference/bpreqi-fields.md)   
 [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)   
 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)   
 [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)   
 [BP_CONDITION](../../../extensibility/debugger/reference/bp-condition.md)   
 [BP_PASSCOUNT](../../../extensibility/debugger/reference/bp-passcount.md)   
 [BP_FLAGS](../../../extensibility/debugger/reference/bp-flags.md)   
 [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)
