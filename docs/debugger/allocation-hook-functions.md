---
title: 割り当てフック関数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.debug.hooks
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- memory allocation, logging allocation information
- insufficient memory
- debugging [C++], hook functions
- _CrtSetAllocHook function
- allocation hooks
- hooks, allocation
ms.assetid: 6bfbdb65-8cb1-4c21-8c45-7194a2b77c1e
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f684c6c66448fdab2ee7607a81ff7ed769a5e607
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72745818"
---
# <a name="allocation-hook-functions"></a>割り当てフック関数
[_CrtSetAllocHook](/cpp/c-runtime-library/reference/crtsetallochook)を使用してインストールされた割り当てフック関数は、メモリの割り当て、再割り当て、または解放のたびに呼び出されます。 この種類のフックは、さまざまな目的で使用できます。 これを使用して、アプリケーションがメモリ不足の状況をどのように処理するかをテストします。たとえば、割り当てパターンを調べる場合や、後で分析するためのログ割り当て情報を記録する場合です。

> [!NOTE]
> 割り当てフック関数の中で C ランタイム ライブラリの関数を使用する場合は、「[割り当てフック関数と C ランタイムのメモリ割り当て](../debugger/allocation-hooks-and-c-run-time-memory-allocations.md)」で説明する制限事項があるので注意してください。

 割り当て用のフック関数には、次の例のようなプロトタイプが必要です。

```cpp
int YourAllocHook(int nAllocType, void *pvData,
        size_t nSize, int nBlockUse, long lRequest,
        const unsigned char * szFileName, int nLine )
```

 [_CrtSetAllocHook](/cpp/c-runtime-library/reference/crtsetallochook) に渡すポインターは **_CRT_ALLOC_HOOK** 型です。これらは、CRTDBG.H で次のように定義されています。

```cpp
typedef int (__cdecl * _CRT_ALLOC_HOOK)
    (int, void *, size_t, int, long, const unsigned char *, int);
```

 ランタイムライブラリがフックを呼び出すと、 *Nalloctype*引数によって、実行される割り当て操作 ( **_HOOK_ALLOC**、 **_HOOK_REALLOC**、または **_HOOK_FREE**) が示されます。 無料または再割り当ての場合、`pvData` には、解放されるブロックのユーザーアーティクルへのポインターがあります。 ただし、割り当ての場合、割り当てが行われていないため、このポインターは null になります。 残りの引数には、対象の割り当てのサイズ、ブロックの種類、関連付けられている順次要求番号、およびファイル名へのポインターが含まれます。 引数には、割り当てが行われた行番号も含まれます (使用可能な場合)。 フック関数は、分析などの必要なタスクを実行した後で、割り当て処理を継続できる場合は **TRUE**、継続できない場合は **FALSE** を返すようにします。 この種のフック関数の簡単なものとしては、それまでに割り当てられたメモリの総量をチェックし、その量が少なめに設定した上限を超えている場合は **FALSE** を返す関数が考えられます。 この関数を使用すると、メモリがかなり不足している場合だけに発生するメモリ割り当てエラーを意図的に発生させることができます。 さらに複雑なフック関数としては、割り当てパターンを追跡したり、メモリの使用状況を分析したり、特定の状態が発生したときにレポートを作成したりする関数が考えられます。

## <a name="see-also"></a>関連項目

- [割り当てフック関数と C ランタイムのメモリ割り当て](../debugger/allocation-hooks-and-c-run-time-memory-allocations.md)
- [デバッグ用フック関数の作成](../debugger/debug-hook-function-writing.md)
