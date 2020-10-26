---
title: IDebugProviderProgramNode2 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProviderProgramNode2
helpviewer_keywords:
- IDebugProviderProgramNode2
ms.assetid: f0bca1cc-afbe-44cf-b5aa-d078aa685d24
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a81668d5c45dd4b3363821972914e3f9dc10266a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65692211"
---
# <a name="idebugproviderprogramnode2"></a>IDebugProviderProgramNode2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このインターフェイスは、プロセスの境界を越えてプログラムに関連するインターフェイスをマーシャリングします。  
  
## <a name="syntax"></a>構文  
  
```  
IDebugProviderProgramNode2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>実装側の注意  
 デバッグエンジン (DE) は、プロセスの境界を越えたマーシャリングインターフェイスをサポートするために、 [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) を実装する同じオブジェクトにこのインターフェイスを実装します。  
  
## <a name="notes-for-callers"></a>呼び出し元に関する注意事項  
 インターフェイスの [QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3) を呼び出して、 `IDebugProgramNode2` このインターフェイスを取得します。 このインターフェイスを取得できない場合、DE はインターフェイスのマーシャリングをサポートしません。  
  
## <a name="methods-in-vtable-order"></a>Vtable の順序でのメソッド  
 このインターフェイスは、次のメソッドを実装します。  
  
|Method|説明|  
|------------|-----------------|  
|[UnmarshalDebuggeeInterface](../../../extensibility/debugger/reference/idebugproviderprogramnode2-unmarshaldebuggeeinterface.md)|プロセスの境界を越えて、指定されたインターフェイスを取得します。|  
  
## <a name="remarks"></a>解説  
 このインターフェイスは、デバッグ中のプログラムとは別のプロセス空間で DE が実行されるときに実装されます。たとえば、デバッグ中のプログラムのプロセス空間ではなく、Visual Studio のプロセス領域で DE が実行されている場合などです。  
  
## <a name="requirements"></a>必要条件  
 ヘッダー: msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)   
 [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
