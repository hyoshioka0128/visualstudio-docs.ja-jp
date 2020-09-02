---
title: IDebugPortEx2 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugPortEx2
helpviewer_keywords:
- IDebugPortEx2 interface
ms.assetid: 144724d0-38ee-4c9b-87ca-8a504371182b
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: bb866c5cb968a4f03c718f04193026ac5308f7d4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65681119"
---
# <a name="idebugportex2"></a>IDebugPortEx2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このインターフェイスを使用すると、セッションデバッグマネージャー (SDM) は、ポートで実行されているプログラムとプロセスを制御できます。  
  
## <a name="syntax"></a>構文  
  
```  
IDebugPortEx2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>実装側の注意  
 カスタムポートサプライヤーは、 [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)を実装するのと同じオブジェクトにこのインターフェイスを実装します。  
  
## <a name="notes-for-callers"></a>呼び出し元に関する注意事項  
 SDM は、インターフェイスの [QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3) を呼び出して、 `IDebugPort2` このインターフェイスを取得します。  
  
## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド  
 次の表に、のメソッドを示し `IDebugPortEx2` ます。  
  
|Method|説明|  
|------------|-----------------|  
|[LaunchSuspended](../../../extensibility/debugger/reference/idebugportex2-launchsuspended.md)|実行可能ファイルを起動します。|  
|[ResumeProcess](../../../extensibility/debugger/reference/idebugportex2-resumeprocess.md)|プロセスの実行を再開します。|  
|[CanTerminateProcess](../../../extensibility/debugger/reference/idebugportex2-canterminateprocess.md)|プロセスを終了できるかどうかを判断します。|  
|[TerminateProcess](../../../extensibility/debugger/reference/idebugportex2-terminateprocess.md)|プロセスを終了します。|  
|[GetPortProcessId](../../../extensibility/debugger/reference/idebugportex2-getportprocessid.md)|ポート自体のプロセス ID を取得します。|  
|[GetProgram](../../../extensibility/debugger/reference/idebugportex2-getprogram.md)|プログラムノードに関連付けられているプログラムを取得します。|  
  
## <a name="remarks"></a>解説  
 このインターフェイスは、通常、SDM とカスタムポート供給業者の間でプライベートです。  
  
 必要に応じて、デバッグエンジン (DE) は、 [launchsuspended](../../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)に渡された[IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)インターフェイスでこのインターフェイスを検索し、 [launchsuspended](../../../extensibility/debugger/reference/idebugportex2-launchsuspended.md)を使用してプログラムを起動することができます。 ただし、これは必須ではありません。また、DE は、要求プログラムを起動するために必要な操作を行うことができます。  
  
## <a name="requirements"></a>必要条件  
 ヘッダー: portpriv. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)   
 [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)
