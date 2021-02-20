---
title: メモリ管理時間 | Microsoft Docs
description: ページングなど、メモリ管理操作に関連付けられているイベントによってスレッドがブロックされていることを、このシナリオがどのように意味するのか学習します。
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.cv.threads.timeline.paging
helpviewer_keywords:
- Concurrency Visualizer, Paging Time
ms.assetid: 67af3509-3a7d-435d-bc37-5262448da915
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: ad3c913e6c983749e53940f5e75ad3bdba48bf92
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99873633"
---
# <a name="memory-management-time"></a>メモリ管理時間
タイムライン内のこれらのセグメントは、メモリ管理として分類されたブロック時間に関連付けられます。 このシナリオは、ページングなど、メモリ管理操作に関連付けられているイベントによって、スレッドがブロックされていることを意味します。 この期間中、コンカレンシー ビジュアライザーがメモリ管理としてカウントする API またはカーネルの状態で、スレッドがブロックされています。 これには、ページングやメモリの割り当てなどのイベントが含まれます。

 メモリ管理として分類されたブロックの基になる理由をよく理解するために、関連のコール スタックとプロファイル レポートを確認してください。

## <a name="see-also"></a>関連項目
- [スレッド ビュー](../profiling/threads-view-parallel-performance.md)