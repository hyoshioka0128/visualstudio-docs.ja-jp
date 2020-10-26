---
title: デバッグ バージョンのヒープ割り当て関数 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.crt
dev_langs:
- FSharp
- VB
- CSharp
- C++
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
caps.latest.revision: 20
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 13f8d8b79ecf586048aacf3cd9442c596f184be3
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65691166"
---
# <a name="debug-versions-of-heap-allocation-functions"></a>デバッグ バージョンのヒープ割り当て関数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

C ランタイム ライブラリには、デバッグ バージョンの特殊なヒープ割り当て関数があります。 これらの関数は、リリース バージョンの関数名の末尾に "_dbg" を追加した名前になっています。 ここでは、CRT 関数のリリース バージョンと _dbg バージョンとの相違点について、`malloc` と `_malloc_dbg` を例にして説明します。  
  
 [_DEBUG](https://msdn.microsoft.com/library/a9901568-4846-4731-a404-399d947e2e7a) が定義されている場合、CRT ではすべての [malloc](https://msdn.microsoft.com/library/144fcee2-be34-4a03-bb7e-ed6d4b99eea0) 呼び出しが [_malloc_dbg](https://msdn.microsoft.com/library/c97eca51-140b-4461-8bd2-28965b49ecdb) にマップされます。 したがって、`_malloc_dbg` の代わりに `malloc` を使用するようにコードを書き直さなくても、デバッグ中は利用できます。  
  
 しかし、明示的に `_malloc_dbg` を呼び出すこともできます。 明示的に `_malloc_dbg` を呼び出すと、さらに次の利点があります。  
  
- `_CLIENT_BLOCK` 型の割り当てを追跡できます。  
  
- 割り当て要求が発生したソース ファイルと行番号を格納できます。  
  
  `malloc` 呼び出しを `_malloc_dbg` に変換しない場合は、[_CRTDBG_MAP_ALLOC](https://msdn.microsoft.com/library/435242b8-caea-4063-b765-4a608200312b) を定義することでソース ファイル情報を取得できます。これにより、`malloc` のラッパーに依存する代わりに、プリプロセッサで `malloc` へのすべての呼び出しが `_malloc_dbg` に直接マップされます。  
  
  クライアント ブロック内の個々の割り当て型を追跡するには、`_malloc_dbg` パラメーターを `blockType` に設定して、直接 `_CLIENT_BLOCK` を呼び出す必要があります。  
  
  _DEBUG が定義されていない場合、`malloc` 呼び出しはそのままですが、`_malloc_dbg` 呼び出しは `malloc` に変換されます。[_CRTDBG_MAP_ALLOC](https://msdn.microsoft.com/library/435242b8-caea-4063-b765-4a608200312b) の定義は無視され、割り当て要求に関連するソース ファイル情報は提供されません。 `malloc` にはブロック型を指定するパラメーターがないため、`_CLIENT_BLOCK` 型への割り当て要求は標準の割り当てとして扱われます。  
  
## <a name="see-also"></a>参照  
 [CRT のデバッグ技術](../debugger/crt-debugging-techniques.md)
