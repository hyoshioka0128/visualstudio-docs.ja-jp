---
title: 中断モードでのステップ実行 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- break mode, stepping
- stepping, in break mode
- debugging [Debugging SDK], stepping in break mode
ms.assetid: b08dc8ee-6c63-4462-a097-6f525cfbb35a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 3161fc1c1ec8b44d96b3793198ac630ba2e32d67
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80712853"
---
# <a name="stepping-in-break-mode"></a>中断モードでのステップ実行
次のセクションでは、デバッガーが中断モードで、コードをステップ実行する必要がある場合に発生するプロセスについて説明します。

## <a name="stepping-process"></a>ステッピングプロセス

1. [ステップを実行するには](../../extensibility/debugger/reference/idebugprogram2-step.md)、[ステップKIND](../../extensibility/debugger/reference/stepkind.md)引数と[STEPUNIT](../../extensibility/debugger/reference/stepunit.md)引数を指定してステップを呼び出します。

2. 手順が完了したら、停止イベントとして[IDebugStepCompleteEvent2](../../extensibility/debugger/reference/idebugstepcompleteevent2.md)を送信します。

## <a name="see-also"></a>関連項目
- [デバッガ イベントの呼び出し](../../extensibility/debugger/calling-debugger-events.md)
