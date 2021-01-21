---
title: Threads |Microsoft Docs
description: この記事では、Visual Studio のデバッガーアーキテクチャにおけるスレッドの定義とロールについて説明します。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: b259ffd7814b42145489ee5990cee6da891a9d10
ms.sourcegitcommit: d10f37dfdba5d826e7451260c8370fd1efa2c4e4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2020
ms.locfileid: "96995955"
---
# <a name="threads"></a>スレッド
デバッガーアーキテクチャでは、 *スレッド* は次のようになります。

- は計算の基本単位です。 スレッドは、単一の呼び出し履歴のコンテキスト内で命令を順番に実行し、1つのコードコンテキストから次のコンテキストに移動します。

- は、自身とそれが実行されているプログラムを識別できます。 スレッドには名前を付け、中断し、再開することができます。 スレッドは、関連付けられているスタックフレームを列挙することもできます。また、状況によっては、別のスタックフレームに移動できます。 スタックフレームのコンテキストが指定されている場合、スレッドは、関連付けられている論理スレッド (存在する場合) を返すことができます。 スレッドには、IDE の [ **スレッド** ] ウィンドウに表示できる、中断カウントなどのプロパティがあります。

- は [IDebugThread2](../../extensibility/debugger/reference/idebugthread2.md) インターフェイスによって表されます。通常は、プログラムを実行した結果として、デバッグエンジン (DE) または仮想マシンによって作成されます。

## <a name="see-also"></a>こちらもご覧ください
- [Programs](../../extensibility/debugger/programs.md)
- [スタックフレーム](../../extensibility/debugger/stack-frames.md)
- [デバッグエンジン](../../extensibility/debugger/debug-engine.md)
- [デバッガーの概念](../../extensibility/debugger/debugger-concepts.md)
- [セッションデバッグマネージャー](../../extensibility/debugger/session-debug-manager.md)
