---
title: IDebugProgramHost2 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProgramHost2
helpviewer_keywords:
- IDebugProgramHost2 interface
ms.assetid: 2c37b3aa-97a9-4665-8709-edd917f18cb1
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2bcb65872f9f451e1cc4e5030532e0a444af1139
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65687781"
---
# <a name="idebugprogramhost2"></a>IDebugProgramHost2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このインターフェイスは、プログラムに関するホスト (プロセス) 情報を提供します。  
  
## <a name="syntax"></a>Syntax  
  
```  
IDebugProgramHost2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>実装側の注意  
 デバッグエンジンは、ホストプロセスに関する情報を提供するために、 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) インターフェイスと同じオブジェクトにこのインターフェイスを実装します。 これは省略可能なインターフェイスです。  
  
## <a name="notes-for-callers"></a>呼び出し元に関する注意事項  
 インターフェイスの [QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3) を呼び出して、 `IDebugProgram2` このインターフェイスを取得します。  
  
## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド  
 次の表に、のメソッドを示し `IDebugProgramHost2` ます。  
  
|メソッド|説明|  
|------------|-----------------|  
|[GetHostName](../../../extensibility/debugger/reference/idebugprogramhost2-gethostname.md)|このプログラムのホストプロセスのタイトル、フレンドリ名、またはファイル名を取得します。|  
|[GetHostId](../../../extensibility/debugger/reference/idebugprogramhost2-gethostid.md)|このプログラムのホストプロセスのプロセス識別子を取得します。|  
|[GetHostMachineName](../../../extensibility/debugger/reference/idebugprogramhost2-gethostmachinename.md)|このプログラムのホストプロセスが実行されているコンピューターの名前を取得します。|  
  
## <a name="requirements"></a>要件  
 ヘッダー: msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)   
 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
