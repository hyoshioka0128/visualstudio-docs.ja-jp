---
title: ブレークポイントの作成 |Microsoft Docs
description: ブレークポイントをバインドするために必要なモジュールが読み込まれるときに、セッションデバッグマネージャーが行うメソッド呼び出しについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- breakpoints, creating
- debugging [Debugging SDK], creating breakpoints
ms.assetid: 6f9f87bb-192e-45e0-9a7a-ffe729e87f7d
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: dcd81b79fa43d86036a7fd1ac0ad813e6e2ebb78
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99894973"
---
# <a name="create-a-breakpoint"></a>ブレークポイントの作成
次に、ブレークポイントを作成するプロセスについて説明します。

## <a name="methods-in-breakpoint-creation"></a>ブレークポイント作成時のメソッド
 ブレークポイントをバインドするために必要なモジュールが読み込まれると、セッションデバッグマネージャー (SDM) は次のメソッドを呼び出します。

1. [IDebugPendingBreakpoint2::Enable](../../extensibility/debugger/reference/idebugpendingbreakpoint2-enable.md)

2. [IDebugPendingBreakpoint2::Virtualize](../../extensibility/debugger/reference/idebugpendingbreakpoint2-virtualize.md)

3. [IDebugPendingBreakpoint2::CanBind](../../extensibility/debugger/reference/idebugpendingbreakpoint2-canbind.md)

    > [!NOTE]
    > **Canbind** は、ユーザーが [ **ブレークポイント** ] ウィンドウからブレークポイントを作成した場合にのみ呼び出されます。

4. [IDebugPendingBreakpoint2::Bind](../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)

5. [IDebugPendingBreakpoint2::EnumBoundBreakpoints](../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumboundbreakpoints.md)

## <a name="see-also"></a>関連項目
- [デバッガーイベントの呼び出し](../../extensibility/debugger/calling-debugger-events.md)
