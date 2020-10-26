---
title: IEnumDebugAddresses |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IEnumDebugAddresses
helpviewer_keywords:
- IEnumDebugAddresses interface
ms.assetid: 5f6f6751-e6d8-4c5a-8e81-414b6e5d8cc5
caps.latest.revision: 7
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2373a26da1f6c3b327bea3a6f2402beb7d8bce45
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68196140"
---
# <a name="ienumdebugaddresses"></a>IEnumDebugAddresses
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このインターフェイスは、 [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) インターフェイスを実装するオブジェクトのコレクションを表します。  
  
## <a name="syntax"></a>Syntax  
  
```  
IEnumDebugAdresses : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>実装側の注意  
 このインターフェイスは、 [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) インターフェイスを実装するオブジェクトのセットを提供するために、シンボルプロバイダーによって実装されます。 これは、 [GetCount](../../../extensibility/debugger/reference/ienumdebugaddresses-getcount.md) メソッドが存在するため、標準の COM 列挙ではないことに注意してください。  
  
## <a name="notes-for-callers"></a>呼び出し元に関する注意事項  
 このインターフェイスは、 [Getアドレス Fromcontext](../../../extensibility/debugger/reference/idebugsymbolprovider-getaddressesfromcontext.md) と [Getアドレス fromposition](../../../extensibility/debugger/reference/idebugsymbolprovider-getaddressesfromposition.md)によって返されます。  
  
## <a name="methods-in-vtable-order"></a>Vtable の順序でのメソッド  
 このインターフェイスは、次のメソッドを実装します。  
  
|メソッド|説明|  
|------------|-----------------|  
|[次へ](../../../extensibility/debugger/reference/ienumdebugaddresses-next.md)|列挙体から次の [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) オブジェクトのセットを取得します。|  
|[Skip](../../../extensibility/debugger/reference/ienumdebugaddresses-skip.md)|指定された数のエントリをスキップします。|  
|[リセット](../../../extensibility/debugger/reference/ienumdebugaddresses-reset.md)|列挙体を最初のエントリにリセットします。|  
|[複製](../../../extensibility/debugger/reference/ienumdebugaddresses-clone.md)|現在の列挙体のコピーを取得します。|  
|[GetCount](../../../extensibility/debugger/reference/ienumdebugaddresses-getcount.md)|列挙体のエントリ数を取得します。|  
  
## <a name="remarks"></a>注釈  
 このインターフェイスは、通常、式エバリュエーターに渡す適切なアドレスを決定するために、デバッグエンジンによって使用されます。  
  
## <a name="requirements"></a>要件  
 ヘッダー: sh. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [シンボルプロバイダーインターフェイス](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)   
 [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)   
 [Getアドレス Fromcontext](../../../extensibility/debugger/reference/idebugsymbolprovider-getaddressesfromcontext.md)   
 [GetAddressesFromPosition](../../../extensibility/debugger/reference/idebugsymbolprovider-getaddressesfromposition.md)
