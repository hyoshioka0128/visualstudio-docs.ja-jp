---
title: デバッガーイベントの呼び出し |Microsoft Docs
description: デバッグセッションのイベントは、特定の順序で発生します。 この記事では、一般的なデバッグセッションで発生するイベントの呼び出し順序を示します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- debugging [Debugging SDK], events
ms.assetid: b3440ac3-80af-40c6-bef4-cbf00fa67885
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 832b42e62731a087048b4aa50e19b74c408343c5
ms.sourcegitcommit: 8e9c38da7bcfbe9a461c378083846714933a0e1e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/09/2020
ms.locfileid: "96914389"
---
# <a name="call-debugger-events"></a>デバッガーイベントの呼び出し
デバッグセッションのイベントは、特定の順序で発生します。

## <a name="discussion"></a>ディスカッション
 デバッグエンジン (DE) とセッションデバッグマネージャー (SDM) との間の呼び出しのパターンを理解するために、一般的なデバッグセッションで発生するイベントの呼び出し順序を次に示します。

1. [プログラムへのアタッチとデタッチ](../../extensibility/debugger/attaching-and-detaching-to-a-program.md)

2. [デバッガーを起動しています](../../extensibility/debugger/launching-the-debugger.md)

3. [プログラムを終了する](../../extensibility/debugger/terminating-a-program.md)

4. [ブレークポイントの作成](../../extensibility/debugger/creating-a-breakpoint.md)

5. [ブレークポイントがバインドまたはバインド解除するとき](../../extensibility/debugger/when-a-breakpoint-binds-or-becomes-unbound.md)

6. [ブレークポイントエラー](../../extensibility/debugger/breakpoint-errors.md)

7. [Hitting a breakpoint](../../extensibility/debugger/hitting-a-breakpoint.md)

8. [ブレークポイントの削除](../../extensibility/debugger/deleting-a-breakpoint.md)

9. [中断モードに入る](../../extensibility/debugger/entering-break-mode.md)

10. [中断モードでのステップ実行](../../extensibility/debugger/stepping-in-break-mode.md)

11. [中断モードでの式の評価](../../extensibility/debugger/expression-evaluation-in-break-mode.md)

12. [例外処理](../../extensibility/debugger/exception-handling-visual-studio-sdk.md)

## <a name="see-also"></a>関連項目
- [カスタムデバッグエンジンの作成](../../extensibility/debugger/creating-a-custom-debug-engine.md)
