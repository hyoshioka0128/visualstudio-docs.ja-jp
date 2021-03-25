---
title: プロセス |Microsoft Docs
description: この記事では、Visual Studio のデバッガーアーキテクチャにおけるプロセスの定義とロールについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], processes
ms.assetid: a6a1efdc-b243-40c8-a778-6f69f6b018be
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 46e25ddfbe60e1b9ee456e586c6f424fc489f626
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105067713"
---
# <a name="processes"></a>プロセス
デバッガーのアーキテクチャでは、 *プロセス* は次のようになります。

- は、一連のプログラムのコンテナーです。 これは、スレッドのセットのコンテナーである Windows プロセスによく似ています。

- 名前、識別子、または物理識別子を使用して識別できます。

- 実行中のすべてのプログラム (およびそのスレッド) を列挙できます。

- 自体、それが実行されているポート、およびそれを含むコンピューターを記述できます。

- 1つまたは複数のプログラムを作成したり、作成したプログラムを終了したり、プログラムを停止させたりすることができます。

- は、プロセスの起動時に作成される [IDebugProcess2](../../extensibility/debugger/reference/idebugprocess2.md) インターフェイスによって表されます。 プロセスは、セッションデバッグマネージャー (SDM) または [Launchsuspended](../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)のいずれかによって起動されます。

  デバッグパッケージは、 [attach](../../extensibility/debugger/reference/idebugprocess2-attach.md)を呼び出すことによってプロセスにデバッグエンジン (de) をアタッチできます。これは、処理可能なプロセスで実行されているすべてのプログラムに、de がアタッチされることを意味します。 たとえば、共通言語ランタイムがプロセスにアタッチされていない場合は、マネージコードを実行しているプログラムのみにアタッチされます。

## <a name="see-also"></a>こちらもご覧ください
- [Programs](../../extensibility/debugger/programs.md)
- [スレッド](../../extensibility/debugger/threads.md)
- [デバッガーの概念](../../extensibility/debugger/debugger-concepts.md)
- [パッケージのデバッグ](../../extensibility/debugger/debug-package.md)
- [デバッグエンジン](../../extensibility/debugger/debug-engine.md)
- [IDebugProcess2](../../extensibility/debugger/reference/idebugprocess2.md)
- [LaunchSuspended](../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)
- [[アタッチ]](../../extensibility/debugger/reference/idebugprocess2-attach.md)
