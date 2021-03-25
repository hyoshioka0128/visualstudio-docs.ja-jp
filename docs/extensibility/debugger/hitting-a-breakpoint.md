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
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e093437fcc8b3e1e2663c2a46ebb3b70d32efbec
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105059952"
---
# <a name="hit-a-breakpoint"></a>ブレークポイントに到達する
次のセクションでは、デバッグエンジン (DE) が実行中またはステップ実行中にブレークポイントにヒットした場合のプロセスについて説明します。

## <a name="troubleshoot-a-hit-breakpoint"></a>ヒットブレークポイントのトラブルシューティング

1. DE は、 [IDebugBreakpointEvent2](../../extensibility/debugger/reference/idebugbreakpointevent2.md) インターフェイスを **EVENT_SYNC_STOP** として送信します。

2. セッションデバッグマネージャー (SDM) は、 [IDebugBreakpointEvent2::: EnumBreakpoints ブレークポイント](../../extensibility/debugger/reference/idebugbreakpointevent2-enumbreakpoints.md) を呼び出して、ヒットしたブレークポイントを取得します。

## <a name="see-also"></a>こちらもご覧ください
- [デバッガーイベントの呼び出し](../../extensibility/debugger/calling-debugger-events.md)
