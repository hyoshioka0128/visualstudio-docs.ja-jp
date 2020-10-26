---
title: IDebugPropertyDestroyEvent2 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugPropertyDestroyEvent2
helpviewer_keywords:
- IDebugPropertyDestroyEvent2 interface
ms.assetid: 301b7a75-ecfa-46f1-9131-66cf3e4be147
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 034040ecd8df3368f53cb7a3bf99197e962e2b56
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65702301"
---
# <a name="idebugpropertydestroyevent2"></a>IDebugPropertyDestroyEvent2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このインターフェイスは、特定のドキュメントに関連付けられているプロパティが破棄されるときに、デバッグエンジン (DE) によってセッションデバッグマネージャー (SDM) に送信されます。  
  
## <a name="syntax"></a>構文  
  
```  
IDebugPropertyDestroyEvent2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>実装側の注意  
 DE は、プロパティが破棄されたことを報告するために、このインターフェイスを実装します。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)インターフェイスは、このインターフェイスと同じオブジェクトに実装する必要があります。 SDM は、 [QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3) を使用してインターフェイスにアクセスし `IDebugEvent2` ます。 このインターフェイスは、スクリプトに関連付けられたプロパティを DE が以前に作成した場合に実装されます。プロパティを破棄すると、関連付けられているスクリプトが IDE から削除されます。  
  
## <a name="notes-for-callers"></a>呼び出し元に関する注意事項  
 DE は、このイベントオブジェクトを作成し、プロパティを報告するために送信します。 イベントは、デバッグ対象のプログラムにアタッチされているときに、SDM によって提供される [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) callback 関数を使用して送信されます。  
  
## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド  
 次の表は、のメソッドを示して `IDebugPropertyDestroyEvent2` います。  
  
|Method|説明|  
|------------|-----------------|  
|[GetDebugProperty](../../../extensibility/debugger/reference/idebugpropertydestroyevent2-getdebugproperty.md)|破棄されるプロパティを取得します。|  
  
## <a name="remarks"></a>解説  
 これらのイベントが使用される理由の詳細については、 [IDebugPropertyCreateEvent2](../../../extensibility/debugger/reference/idebugpropertycreateevent2.md) の解説を参照してください。  
  
## <a name="requirements"></a>必要条件  
 ヘッダー: msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)   
 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)   
 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)   
 [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)   
 [IDebugPropertyCreateEvent2](../../../extensibility/debugger/reference/idebugpropertycreateevent2.md)
