---
title: IDebugBreakpointRequest3 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugBreakpointRequest3
helpviewer_keywords:
- IDebugBreakpointRequest3
ms.assetid: 8a042beb-b319-48e3-b3c8-9c8336ab371b
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 50ea30c736a4606a7745e52057f2ca8f9afd2c5f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65673761"
---
# <a name="idebugbreakpointrequest3"></a>IDebugBreakpointRequest3
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このインターフェイスは、任意の種類のブレークポイントを作成およびバインドするために必要な情報を表します。 [IDebugBreakpointRequest2](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md)の拡張機能です。  
  
## <a name="syntax"></a>構文  
  
```  
IDebugBreakpointRequest3 : IDebugBreakpointRequest2  
```  
  
## <a name="notes-for-implementers"></a>実装側の注意  
 通常、セッションデバッグマネージャー (SDM) は、このインターフェイスを実装します。  
  
## <a name="notes-for-callers"></a>呼び出し元に関する注意事項  
 デバッグエンジン (DE) は、 [Creatependingbreakpoint ポイント](../../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md)への呼び出しで受信した IDebugBreakpointRequest2 インターフェイスで[QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3)を呼び出すことによって、このインターフェイスにアクセスします。  
  
## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド  
 [IDebugBreakpointRequest2](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md)から継承されたメソッドに加えて、 `IDebugBreakpointRequest3` インターフェイスは次のメソッドを公開します。  
  
|Method|説明|  
|------------|-----------------|  
|[GetRequestInfo2](../../../extensibility/debugger/reference/idebugbreakpointrequest3-getrequestinfo2.md)|このブレークポイント要求を説明するブレークポイント要求情報を取得します。|  
  
## <a name="remarks"></a>解説  
 このインターフェイスは、 [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md) 構造体に追加情報を提供するために使用されます。 この追加情報には、DE のベンダー ID (GUID の形式)、トレースポイントの名前、およびブレークポイント制約の名前が含まれます。  
  
## <a name="requirements"></a>必要条件  
 ヘッダー: msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [IDebugBreakpointRequest2](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md)   
 [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)
