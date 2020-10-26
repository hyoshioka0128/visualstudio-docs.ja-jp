---
title: IDebugStopCompleteEvent2 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- IDebugStopCompleteEvent2 interface
ms.assetid: ff3e89f4-61bb-489d-901c-447260100218
caps.latest.revision: 7
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a9c2a6a6e69bf47751706710801dd78c832ccd2c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62546923"
---
# <a name="idebugstopcompleteevent2"></a>IDebugStopCompleteEvent2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

デバッグエンジン (DE) は、プログラムが停止したときに、この省略可能なイベントをセッションデバッグマネージャー (SDM) に送信できます。  
  
## <a name="syntax"></a>Syntax  
  
```  
IDebugStopCompleteEvent2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>実装側の注意  
 これは、の新しいインターフェイスです [!INCLUDE[vsprvslong](../../../includes/vsprvslong-md.md)] 。 以前のリリースでは、非同期停止はサポートされていませんでした。  
  
 [Stop](../../../extensibility/debugger/reference/idebugengineprogram2-stop.md) は、マルチプロセスまたは複数プログラムのシナリオで SDM によって呼び出されます。 あるプログラムが SDM に停止イベントを送信すると、SDM は他のプログラムも停止するように要求します。  
  
 これは、プログラムが停止したことを SDM に非同期に通知するために使用されます。 これは、デバッグ対象のプログラム内でコードが実行されていない可能性があるインタープリターデバッグエンジンに便利です。そのため、 [停止](../../../extensibility/debugger/reference/idebugengineprogram2-stop.md) を同期的に完了することはできません。 デバッグエンジンがこの非同期通知を使用する場合は、Stop から戻る必要があり `S_ASYNC_STOP` ます。 [Stop](../../../extensibility/debugger/reference/idebugengineprogram2-stop.md)  
  
## <a name="requirements"></a>要件  
 ヘッダー: msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
