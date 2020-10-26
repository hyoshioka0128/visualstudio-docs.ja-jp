---
title: 中断モードでステップインする |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- break mode, stepping
- stepping, in break mode
- debugging [Debugging SDK], stepping in break mode
ms.assetid: b08dc8ee-6c63-4462-a097-6f525cfbb35a
caps.latest.revision: 8
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 482d7131692c1e22483c80f4b4bb22e07a6caf1a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62423362"
---
# <a name="stepping-in-break-mode"></a>中断モードへのステップイン
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

デバッガーが中断モードになっていて、コードをステップ実行する必要がある場合に発生するプロセスを次に示します。  
  
## <a name="stepping-process"></a>ステップ実行プロセス  
  
1. ステップを実行するには、 [Stepkind](../../extensibility/debugger/reference/stepkind.md)引数と[stepkind](../../extensibility/debugger/reference/stepunit.md)引数を指定して[IDebugProgram2:: step](../../extensibility/debugger/reference/idebugprogram2-step.md)を呼び出します。  
  
2. ステップが完了したら、停止イベントとして [IDebugStepCompleteEvent2](../../extensibility/debugger/reference/idebugstepcompleteevent2.md) を送信します。  
  
## <a name="see-also"></a>参照  
 [デバッガーのイベントの呼び出し](../../extensibility/debugger/calling-debugger-events.md)
