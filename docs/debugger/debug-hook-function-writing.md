---
title: デバッグ用フック関数の作成 | Microsoft Docs
description: カスタムで作成できるさまざまなデバッグ用フック関数について説明します。デバッグ用フック関数を使用すると、デバッガーが通常行う処理内部の定義済みの位置にコードを挿入できます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vc.hooks
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging [C++], CRT debug support
- debug hook functions
- hooks, debug
- hooks
- debugging [CRT], debug hook functions
ms.assetid: 5510635f-cf69-4907-b72d-ae27af1f19af
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 76727da1ed057902d8f757594f5ed2e07bcf3cea
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99857546"
---
# <a name="debug-hook-function-writing"></a>デバッグ用フック関数の作成
ここでは、カスタムで作成できるさまざまなデバッグ用フック関数について説明します。デバッグ用フック関数を使用すると、デバッガーが通常行う処理内部の定義済みの位置にコードを挿入できます。

## <a name="in-this-section"></a>このセクションの内容
 [クライアント ブロック用のフック関数](../debugger/client-block-hook-functions.md) _CLIENT_BLOCK 型のブロックに格納されたデータの内容を検証または報告する関数を作成するためのガイダンスとプロトタイプを提供します。

 [割り当て用フック関数](../debugger/allocation-hook-functions.md) 割り当て用フック関数を定義し、そのさまざまな使用方法を探求します。また、制限事項について説明し、プロトタイプを提供します。

 [割り当て用フック関数と CRT のメモリ割り当て](../debugger/allocation-hooks-and-c-run-time-memory-allocations.md) 割り当て用フック関数では、内部メモリを割り当てる C ランタイム ライブラリ関数を呼び出す場合、`_CRT_BLOCK` 型ブロックを明示的に無視する必要があるという制限について説明します。 また、割り当てフック関数が `_CRT_BLOCK` ブロックを無視しない場合の結果を例と共に示し、既定の割り当てフック関数 **CrtDefaultAllocHook** を変更する方法について説明します。

 [レポート用フック関数](../debugger/report-hook-functions.md) `_CrtSetReportHook`について説明します。これは、レポートをフィルター処理して特定の種類の割り当てだけを選択するために使用できます。 また、プロトタイプを説明します。

## <a name="related-sections"></a>関連項目

- [CRT のデバッグ技術](../debugger/crt-debugging-techniques.md) - CRT デバッグ ライブラリの使用、レポート用マクロ、`malloc` と `_malloc_dbg` の違い、デバッグ用フック関数の作成、CRT デバッグ ヒープなど、C ランタイム ライブラリのデバッグ技法を説明するリンクを提供します。