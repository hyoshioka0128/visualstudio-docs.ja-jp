---
title: IDebugProgram3 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- IDebugProgram3 interface
ms.assetid: 4301ba23-c00c-4ce5-8b1e-3f27da312034
caps.latest.revision: 6
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: ae6de25108cf93314db17a2ac8de9ce8b1dcaed2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68148609"
---
# <a name="idebugprogram3"></a>IDebugProgram3
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このインターフェイスは、プロセスで実行されているプログラムを表し、スレッド情報を提供することによって [実行](../../../extensibility/debugger/reference/idebugprogram2-execute.md) を拡張します。  
  
## <a name="syntax"></a>Syntax  
  
```  
IDebugProgram3 : IDebugProgram3  
```  
  
## <a name="notes-for-implementers"></a>実装側の注意  
 デバッグエンジン (DE) とカスタムポート供給業者は、プロセス内のプログラムを表すために、このインターフェイスを実装します。 また、セッションデバッグマネージャー (SDM) は、このインターフェイスを実装して、 [アタッチ](../../../extensibility/debugger/reference/idebugprogram2-attach.md)する情報を提供します。  
  
## <a name="notes-for-callers"></a>呼び出し元に関する注意事項  
 [IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)イベントは、新しいプログラムに対してこのインターフェイスを返します。 このインターフェイスは、複数のインターフェイスの多くのメソッドのパラメーターとしても使用されます。  
  
## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド  
 次の表に、のメソッドを示し `IDebugProgram3` ます。  
  
|メソッド|説明|  
|------------|-----------------|  
|[ExecuteOnThread](../../../extensibility/debugger/reference/idebugprogram3-executeonthread.md)|プログラムを実行します。 スレッドは、実行時にユーザーが表示しているスレッドにデバッガー情報を提供するために返されます。|  
  
## <a name="requirements"></a>要件  
 ヘッダー: msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="remarks"></a>注釈  
 プログラムは、特定の実行時アーキテクチャで実行されるスレッドコンテナーであり、プロセスは1つ以上のプログラムで構成されます。  
  
## <a name="see-also"></a>参照  
 [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)   
 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)   
 [GetProgram](../../../extensibility/debugger/reference/idebugthread2-getprogram.md)   
 [次に](../../../extensibility/debugger/reference/ienumdebugprograms2-next.md)   
 [場合](../../../extensibility/debugger/reference/idebugportevents2-event.md)   
 [外付け](../../../extensibility/debugger/reference/idebugengine2-attach.md)   
 [DestroyProgram](../../../extensibility/debugger/reference/idebugengine2-destroyprogram.md)   
 [場合](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)   
 [Attach_V7](../../../extensibility/debugger/reference/idebugprogramnode2-attach-v7.md)
