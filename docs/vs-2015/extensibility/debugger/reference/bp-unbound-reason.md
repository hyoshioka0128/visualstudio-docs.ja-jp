---
title: BP_UNBOUND_REASON |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- BP_UNBOUND_REASON
helpviewer_keywords:
- BP_UNBOUND_REASON enumeration
ms.assetid: 939b6f9c-113b-471d-9f30-b03871af6285
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: ddff6130e2243d10c00cefec160d057516d60932
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68153280"
---
# <a name="bp_unbound_reason"></a>BP_UNBOUND_REASON
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

ブレークポイントがバインド解除された理由を示します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
enum enum_BP_UNBOUND_REASON {   
   BPUR_UNKNOWN           = 0x0000,  
   BPUR_CODE_UNLOADED     = 0x0002,  
   BPUR_BREAKPOINT_REBIND = 0x0003,  
   BPUR_BREAKPOINT_ERROR  = 0x0004  
};  
typedef DWORD BP_UNBOUND_REASON;  
```  
  
```csharp  
public enum enum_BP_UNBOUND_REASON {   
   BPUR_UNKNOWN           = 0x0000,  
   BPUR_CODE_UNLOADED     = 0x0002,  
   BPUR_BREAKPOINT_REBIND = 0x0003,  
   BPUR_BREAKPOINT_ERROR  = 0x0004  
};  
```  
  
## <a name="members"></a>メンバー  
 BPUR_UNKNOWN  
 理由は不明です。  
  
 BPUR_CODE_UNLOADED  
 ブレークポイントを含むコードはアンロードされました。  
  
 BPUR_BREAKPOINT_REBIND  
 ブレークポイントは別の場所に再バインドされています。 これは、ブレークポイントが移動したとき、または無効になったパスを持つファイルにブレークポイントがバインドされたときに発生する可能性があります。  
  
 BPUR_ BREAKPOINT_ERROR  
 ブレークポイントは、バインド後にエラーが発生していると判断されます。 これは、条件が有効でなくなったマネージブレークポイントに発生します。  
  
## <a name="remarks"></a>注釈  
 [Getreason](../../../extensibility/debugger/reference/idebugbreakpointunboundevent2-getreason.md)メソッドによって返されます。  
  
## <a name="requirements"></a>要件  
 ヘッダー: msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [列挙](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [GetReason](../../../extensibility/debugger/reference/idebugbreakpointunboundevent2-getreason.md)
