---
title: I/O 時間 (スレッド ビュー) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.cv.threads.timeline.io
helpviewer_keywords:
- Concurrency Visualizer, I/O time (Threads View)
ms.assetid: 0c4ec14d-d8dd-49c1-999c-dcbf4e8e1dc8
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 86c14292edcf8f132a14b67e931c5121105a9dc8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68187441"
---
# <a name="io-time-threads-view"></a>I/O 時間 (スレッド ビュー)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

タイムライン内のこれらのセグメントは、I/O として分類されたブロック時間に関連付けられます。 つまり、スレッドは I/O 操作の完了を待ちます。 スレッドは API でブロックされている可能性があります。あるいは、コンカレンシー ビジュアライザーが I/O としてカウントしている I/O 関連のカーネル待機によりブロックされている可能性があります。 `CreateFile()`、`ReadFile()`、`WSARecv()` のような API がこのグループに属します。  
  
## <a name="see-also"></a>参照  
 [スレッド ビュー](../profiling/threads-view-parallel-performance.md)
