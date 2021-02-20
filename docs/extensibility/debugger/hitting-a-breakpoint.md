---
title: ブレークポイントのヒット |Microsoft Docs
description: この記事では、デバッグエンジンが実行中またはステップ実行中にブレークポイントにヒットしたときに行われる処理について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], hitting breakpoints
- breakpoints, hitting
ms.assetid: a77816e3-b15b-46a0-90cd-be7242e4d6c9
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 808bf95631bb4106d071c29d7af233d071ef5229
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99947724"
---
# <a name="hit-a-breakpoint"></a>ブレークポイントに到達する
次のセクションでは、デバッグエンジン (DE) が実行中またはステップ実行中にブレークポイントにヒットした場合のプロセスについて説明します。

## <a name="troubleshoot-a-hit-breakpoint"></a>ヒットブレークポイントのトラブルシューティング

1. DE は、 [IDebugBreakpointEvent2](../../extensibility/debugger/reference/idebugbreakpointevent2.md) インターフェイスを **EVENT_SYNC_STOP** として送信します。

2. セッションデバッグマネージャー (SDM) は、 [IDebugBreakpointEvent2::: EnumBreakpoints ブレークポイント](../../extensibility/debugger/reference/idebugbreakpointevent2-enumbreakpoints.md) を呼び出して、ヒットしたブレークポイントを取得します。

## <a name="see-also"></a>関連項目
- [デバッガーイベントの呼び出し](../../extensibility/debugger/calling-debugger-events.md)
