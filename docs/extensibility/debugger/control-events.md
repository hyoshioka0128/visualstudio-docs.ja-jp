---
title: コントロール イベント |マイクロソフトドキュメント
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
ms.openlocfilehash: bc2c3ad9c9b63923bdf2f107e7bc582f3c76cd62
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739090"
---
# <a name="control-events"></a>コントロール イベント
プログラムの制御された実行中にイベントを送信する必要があります。 すべてのイベントは[IDebugEvent2](../../extensibility/debugger/reference/idebugevent2.md)インターフェイスを使用して送信され、メソッドを実装する必要がある属性[があります](../../extensibility/debugger/reference/idebugevent2-getattributes.md)。

## <a name="additional-methods"></a>その他の方法
 イベントによっては、次のように追加のメソッドの実装が必要です。

- デバッグ エンジン (DE) が初期化されたときに[IDebugEngineCreateEvent2](../../extensibility/debugger/reference/idebugenginecreateevent2.md)インターフェイスを送信するには、[メソッド](../../extensibility/debugger/reference/idebugenginecreateevent2-getengine.md)を実装する必要があります。

- 実行制御には[、IDebugBreakEvent2 および IDebugStepCompleteEvent2](../../extensibility/debugger/reference/idebugbreakevent2.md)インターフェイスなどのコントロール イベントの実装[が](../../extensibility/debugger/reference/idebugstepcompleteevent2.md)必要です。 **IDebugBreakEvent2**は非同期の中断に対してのみ必要です。

- 関数へのステップ インには、[インターフェイス](../../extensibility/debugger/reference/idebugstepcompleteevent2.md)とそのメソッドの実装が必要です。

  ブレークポイントから派生するイベントには[、IDebugBreakpointErrorEvent2、IDebugBreakpointEvent2、](../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md)および[IDebugBreakpointBoundEvent2](../../extensibility/debugger/reference/idebugbreakpointboundevent2.md)インターフェイスの実装と[、IDebugBreakpointBoundEvent2::GetPendingBreakpoint](../../extensibility/debugger/reference/idebugbreakpointboundevent2-getpendingbreakpoint.md)ブレークポイント[IDebugBreakpointEvent2](../../extensibility/debugger/reference/idebugbreakpointevent2.md)と[列挙型ブレークポイントのメソッドが必要です](../../extensibility/debugger/reference/idebugbreakpointboundevent2-enumboundbreakpoints.md)。

  非同期式の評価では[、IDebugExpression 評価コンプリート イベント 2](../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md)インターフェイスとその[IDebug 式の評価完了イベント2::GetExpression](../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2-getexpression.md)[と GetResult](../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2-getresult.md)メソッドを実装する必要があります。

  同期イベントは、メソッドを実装[する必要があります](../../extensibility/debugger/reference/idebugengine2-continuefromsynchronousevent.md)。

  エンジンが文字列形式の出力を書き込むには[、メソッドを](../../extensibility/debugger/reference/idebugoutputstringevent2-getstring.md)実装する必要があります。

## <a name="see-also"></a>関連項目
- [実行制御と状態評価](../../extensibility/debugger/execution-control-and-state-evaluation.md)
