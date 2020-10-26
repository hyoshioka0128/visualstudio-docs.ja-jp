---
title: IDebugPortEvents2 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugPortEvents2
helpviewer_keywords:
- IDebugPortEvents2 interface
ms.assetid: 2c017094-3ba2-4067-83f9-147df1d96bce
caps.latest.revision: 19
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 5e0f6455e6df8db88b1aae1a7b7f6965c0ee524b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68188532"
---
# <a name="idebugportevents2"></a>IDebugPortEvents2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このインターフェイスは、特定のポートでのプロセスとプログラムの作成と破棄をリスナーに通知します (通常、セッションデバッグマネージャー (SDM) またはデバッグエンジン)。 この情報は、ポートで実行されているプロセスとプログラムのリアルタイムビューを表示するために使用できます。  
  
## <a name="syntax"></a>Syntax  
  
```  
IDebugPortEvents2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>実装側の注意  
 通常、Visual Studio は、プログラムの作成と破棄に関する通知を受信するために、このインターフェイスを実装します。 デバッグエンジンは、このインターフェイスを実装して、このようなポートイベントをリッスンすることもできます。  
  
## <a name="notes-for-callers"></a>呼び出し元に関する注意事項  
 インターフェイスに対して、すべての [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md) インターフェイスのクエリを実行でき <xref:System.Runtime.InteropServices.ComTypes.IConnectionPointContainer> ます。 次に、インターフェイスを <xref:System.Runtime.InteropServices.ComTypes.IConnectionPointContainer.FindConnectionPoint%2A> 取得するために、のメソッド `IDebugPortEvents2` がインターフェイスで呼び出され <xref:System.Runtime.InteropServices.ComTypes.IConnectionPointContainer> <xref:System.Runtime.InteropServices.ComTypes.IConnectionPoint> ます。 最後に、 <xref:System.Runtime.InteropServices.ComTypes.IConnectionPoint.Advise%2A> <xref:System.Runtime.InteropServices.ComTypes.IConnectionPoint> [イベント](../../../extensibility/debugger/reference/idebugportevents2-event.md) メソッドを介してイベントを送信するために、インターフェイスのメソッドが呼び出されます。  
  
## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド  
 次の表は、のメソッドを示して `IDebugPortEvents2` います。  
  
|メソッド|説明|  
|------------|-----------------|  
|[Event](../../../extensibility/debugger/reference/idebugportevents2-event.md)|ポートでのプロセスとプログラムの作成と破棄を説明するイベントを送信します。|  
  
## <a name="remarks"></a>注釈  
 `IDebugPortEvents2` は、既にデバッグされているプロセスで実行されるプログラムをデバッグするために SDM によっても使用されます。  
  
 ポートイベントは、このインターフェイスによって SDM に渡されます。  
  
## <a name="requirements"></a>要件  
 ヘッダー: msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)   
 [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)
