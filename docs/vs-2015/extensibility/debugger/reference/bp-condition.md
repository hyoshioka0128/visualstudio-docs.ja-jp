---
title: BP_CONDITION |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- BP_CONDITION
helpviewer_keywords:
- BP_CONDITION structure
ms.assetid: 407f87a3-2878-429b-8c65-b68feb36622a
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 8d49c912ae14154fc552c76fc011596f4f22166f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68153562"
---
# <a name="bp_condition"></a>BP_CONDITION
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

ブレークポイントが発生する条件について説明します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
typedef struct _BP_CONDITION {   
   IDebugThread2* pThread;  
   BP_COND_STYLE  styleCondition;  
   BSTR           bstrContext;  
   BSTR           bstrCondition;  
   UINT           nRadix;  
} BP_CONDITION;  
```  
  
```csharp  
public struct BP_CONDITION {   
   public IDebugThread2 pThread;  
   public uint          styleCondition;  
   public string        bstrContext;  
   public string        bstrCondition;  
   public uint          nRadix;  
};  
```  
  
## <a name="members"></a>メンバー  
 `pThread`  
 ブレークポイントを含むアプリケーションのアクティブスレッドを表す [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md) オブジェクト。  
  
 `styleCondition`  
 このブレークポイント条件のスタイルを記述する [BP_COND_STYLE](../../../extensibility/debugger/reference/bp-cond-style.md) 列挙体の値。  
  
 `bstrContext`  
 ブレークポイントの位置。  
  
 `bstrCondition`  
 ブレークポイントの発生条件。  
  
 `nRadix`  
 数値情報の評価に使用される基数。  
  
## <a name="remarks"></a>注釈  
 この構造体は、 [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md) および [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md) 構造体のメンバーです。  
  
 この構造体は、 [setcondition](../../../extensibility/debugger/reference/idebugboundbreakpoint2-setcondition.md) メソッドおよび [setcondition](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-setcondition.md) メソッドにパラメーターとしても渡されます。  
  
## <a name="requirements"></a>要件  
 ヘッダー: msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)   
 [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)   
 [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)   
 [SetCondition](../../../extensibility/debugger/reference/idebugboundbreakpoint2-setcondition.md)   
 [SetCondition](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-setcondition.md)   
 [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)   
 [BP_COND_STYLE](../../../extensibility/debugger/reference/bp-cond-style.md)
