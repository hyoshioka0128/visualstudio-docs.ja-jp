---
title: プログラムを終了する |マイクロソフトドキュメント
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
ms.openlocfilehash: 985b20fe75f8ceee3d434ac681b437c51baf85e8
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80712521"
---
# <a name="terminating-a-program"></a>プログラムの終了
次のセクションでは、1 つのスレッドを使用した単一のプログラムの終了について説明します。

## <a name="termination-process"></a>終了プロセス

1. デは、有効な[IDebugThread2](../../extensibility/debugger/reference/idebugthreaddestroyevent2.md)を使用して[IDebug スレッドデストロイイベント2](../../extensibility/debugger/reference/idebugthread2.md)を送信します。

2. デは、有効な[IDebugProgram2](../../extensibility/debugger/reference/idebugprogramdestroyevent2.md)を使用して[IDebug プログラムデストロイイベント2 を](../../extensibility/debugger/reference/idebugprogram2.md)送信します。

   IDE はデザイン モードに入ります。 デバッグ エンジンまたはランタイム環境は、ポートからプログラムを削除する[IDebugPortNotify2::RemoveProgramNode](../../extensibility/debugger/reference/idebugportnotify2-removeprogramnode.md)を呼び出します。

## <a name="see-also"></a>関連項目
- [デバッガ イベントの呼び出し](../../extensibility/debugger/calling-debugger-events.md)
