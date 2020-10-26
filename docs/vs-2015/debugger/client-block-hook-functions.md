---
title: Client ブロック用のフック関数 | Microsoft Docs
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
- client blocks, validating and reporting data
- debugging [C++], hook functions
- _CrtSetDumpClient function
- client blocks, hook functions
- hooks, client block
ms.assetid: f21c197e-565d-4e3f-9b27-4c018c9b87fc
caps.latest.revision: 18
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: c5b1c754255ba0bc659c9b6968ad8ba0dea629ec
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65702326"
---
# <a name="client-block-hook-functions"></a>Client ブロック用のフック関数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

`_CLIENT_BLOCK` 型のブロックに格納されているデータの内容を検証したりレポートしたりするために、専用の関数を作成できます。 作成する関数には、CRTDBG.H で定義されている次のようなプロトタイプが必要です。  
  
```  
void YourClientDump(void *, size_t)  
  
```  
  
 つまり、独自のフック関数は、対象となる割り当てブロックの先頭への **void** ポインターと、割り当てサイズを示す **size_t** 型の値を受け取り、`void` を返すようにする必要があります。 それ以外の内容については、自由に決定できます。  
  
 作成したフック関数を [_CrtSetDumpClient](https://msdn.microsoft.com/library/f3dd06d0-c331-4a12-b68d-25378d112033) を使用して組み込むと、`_CLIENT_BLOCK` 型のブロックがダンプされるたびに、このフック関数が呼び出されます。 [_CrtReportBlockType](https://msdn.microsoft.com/library/0f4b9da7-bebb-4956-9541-b2581640ec6b) を使用すると、ダンプされたブロックの型や、その細分化された型に関する情報を取得できます。  
  
 `_CrtSetDumpClient` に渡す独自の関数へのポインターは **_CRT_DUMP_CLIENT** 型です。これらは、CRTDBG.H で次のように定義されています。  
  
```  
typedef void (__cdecl *_CRT_DUMP_CLIENT)  
   (void *, size_t);  
```  
  
## <a name="see-also"></a>参照  
 [デバッグ用フック関数の作成](../debugger/debug-hook-function-writing.md)   
 [crt_dbg2 サンプル](https://msdn.microsoft.com/21e1346a-6a17-4f57-b275-c76813089167)   
 [_CrtReportBlockType](https://msdn.microsoft.com/library/0f4b9da7-bebb-4956-9541-b2581640ec6b)
