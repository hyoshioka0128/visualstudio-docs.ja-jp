---
title: 実行時間 (スレッド ビュー) | Microsoft ドキュメント
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.cv.threads.timeline.execution
helpviewer_keywords:
- Concurrency Visualizer, Execution Time (Threads View)
ms.assetid: 80c100f8-2502-4613-bfef-4f4f2e09cc8d
caps.latest.revision: 15
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: b4306e030c2f48d87b12ba6338a847dc9e9aa892
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68179033"
---
# <a name="execution-time-threads-view"></a>実行時間 (スレッド ビュー)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

スレッド ビュー タイムラインのこれらのセグメントは、スレッドがシステムの論理コア上で動作中である場合、実行時間を表します。  
  
 スレッド ステータスの変更は、カーネル コンテキスト スイッチ イベントを介して検出されます。 Windows イベント トレーシング (ETW) でミリ秒ごとにサンプル履歴がキャプチャされます。 非常に短い緑のセグメントでは、サンプルが取得されない可能性があります。 そのため、一部の短い実行セグメントには、呼び出し履歴が表示されない場合があります。  
  
 実行セグメントをクリックすると、コンカレンシー ビジュアライザーがクリックの位置に最も近いサンプル履歴を表示します。 そのサンプル履歴の場所は、タイムラインの上に黒の矢印 (キャレット) で示され、サンプル履歴が **[現在]** タブに表示されます。  
  
 現在のビューのすべての実行セグメントについて、従来のサンプリング プロファイルを参照するには、表示されているタイムライン プロファイルで **[実行]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [実行プロファイルレポート](../profiling/execution-profile-report.md)   
 [スレッド ビュー](../profiling/threads-view-parallel-performance.md)
