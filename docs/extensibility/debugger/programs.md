---
title: プログラム |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], programs
- programs, debugging
ms.assetid: e1f955d8-95da-493b-837e-e97741a26d7e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d3fd1db5add74d2d94467e1f369916feb5f30d4a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738210"
---
# <a name="programs"></a>プログラム
デバッガアーキテクチャでは、*プログラム*:

- スレッドのセットとモジュールのセットの両方のコンテナーです。 Windows オペレーティング システムでは、プログラムに単一のたとえはありません。

     プログラムはサブプロセスの一種です。 たとえば、Web サイトをデバッグする場合、スクリプトはプログラムとして見ることができます。 スクリプトは、他のスクリプトとは無関係にスクリプト エンジン プロセスで実行されますが、スレッドの独自のセットもあります。 デバッグ エンジン (DE) は、プロセスまたはスレッドではなく、プログラムにアタッチします。

- 自分自身とそれが実行されているプロセスを識別できます。 プログラムをアタッチしたり、プログラムを作成した DE にデタッチしたり、記述したりすることもできます。 プログラムは、実行、停止、続行、および終了することもできます。

- すべてのスレッドを列挙できます。 プログラムは独自の逆アセンブリ ストリームを提供することもでき、特定のドキュメント位置のすべてのコード コンテキストを列挙できます。

- [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)インターフェイスによって表され、プログラムがアタッチされる前に作成されるか、実装に応じてアタッチ プロセスの一部として作成されます。 ポートがプロセスのプログラムを列挙すると、各プログラムは、引数として渡された対応する[IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)インターフェイスに従って作成[AddProgramNode](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md)されます。 デバッグ エンジンはプログラム`IDebugProgram2`を表すインターフェイスも作成しますが、これらのプログラムはプログラム ノードに従って作成されません。 DE`IDebugProgramNode2`によって作成されたインターフェイスは実際のデバッグに使用され、ポートによって作成されたインターフェイスはプロセスで実行されているプログラムを検出するためだけに使用されます。

## <a name="see-also"></a>関連項目
- [プロセス](../../extensibility/debugger/processes.md)
- [プログラムノード](../../extensibility/debugger/program-nodes.md)
- [モジュール](../../extensibility/debugger/modules.md)
- [デバッガーの概念](../../extensibility/debugger/debugger-concepts.md)
- [デバッグ エンジン](../../extensibility/debugger/debug-engine.md)
- [ドキュメントの位置](../../extensibility/debugger/document-position.md)
- [コード コンテキスト](../../extensibility/debugger/code-context.md)
- [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)
- [AddProgramNode](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md)
