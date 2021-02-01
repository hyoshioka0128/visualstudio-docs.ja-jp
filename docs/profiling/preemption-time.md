---
title: 優先時間 | Microsoft Docs
description: 優先時間と、タイムライン内のこれらのセグメントが優先として分類されるブロック時間と関連付けられていることについて学習します。
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.cv.threads.timeline.preemption
helpviewer_keywords:
- Concurrency Visualizer, Preemption Time
ms.assetid: 6b78f91e-a006-440c-83fb-e7368040951d
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a102b11fdc7608b94b97105b061e28860f41a9a1
ms.sourcegitcommit: 18729d7c99c999865cc2defb17d3d956eb3fe35c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2021
ms.locfileid: "98719514"
---
# <a name="preemption-time"></a>優先時間
タイムライン内のこれらのセグメントは、優先として分類されるブロック時間と関連付けられています。 このカテゴリは、次のいずれかの理由によってスレッドが切り替えられたことを意味します。

- より優先順位の高いスレッドを使用してスケジューラが置換した。

- そのスレッドの実行クォンタムが期限切れになり、別のスレッドの実行準備が整った。

  この期間中、コンカレンシー ビジュアライザーが優先としてカウントしているカーネル待機理由によって、1 つのスレッドがブロックされています。 優先セグメントは、1 つのスレッドが論理コアから排除されたときに開始し、そのスレッドが実行を再開したときに終了します。

  優先セグメントのツールヒントには、優先の原因となったプロセスまたはスレッドの名前が表示されます。 ただし、優先されたプロセスまたはスレッドが優先期間を通じて実際に実行されることを意味するものではありません。

## <a name="see-also"></a>関連項目
- [スレッド ビュー](../profiling/threads-view-parallel-performance.md)