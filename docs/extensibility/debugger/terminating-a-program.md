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
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1b2b883611d5479f0febc169b32f7f378230be4c
ms.sourcegitcommit: d10f37dfdba5d826e7451260c8370fd1efa2c4e4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2020
ms.locfileid: "96995981"
---
# <a name="terminating-a-program"></a>プログラムを終了する
次のセクションでは、1つのスレッドで1つのプログラムを終了する方法について説明します。

## <a name="termination-process"></a>終了プロセス

1. DE は、有効な[IDebugThread2](../../extensibility/debugger/reference/idebugthread2.md)を持つ[IDebugThreadDestroyEvent2](../../extensibility/debugger/reference/idebugthreaddestroyevent2.md)を送信します。

2. DE は、有効な[IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)を持つ[IDebugProgramDestroyEvent2](../../extensibility/debugger/reference/idebugprogramdestroyevent2.md)を送信します。

   IDE がデザインモードになります。 デバッグエンジンまたはランタイム環境は、 [IDebugPortNotify2:: RemoveProgramNode](../../extensibility/debugger/reference/idebugportnotify2-removeprogramnode.md) を呼び出して、ポートからプログラムを削除します。

## <a name="see-also"></a>こちらもご覧ください
- [呼び出し (デバッガーイベントを)](../../extensibility/debugger/calling-debugger-events.md)
