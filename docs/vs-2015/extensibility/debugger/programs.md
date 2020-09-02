---
title: プログラム |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], programs
- programs, debugging
ms.assetid: e1f955d8-95da-493b-837e-e97741a26d7e
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 9070b33c7522cdc13fd6217956fcab72cd83f8d1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68153645"
---
# <a name="programs"></a>プログラム
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

デバッガーアーキテクチャに関して、 **プログラム**は次のようになります。  
  
- は、一連のスレッドと一連のモジュールの両方のコンテナーです。 プログラムには、Windows オペレーティングシステムに1つの例えがありません。  
  
     プログラムは一種のサブプロセスです。 たとえば、Web サイトをデバッグするときに、スクリプトをプログラムとして表示できます。 スクリプトは、他のスクリプトに依存せずにスクリプトエンジンプロセスで実行されますが、独自のスレッドセットも持っています。 デバッグエンジン (DE) は、プロセスやスレッドではなく、プログラムにアタッチします。  
  
- は、自身と、それが実行されているプロセスを識別できます。また、アタッチしてからデタッチし、それを作成した DE (存在する場合) を記述することもできます。 プログラムは、実行、停止、続行、および終了することができます。  
  
- すべてのスレッドを列挙できます。 プログラムは、独自の逆アセンブリストリームを提供し、特定のドキュメント位置のすべてのコードコンテキストを列挙することもできます。  
  
- は、実装に応じて、プログラムがアタッチされる前、またはアタッチプロセスの一部として作成される [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md) インターフェイスによって表されます。 ポートがプロセスのプログラムを列挙すると、各プログラムは、 [Addprogramnode](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md)に引数として渡される対応する[IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)インターフェイスに従って作成されます。 デバッグエンジンも `IDebugProgram2` プログラムを表すインターフェイスを作成しますが、これらのプログラムはプログラムノードに従って作成されません。 `IDebugProgramNode2`DE によって作成されたインターフェイスは実際のデバッグに使用されますが、ポートによって作成されたインターフェイスは、プロセスで実行されているプログラムを検出するためにのみ使用されます。  
  
## <a name="see-also"></a>参照  
 [プロセス](../../extensibility/debugger/processes.md)   
 [プログラムノード](../../extensibility/debugger/program-nodes.md)   
 [モジュール](../../extensibility/debugger/modules.md)   
 [デバッガーの概念](../../extensibility/debugger/debugger-concepts.md)   
 [デバッグエンジン](../../extensibility/debugger/debug-engine.md)   
 [ドキュメントの位置](../../extensibility/debugger/document-position.md)   
 [コードコンテキスト](../../extensibility/debugger/code-context.md)   
 [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)   
 [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)   
 [AddProgramNode](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md)
