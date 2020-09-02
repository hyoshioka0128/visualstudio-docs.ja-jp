---
title: コア ビュー | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.performance.view.cores
helpviewer_keywords:
- Concurrency Visualizer, Cores View
ms.assetid: e47af672-9785-4899-bd45-4d9dda3c396f
caps.latest.revision: 21
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 869980fe7bbb773d566dffd38088b003e3a97a3d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68145643"
---
# <a name="cores-view"></a>コア ビュー
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

コア ビューは、スレッドの実行が論理プロセッサ コアにどのようなマップされたかを示しています。 サーバー アプリケーションを開発している場合、このビューは、スレッド アフィニティまたはスレッド プール管理を使ってキャッシュのパフォーマンスを最適化するのに役立ちます。 また、スレッド アフィニティを使うことでコア間の移行の問題が悪化した可能性がある場合の調査にも役立ちます。 コア ビューには、グラフと凡例の 2 つの部分があります。  
  
 グラフでは、Y 軸に論理コア、X 軸に時間が表示されます。 グラフではすべてのスレッドに固有の色が使われていて、時間経過を追ってコア間のスレッドの移動を追跡できます。 凡例領域でスレッドを選ぶことにより、このグラフ上のスレッドをフィルター処理できます。  
  
 凡例領域には、グラフの各色に対するエントリがあります。 各エントリには、スレッドの色と名前、クロスコア コンテキスト スイッチの数、コンテキスト スイッチの総数、およびクロスコア コンテキスト スイッチの割合が示されます。 凡例は、クロスコア コンテキスト スイッチの数が多い順に並べられています。 表示されている時間範囲中に実行されたスレッドのみが一覧表示されます。  ズームまたはパンすると、リストが更新されます。  
  
## <a name="see-also"></a>参照  
 [同時実行ビジュアライザー](../profiling/concurrency-visualizer.md)   
 [使用状況ビュー](../profiling/utilization-view.md)   
 [スレッド ビュー](../profiling/threads-view-parallel-performance.md)
