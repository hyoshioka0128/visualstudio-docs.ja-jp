---
title: IDebugAddress2 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugAddress2
helpviewer_keywords:
- IDebugAddress2 interface
ms.assetid: b150e0ed-4ac0-4f8c-9732-4b3e54b9d243
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: ca14e6236fc7e12ea259b97f7f2ddb69fe052f55
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65692837"
---
# <a name="idebugaddress2"></a>IDebugAddress2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このインターフェイスは、アドレスがこのインターフェイスによって表されるオブジェクトを所有するプロセスの ID へのアクセスを提供します。  
  
## <a name="syntax"></a>構文  
  
```  
IDebugAddress2 : IDebugAddress  
```  
  
## <a name="notes-for-implementers"></a>実装側の注意  
 シンボルプロバイダーは、 [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) インターフェイスを実装する同じオブジェクトにこのインターフェイスを実装します。 このインターフェイスは、このアドレスに関連するオブジェクトを所有するプロセスの ID へのアクセスを提供します。  
  
## <a name="notes-for-callers"></a>呼び出し元に関する注意事項  
 [QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3)を使用して、 [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)インターフェイスからこのインターフェイスを取得します。  
  
## <a name="methods-in-vtable-order"></a>Vtable の順序でのメソッド  
 このインターフェイスは、 [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) インターフェイスから継承されたメソッドに加えて、次のメソッドを実装します。  
  
|Method|説明|  
|------------|-----------------|  
|[GetProcessID](../../../extensibility/debugger/reference/idebugaddress2-getprocessid.md)|このインターフェイスによって表されるオブジェクトを所有するプロセスの ID を取得します。|  
  
## <a name="requirements"></a>必要条件  
 ヘッダー: sh. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [シンボルプロバイダーインターフェイス](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)   
 [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)
