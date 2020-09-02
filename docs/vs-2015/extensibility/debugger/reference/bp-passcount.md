---
title: BP_PASSCOUNT |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- BP_PASSCOUNT
helpviewer_keywords:
- BP_PASSCOUNT structure
ms.assetid: 791ac175-b897-4c70-873e-240da7e0ac89
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: b99cbd777755a9a48869299b5cea523ecacbb4a4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68153375"
---
# <a name="bp_passcount"></a>BP_PASSCOUNT
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

条件付きブレークポイントが発生する回数と条件について説明します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
typedef struct _BP_PASSCOUNT {   
   DWORD              dwPassCount;  
   BP_PASSCOUNT_STYLE stylePassCount;  
} BP_PASSCOUNT;  
```  
  
```csharp  
public struct BP_PASSCOUNT {   
   public uint dwPassCount;  
   public uint stylePassCount;  
};  
```  
  
## <a name="members"></a>メンバー  
 `dwPassCount`  
 ブレークポイントを実行する前に、そのブレークポイントを通過する回数。  
  
 `stylePassCount`  
 ブレークポイントのパスカウントのスタイルを指定する [BP_PASSCOUNT_STYLE](../../../extensibility/debugger/reference/bp-passcount-style.md) 列挙の値です。  
  
## <a name="remarks"></a>注釈  
 この構造体は、 [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md) 構造体のメンバーです。  
  
 この構造体は、パラメーターとして[Setpass count](../../../extensibility/debugger/reference/idebugboundbreakpoint2-setpasscount.md) および[setpass count](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-setpasscount.md) メソッドにも渡されます。  
  
## <a name="requirements"></a>要件  
 ヘッダー: msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)   
 [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)   
 [Setpass Count](../../../extensibility/debugger/reference/idebugboundbreakpoint2-setpasscount.md)   
 [Setpass Count](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-setpasscount.md)   
 [BP_PASSCOUNT_STYLE](../../../extensibility/debugger/reference/bp-passcount-style.md)
