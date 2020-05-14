---
title: ポインターがメモリ アドレスを破壊しているかどうか見つけるには | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
- C++
helpviewer_keywords:
- addresses, pointers corrupting memory address
- memory, corruption
- pointers, corrupting memory addresses
- memory address corruption by pointers
- debugging [C++], memory corruption
- corrupted memory address
ms.assetid: a147c939-4fb1-415c-8410-cf303781e9e8
caps.latest.revision: 22
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 1d4f23b885b2e72e53d288946df18e038d9d956d
ms.sourcegitcommit: 374f5ec9a5fa18a6d4533fa2b797aa211f186755
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2020
ms.locfileid: "77476781"
---
# <a name="how-can-i-find-out-if-my-pointers-corrupt-a-memory-address"></a>ポインターがメモリ アドレスを破壊しているかどうか見つけるには
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

問題の説明  
 ポインターの 1 つがアドレス 0x00408000 のメモリを破壊してしまったようです。 どうなっているのか調べる方法はありますか。  
  
## <a name="solution"></a>解決策:  
  
#### <a name="check-for-heap-corruption"></a>ヒープ破損のチェック  
  
- メモリの破損は、その多くがヒープの破損に起因します。 グローバル フラグ ユーティリティ (gflags.exe) または pageheap.exe を使用してください。 「 [GFlags と PageHeap](/windows-hardware/drivers/debugger/gflags-and-pageheap) 」および「 [PageHeap ユーティリティを使用して Microsoft Visual C++プロジェクトのメモリエラーを検出する方法](https://support.microsoft.com/help/264471/how-to-use-the-pageheap-utility-to-detect-memory-errors-in-a-microsoft)」を参照してください。
  
#### <a name="to-find-where-the-memory-address-is-modified"></a>メモリ アドレスの変更箇所を見つけるには  
  
1. 0x00408000 にデータ ブレークポイントを設定します。 「[データ変更ブレークポイントを設定する (ネイティブ C++ のみ)](../debugger/using-breakpoints.md#BKMK_set_a_data_breakpoint_native_cplusplus_only)」を参照してください。  
  
2. ブレークポイントにヒットしたら、**[メモリ]** ウィンドウを使用して、0x00408000 から始まるメモリの内容を表示します。 詳細については、「[メモリウィンドウ](../debugger/memory-windows.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [ネイティブ コードのデバッグに関する FAQ](../debugger/debugging-native-code-faqs.md)   
 [ネイティブ コードのデバッグ](../debugger/debugging-native-code.md)
