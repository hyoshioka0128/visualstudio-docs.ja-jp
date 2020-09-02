---
title: IDebugCoreServer2 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugCoreServer2
helpviewer_keywords:
- IDebugCoreServer2 interface
ms.assetid: 9c47d0a6-9eb1-464e-bd44-fa2b552d4d36
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: c0bca6ccd3738518df339084b0f6463be181e52d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68192912"
---
# <a name="idebugcoreserver2"></a>IDebugCoreServer2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このインターフェイスは、ネットワーク上のコンピューター上のサーバーから情報を表示して取得するために使用されます。  
  
## <a name="syntax"></a>Syntax  
  
```  
IDebugCoreServer2 : IUknown  
```  
  
## <a name="notes-for-implementers"></a>実装側の注意  
 このインターフェイスは、サーバーを表すために Visual Studio によって実装されます。 Visual Studio の各インスタンスは、このインターフェイスのインスタンスを作成します。  
  
## <a name="notes-for-callers"></a>呼び出し元に関する注意事項  
 カスタムポート供給業者は、 [イベント](../../../extensibility/debugger/reference/idebugportevents2-event.md)の呼び出しでこのインターフェイスを受け取ります。  
  
 デバッグエンジンは、 [Getserver](../../../extensibility/debugger/reference/idebugdefaultport2-getserver.md) (から派生したインターフェイスである [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)を返す) を呼び出すことによって、このインターフェイスを間接的に取得でき `IDebugCoreServer2` ます。  
  
## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド  
 次の表に、のメソッドを示し `IDebugCoreServer2` ます。  
  
|メソッド|説明|  
|------------|-----------------|  
|[GetMachineInfo](../../../extensibility/debugger/reference/idebugcoreserver2-getmachineinfo.md)|コンピューターの名前と属性を取得します。|  
|[GetMachineName](../../../extensibility/debugger/reference/idebugcoreserver2-getmachinename.md)|コンピューターの名前を取得します。|  
|[GetPortSupplier](../../../extensibility/debugger/reference/idebugcoreserver2-getportsupplier.md)|コンピューター上に存在するポート供給元を取得します。|  
|[GetPort](../../../extensibility/debugger/reference/idebugcoreserver2-getport.md)|コンピューターに既に存在するポートを取得します。|  
|[EnumPorts](../../../extensibility/debugger/reference/idebugcoreserver2-enumports.md)|コンピューター上のすべてのポートの列挙子を作成します。|  
|[EnumPortSuppliers](../../../extensibility/debugger/reference/idebugcoreserver2-enumportsuppliers.md)|コンピューター上のすべてのポートサプライヤーの列挙子を作成します。|  
|[GetMachineUtilities_V7](../../../extensibility/debugger/reference/idebugcoreserver2-getmachineutilities-v7.md)|コンピューターのマシンユーティリティを取得します。|  
  
## <a name="remarks"></a>注釈  
 このインターフェイスは、ネットワーク上のコンピューター上で実行されているプロセスを参照するために Visual Studio によっても使用されます。  
  
## <a name="requirements"></a>要件  
 ヘッダー: msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)   
 [場合](../../../extensibility/debugger/reference/idebugportevents2-event.md)   
 [GetServer](../../../extensibility/debugger/reference/idebugdefaultport2-getserver.md)   
 [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)
