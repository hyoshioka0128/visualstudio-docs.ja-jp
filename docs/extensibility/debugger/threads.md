---
title: スレッド |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], threads
- threading [Debugging SDK]
ms.assetid: 2243d24a-c3d2-41d1-abbb-6db21a2db9ee
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8ed5c06e0c42dac1f0539cc2c7c5886d95b23ae1
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80712479"
---
# <a name="threads"></a>Threads
デバッガアーキテクチャでは、*スレッド*:

- 計算の基本単位です。 スレッドは、1 つのコード コンテキストから次のコード コンテキストに移動して、1 つの呼び出し履歴のコンテキスト内で命令を順番に実行します。

- 自分自身と、それが実行されているプログラムを識別できます。 スレッドは、名前付け、中断、および再開が可能です。 スレッドは、関連付けられたスタック フレームを列挙することもでき、状況によっては、別のスタック フレームに移動することもできます。 スタック フレームのコンテキストを指定すると、スレッドは関連付けられている論理スレッドがあれば、その論理スレッドを返すことができます。 スレッドには、IDE の「**スレッド」** ウィンドウに表示できる、中断カウントなどのプロパティーがあります。

- 通常はプログラムの実行の結果としてデバッグ エンジン (DE) または仮想マシンによって作成される[IDebugThread2](../../extensibility/debugger/reference/idebugthread2.md)インターフェイスによって表されます。

## <a name="see-also"></a>関連項目
- [Programs](../../extensibility/debugger/programs.md)
- [スタック フレーム](../../extensibility/debugger/stack-frames.md)
- [デバッグ エンジン](../../extensibility/debugger/debug-engine.md)
- [デバッガーの概念](../../extensibility/debugger/debugger-concepts.md)
- [セッション デバッグ マネージャー](../../extensibility/debugger/session-debug-manager.md)
