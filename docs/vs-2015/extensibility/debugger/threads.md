---
title: Threads |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], threads
- threading [Debugging SDK]
ms.assetid: 2243d24a-c3d2-41d1-abbb-6db21a2db9ee
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 028ad25495ba01d9763c8bec3bbb9c4480d72ff8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68185355"
---
# <a name="threads"></a>Threads
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

デバッガーアーキテクチャに関して、 **スレッド**は次のようになります。  
  
- は計算の基本単位です。 スレッドは、単一の呼び出し履歴のコンテキスト内で命令を順番に実行し、1つのコードコンテキストから次のコンテキストに移動します。  
  
- は、自身とそれが実行されているプログラムを識別できます。また、名前を付けて、中断し、再開することができます。 スレッドは、関連付けられているスタックフレームを列挙することもできます。また、状況によっては、別のスタックフレームに移動できます。 スタックフレームのコンテキストが指定されている場合、スレッドは、関連付けられている論理スレッド (存在する場合) を返すことができます。 スレッドには、IDE の [スレッド] ウィンドウに表示できる、中断カウントなどのプロパティがあります。  
  
- は [IDebugThread2](../../extensibility/debugger/reference/idebugthread2.md) インターフェイスによって表されます。通常は、プログラムを実行した結果として、デバッグエンジン (DE) または仮想マシンによって作成されます。  
  
## <a name="see-also"></a>参照  
 [プログラム](../../extensibility/debugger/programs.md)   
 [スタックフレーム](../../extensibility/debugger/stack-frames.md)   
 [デバッグエンジン](../../extensibility/debugger/debug-engine.md)   
 [デバッガーの概念](../../extensibility/debugger/debugger-concepts.md)   
 [セッション デバッグ マネージャー](../../extensibility/debugger/session-debug-manager.md)
