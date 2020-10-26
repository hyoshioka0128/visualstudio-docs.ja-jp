---
title: プログラムを終了する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- programs, termination events
- debugging [Debugging SDK], terminating a program
ms.assetid: eedda0a3-5e05-44fe-841d-a2f4866ac72d
caps.latest.revision: 8
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f0b9ad248751af0885fa4edc0275be2ede5ddd9f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62421864"
---
# <a name="terminating-a-program"></a>プログラムの終了
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

1つのスレッドで1つのプログラムを終了する方法の説明を次に示します。  
  
## <a name="termination-process"></a>終了プロセス  
  
1. DE は、有効な[IDebugThread2](../../extensibility/debugger/reference/idebugthread2.md)を持つ[IDebugThreadDestroyEvent2](../../extensibility/debugger/reference/idebugthreaddestroyevent2.md)を送信します。  
  
2. DE は、有効な[IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)を持つ[IDebugProgramDestroyEvent2](../../extensibility/debugger/reference/idebugprogramdestroyevent2.md)を送信します。  
  
   IDE がデザインモードになります。 デバッグエンジンまたはランタイム環境は、 [IDebugPortNotify2:: RemoveProgramNode](../../extensibility/debugger/reference/idebugportnotify2-removeprogramnode.md) を呼び出して、ポートからプログラムを削除します。  
  
## <a name="see-also"></a>参照  
 [デバッガーのイベントの呼び出し](../../extensibility/debugger/calling-debugger-events.md)
