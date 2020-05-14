---
title: プログラムノード |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- program nodes, debugging context
- debugging [Debugging SDK], program nodes
- program nodes, adding
- program nodes, superceding
ms.assetid: 1c5a5c13-c14d-42c3-af11-4c63f1032c8d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2943f74c7316495be93c2f5c20998ffa685f5d01
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738219"
---
# <a name="program-nodes"></a>プログラムノード
デバッガアーキテクチャでは、*プログラムノード*:

- プログラムの軽量説明です。

- 自分自身とそれが実行されているプロセスを識別できます。 プログラム ノードは、アタッチ、デタッチ、およびデバッグ エンジン (存在する場合) を作成したデバッグ エンジン (DE) を記述できます。

- 通常は DE またはポートによって作成される[IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)インターフェイスによって表されます。 プログラム ノードは[、AddProgramNode](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md)を呼び出すことによってポートに追加されます。 プログラム ノードがポートに追加されると、このプログラム ノードが表すプログラムを含むプロセスに追加されます。

  デバッグ・セッションが開始された後、デバッグ・パッケージの実装に応じて、プログラム・ノードを使用して対応するプログラムが作成されます。 プロセスがプログラムに対して照会されると、プログラムはプログラム ノードごとに 1 つずつ列挙されます。

  プログラムがアタッチされる前に、IDE はプログラムの軽量説明のみを必要とします。 この情報はプログラム・ノードから取得できます。 プログラムがアタッチされると、IDE は、プログラムで実行されているすべてのスレッドの一覧など、より詳細な情報を表示します。 この情報はプログラム自体から取得されます。

## <a name="see-also"></a>関連項目
- [Programs](../../extensibility/debugger/programs.md)
- [プロセス](../../extensibility/debugger/processes.md)
- [デバッグ エンジン](../../extensibility/debugger/debug-engine.md)
- [デバッガーの概念](../../extensibility/debugger/debugger-concepts.md)
- [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)
- [AddProgramNode](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md)
