---
title: コア ビュー | Microsoft Docs
description: コア ビューから与えられる情報について学習します。 スレッド アフィニティまたはスレッド プール管理を利用し、キャッシュ パフォーマンスを最適化する際に役立つことがあります。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.performance.view.cores
helpviewer_keywords:
- Concurrency Visualizer, Cores View
ms.assetid: e47af672-9785-4899-bd45-4d9dda3c396f
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: c4f04fd5021e0ac11cd04e2e04df96da19af1c77
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99951668"
---
# <a name="cores-view"></a>コア ビュー
**コア ビュー** には、スレッド実行が論理プロセッサのコアにどのようにマッピングされたかを示します (**[分析]** > **[コンカレンシー ビジュアライザー]** を選択して、コンカレンシー ビジュアライザーを開始します)。 サーバー アプリケーションを開発している場合、このビューは、スレッド アフィニティまたはスレッド プール管理を使ってキャッシュのパフォーマンスを最適化するのに役立ちます。 また、スレッド アフィニティを使うことでコア間の移行の問題が悪化した可能性がある場合の調査にも役立ちます。 コア ビューには、グラフと凡例の 2 つの部分があります。

 グラフでは、Y 軸に論理コア、X 軸に時間が表示されます。 グラフではすべてのスレッドに固有の色が使われていて、時間経過を追ってコア間のスレッドの移動を追跡できます。 凡例領域でスレッドを選ぶことにより、このグラフ上のスレッドをフィルター処理できます。

 凡例領域には、グラフの各色に対するエントリがあります。 各エントリには、スレッドの色と名前、クロスコア コンテキスト スイッチの数、コンテキスト スイッチの総数、およびクロスコア コンテキスト スイッチの割合が示されます。 凡例は、クロスコア コンテキスト スイッチの数が多い順に並べられています。 表示されている時間範囲中に実行されたスレッドのみが一覧表示されます。  ズームまたはパンすると、リストが更新されます。

## <a name="see-also"></a>関連項目
- [コンカレンシー ビジュアライザー](../profiling/concurrency-visualizer.md)
- [使用状況ビュー](../profiling/utilization-view.md)
- [スレッド ビュー](../profiling/threads-view-parallel-performance.md)