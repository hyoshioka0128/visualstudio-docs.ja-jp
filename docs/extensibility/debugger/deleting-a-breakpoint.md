---
title: ブレークポイントを削除する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- breakpoints, deleting
- debugging [Debugging SDK], deleting breakpoints
ms.assetid: 75a046cc-d20a-4c79-ad2d-1f18426ac5d0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a77be200a11eb7b3985a4c1a47e4cddaa543f900
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738940"
---
# <a name="deleting-a-breakpoint"></a>ブレークポイントの削除
保留中のブレークポイントを削除する場合のプロセスを次に示します。

## <a name="deletion-process"></a>削除プロセス
 セッション デバッグ マネージャー (SDM) は、保留中のブレークポイントとバインドされているすべてのバインドされたブレークポイントを削除する[IDebugPendingBreakpoint2::Delete](../../extensibility/debugger/reference/idebugpendingbreakpoint2-delete.md)メソッドを呼び出します。

> [!NOTE]
> バインドされた単一のブレークポイントは[、IDebugBoundBreakpoint2::Delete](../../extensibility/debugger/reference/idebugboundbreakpoint2-delete.md)の呼び出しによっても削除できます。

## <a name="see-also"></a>関連項目
- [デバッガー イベントの呼び出し](../../extensibility/debugger/calling-debugger-events.md)
