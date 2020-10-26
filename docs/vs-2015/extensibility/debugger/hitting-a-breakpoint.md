---
title: ブレークポイントのヒット |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], hitting breakpoints
- breakpoints, hitting
ms.assetid: a77816e3-b15b-46a0-90cd-be7242e4d6c9
caps.latest.revision: 8
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 0ddf7fd92ac0b2f745f9e73170de22e9724dad76
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68152689"
---
# <a name="hitting-a-breakpoint"></a>ブレークポイントのヒット
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

次に、デバッグエンジン (DE) が実行中またはステップ実行中にブレークポイントにヒットした場合のプロセスについて説明します。  
  
## <a name="troubleshooting-a-hit-breakpoint"></a>ヒットブレークポイントのトラブルシューティング  
  
1. DE は、 [IDebugBreakpointEvent2](../../extensibility/debugger/reference/idebugbreakpointevent2.md) インターフェイスを **EVENT_SYNC_STOP**として送信します。  
  
2. セッションデバッグマネージャー (SDM) は、 [IDebugBreakpointEvent2::: EnumBreakpoints ブレークポイント](../../extensibility/debugger/reference/idebugbreakpointevent2-enumbreakpoints.md) を呼び出して、ヒットしたブレークポイントを取得します。  
  
## <a name="see-also"></a>参照  
 [デバッガーのイベントの呼び出し](../../extensibility/debugger/calling-debugger-events.md)
