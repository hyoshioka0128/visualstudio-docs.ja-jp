---
title: IDebugProcessEx2 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProcessEx2
helpviewer_keywords:
- IDebugProcessEx2 interface
ms.assetid: 44e309ba-1d6f-499b-aa7e-9b34858a6d57
caps.latest.revision: 22
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: d2b036bd68aca126675f26b9823d2c786a0ae652
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65675329"
---
# <a name="idebugprocessex2"></a>IDebugProcessEx2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このインターフェイスを使用すると、セッションデバッグマネージャー (SDM) は、プロセスにアタッチするプロセスまたはプロセスからデタッチするプロセスを通知できます。  
  
## <a name="syntax"></a>構文  
  
```  
IDebugProcessEx2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>実装側の注意  
 カスタムポートサプライヤーは、次の目的で、 [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md) インターフェイスと同じオブジェクトにこのインターフェイスを実装します。  
  
- プロセスに接続されているセッションの追跡をサポートする  
  
- 複数のデバッグエンジン間での自動アタッチをサポートする  
  
  カスタムポート供給業者は、選択した場合、このインターフェイスを実装できます。  
  
## <a name="notes-for-callers"></a>呼び出し元に関する注意事項  
  
- SDM は、インターフェイスの [QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3) を呼び出して、 `IDebugProcess2` このインターフェイスを取得します。  
  
## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド  
 次の表に、のメソッドを示し `IDebugProcessEx2` ます。  
  
|Method|説明|  
|------------|-----------------|  
|[[アタッチ]](../../../extensibility/debugger/reference/idebugprocessex2-attach.md)|セッションがプロセスをデバッグ中であることをプロセスに通知します。|  
|[[デタッチ]](../../../extensibility/debugger/reference/idebugprocessex2-detach.md)|セッションがプロセスのデバッグを終了したことをプロセスに通知します。|  
|[AddImplicitProgramNodes](../../../extensibility/debugger/reference/idebugprocessex2-addimplicitprogramnodes.md)|デバッグエンジンの一覧のプログラムノードを追加します。|  
  
## <a name="remarks"></a>解説  
 このインターフェイスは、SDM とプロセスとの間でプライベートです。  
  
## <a name="requirements"></a>必要条件  
 ヘッダー: Portpriv. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)   
 [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
