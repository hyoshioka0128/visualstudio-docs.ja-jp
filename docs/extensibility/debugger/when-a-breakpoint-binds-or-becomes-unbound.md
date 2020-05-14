---
title: ブレークポイントがバインドまたはバインド解除されたとき |マイクロソフトドキュメント
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
ms.openlocfilehash: 3253841778fe5a07e00b644423495b8ceee1a335
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80712331"
---
# <a name="when-a-breakpoint-binds-or-becomes-unbound"></a>ブレークポイントがバインドまたはバインド解除されたとき
呼び出しが行われたときにブレークポイントをバインドできない場合、 [IDebugPendingBreakpoint2::CanBind](../../extensibility/debugger/reference/idebugpendingbreakpoint2-canbind.md)メソッド、バインド時間とブレークポイントの作成時間が異なります。

## <a name="methods-called"></a>呼び出されたメソッド
 セッション デバッグ マネージャー (SDM) は、次のメソッドを呼び出します。

1. [IDebugEngine2::保留中のブレークポイントを作成します](../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md)。 デは[、IDebugPendingブレークポイント2を](../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)返します。

2. [Iデバッグ保留中のブレークポイント2::有効に](../../extensibility/debugger/reference/idebugpendingbreakpoint2-enable.md)します。

3. [IDebug保留中のブレークポイント2::仮想化](../../extensibility/debugger/reference/idebugpendingbreakpoint2-virtualize.md).

4. [メソッドを返](../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)し、S_OK返します。 デは[、IDebug ブレークポイントバインド イベント 2](../../extensibility/debugger/reference/idebugbreakpointboundevent2.md)または[I デバッグ ブレークポイントエラー イベント 2](../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md)を送信します。

5. 検証[し、](../../extensibility/debugger/reference/idebugbreakpointboundevent2-enumboundbreakpoints.md)バインド[されたブレークポイント](../../extensibility/debugger/reference/idebugbreakpointboundevent2-getpendingbreakpoint.md)を取得するメソッドをメソッド。

## <a name="see-also"></a>関連項目
- [デバッガ イベントの呼び出し](../../extensibility/debugger/calling-debugger-events.md)
