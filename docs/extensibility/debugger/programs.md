---
title: プログラム |Microsoft Docs
description: この記事では、Visual Studio のデバッガーアーキテクチャにおけるプログラムの定義とロールについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], programs
- programs, debugging
ms.assetid: e1f955d8-95da-493b-837e-e97741a26d7e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 0769d2abc650305095115d1c645e3037096974de
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105094615"
---
# <a name="programs"></a>プログラム
デバッガーアーキテクチャでは、 *プログラム* は次のようになります。

- は、一連のスレッドと一連のモジュールの両方のコンテナーです。 プログラムには、Windows オペレーティングシステムに1つの例えがありません。

     プログラムは一種のサブプロセスです。 たとえば、Web サイトをデバッグするときに、スクリプトをプログラムとして表示できます。 スクリプトは、他のスクリプトに依存せずにスクリプトエンジンプロセスで実行されますが、独自のスレッドセットも持っています。 デバッグエンジン (DE) は、プロセスやスレッドではなく、プログラムにアタッチします。

- は、自身と、それが実行されているプロセスを識別できます。 プログラムをにアタッチしてからデタッチし、それを作成した DE を記述します (存在する場合)。 プログラムは、実行、停止、続行、および終了することもできます。

- すべてのスレッドを列挙できます。 プログラムは、独自の逆アセンブリストリームを提供し、特定のドキュメント位置のすべてのコードコンテキストを列挙することもできます。

- は、実装に応じて、プログラムがアタッチされる前、またはアタッチプロセスの一部として作成される [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md) インターフェイスによって表されます。 ポートがプロセスのプログラムを列挙すると、各プログラムは、 [Addprogramnode](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md)に引数として渡される対応する[IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)インターフェイスに従って作成されます。 デバッグエンジンも `IDebugProgram2` プログラムを表すインターフェイスを作成しますが、これらのプログラムはプログラムノードに従って作成されません。 `IDebugProgramNode2`DE によって作成されたインターフェイスは実際のデバッグに使用されますが、ポートによって作成されたインターフェイスは、プロセスで実行されているプログラムを検出するためにのみ使用されます。

## <a name="see-also"></a>こちらもご覧ください
- [プロセス](../../extensibility/debugger/processes.md)
- [プログラムノード](../../extensibility/debugger/program-nodes.md)
- [モジュール](../../extensibility/debugger/modules.md)
- [デバッガーの概念](../../extensibility/debugger/debugger-concepts.md)
- [デバッグエンジン](../../extensibility/debugger/debug-engine.md)
- [ドキュメントの位置](../../extensibility/debugger/document-position.md)
- [コードコンテキスト](../../extensibility/debugger/code-context.md)
- [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)
- [AddProgramNode](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md)
