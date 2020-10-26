---
title: IDebugProgramEx2 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProgramEx2
helpviewer_keywords:
- IDebugProgramEx2 interface
ms.assetid: 663359ed-635a-4539-addb-0cc52f19d1bd
caps.latest.revision: 19
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2d3abc956d736f5c9273134b41c0fc9c2dc7db62
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65688935"
---
# <a name="idebugprogramex2"></a>IDebugProgramEx2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このインターフェイスを使用すると、セッションデバッグマネージャー (SDM) をプログラムにアタッチし、プログラムに関連付けられたプログラムノードを取得できます。  
  
## <a name="syntax"></a>Syntax  
  
```  
IDebugProgramEx2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>実装側の注意  
 カスタムポートサプライヤーは、 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) インターフェイスと同じオブジェクトにこのインターフェイスを実装して、SDM がプログラムにアタッチされるようにします。同時に、ポートサプライヤーがプログラムにアタッチされているすべてのセッションを追跡できるようにします。 カスタムポート供給業者は、選択した場合、このインターフェイスを実装できます。  
  
## <a name="notes-for-callers"></a>呼び出し元に関する注意事項  
 SDM は、インターフェイスの [QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3) を呼び出して、 `IDebugProgram2` プログラムにアタッチされたセッションを追跡するために、このインターフェイスを取得します。  
  
## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド  
 次の表に、のメソッドを示し `IDebugProgramEx2` ます。  
  
|メソッド|説明|  
|------------|-----------------|  
|[[アタッチ]](../../../extensibility/debugger/reference/idebugprogramex2-attach.md)|セッションにプログラムをアタッチします。|  
|[GetProgramNode](../../../extensibility/debugger/reference/idebugprogramex2-getprogramnode.md)|プログラムに関連付けられているプログラムノードを取得します。|  
  
## <a name="remarks"></a>注釈  
 このインターフェイスは、SDM とプログラムの間でプライベートです。  
  
## <a name="requirements"></a>要件  
 ヘッダー: Portpriv. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)   
 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
