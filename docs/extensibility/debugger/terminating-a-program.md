---
title: プログラムを終了する |Microsoft Docs
description: この記事では、IDE がデバッグエンジンを使用して1つのスレッドで1つのプログラムを終了する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- programs, termination events
- debugging [Debugging SDK], terminating a program
ms.assetid: eedda0a3-5e05-44fe-841d-a2f4866ac72d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: db67e0a391f40fc17a80e616e10aa46a600337a4
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105057859"
---
# <a name="terminating-a-program"></a>プログラムを終了する
次のセクションでは、1つのスレッドで1つのプログラムを終了する方法について説明します。

## <a name="termination-process"></a>終了プロセス

1. DE は、有効な[IDebugThread2](../../extensibility/debugger/reference/idebugthread2.md)を持つ[IDebugThreadDestroyEvent2](../../extensibility/debugger/reference/idebugthreaddestroyevent2.md)を送信します。

2. DE は、有効な[IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)を持つ[IDebugProgramDestroyEvent2](../../extensibility/debugger/reference/idebugprogramdestroyevent2.md)を送信します。

   IDE がデザインモードになります。 デバッグエンジンまたはランタイム環境は、 [IDebugPortNotify2:: RemoveProgramNode](../../extensibility/debugger/reference/idebugportnotify2-removeprogramnode.md) を呼び出して、ポートからプログラムを削除します。

## <a name="see-also"></a>こちらもご覧ください
- [呼び出し (デバッガーイベントを)](../../extensibility/debugger/calling-debugger-events.md)
