---
title: プログラムノード |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80738219"
---
# <a name="program-nodes"></a>プログラムノード
デバッガーアーキテクチャでは、 *プログラムノード*は次のようになります。

- は、プログラムの簡易な説明です。

- は、自身と、それが実行されているプロセスを識別できます。 プログラムノードをアタッチしてからデタッチし、それを作成したデバッグエンジン (DE) を記述することができます (存在する場合)。

- は、通常、DE またはポートによって作成される [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md) インターフェイスによって表されます。 プログラムノードは、 [Addprogramnode](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md)を呼び出すことによってポートに追加されます。 プログラムノードがポートに追加されると、このプログラムノードが表すプログラムを含むプロセスに追加されます。

  デバッグセッションの開始後、デバッグパッケージの実装によっては、プログラムノードを使用して対応するプログラムが作成されます。 プログラムのプロセスが照会されると、プログラムが列挙されます。プログラムノードごとに1つのプログラムが列挙されます。

  プログラムをにアタッチする前に、IDE には、プログラムの簡易記述のみが必要です。 この情報は、プログラムノードから取得できます。 プログラムがにアタッチされると、IDE では、プログラムで実行されているすべてのスレッドの一覧など、より詳細な情報が表示されます。 この情報は、プログラム自体から取得されます。

## <a name="see-also"></a>関連項目
- [Programs](../../extensibility/debugger/programs.md)
- [処理](../../extensibility/debugger/processes.md)
- [デバッグエンジン](../../extensibility/debugger/debug-engine.md)
- [デバッガーの概念](../../extensibility/debugger/debugger-concepts.md)
- [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)
- [AddProgramNode](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md)
