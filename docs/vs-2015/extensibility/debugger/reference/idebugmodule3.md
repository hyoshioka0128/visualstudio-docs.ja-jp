---
title: IDebugModule3 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugModule3
helpviewer_keywords:
- IDebugModule3 interface
ms.assetid: 44f8e96e-9c59-4ffc-9a08-9c908a0e4de7
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 326efe27ae35de1550ebc8230ab3c94229589640
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65690952"
---
# <a name="idebugmodule3"></a>IDebugModule3
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このインターフェイスは、シンボルの別の場所と Mycode の状態をサポートするモジュールを表します。  
  
## <a name="syntax"></a>Syntax  
  
```  
IDebugModule3 : IDebugModule2  
```  
  
## <a name="notes-for-implementers"></a>実装側の注意  
 デバッグエンジン (DE) は、このインターフェイスを実装して、シンボルの別の場所をサポートし、また Mycode の状態を操作します ("ジャスト Mycode" の定義については、「 [Visual Studio デバッガーの用語集](../../../extensibility/debugger/reference/visual-studio-debugger-glossary.md) 」を参照してください)。  
  
## <a name="notes-for-callers"></a>呼び出し元に関する注意事項  
 [Getシンボル Searchinfo](../../../extensibility/debugger/reference/idebugsymbolsearchevent2-getsymbolsearchinfo.md)を呼び出すと、このインターフェイスが返されます。 DE は、[イベント](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)メソッドを使用して、 [IDebugSymbolSearchEvent2](../../../extensibility/debugger/reference/idebugsymbolsearchevent2.md)インターフェイスをセッションデバッグマネージャー (SDM) に送信します。 また、 [IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md)インターフェイスで[QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3)を呼び出すと、このインターフェイスが返されます。  
  
## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド  
 このインターフェイスは、 [IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md) インターフェイスのメソッドに加えて、次のメソッドを実装します。  
  
|メソッド|説明|  
|------------|-----------------|  
|[GetSymbolInfo](../../../extensibility/debugger/reference/idebugmodule3-getsymbolinfo.md)|シンボルの検索対象となるパスと、各パスを検索した結果の一覧を返します。|  
|[LoadSymbols](../../../extensibility/debugger/reference/idebugmodule3-loadsymbols.md)|現在のモジュールのシンボルを読み込んで初期化します。|  
|[IsUserCode](../../../extensibility/debugger/reference/idebugmodule3-isusercode.md)|モジュールがユーザーコードを表すかどうかを指定するフラグを返します。|  
|[SetJustMyCodeState](../../../extensibility/debugger/reference/idebugmodule3-setjustmycodestate.md)|モジュールをユーザーコードと見なすかどうかを指定します。|  
  
## <a name="remarks"></a>注釈  
 Visual Studio は、このインターフェイスの一般的なコンシューマーです。  
  
## <a name="requirements"></a>要件  
 ヘッダー: msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)   
 [IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md)   
 [IDebugSymbolSearchEvent2](../../../extensibility/debugger/reference/idebugsymbolsearchevent2.md)   
 [GetSymbolSearchInfo](../../../extensibility/debugger/reference/idebugsymbolsearchevent2-getsymbolsearchinfo.md)
