---
title: IDebugBreakpointRequest2 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugBreakpointRequest2
helpviewer_keywords:
- IDebugBreakpointRequest2 interface
ms.assetid: 01ac4013-96f9-4235-b289-f55f9e99558f
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 263b947fff45eafd2d2e5afc029572b69ea24b82
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68158779"
---
# <a name="idebugbreakpointrequest2"></a>IDebugBreakpointRequest2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このインターフェイスは、任意の種類のブレークポイントを作成およびバインドするために必要な情報を表します。  
  
## <a name="syntax"></a>Syntax  
  
```  
IDebugBreakpointRequest2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>実装側の注意  
 通常、セッションデバッグマネージャー (SDM) は、このインターフェイスを実装します。  
  
## <a name="notes-for-callers"></a>呼び出し元に関する注意事項  
 デバッグエンジン (DE) は、保留中のブレークポイントを作成するために、 [Creatependingbreakpoint ポイント](../../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md) の呼び出しによってこのインターフェイスを受信します。 [Getbreakpointrequest](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-getbreakpointrequest.md)を呼び出すと、このインターフェイスを DE から取得できます。  
  
## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド  
 次の表に、のメソッドを示し `IDebugBreakpointRequest2` ます。  
  
|メソッド|説明|  
|------------|-----------------|  
|[GetLocationType](../../../extensibility/debugger/reference/idebugbreakpointrequest2-getlocationtype.md)|このブレークポイント要求のブレークポイントの位置の種類を取得します。|  
|[GetRequestInfo](../../../extensibility/debugger/reference/idebugbreakpointrequest2-getrequestinfo.md)|このブレークポイント要求を説明するブレークポイント要求情報を取得します。|  
  
## <a name="remarks"></a>注釈  
 デバッグ中のプログラムが読み込まれると、 [バインド](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md) を呼び出すと、保留中のブレークポイントがプログラム内の要求された場所にバインドされます。  
  
## <a name="requirements"></a>要件  
 ヘッダー: msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [CreatePendingBreakpoint ポイント](../../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md)   
 [GetBreakpointRequest](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-getbreakpointrequest.md)   
 [束縛](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)
