---
title: 中断モードでステップインする |Microsoft Docs
description: デバッガーが中断モードのときに発生するプロセスについて説明します。 次に、デバッガーはコードをステップ実行する必要があります。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- break mode, stepping
- stepping, in break mode
- debugging [Debugging SDK], stepping in break mode
ms.assetid: b08dc8ee-6c63-4462-a097-6f525cfbb35a
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 4f284fecf32a94f7187ecd34798f9ac21f476804
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99960677"
---
# <a name="stepping-in-break-mode"></a>中断モードでのステップ実行
次のセクションでは、デバッガーが中断モードであり、コードをステップ実行する必要がある場合に発生するプロセスについて説明します。

## <a name="stepping-process"></a>ステップ実行プロセス

1. ステップを実行するには、 [Stepkind](../../extensibility/debugger/reference/stepkind.md)引数と[stepkind](../../extensibility/debugger/reference/stepunit.md)引数を指定して[IDebugProgram2:: step](../../extensibility/debugger/reference/idebugprogram2-step.md)を呼び出します。

2. ステップが完了したら、停止イベントとして [IDebugStepCompleteEvent2](../../extensibility/debugger/reference/idebugstepcompleteevent2.md) を送信します。

## <a name="see-also"></a>関連項目
- [呼び出し (デバッガーイベントを)](../../extensibility/debugger/calling-debugger-events.md)
