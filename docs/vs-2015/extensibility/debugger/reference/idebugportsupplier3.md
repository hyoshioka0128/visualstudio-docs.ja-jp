---
title: IDebugPortSupplier3 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugPortSupplier3
helpviewer_keywords:
- IDebugPortSupplier3 interface
ms.assetid: e458cd02-2370-4435-8953-17d7a60ce152
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: e4ece720cf6880bba528dee99cdbdeb25c10087a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65674127"
---
# <a name="idebugportsupplier3"></a>IDebugPortSupplier3
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このインターフェイスを使用すると、呼び出し元は、ポートの供給者がデバッガーの呼び出しの間にポートを (ディスクに書き込むことによって) 保持できるかどうかを判断し、保存されたポートの一覧を取得できます。  
  
## <a name="syntax"></a>構文  
  
```  
IDebugPortSupplier3 : IDebugPortSupplier2  
```  
  
## <a name="notes-for-implementers"></a>実装側の注意  
 カスタムポート供給業者は、このインターフェイスを実装して、ディスクへのポート情報の永続化または保存をサポートします。 このインターフェイスは、 [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md) インターフェイスと同じオブジェクトに実装する必要があります。  
  
## <a name="notes-for-callers"></a>呼び出し元に関する注意事項  
 このインターフェイスを取得するには、インターフェイスで [QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3) を呼び出し `IDebugPortSupplier2` ます。  
  
## <a name="methods-in-vtable-order"></a>Vtable の順序でのメソッド  
 このインターフェイスは、 [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md) インターフェイスから継承されたメソッドに加えて、次の機能をサポートしています。  
  
|Method|説明|  
|------------|-----------------|  
|[CanPersistPorts](../../../extensibility/debugger/reference/idebugportsupplier3-canpersistports.md)|ポートサプライヤーがデバッガーの呼び出し間でポートを (ディスクに書き込むことによって) 永続化できるかどうかを示す値を返します。|  
|[EnumPersistedPorts](../../../extensibility/debugger/reference/idebugportsupplier3-enumpersistedports.md)|このポートサプライヤーによってディスクに書き込まれたすべてのポートを列挙するために使用できるオブジェクトを返します。|  
  
## <a name="remarks"></a>解説  
 ポートサプライヤーが呼び出しの間にポートを永続化できる場合は、このインターフェイスを実装する必要があります。 ポートサプライヤーがインスタンス化され、ポート供給元が破壊されたときにディスクに書き込まれる場合は、ポートを読み込む必要があります。  
  
 通常、デバッグエンジンは、ポート供給元とは通信せず、このインターフェイスを使用しません。  
  
## <a name="requirements"></a>必要条件  
 ヘッダー: msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)   
 [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md)
