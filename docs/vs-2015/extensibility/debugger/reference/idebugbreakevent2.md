---
title: IDebugBreakEvent2 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugBreakEvent2
helpviewer_keywords:
- IDebugBreakEvent2 interface
ms.assetid: 57dfdbc2-4e68-4dbf-9579-006cd6fb1c62
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 98e8c1b1669b3fdd1f442c6987e4e9d2b9fc4835
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65675377"
---
# <a name="idebugbreakevent2"></a>IDebugBreakEvent2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このインターフェイスは、非同期中断が正常に完了したことをセッションデバッグマネージャー (SDM) に通知します。  
  
## <a name="syntax"></a>構文  
  
```  
IDebugBreakEvent2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>実装側の注意  
 DE は、プログラムでのユーザーの中断をサポートするために、このインターフェイスを実装します。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)インターフェイスは、このインターフェイスと同じオブジェクトに実装する必要があります (SDM は[QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3)を使用してインターフェイスにアクセスし `IDebugEvent2` ます)。  
  
## <a name="notes-for-callers"></a>呼び出し元に関する注意事項  
 ユーザーがデバッグ中のプログラムの一時停止を要求した場合、SDM は [Causebreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md) を呼び出します。 プログラムが正常に一時停止されると、DE がイベントを送信し `IDebugBreakEvent2` ます。 このイベントは、デバッグ対象のプログラムにアタッチされるときに、SDM によって提供される [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) callback 関数を使用して送信されます。  
  
## <a name="remarks"></a>解説  
 たとえば、ユーザーは、[**デバッグ**] メニューの [**すべて中断**] を選択して、無限ループを実行しているプログラムを中断できます。 SDM は、 [Causebreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md)を呼び出すことにより、プログラムを停止するように指示します。 `IDebugBreakEvent2`プログラムが最後に停止したときに、DE によって送信されます。  
  
## <a name="requirements"></a>必要条件  
 ヘッダー: msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [CauseBreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md)   
 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)   
 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
