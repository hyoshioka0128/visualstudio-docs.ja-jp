---
title: プロセス |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], processes
ms.assetid: a6a1efdc-b243-40c8-a778-6f69f6b018be
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 82718a7ceb7a18f9978840f35ca0c5fce5628e81
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68153666"
---
# <a name="processes"></a>処理
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

デバッガーのアーキテクチャに関しては、次のような **プロセス**があります。  
  
- は、一連のプログラムのコンテナーです。 これは、スレッドのセットのコンテナーである Windows プロセスによく似ています。  
  
- 名前、識別子、または物理識別子を使用して識別できます。  
  
- 実行中のすべてのプログラム (およびそのスレッド) を列挙できます。  
  
- 自体、それが実行されているポート、およびそれを含むコンピューターを記述できます。  
  
- 1つまたは複数のプログラムを作成したり、作成したプログラムを終了したり、プログラムを停止させたりすることができます。  
  
- は、プロセスの起動時に作成される [IDebugProcess2](../../extensibility/debugger/reference/idebugprocess2.md) インターフェイスによって表されます。 プロセスは、セッションデバッグマネージャー (SDM) または [Launchsuspended](../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)のいずれかによって起動されます。  
  
  デバッグパッケージは、 [attach](../../extensibility/debugger/reference/idebugprocess2-attach.md)を呼び出すことにより、デバッグエンジン (DE) をプロセスにアタッチできます。 これは、処理可能なプロセスで実行されているすべてのプログラムに、DE がアタッチされることを意味します。 たとえば、共通言語ランタイムがプロセスにアタッチされていない場合は、マネージコードを実行しているプログラムのみにアタッチされます。  
  
## <a name="see-also"></a>参照  
 [プログラム](../../extensibility/debugger/programs.md)   
 [レッド](../../extensibility/debugger/threads.md)   
 [デバッガーの概念](../../extensibility/debugger/debugger-concepts.md)   
 [パッケージのデバッグ](../../extensibility/debugger/debug-package.md)   
 [デバッグエンジン](../../extensibility/debugger/debug-engine.md)   
 [IDebugProcess2](../../extensibility/debugger/reference/idebugprocess2.md)   
 [LaunchSuspended](../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)   
 [[アタッチ]](../../extensibility/debugger/reference/idebugprocess2-attach.md)
