---
title: ブレークポイントがバインドまたはバインド解除した場合 |Microsoft Docs
description: 非バインドブレークポイントについて学習します。 呼び出しの実行時にブレークポイントをバインドできない場合、バインド時間とブレークポイントの作成時間は異なります。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], breakpoint unbound events
- breakpoint bound events
ms.assetid: 61bf00b2-8293-49d3-b919-1efb0dec9151
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a48bd7ff011b6e8de6e9321a00b6bc20d54f0f0b
ms.sourcegitcommit: d10f37dfdba5d826e7451260c8370fd1efa2c4e4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2020
ms.locfileid: "96995916"
---
# <a name="when-a-breakpoint-binds-or-becomes-unbound"></a>ブレークポイントがバインドまたはバインド解除したとき
[IDebugPendingBreakpoint2:: CanBind](../../extensibility/debugger/reference/idebugpendingbreakpoint2-canbind.md)メソッドに対して呼び出しが行われたときにブレークポイントがバインドできない場合、バインド時間とブレークポイントの作成時間は異なります。

## <a name="methods-called"></a>呼び出されるメソッド
 セッションデバッグマネージャー (SDM) は、次のメソッドを呼び出します。

1. [IDebugEngine2:: CreatePendingBreakpoint ポイント](../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md)。 DE は、 [IDebugPendingBreakpoint2](../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)を返します。

2. [IDebugPendingBreakpoint2:: Enable](../../extensibility/debugger/reference/idebugpendingbreakpoint2-enable.md)。

3. [IDebugPendingBreakpoint2:: 仮想](../../extensibility/debugger/reference/idebugpendingbreakpoint2-virtualize.md)化。

4. [IDebugPendingBreakpoint2:: Bind](../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)メソッドと S_OK を返します。 DE は、 [IDebugBreakpointBoundEvent2](../../extensibility/debugger/reference/idebugbreakpointboundevent2.md) または [IDebugBreakpointErrorEvent2](../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md)を送信します。

5. [IDebugBreakpointBoundEvent2:: GetPendingBreakpoint](../../extensibility/debugger/reference/idebugbreakpointboundevent2-getpendingbreakpoint.md) ポイントと [IDebugBreakpointBoundEvent2:: enumboundbreakpoints ブレーク](../../extensibility/debugger/reference/idebugbreakpointboundevent2-enumboundbreakpoints.md) ポイントメソッドを検証し、バインドされたブレークポイントを取得します。

## <a name="see-also"></a>こちらもご覧ください
- [呼び出し (デバッガーイベントを)](../../extensibility/debugger/calling-debugger-events.md)
