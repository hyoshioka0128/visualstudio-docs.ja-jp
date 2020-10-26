---
title: IDebugBreakpointErrorEvent2 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugBreakpointErrorEvent2
helpviewer_keywords:
- IDebugBreakpointErrorEvent2
ms.assetid: adee79df-8db5-4510-a7df-c50f4dbf5e35
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 22ad0a7e1b14b036239d7b6a5931badb5787b752
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65684816"
---
# <a name="idebugbreakpointerrorevent2"></a>IDebugBreakpointErrorEvent2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このインターフェイスは、警告またはエラーのために、読み込まれたプログラムに保留中のブレークポイントをバインドできなかったことをセッションデバッグマネージャー (SDM) に通知します。  
  
## <a name="syntax"></a>Syntax  
  
```  
IDebugBreakpointErrorEvent2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>実装側の注意  
 DE は、ブレークポイントのサポートの一部として、このインターフェイスを実装します。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)インターフェイスは、このインターフェイスと同じオブジェクトに実装する必要があります (SDM は[QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3)を使用してインターフェイスにアクセスし `IDebugEvent2` ます)。  
  
## <a name="notes-for-callers"></a>呼び出し元に関する注意事項  
 DE は、デバッグ中のプログラムに保留中のブレークポイントをバインドできない場合に、このイベントオブジェクトを作成して送信します。 イベントは、デバッグ対象のプログラムにアタッチされるときに、SDM によって提供される [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) callback 関数を使用して送信されます。  
  
## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド  
 次の表に、のメソッドを示し `IDebugBreakpointErrorEvent2` ます。  
  
|メソッド|説明|  
|------------|-----------------|  
|[GetErrorBreakpoint](../../../extensibility/debugger/reference/idebugbreakpointerrorevent2-geterrorbreakpoint.md)|警告またはエラーを説明する [IDebugErrorBreakpoint2](../../../extensibility/debugger/reference/idebugerrorbreakpoint2.md) インターフェイスを取得します。|  
  
## <a name="remarks"></a>注釈  
 ブレークポイントがバインドされるたびに、イベントが SDM に送信されます。 ブレークポイントをバインドできない場合は、が送信されます。 `IDebugBreakpointErrorEvent2` それ以外の場合は、 [IDebugBreakpointBoundEvent2](../../../extensibility/debugger/reference/idebugbreakpointboundevent2.md) が送信されます。  
  
 たとえば、保留中のブレークポイントに関連付けられている条件が解析または評価に失敗した場合、この時点では、保留中のブレークポイントをバインドできないという警告が送信されます。 これは、ブレークポイントのコードがまだ読み込まれていない場合に発生する可能性があります。  
  
## <a name="requirements"></a>要件  
 ヘッダー: msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)   
 [IDebugErrorBreakpoint2](../../../extensibility/debugger/reference/idebugerrorbreakpoint2.md)   
 [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)   
 [IDebugBreakpointBoundEvent2](../../../extensibility/debugger/reference/idebugbreakpointboundevent2.md)   
 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
