---
title: ブレークポイントのヒット |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], hitting breakpoints
- breakpoints, hitting
ms.assetid: a77816e3-b15b-46a0-90cd-be7242e4d6c9
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6e75eb1e807e72f3bd035b5dd0534860f5fd8df2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80738569"
---
# <a name="hit-a-breakpoint"></a>ブレークポイントに到達する
次のセクションでは、デバッグエンジン (DE) が実行中またはステップ実行中にブレークポイントにヒットした場合のプロセスについて説明します。

## <a name="troubleshoot-a-hit-breakpoint"></a>ヒットブレークポイントのトラブルシューティング

1. DE は、 [IDebugBreakpointEvent2](../../extensibility/debugger/reference/idebugbreakpointevent2.md) インターフェイスを **EVENT_SYNC_STOP**として送信します。

2. セッションデバッグマネージャー (SDM) は、 [IDebugBreakpointEvent2::: EnumBreakpoints ブレークポイント](../../extensibility/debugger/reference/idebugbreakpointevent2-enumbreakpoints.md) を呼び出して、ヒットしたブレークポイントを取得します。

## <a name="see-also"></a>関連項目
- [デバッガーイベントの呼び出し](../../extensibility/debugger/calling-debugger-events.md)
