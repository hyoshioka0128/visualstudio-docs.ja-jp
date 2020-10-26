---
title: ブレークポイントのエラー |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- breakpoints, errors
- debugging [Debugging SDK], breakpoint errors
- errors [Debugging SDK]
ms.assetid: 79221c6b-a924-4c8e-a778-e312e4e0c0c8
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: e98dc5e4645ac67ecdf5ebb06ecf0f31510202e2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68147984"
---
# <a name="breakpoint-errors"></a>ブレークポイント エラー
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

ブレークポイントがコードにバインドしようとして失敗した場合のプロセスを次に示します。  
  
## <a name="troubleshooting-a-breakpoint-error"></a>ブレークポイントエラーのトラブルシューティング  
  
1. デバッグエンジン (DE) は、セッションデバッグマネージャー (SDM) に [IDebugBreakpointErrorEvent2](../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md) を送信します。  
  
2. SDM は [IDebugBreakpointErrorEvent2:: GetErrorBreakpoint](../../extensibility/debugger/reference/idebugbreakpointerrorevent2-geterrorbreakpoint.md) (IDebugErrorBreakpoint2 * * `ppErrorBP` ) を呼び出して、エラーのブレークポイントを取得します。  
  
3. SDM は、 [IDebugErrorBreakpoint2:: GetPendingBreakpoint ポイント](../../extensibility/debugger/reference/idebugerrorbreakpoint2-getpendingbreakpoint.md) を呼び出して、エラーブレークポイントが発生した保留中のブレークポイントを取得します。  
  
4. SDM は [IDebugErrorBreakpoint2:: GetBreakpointResolution](../../extensibility/debugger/reference/idebugerrorbreakpoint2-getbreakpointresolution.md) を呼び出して、エラーブレークポイントのバインドに失敗した理由を取得します。  
  
## <a name="see-also"></a>参照  
 [デバッガーのイベントの呼び出し](../../extensibility/debugger/calling-debugger-events.md)
