---
title: ブレークポイントがバインドまたはバインド解除した場合 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], breakpoint unbound events
- breakpoint bound events
ms.assetid: 61bf00b2-8293-49d3-b919-1efb0dec9151
caps.latest.revision: 8
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f1425edc2c8fc3fe8c38c133388f90b18b516b09
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68162174"
---
# <a name="when-a-breakpoint-binds-or-becomes-unbound"></a>ブレークポイントがいつバインド、または非バインドになるか
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

[IDebugPendingBreakpoint2:: CanBind](../../extensibility/debugger/reference/idebugpendingbreakpoint2-canbind.md)メソッドに対して呼び出しが行われたときにブレークポイントがバインドできない場合、バインド時間とブレークポイントの作成時間は異なります。  
  
## <a name="methods-called"></a>呼び出されるメソッド  
 セッションデバッグマネージャー (SDM) は、次のメソッドを呼び出します。  
  
1. [IDebugEngine2:: CreatePendingBreakpoint ポイント](../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md)。 DE は、 [IDebugPendingBreakpoint2](../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)を返します。  
  
2. [IDebugPendingBreakpoint2:: Enable](../../extensibility/debugger/reference/idebugpendingbreakpoint2-enable.md)。  
  
3. [IDebugPendingBreakpoint2:: 仮想](../../extensibility/debugger/reference/idebugpendingbreakpoint2-virtualize.md)化。  
  
4. [IDebugPendingBreakpoint2:: Bind](../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)メソッドと S_OK を返します。 DE は、 [IDebugBreakpointBoundEvent2](../../extensibility/debugger/reference/idebugbreakpointboundevent2.md) または [IDebugBreakpointErrorEvent2](../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md)を送信します。  
  
5. [IDebugBreakpointBoundEvent2:: GetPendingBreakpoint](../../extensibility/debugger/reference/idebugbreakpointboundevent2-getpendingbreakpoint.md) ポイントと [IDebugBreakpointBoundEvent2:: enumboundbreakpoints ブレーク](../../extensibility/debugger/reference/idebugbreakpointboundevent2-enumboundbreakpoints.md) ポイントメソッドを検証し、バインドされたブレークポイントを取得します。  
  
## <a name="see-also"></a>参照  
 [デバッガーのイベントの呼び出し](../../extensibility/debugger/calling-debugger-events.md)
