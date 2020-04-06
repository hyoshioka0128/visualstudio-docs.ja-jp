---
title: プロセス |マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738240"
---
# <a name="processes"></a>処理
デバッガアーキテクチャでは、*プロセス*:

- プログラムのセットのコンテナーです。 これは、スレッドのセットのコンテナーである Windows プロセスとよく似ています。

- 名前、識別子、または物理識別子で自分自身を識別できます。

- 実行中のすべてのプログラム (およびそのスレッド) を列挙できます。

- 自分自身、それが実行されているポート、およびそれを含むマシンを記述できます。

- 1 つ以上のプログラムを作成したり、プログラムを終了したり、プログラムを停止したりします。

- プロセスが起動されたときに作成される[IDebugProcess2](../../extensibility/debugger/reference/idebugprocess2.md)インターフェイスによって表されます。 プロセスは、セッション デバッグ マネージャー (SDM) または[LaunchSuspended](../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)によって起動されます。

  デバッグ パッケージは[、Attach](../../extensibility/debugger/reference/idebugprocess2-attach.md)を呼び出すことによってプロセスにデバッグ エンジン (DE) をアタッチできます。 たとえば、共通言語ランタイム DE がプロセスにアタッチする場合、マネージ コードを実行しているプログラムにのみアタッチされます。

## <a name="see-also"></a>関連項目
- [Programs](../../extensibility/debugger/programs.md)
- [スレッド](../../extensibility/debugger/threads.md)
- [デバッガーの概念](../../extensibility/debugger/debugger-concepts.md)
- [デバッグ パッケージ](../../extensibility/debugger/debug-package.md)
- [デバッグ エンジン](../../extensibility/debugger/debug-engine.md)
- [IDebugProcess2](../../extensibility/debugger/reference/idebugprocess2.md)
- [LaunchSuspended](../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)
- [Attach](../../extensibility/debugger/reference/idebugprocess2-attach.md)
