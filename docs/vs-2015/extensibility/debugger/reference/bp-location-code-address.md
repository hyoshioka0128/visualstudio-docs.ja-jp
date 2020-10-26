---
title: BP_LOCATION_CODE_ADDRESS |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- BP_LOCATION_CODE_ADDRESS
helpviewer_keywords:
- BP_LOCATION_CODE_ADDRESS structure
ms.assetid: 83c9da8b-19d9-4be5-b225-854543654901
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: b23073c41f5da7d1563a6be46e0d114334527b35
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68153505"
---
# <a name="bp_location_code_address"></a>BP_LOCATION_CODE_ADDRESS
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

コード内のアドレスのブレークポイントの位置を記述します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
typedef struct _BP_LOCATION_CODE_ADDRESS {   
   BSTR bstrContext;  
   BSTR bstrModuleUrl;  
   BSTR bstrFunction;  
   BSTR bstrAddress;  
} BP_LOCATION_CODE_ADDRESS;  
```  
  
## <a name="members"></a>メンバー  
 `bstrContext`  
 ブレークポイントのコンテキスト。通常は、呼び出し履歴に表示されるメソッドまたは関数の名前です。  
  
 `bstrModuleUrl`  
 ブレークポイントを含むモジュールの URL です。  
  
 `bstrFunction`  
 ブレークポイントを含む関数の名前。  
  
 `bstrAddress`  
 [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)オブジェクトにバインドするために式エバリュエーターによって解析される、ブレークポイントのアドレス。  
  
## <a name="remarks"></a>注釈  
 この構造体は、共用体の一部として [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md) 構造体のメンバーになります。  
  
## <a name="requirements"></a>要件  
 ヘッダー: msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)   
 [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)   
 [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)
