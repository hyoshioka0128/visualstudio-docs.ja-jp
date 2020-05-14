---
title: デバッガ イベントの呼び出し |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], events
ms.assetid: b3440ac3-80af-40c6-bef4-cbf00fa67885
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 869bd87952aebf8ad640c5aeb439c9e99929f4c1
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739167"
---
# <a name="call-debugger-events"></a>デバッガー イベントの呼び出し
デバッグ セッションのイベントは、特定の順序で発生します。

## <a name="discussion"></a>ディスカッション
 デバッグ エンジン (DE) とセッション デバッグ マネージャー (SDM) 間の呼び出しのパターンを理解するために、次は、一般的なデバッグ セッションで発生するイベントの呼び出し順序を表します。

1. [プログラムへのアタッチとデタッチ](../../extensibility/debugger/attaching-and-detaching-to-a-program.md)

2. [デバッガの起動](../../extensibility/debugger/launching-the-debugger.md)

3. [プログラムの終了](../../extensibility/debugger/terminating-a-program.md)

4. [ブレークポイントの作成](../../extensibility/debugger/creating-a-breakpoint.md)

5. [ブレークポイントがバインドまたはバインド解除されるとき](../../extensibility/debugger/when-a-breakpoint-binds-or-becomes-unbound.md)

6. [ブレークポイント エラー](../../extensibility/debugger/breakpoint-errors.md)

7. [Hitting a breakpoint](../../extensibility/debugger/hitting-a-breakpoint.md)

8. [ブレークポイントの削除](../../extensibility/debugger/deleting-a-breakpoint.md)

9. [ブレーク モードに入る](../../extensibility/debugger/entering-break-mode.md)

10. [中断モードでのステップ実行](../../extensibility/debugger/stepping-in-break-mode.md)

11. [ブレークモードでの式評価](../../extensibility/debugger/expression-evaluation-in-break-mode.md)

12. [例外処理](../../extensibility/debugger/exception-handling-visual-studio-sdk.md)

## <a name="see-also"></a>関連項目
- [カスタム デバッグ エンジンの作成](../../extensibility/debugger/creating-a-custom-debug-engine.md)
