---
title: IDebugQueryEngine2 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugQueryEngine2
helpviewer_keywords:
- IDebugQueryEngine2 interface
ms.assetid: 8f0e1838-a818-4459-9138-a3dceb7408de
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 7274d621e47c9c705cc0ce6bc4ad49f24e144f59
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65683279"
---
# <a name="idebugqueryengine2"></a>IDebugQueryEngine2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このインターフェイスを使用すると、セッションデバッグマネージャー (SDM) は、デバッグエンジン (DE) を表すインターフェイスを取得できます。  
  
## <a name="syntax"></a>構文  
  
```  
IDebugQueryEngine2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>実装側の注意  
 De は、de 自体の[IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)インターフェイスへのアクセスを許可するために、最も一般的な de インターフェイス ( [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)、 [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)、 [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)など) を実装するオブジェクトに対してこのインターフェイスを実装します。  
  
## <a name="notes-for-callers"></a>呼び出し元に関する注意事項  
 このインターフェイスを取得するには、一般的な DE インターフェイスで [QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3) を呼び出します。  
  
## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド  
 次の表に、のメソッドを示し `IDebugQueryEngine2` ます。  
  
|Method|説明|  
|------------|-----------------|  
|[GetEngineInterface](../../../extensibility/debugger/reference/idebugqueryengine2-getengineinterface.md)|カスタムデバッグエンジン (DE) インターフェイスを取得します。|  
  
## <a name="remarks"></a>解説  
 このインターフェイスは、通常、 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) インターフェイスを実装するオブジェクトに実装されます。これは、関数を使用した因果関係のステップ実行をサポートするためです。つまり、デバッガーが関数からステップアウトすると、次に実行される関数がスタック上の前の関数ではなく、別のスレッドの関数が完全になることがあります。 "因果関係" の定義については、「 [Visual Studio デバッガー用語集](../../../extensibility/debugger/reference/visual-studio-debugger-glossary.md)」を参照してください。  
  
## <a name="requirements"></a>必要条件  
 ヘッダー: msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)   
 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)   
 [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)   
 [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)   
 [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
