---
title: 割り当てフック関数 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.hooks
dev_langs:
- FSharp
- VB
- CSharp
- C++
- C++
helpviewer_keywords:
- memory allocation, logging allocation information
- insufficient memory
- debugging [C++], hook functions
- _CrtSetAllocHook function
- allocation hooks
- hooks, allocation
ms.assetid: 6bfbdb65-8cb1-4c21-8c45-7194a2b77c1e
caps.latest.revision: 17
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 81135546ffa208a4efb96569cd7968dfe560cdf9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65702519"
---
# <a name="allocation-hook-functions"></a>割り当てフック関数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[_CrtSetAllocHook](https://msdn.microsoft.com/library/405df37b-2fd1-42c8-83bc-90887f17f29d)を使用してインストールされた割り当てフック関数は、メモリの割り当て、再割り当て、または解放のたびに呼び出されます。 この種のフック関数はさまざまな目的に利用できます。 たとえば、メモリ不足の状態でアプリケーションの動作をテストしたり、割り当てパターンを調査したり、後から分析するために割り当て情報を記録したりなどの目的に利用できます。  
  
> [!NOTE]
> 割り当てフック関数の中で C ランタイム ライブラリの関数を使用する場合は、「[割り当てフック関数と C ランタイムのメモリ割り当て](../debugger/allocation-hooks-and-c-run-time-memory-allocations.md)」で説明する制限事項があるので注意してください。  
  
 割り当て用のフック関数には、次のようなプロトタイプが必要です。  
  
```  
int YourAllocHook(int nAllocType, void *pvData,  
        size_t nSize, int nBlockUse, long lRequest,  
        const unsigned char * szFileName, int nLine )  
```  
  
 [_CrtSetAllocHook](https://msdn.microsoft.com/library/405df37b-2fd1-42c8-83bc-90887f17f29d) に渡すポインターは **_CRT_ALLOC_HOOK** 型です。これらは、CRTDBG.H で次のように定義されています。  
  
```  
typedef int (__cdecl * _CRT_ALLOC_HOOK)  
    (int, void *, size_t, int, long, const unsigned char *, int);  
```  
  
 ランタイムライブラリがフックを呼び出すと、 *Nalloctype* 引数は、実行される割り当て操作 (**_HOOK_ALLOC**、 **_HOOK_REALLOC**、または **_HOOK_FREE**) を示します。 メモリの解放または再割り当ての場合、引数 `pvData` には、解放されるブロックへのポインターが格納されます。 一方、割り当ての場合は、まだ割り当てが行われていないため、このポインターは null になります。 その他の引数には、必要に応じて、対象ブロックの割り当てサイズ、ブロック型、順番に付けられた割り当て要求番号、割り当てが行われた場所のファイル名と行番号へのポインターが格納されます。 フック関数は、分析などの必要なタスクを実行した後で、割り当て処理を継続できる場合は **TRUE**、継続できない場合は **FALSE** を返すようにします。 この種のフック関数の簡単なものとしては、それまでに割り当てられたメモリの総量をチェックし、その量が少なめに設定した上限を超えている場合は **FALSE** を返す関数が考えられます。 この関数を使用すると、メモリがかなり不足している場合だけに発生するメモリ割り当てエラーを意図的に発生させることができます。 さらに複雑なフック関数としては、割り当てパターンを追跡したり、メモリの使用状況を分析したり、特定の状態が発生したときにレポートを作成したりする関数が考えられます。  
  
## <a name="see-also"></a>参照  
 [割り当てフックと C ランタイムのメモリ割り当て](../debugger/allocation-hooks-and-c-run-time-memory-allocations.md)   
 [デバッグ用フック関数の作成](../debugger/debug-hook-function-writing.md)   
 [crt_dbg2 のサンプル](https://msdn.microsoft.com/21e1346a-6a17-4f57-b275-c76813089167)
