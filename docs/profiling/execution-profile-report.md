---
title: 実行プロファイル レポート | Microsoft ドキュメント
description: 実行プロファイル レポートについて学習します。これは、Visual Studio のコンカレンシー ビジュアライザー拡張機能の従来のサンプリング プロファイルです。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.cv.threads.report.execution
helpviewer_keywords:
- Concurrency Visualizer, Execution Profile Report
ms.assetid: c8128472-a8ed-46f4-b1c8-a25358d6f2c1
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: e7a61e3a9ba159977d4a835126b2a584be1597c1
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99955256"
---
# <a name="execution-profile-report"></a>実行プロファイル レポート
実行プロファイル レポートは、従来のサンプリング プロファイルです。 サンプルは、論理コア上でスレッドが実行されている期間中におよそミリ秒ごとに取得されます。コンカレンシー ビジュアライザーが、累積された一連のサンプル セットを照合して、標準的なコール ツリーをビルドします。 このテーブルのデータは、現在の時間範囲と非表示のスレッドの影響、および適用されるフィルターの影響を受ける場合があります。

- [マイ コードのみ] が選択されている場合、ユーザー コードのあるスタック フレームと、そのユーザー コードの 1 つ下のレベルのみが表示されます。

- [不要項目の非表示] 値が設定されている場合、指定した頻度を下回る照合済みスタックはレポートから除外されます。

  次の表は、テーブル内の列を示しています。

|列|説明|
|------------|-----------------|
|名前|呼び出し履歴の各レベルの関数の名前。|
|包括サンプル|このレベルの呼び出し履歴のツリーにまとめられたすべてのスタックについて集められたサンプルの合計数。 包括数は、この関数の排他サンプルと、すべての子ノードの包括カウンターの合計です。|
|排他サンプル|この関数が呼び出し履歴の最も低いレベルにある、収集されたサンプルの合計数。|
|% 包括|包括サンプル列に表示されているサンプルの合計の割合。 割合は小数点以下 2 桁に丸めて表示されます。|
|% 排他|排他サンプル列に表示されているサンプルの合計の割合。 割合は小数点以下 2 桁に丸めて表示されます。|
|詳細|関数の完全修飾名。 これには、利用できる場合、行数が含まれます。|

 このレポートの表については、[実行時間 (スレッド ビュー)](../profiling/execution-time-threads-view.md) ビューで確認できます。

## <a name="see-also"></a>関連項目
- [スレッド ビュー](../profiling/threads-view-parallel-performance.md)