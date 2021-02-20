---
title: デバッグ バージョンのヒープ割り当て関数 | Microsoft Docs
description: C ランタイム ライブラリでデバッグ バージョンのヒープ割り当て関数を使用します。 これらの関数は、リリース バージョンの関数名の末尾に "_dbg" を追加した名前になっています。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.debug.crt
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- _CRTDBG_MAP_ALLOC macro
- debugging [CRT], heap allocation functions
- debugging memory leaks, CRT debug library functions
- malloc function
- memory leaks, CRT debug library functions
- heap allocation, debug
- _malloc_dbg function
ms.assetid: 91748bdc-f4cd-4d8b-ab98-0493dab7ed0d
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 9eedf9259f7bc62f32ca563d863a7fb686b8f6f2
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99873120"
---
# <a name="debug-versions-of-heap-allocation-functions"></a>デバッグ バージョンのヒープ割り当て関数
C ランタイム ライブラリには、デバッグ バージョンの特殊なヒープ割り当て関数があります。 これらの関数は、リリース バージョンの関数名の末尾に "_dbg" を追加した名前になっています。 ここでは、CRT 関数のリリース バージョンと _dbg バージョンとの相違点について、`malloc` と `_malloc_dbg` を例にして説明します。

 [_DEBUG](/cpp/c-runtime-library/debug) が定義されている場合、CRT ではすべての [malloc](/cpp/c-runtime-library/reference/malloc) 呼び出しが [_malloc_dbg](/cpp/c-runtime-library/reference/malloc-dbg) にマップされます。 したがって、`_malloc_dbg` の代わりに `malloc` を使用するようにコードを書き直さなくても、デバッグ中は利用できます。

 しかし、明示的に `_malloc_dbg` を呼び出すこともできます。 明示的に `_malloc_dbg` を呼び出すと、さらに次の利点があります。

- `_CLIENT_BLOCK` 型の割り当てを追跡できます。

- 割り当て要求が発生したソース ファイルと行番号を格納できます。

  `malloc` 呼び出しを `_malloc_dbg` に変換しない場合は、[_CRTDBG_MAP_ALLOC](/cpp/c-runtime-library/crtdbg-map-alloc) を定義することでソース ファイル情報を取得できます。これにより、`malloc` のラッパーに依存する代わりに、プリプロセッサで `malloc` へのすべての呼び出しが `_malloc_dbg` に直接マップされます。

  クライアント ブロック内の個々の割り当て型を追跡するには、`_malloc_dbg` パラメーターを `blockType` に設定して、直接 `_CLIENT_BLOCK` を呼び出す必要があります。

  _DEBUG が定義されていない場合、`malloc` 呼び出しはそのままですが、`_malloc_dbg` 呼び出しは `malloc` に変換されます。[_CRTDBG_MAP_ALLOC](/cpp/c-runtime-library/crtdbg-map-alloc) の定義は無視され、割り当て要求に関連するソース ファイル情報は提供されません。 `malloc` にはブロック型を指定するパラメーターがないため、`_CLIENT_BLOCK` 型への割り当て要求は標準の割り当てとして扱われます。

## <a name="see-also"></a>関連項目

- [CRT のデバッグ技術](../debugger/crt-debugging-techniques.md)