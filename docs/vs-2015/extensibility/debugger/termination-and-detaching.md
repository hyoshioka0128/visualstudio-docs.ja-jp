---
title: 終了とデタッチ |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- programs, termination events
- debug engines, detaching from programs
ms.assetid: 268c1e51-6363-45d1-964c-1ab99bdfa4f9
caps.latest.revision: 8
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: d92fe88826baf19ba66b200990aee7797e91f87b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68176675"
---
# <a name="termination-and-detaching"></a>切り離しとデタッチ
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

通常の終了について次に説明します。  
  
## <a name="discussion"></a>考察 (Discussion)  
 [IDebugLoadCompleteEvent2](../../extensibility/debugger/reference/idebugloadcompleteevent2.md)または[IDebugEntryPointEvent2](../../extensibility/debugger/reference/idebugentrypointevent2.md)インターフェイスが続行されると、デバッグ対象のアプリケーションにブレークポイント、例外、実行時エラー、または無限ループがない場合は、デバッグ中のプログラムが完了するまで実行されます。 これは通常の終了です。  
  
 通常の終了を実装するには、 [IDebugProgramDestroyEvent2](../../extensibility/debugger/reference/idebugprogramdestroyevent2.md) を送信する必要があります。 このためには、 [IDebugProgramDestroyEvent2:: GetExitCode](../../extensibility/debugger/reference/idebugprogramdestroyevent2-getexitcode.md) メソッドを実装する必要があります。  
  
## <a name="see-also"></a>参照  
 [カスタム デバッグ エンジンの作成](../../extensibility/debugger/creating-a-custom-debug-engine.md)
