---
title: BP_RES_DATA_FLAGS |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- BP_RES_DATA_FLAGS
helpviewer_keywords:
- BP_RES_DATA_FLAGS enumeration
ms.assetid: d97611e2-def6-45a9-ad7d-eedf2ad4c82b
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 68d1c0705ae7d27bf281f5d65e9385228cd36bc4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68153340"
---
# <a name="bp_res_data_flags"></a>BP_RES_DATA_FLAGS
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

データブレークポイントをエミュレートするか、ハードウェアで実装するかを指定します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
enum enum_BP_RES_DATA_FLAGS {   
   BP_RES_DATA_EMULATED = 0x0001  
};  
typedef DWORD BP_RES_DATA_FLAGS;  
```  
  
```csharp  
public enum enum_BP_RES_DATA_FLAGS {   
   BP_RES_DATA_EMULATED = 0x0001  
};  
```  
  
## <a name="members"></a>メンバー  
 BP_RES_DATA_EMULATED  
 データブレークポイントをエミュレートすることを指定します。  
  
## <a name="remarks"></a>注釈  
 `dwFlags` [BP_RESOLUTION_DATA](../../../extensibility/debugger/reference/bp-resolution-data.md)構造体のメンバーに使用されます。  
  
## <a name="requirements"></a>要件  
 ヘッダー: msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [列挙](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [BP_RESOLUTION_DATA](../../../extensibility/debugger/reference/bp-resolution-data.md)
