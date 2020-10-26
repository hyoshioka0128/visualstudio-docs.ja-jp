---
title: IDebugProgramNode2 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProgramNode2
helpviewer_keywords:
- IDebugProgramNode2 interface
ms.assetid: 80e511d8-9b40-4a85-aa5d-952fa5ee6ae7
caps.latest.revision: 21
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 1188f18e4a6f604dfd82991433bc0ffe0a07ad47
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68148567"
---
# <a name="idebugprogramnode2"></a>IDebugProgramNode2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このインターフェイスは、デバッグできるプログラムを表します。  
  
## <a name="syntax"></a>Syntax  
  
```  
IDebugProgramNode2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>実装側の注意  
 デバッグエンジン (DE) またはカスタムポート供給業者は、このインターフェイスを実装して、デバッグ可能なプログラムを表します。 このインターフェイスは、通常、 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) インターフェイスを実装するのと同じオブジェクトに実装されます。 このインターフェイスは、 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] [Publishprogramnode](../../../extensibility/debugger/reference/idebugprogrampublisher2-publishprogramnode.md)を呼び出すことによってに登録されます。  
  
## <a name="notes-for-callers"></a>呼び出し元に関する注意事項  
 [Getproviderprogramnode](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprogramnode.md)を呼び出して、このインターフェイスを返します。 カスタムポート供給業者は、 [Addprogramnode](../../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md)への呼び出しによってこのインターフェイスを受け取ります。 DE は、 [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md)の呼び出しを通じてこのインターフェイスを受信します。  
  
## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド  
 次の表に、のメソッドを示し `IDebugProgramNode2` ます。  
  
|メソッド|説明|  
|------------|-----------------|  
|[GetProgramName](../../../extensibility/debugger/reference/idebugprogramnode2-getprogramname.md)|プログラムの名前を取得します。|  
|[GetHostName](../../../extensibility/debugger/reference/idebugprogramnode2-gethostname.md)|プログラムをホストしているプロセスの名前を取得します。|  
|[GetHostPid](../../../extensibility/debugger/reference/idebugprogramnode2-gethostpid.md)|プログラムをホストしているプロセスのシステムプロセス識別子を取得します。|  
|[GetHostMachineName_V7](../../../extensibility/debugger/reference/idebugprogramnode2-gethostmachinename-v7.md)|れ. 使用しないでください。|  
|[Attach_V7](../../../extensibility/debugger/reference/idebugprogramnode2-attach-v7.md)|れ. 使用しないでください。 別の方法については、 [IDebugProgramNodeAttach2](../../../extensibility/debugger/reference/idebugprogramnodeattach2.md) インターフェイスを参照してください。|  
|[GetEngineInfo](../../../extensibility/debugger/reference/idebugprogramnode2-getengineinfo.md)|このプログラムを実行している DE の名前と識別子を取得します。|  
|[DetachDebugger_V7](../../../extensibility/debugger/reference/idebugprogramnode2-detachdebugger-v7.md)|れ. 使用しないでください。|  
  
## <a name="remarks"></a>注釈  
 セッションデバッグマネージャー (SDM) は、通常、このインターフェイスを取得するために [Getproviderprogramnode](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprogramnode.md) を呼び出します。  
  
## <a name="requirements"></a>要件  
 ヘッダー: Msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)   
 [IDebugProgramNodeAttach2](../../../extensibility/debugger/reference/idebugprogramnodeattach2.md)   
 [AddProgramNode](../../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md)   
 [RemoveProgramNode](../../../extensibility/debugger/reference/idebugportnotify2-removeprogramnode.md)   
 [外付け](../../../extensibility/debugger/reference/idebugengine2-attach.md)   
 [GetProviderProgramNode](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprogramnode.md)   
 [PublishProgramNode](../../../extensibility/debugger/reference/idebugprogrampublisher2-publishprogramnode.md)
