---
title: IDebugErrorEvent2 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugErrorEvent2
helpviewer_keywords:
- IDebugErrorEvent2 interface
ms.assetid: 275b6f38-b3d4-4cae-8491-491177f524fb
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 83170c72eeabaae2ac193e47ddc91e1ec1e54046
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65695419"
---
# <a name="idebugerrorevent2"></a>IDebugErrorEvent2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このインターフェイスは、ユーザーに報告されるエラーメッセージを指定します。  
  
## <a name="syntax"></a>Syntax  
  
```  
IDebugErrorEvent2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>実装側の注意  
 デバッグエンジン (DE) は、このインターフェイスを実装して、エラーを人間が判読できるメッセージとして報告します。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)インターフェイスは、このインターフェイスと同じオブジェクトに実装する必要があります。 SDM は、 [QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3) を使用してインターフェイスにアクセスし `IDebugEvent2` ます。  
  
## <a name="notes-for-callers"></a>呼び出し元に関する注意事項  
 DE は、このイベントオブジェクトを作成して送信し、エラーを報告します。 イベントは、デバッグ対象のプログラムにアタッチされたときに SDM によって提供される [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) callback 関数を使用して送信されます。  
  
## <a name="methods-in-vtable-order"></a>Vtable の順序でのメソッド  
 このインターフェイスは、次のメソッドを実装します。  
  
|メソッド|説明|  
|------------|-----------------|  
|`GetErrorMessage`|人間が判読できる文字列としてエラーを返します。|  
  
## <a name="remarks"></a>注釈  
 デバッグエンジンがエラーを検出した場合、このインターフェイスを使用して、Visual Studio を通じてユーザーにメッセージを報告できます。  
  
## <a name="requirements"></a>要件  
 ヘッダー: msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)   
 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
