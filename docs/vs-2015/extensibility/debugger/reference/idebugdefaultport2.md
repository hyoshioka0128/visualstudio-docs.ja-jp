---
title: IDebugDefaultPort2 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugDefaultPort2
helpviewer_keywords:
- IDebugDefaultPort2 interface
ms.assetid: 7b3452af-9a96-4c4c-9946-4339b72d3d7b
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: ca0b6b7e9753b346b8a995ffd8ddcb6cc53fe7c0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65697512"
---
# <a name="idebugdefaultport2"></a>IDebugDefaultPort2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このインターフェイスには、ポートのサーバーと通知機能にアクセスするためのメソッドがいくつか用意されています。  
  
## <a name="syntax"></a>構文  
  
```  
IDebugDefaultPort2 : IDebugPort2  
```  
  
## <a name="notes-for-implementers"></a>実装側の注意  
 Visual Studio は、プログラムにアクセスするためのデバッグポートを表すために、このインターフェイスを実装します。 カスタムポート供給業者は、リモートデバッグを処理する場合にこのインターフェイスを実装することもできます。  
  
## <a name="notes-for-callers"></a>呼び出し元に関する注意事項  
 [IDebugProgramProvider2](../../../extensibility/debugger/reference/idebugprogramprovider2.md)インターフェイスのメソッドの引数によって、このインターフェイスが提供されます。 [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)インターフェイスで[QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3)を呼び出すと、このインターフェイスを取得することもできます。  
  
## <a name="methods-in-vtable-order"></a>Vtable の順序でのメソッド  
 このインターフェイスは、 [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)で定義されているメソッドに加えて、次のメソッドを実装します。  
  
|Method|説明|  
|------------|-----------------|  
|[GetPortNotify](../../../extensibility/debugger/reference/idebugdefaultport2-getportnotify.md)|このポートからポート通知インターフェイスを取得します。|  
|[GetServer](../../../extensibility/debugger/reference/idebugdefaultport2-getserver.md)|このポートをホストしているサーバーへのインターフェイスを取得します。|  
|[QueryIsLocal](../../../extensibility/debugger/reference/idebugdefaultport2-queryislocal.md)|このポートがローカルコンピューター上で実行されているかどうかを判断します。|  
  
## <a name="remarks"></a>解説  
 名前 " `IDebugDefaultPort2` " は、既定のポートを表すものではないため、名称の1つです。 "IDebugPort3" という名前を指定することもできます。  
  
## <a name="requirements"></a>必要条件  
 ヘッダー: msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)   
 [IDebugProgramProvider2](../../../extensibility/debugger/reference/idebugprogramprovider2.md)
