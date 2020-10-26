---
title: IDebugMessageEvent2 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugMessageEvent2
helpviewer_keywords:
- IDebugMessageEvent2 interface
ms.assetid: a9ff3d00-e9ac-4cd6-bda9-584a4815aff8
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: e7bb6b014ef8aa662abd42ab2989d47f703880a4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65685979"
---
# <a name="idebugmessageevent2"></a>IDebugMessageEvent2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このインターフェイスは、ユーザーからの応答を必要とするメッセージを Visual Studio に送信するために、デバッグエンジン (DE) によって使用されます。  
  
## <a name="syntax"></a>Syntax  
  
```  
IDebugMessageEvent2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>実装側の注意  
 DE は、ユーザーの応答を必要とするメッセージを Visual Studio に送信するために、このインターフェイスを実装します。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)インターフェイスは、このインターフェイスと同じオブジェクトに実装する必要があります。 SDM は、 [QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3) を使用してインターフェイスにアクセスし `IDebugEvent2` ます。  
  
 このインターフェイスの実装では、Visual Studio の [Setresponse](../../../extensibility/debugger/reference/idebugmessageevent2-setresponse.md) の呼び出しを DE に伝達する必要があります。 たとえば、これは、DE のメッセージ処理スレッドにポストされたメッセージを使用して実行できます。また、このインターフェイスを実装するオブジェクトは、DE への参照を保持し、に渡された応答で DE にコールバックすることもでき `IDebugMessageEvent2::SetResponse` ます。  
  
## <a name="notes-for-callers"></a>呼び出し元に関する注意事項  
 DE は、このイベントオブジェクトを作成して送信し、応答を必要とするメッセージをユーザーに表示します。 イベントは、デバッグ対象のプログラムにアタッチされているときに、SDM によって提供される [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) callback 関数を使用して送信されます。  
  
## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド  
 次の表に、のメソッドを示し `IDebugMessageEvent2` ます。  
  
|メソッド|説明|  
|------------|-----------------|  
|[GetMessage](../../../extensibility/debugger/reference/idebugmessageevent2-getmessage.md)|表示されるメッセージを取得します。|  
|[SetResponse](../../../extensibility/debugger/reference/idebugmessageevent2-setresponse.md)|メッセージボックスから応答 (存在する場合) を設定します。|  
  
## <a name="remarks"></a>注釈  
 DE は、特定のメッセージに対してユーザーからの特定の応答が必要な場合に、このインターフェイスを使用します。 たとえば、プログラムにリモートでアタッチしようとした後に "アクセスが拒否されました" というメッセージが表示されない場合、DE は、 `IDebugMessageEvent2` メッセージボックスのスタイルを持つイベントでこの特定のメッセージを Visual Studio に送信し `MB_RETRYCANCEL` ます。 これにより、ユーザーはアタッチ操作を再試行またはキャンセルできます。  
  
 DE は、Win32 関数の規則に従うことによって、このメッセージを処理する方法を指定し `MessageBox` ます (詳細については、「 [AfxMessageBox](https://msdn.microsoft.com/library/d66d0328-cdcc-48f6-96a4-badf089099c8) 」を参照してください)。  
  
 [IDebugErrorEvent2](../../../extensibility/debugger/reference/idebugerrorevent2.md)インターフェイスを使用して、ユーザーからの応答を必要としないメッセージを Visual Studio に送信します。  
  
## <a name="requirements"></a>要件  
 ヘッダー: msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)   
 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)   
 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)   
 [IDebugErrorEvent2](../../../extensibility/debugger/reference/idebugerrorevent2.md)
