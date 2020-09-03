---
title: 'IDebugBoundBreakpoint2:: GetHitCount |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugBoundBreakpoint2::GetHitCount
helpviewer_keywords:
- GetHitCount method
- IDebugBoundBreakpoint2::GetHitCount method
ms.assetid: 23481f37-047c-41d2-8286-4da1f4084961
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: e373c19e3213e1e39ca610839478cad613ad4454
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68156245"
---
# <a name="idebugboundbreakpoint2gethitcount"></a>IDebugBoundBreakpoint2::GetHitCount
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このバインドされたブレークポイントの現在のヒットカウントを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT GetHitCount(   
   DWORD* pdwHitCount  
);  
```  
  
```csharp  
int GetHitCount(   
   out uint pdwHitCount  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pdwHitCount`  
 入出力ヒットカウントを返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。 `E_BP_DELETED`バインドされたブレークポイントオブジェクトの状態が `BPS_DELETED` ( [BP_STATE](../../../extensibility/debugger/reference/bp-state.md)列挙体の一部) に設定されている場合は、を返します。  
  
## <a name="remarks"></a>注釈  
 ヒットカウントは、現在のセッションの実行中にこのブレークポイントが発生した回数です。  
  
## <a name="see-also"></a>参照  
 [IDebugBoundBreakpoint2](../../../extensibility/debugger/reference/idebugboundbreakpoint2.md)   
 [BP_STATE](../../../extensibility/debugger/reference/bp-state.md)
