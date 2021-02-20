---
title: スリープ時間 | Microsoft Docs
description: スリープのカテゴリにより、スレッドが自発的にその論理コアを明け渡して、処理を行わなかったことを示すことについて学習します。
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.cv.threads.timeline.sleep
helpviewer_keywords:
- Concurrency Visualizer, Sleep Time
ms.assetid: 3ddb96f9-9bda-4a68-ad4d-ef488a0a68dc
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: a433d11c2684a4a39660759f33d49bd719c2b2ae
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99960170"
---
# <a name="sleep-time"></a>スリープ時間
タイムライン内のこれらのセグメントは、スリープとして分類されるブロック時間と関連付けられています。 スリープのカテゴリは、スレッドが自発的にその論理コアを明け渡して、処理を行わなかったことを示しています。 この期間中、コンカレンシー ビジュアライザーがスリープとしてカウントしている API で、1 つのスレッドがブロックされています。 `Sleep()` や `SwitchToThread()` などの API がこのグループになります。

## <a name="see-also"></a>関連項目
- [スレッド ビュー](../profiling/threads-view-parallel-performance.md)