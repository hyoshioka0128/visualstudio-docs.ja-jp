---
title: コントロールイベント |Microsoft Docs
description: IDebugEvent2 インターフェイスを使用して、プログラムの制御された実行中にイベントを送信する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], events
ms.assetid: 0fc63484-5fb6-4887-9ea4-1905b459ca9d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: bf7f59384d9317e4be173c93b6165d754a35ad8f
ms.sourcegitcommit: 8e9c38da7bcfbe9a461c378083846714933a0e1e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/09/2020
ms.locfileid: "96914245"
---
# <a name="control-events"></a>コントロールイベント
プログラムの制御された実行中にイベントを送信する必要があります。 すべてのイベントは、 [IDebugEvent2](../../extensibility/debugger/reference/idebugevent2.md) インターフェイスを使用して送信され、 [IDebugEvent2:: getattributes](../../extensibility/debugger/reference/idebugevent2-getattributes.md) メソッドの実装を必要とする属性を持っています。

## <a name="additional-methods"></a>その他のメソッド
 一部のイベントでは、次のように、追加のメソッドを実装する必要があります。

- デバッグエンジン (DE) の初期化時に [IDebugEngineCreateEvent2](../../extensibility/debugger/reference/idebugenginecreateevent2.md) インターフェイスを送信するには、 [IDebugEngineCreateEvent2:: getengine](../../extensibility/debugger/reference/idebugenginecreateevent2-getengine.md) メソッドを実装する必要があります。

- 実行制御には、 [IDebugBreakEvent2](../../extensibility/debugger/reference/idebugbreakevent2.md) インターフェイスと[IDebugStepCompleteEvent2](../../extensibility/debugger/reference/idebugstepcompleteevent2.md) インターフェイスとして、このようなコントロールイベントを実装する必要があります。 **IDebugBreakEvent2** は、非同期中断の場合にのみ必要です。

- 関数にステップインするには、 [IDebugStepCompleteEvent2](../../extensibility/debugger/reference/idebugstepcompleteevent2.md) インターフェイスとそのメソッドの実装が必要です。

  ブレークポイントから派生するイベントには、 [IDebugBreakpointErrorEvent2](../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md)、 [IDebugBreakpointEvent2](../../extensibility/debugger/reference/idebugbreakpointevent2.md)、 [IDebugBreakpointBoundEvent2](../../extensibility/debugger/reference/idebugbreakpointboundevent2.md) の各インターフェイスの実装と、 [IDebugBreakpointBoundEvent2:: getpendingbreakpoint ポイント](../../extensibility/debugger/reference/idebugbreakpointboundevent2-getpendingbreakpoint.md) および [enumboundbreakpoints ブレークポイント](../../extensibility/debugger/reference/idebugbreakpointboundevent2-enumboundbreakpoints.md) メソッドが必要です。

  非同期式の評価では、 [IDebugExpressionEvaluationCompleteEvent2](../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md) インターフェイスとその [IDebugExpressionEvaluationCompleteEvent2:: Getexpression](../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2-getexpression.md)[および GetResult](../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2-getresult.md) メソッドを実装する必要があります。

  同期イベントでは、 [IDebugEngine2:: ContinueFromSynchronousEvent](../../extensibility/debugger/reference/idebugengine2-continuefromsynchronousevent.md) メソッドを実装する必要があります。

  エンジンが文字列形式の出力を書き込むには、 [IDebugOutputStringEvent2:: GetString](../../extensibility/debugger/reference/idebugoutputstringevent2-getstring.md) メソッドを実装する必要があります。

## <a name="see-also"></a>関連項目
- [実行制御と状態の評価](../../extensibility/debugger/execution-control-and-state-evaluation.md)
