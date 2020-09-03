---
title: プロセス |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], processes
ms.assetid: a6a1efdc-b243-40c8-a778-6f69f6b018be
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 392c59b90bb117dded0f528bc33a617370b091a7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80738240"
---
# <a name="processes"></a>処理
デバッガーのアーキテクチャでは、 *プロセス*は次のようになります。

- は、一連のプログラムのコンテナーです。 これは、スレッドのセットのコンテナーである Windows プロセスによく似ています。

- 名前、識別子、または物理識別子を使用して識別できます。

- 実行中のすべてのプログラム (およびそのスレッド) を列挙できます。

- 自体、それが実行されているポート、およびそれを含むコンピューターを記述できます。

- 1つまたは複数のプログラムを作成したり、作成したプログラムを終了したり、プログラムを停止させたりすることができます。

- は、プロセスの起動時に作成される [IDebugProcess2](../../extensibility/debugger/reference/idebugprocess2.md) インターフェイスによって表されます。 プロセスは、セッションデバッグマネージャー (SDM) または [Launchsuspended](../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)のいずれかによって起動されます。

  デバッグパッケージは、 [attach](../../extensibility/debugger/reference/idebugprocess2-attach.md)を呼び出すことによってプロセスにデバッグエンジン (de) をアタッチできます。これは、処理可能なプロセスで実行されているすべてのプログラムに、de がアタッチされることを意味します。 たとえば、共通言語ランタイムがプロセスにアタッチされていない場合は、マネージコードを実行しているプログラムのみにアタッチされます。

## <a name="see-also"></a>関連項目
- [Programs](../../extensibility/debugger/programs.md)
- [スレッド](../../extensibility/debugger/threads.md)
- [デバッガーの概念](../../extensibility/debugger/debugger-concepts.md)
- [パッケージのデバッグ](../../extensibility/debugger/debug-package.md)
- [デバッグエンジン](../../extensibility/debugger/debug-engine.md)
- [IDebugProcess2](../../extensibility/debugger/reference/idebugprocess2.md)
- [LaunchSuspended](../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)
- [[アタッチ]](../../extensibility/debugger/reference/idebugprocess2-attach.md)
