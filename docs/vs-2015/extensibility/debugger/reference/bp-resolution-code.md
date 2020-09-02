---
title: BP_RESOLUTION_CODE |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- BP_RESOLUTION_CODE
helpviewer_keywords:
- BP_RESOLUTION_CODE structure
ms.assetid: ac103ec5-771c-4667-92de-b5abb53bbb52
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: b2323ce082a41633afae33e90030b704f2e53f80
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68153326"
---
# <a name="bp_resolution_code"></a>BP_RESOLUTION_CODE
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

コードのブレークポイントの位置を記述します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
typedef struct _BP_RESOLUTION_CODE {   
   IDebugCodeContext2* pCodeContext;  
} BP_RESOLUTION_CODE;  
```  
  
```csharp  
public struct BP_RESOLUTION_CODE {   
   public IDebugCodeContext2 pCodeContext;  
};  
```  
  
## <a name="members"></a>メンバー  
 `pCodeContext`  
 コード内のブレークポイントの位置を識別する [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md) オブジェクト。  
  
## <a name="remarks"></a>注釈  
 この構造体は[BP_RESOLUTION_LOCATION](../../../extensibility/debugger/reference/bp-resolution-location.md)構造体のメンバーであり、 [get解決情報](../../../extensibility/debugger/reference/idebugbreakpointresolution2-getresolutioninfo.md)メソッドによって返される[BP_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-resolution-info.md)構造体のメンバーになります。  
  
## <a name="requirements"></a>要件  
 ヘッダー: msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)   
 [BP_RESOLUTION_LOCATION](../../../extensibility/debugger/reference/bp-resolution-location.md)   
 [BP_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-resolution-info.md)   
 [Get解像度情報](../../../extensibility/debugger/reference/idebugbreakpointresolution2-getresolutioninfo.md)   
 [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
