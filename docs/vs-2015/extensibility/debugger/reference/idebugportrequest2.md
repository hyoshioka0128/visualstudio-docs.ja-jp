---
title: IDebugPortRequest2 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugPortRequest2
helpviewer_keywords:
- IDebugPortRequest2 interface
ms.assetid: 556e610d-7c4b-44a8-965a-76a9d02b601a
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: fa72ae9d2cfbe399c3507406875e9c692d18b678
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68188335"
---
# <a name="idebugportrequest2"></a>IDebugPortRequest2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このインターフェイスは、ポートを表します。 この説明は、ポートをポート供給業者に追加するために使用されます。  
  
## <a name="syntax"></a>Syntax  
  
```  
IDebugPortRequest2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>実装側の注意  
 通常、Visual Studio は、ポートサプライヤーからデバッグポートを取得するプロセスで、このインターフェイスを実装します。  
  
## <a name="notes-for-callers"></a>呼び出し元に関する注意事項  
 このインターフェイスは、デバッグポートを作成するために [Addport](../../../extensibility/debugger/reference/idebugportsupplier2-addport.md) に渡されます。 [Getportrequest](../../../extensibility/debugger/reference/idebugport2-getportrequest.md)を呼び出すと、このインターフェイスが返されます。このインターフェイスは、ポートの作成に使用された要求を表します。  
  
## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド  
 次の表に、のメソッドを示し `IDebugPortRequest2` ます。  
  
|メソッド|説明|  
|------------|-----------------|  
|[GetPortName](../../../extensibility/debugger/reference/idebugportrequest2-getportname.md)|作成するポートの名前を取得します。|  
  
## <a name="remarks"></a>注釈  
 通常、デバッグエンジンは、ポート供給元とは通信せず、このインターフェイスを使用しません。  
  
## <a name="requirements"></a>要件  
 ヘッダー: msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)   
 [AddPort](../../../extensibility/debugger/reference/idebugportsupplier2-addport.md)   
 [GetPortRequest](../../../extensibility/debugger/reference/idebugport2-getportrequest.md)
