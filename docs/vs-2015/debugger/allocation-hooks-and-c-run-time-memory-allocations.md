---
title: 割り当てフック関数と C ランタイムのメモリ割り当て | Microsoft Docs
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
- debugging [C++], hook functions
- memory allocation, troubleshooting allocation hooks
- allocation hooks
- hooks, allocation
ms.assetid: cc34ee96-3d91-41bd-a019-aa3759139e7e
caps.latest.revision: 17
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 8487972c237b9c2ba6bf2594ffc1df43fa0c63cd
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65702437"
---
# <a name="allocation-hooks-and-c-run-time-memory-allocations"></a>割り当てフック関数と C ランタイムのメモリ割り当て
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

メモリ割り当て用のフック関数には重要な制限事項があります。それは、メモリを内部的に割り当てるタイプの C ランタイム ライブラリ関数をフック関数から呼び出す場合、`_CRT_BLOCK` 型のブロック (C ランタイム ライブラリ関数によって内部的に割り当てられるメモリ) を明示的に無視する必要があることです。 割り当て用のフック関数の先頭に次のようなコードを追加すると、`_CRT_BLOCK` 型のブロックを無視できます。  
  
```  
if ( nBlockUse == _CRT_BLOCK )  
    return( TRUE );  
```  
  
 割り当て用のフック関数で `_CRT_BLOCK` 型のブロックを無視しないと、このフック関数から C ランタイム ライブラリ関数を呼び出した場合に、プログラムが無限ループに陥ることがあります。 たとえば、`printf` は内部的にメモリを割り当てます。 フックコードがを呼び出すと、結果として得られる割り当てによってフックが再び呼び出されます。これにより、再び `printf` **printf** が呼び出されます。これは、スタックがオーバーフローするまで続きます。 `_CRT_BLOCK` 型の割り当て処理をレポートする必要がある場合は、この制限事項を回避するために、C ランタイム関数ではなく Windows API 関数を使用して書式設定や出力を行う方法があります。 Windows API は C ランタイム ライブラリのヒープを使用しないため、割り当て用のフック関数を使用しても無限ループに陥る心配はありません。  
  
 ランタイム ライブラリのソース ファイルを調べる場合、既定の割り当て用のフック関数 **CrtDefaultAllocHook** (これは単に **TRUE** を返します) が独自の個別のファイル (DBGHOOK.C) の中にあることがわかります。 アプリケーションの **main** 関数の前に実行されるランタイムのスタートアップ コードによる割り当て時にも割り当てのフックが呼び出されるようにするには、[_CrtSetAllocHook](https://msdn.microsoft.com/library/405df37b-2fd1-42c8-83bc-90887f17f29d) を使用する代わりに、この既定の関数を独自の関数に置き換えることができます。  
  
## <a name="see-also"></a>参照  
 [デバッグ用フック関数の作成](../debugger/debug-hook-function-writing.md)   
 [crt_dbg2 のサンプル](https://msdn.microsoft.com/21e1346a-6a17-4f57-b275-c76813089167)
