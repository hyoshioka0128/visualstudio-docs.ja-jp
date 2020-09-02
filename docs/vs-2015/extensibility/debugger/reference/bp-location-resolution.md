---
title: BP_LOCATION_RESOLUTION |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- BP_LOCATION_RESOLUTION
helpviewer_keywords:
- BP_LOCATION_RESOLUTION structure
ms.assetid: 86ea2c8a-54a3-48e8-83c7-18a515273129
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: d24ae48df790e452145e5aa8c67998d55760bb24
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68153418"
---
# <a name="bp_location_resolution"></a>BP_LOCATION_RESOLUTION
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

特定の位置にあるブレークポイントの解決方法について説明します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
typedef struct _BP_LOCATION_RESOLUTION {   
   IDebugBreakpointResolution2* pResolution;  
} BP_LOCATION_RESOLUTION;  
```  
  
## <a name="members"></a>メンバー  
 pResolution  
 ブレークポイントの種類とその解決情報を決定する [IDebugBreakpointResolution2](../../../extensibility/debugger/reference/idebugbreakpointresolution2.md) オブジェクト。  
  
## <a name="remarks"></a>注釈  
 この構造体は、共用体の一部として [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md) 構造体のメンバーになります。  
  
## <a name="requirements"></a>要件  
 ヘッダー: msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)   
 [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)   
 [IDebugBreakpointResolution2](../../../extensibility/debugger/reference/idebugbreakpointresolution2.md)
