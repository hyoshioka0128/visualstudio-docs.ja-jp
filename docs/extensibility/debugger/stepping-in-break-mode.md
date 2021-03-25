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
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 0ed11d05e4351ac6ba76bc9aa10531a8a96ddf23
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105075407"
---
# <a name="stepping-in-break-mode"></a>中断モードでのステップ実行
次のセクションでは、デバッガーが中断モードであり、コードをステップ実行する必要がある場合に発生するプロセスについて説明します。

## <a name="stepping-process"></a>ステップ実行プロセス

1. ステップを実行するには、 [Stepkind](../../extensibility/debugger/reference/stepkind.md)引数と[stepkind](../../extensibility/debugger/reference/stepunit.md)引数を指定して[IDebugProgram2:: step](../../extensibility/debugger/reference/idebugprogram2-step.md)を呼び出します。

2. ステップが完了したら、停止イベントとして [IDebugStepCompleteEvent2](../../extensibility/debugger/reference/idebugstepcompleteevent2.md) を送信します。

## <a name="see-also"></a>こちらもご覧ください
- [呼び出し (デバッガーイベントを)](../../extensibility/debugger/calling-debugger-events.md)
