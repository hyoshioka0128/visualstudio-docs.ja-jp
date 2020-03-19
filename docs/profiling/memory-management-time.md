---
title: メモリ管理時間 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.cv.threads.timeline.paging
helpviewer_keywords:
- Concurrency Visualizer, Paging Time
ms.assetid: 67af3509-3a7d-435d-bc37-5262448da915
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 442973edb18e75bafda8a9397eac799286c69dfa
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "62963782"
---
# <a name="memory-management-time"></a>メモリ管理時間
タイムライン内のこれらのセグメントは、メモリ管理として分類されたブロック時間に関連付けられます。 このシナリオは、ページングなど、メモリ管理操作に関連付けられているイベントによって、スレッドがブロックされていることを意味します。 この期間中、コンカレンシー ビジュアライザーがメモリ管理としてカウントする API またはカーネルの状態で、スレッドがブロックされています。 これには、ページングやメモリの割り当てなどのイベントが含まれます。

 メモリ管理として分類されたブロックの基になる理由をよく理解するために、関連のコール スタックとプロファイル レポートを確認してください。

## <a name="see-also"></a>参照
- [スレッド ビュー](../profiling/threads-view-parallel-performance.md)