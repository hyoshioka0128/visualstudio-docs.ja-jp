---
title: 切り離しとデタッチ |Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- programs, termination events
- debug engines, detaching from programs
ms.assetid: 268c1e51-6363-45d1-964c-1ab99bdfa4f9
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 143b3a266bab8ad48f7f431234d1bf50c16c9de4
ms.sourcegitcommit: 8d38d5d2f2b75fc1563952c0d6de0fe43af12766
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/26/2018
ms.locfileid: "39276924"
---
# <a name="termination-and-detaching"></a>切り離しとデタッチ
次のセクションでは、通常の終了について説明します。  
  
## <a name="discussion"></a>説明  
 後に、 [IDebugLoadCompleteEvent2](../../extensibility/debugger/reference/idebugloadcompleteevent2.md)または[IDebugEntryPointEvent2](../../extensibility/debugger/reference/idebugentrypointevent2.md)インターフェイスは、ブレークポイント、例外、実行時エラー、またはデバッグするには、アプリケーションで無限ループがない場合デバッグ中のプログラムは、完了まで実行されます。 このプロセスは、正常に終了します。  
  
 送信する必要があります、 [IDebugProgramDestroyEvent2](../../extensibility/debugger/reference/idebugprogramdestroyevent2.md)正常終了を実装します。 正常終了が実行されている必要があります、 [IDebugProgramDestroyEvent2::GetExitCode](../../extensibility/debugger/reference/idebugprogramdestroyevent2-getexitcode.md)メソッド。  
  
## <a name="see-also"></a>関連項目  
 [カスタム デバッグ エンジンを作成します。](../../extensibility/debugger/creating-a-custom-debug-engine.md)