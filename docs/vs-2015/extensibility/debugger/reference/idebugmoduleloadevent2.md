---
title: IDebugModuleLoadEvent2 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugModuleLoadEvent2
helpviewer_keywords:
- IDebugModuleLoadEvent2 interface
ms.assetid: 7d26fb23-5d49-4ba7-b7c5-3aed4d7be81e
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2c6fa8712fb2ead56b78134758a954cb1d9ac68f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65680919"
---
# <a name="idebugmoduleloadevent2"></a>IDebugModuleLoadEvent2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このインターフェイスは、モジュールが読み込まれたとき、またはアンロードされたときに、デバッグエンジン (DE) によってセッションデバッグマネージャー (SDM) に送信されます。  
  
## <a name="syntax"></a>構文  
  
```  
IDebugModuleLoadEvent2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>実装側の注意  
 DE は、モジュールが読み込まれたかアンロードされたことを報告するために、このインターフェイスを実装します。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)インターフェイスは、このインターフェイスと同じオブジェクトに実装する必要があります。 SDM は、 [QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3) を使用してインターフェイスにアクセスし `IDebugEvent2` ます。  
  
## <a name="notes-for-callers"></a>呼び出し元に関する注意事項  
 DE は、モジュールが読み込まれたかアンロードされたことを報告するために、このイベントオブジェクトを作成して送信します。 イベントは、デバッグ対象のプログラムにアタッチされているときに、SDM によって提供される [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) callback 関数を使用して送信されます。  
  
## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド  
 次の表は、のメソッドを示して `IDebugModuleLoadEvent2` います。  
  
|Method|説明|  
|------------|-----------------|  
|[GetModule](../../../extensibility/debugger/reference/idebugmoduleloadevent2-getmodule.md)|読み込まれている、またはアンロードされているモジュールを取得します。|  
  
## <a name="remarks"></a>解説  
 Visual Studio では、 **モジュール** ウィンドウを最新の状態に保つために、このイベントを使用します。  
  
## <a name="requirements"></a>必要条件  
 ヘッダー: msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)   
 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)   
 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
