---
title: ロード テスト結果の分析 - グラフ ビュー (ロード テスト アナライザー)
description: テスト結果をグラフとして表示する方法について説明します。 各グラフがパネルに表示され、ドロップダウン リストにグラフ名が表示されます。
ms.custom: SEO-VS-2020
ms.date: 10/19/2016
ms.topic: conceptual
f1_keywords:
- vs.test.load.monitor.graph.view
helpviewer_keywords:
- graphs, analyzing load tests
- load tests, graphs in Load Test Viewer
- Load Test Viewer, graphs
- load tests, results graphs
- load tests, using graphs
- load test results, graphs
ms.assetid: 4a919cd8-541c-40ee-be3b-352fabc56140
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: e30d81277ae28a3f5d6ca45a259fa66e0f4ee004
ms.sourcegitcommit: 02f14db142dce68d084dcb0a19ca41a16f5bccff
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2020
ms.locfileid: "95441977"
---
# <a name="analyze-load-test-results-in-the-graphs-view-of-the-load-test-analyzer"></a>ロード テスト アナライザーのグラフ ビューでのテスト結果の分析

ロード テストの結果は、複数のペインのデータとして表示されます。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

テスト結果をグラフとして表示するには、**ロード テスト** ツール バーの **[グラフ]** をクリックします。 各グラフがパネルに表示され、ドロップダウン リストの先頭にグラフの名前が表示されます。 パネルに別のグラフを表示するには、一覧から別のグラフ名を選択します。

一度に最高で 4 つのグラフ パネルを表示できます。 **パネル レイアウト** のツール バー ボタンを使用して、異なるパネル レイアウトに切り替えることができます。

複数の組み込みグラフが提供されています。 組み込みグラフをそのまま使用することも、カスタマイズすることもできます。 さらに、独自のグラフを作成することもできます。 詳細については、「[方法: グラフにカウンターを追加および削除する](../test/how-to-add-and-delete-counters-on-graphs-in-load-test-results.md)」および[カスタム グラフを作成する方法](../test/how-to-create-custom-graphs-in-load-test-results.md)に関するページを参照してください。

## <a name="built-in-graphs"></a>組み込みグラフ

次の表は、ロード テストの結果の分析に使用できる組み込みグラフの一覧です。

|グラフ名|[説明]|
|-|-|
|キー インジケーター|ユーザー負荷、スループット、応答時間など、テストのパフォーマンスの基本的な面を示すカウンターです。|
|テストの応答時間|テストの実行に要した時間に関するデータです。|
|ページ応答時間|ロード テスト中にアクセスされた Web ページの平均応答時間です。|
|テスト下のシステム|テスト対象のアプリケーションが実行しているコンピューターに関する情報です。 これには、メモリ使用、プロセッサ、物理ディスク、プロセスについてのデータが含まれます。<br /><br /> 既定では、Available Mbytes カウンターと Processor Time カウンターのみが収集されます。|
|コントローラーおよびエージェント|ロード テストが実行されているコンピューターに関する情報です。 これには、メモリ使用、プロセッサ、物理ディスク、プロセスについてのデータが含まれます。<br /><br /> 既定では、Available Mbytes カウンターと Processor Time カウンターのみが収集されます。|
|トランザクション応答時間|ロード テスト中に発生したトランザクションの平均応答時間です。|

実行時およびテストの実行後のどちらでも、グラフに各種のカウンターを表示できます。

> [!NOTE]
> 自動的に生成される応答時間グラフには、応答時間のパフォーマンス カウンターのみを追加できます。

カウンター情報は、グラフ内と、グラフの下にある凡例内の両方に表示されます。 グラフの一部を拡大表示することもできます。 詳細については、「[方法: グラフの領域にズーム インする](../test/how-to-zoom-in-on-a-region-of-the-graph-in-load-test-results.md)」を参照してください。

## <a name="counters-displayed-in-graphs"></a>グラフに表示されるカウンター

グラフには *カウンター* が表示されます。 カウンターとは、ロード テスト中に収集されるデータであり、1 秒あたりのテスト数や平均テスト時間などです。 カウンターの詳細については、[ロード テストでのコンピューターのカウンター セットとしきい値規則の指定](../test/specify-counter-sets-and-threshold-rules-for-load-testing.md)に関するページを参照してください。

グラフに表示されるカウンターの凡例では、ロード テストの実行に関する役に立つデータの列が示されます。 グラフ内で任意のデータの表示をオフにするには、凡例で行のチェック ボックスをオフにします。

凡例には、次の列があります。

|カウンター|カウンターの名前です。|
|-|-|
|インスタンス|カウンター インスタンスの名前です。|
|カテゴリ|カウンター カテゴリの名前です。|
|Computer|カウンターが収集されているコンピューターの名前です。|
|Color|グラフ内の線の色です。|
|Range|カウンターのグラフで 100 が意味する数値を示します。 たとえば、上限値が 10,000 である範囲の場合、グラフの上端にある 100 は 10,000 を表します。|
|最小|カウンターの最小値 (ミリ秒) を示します。|
|Max|カウンターの最大値 (ミリ秒) を示します。|
|Avg|カウンターの平均値 (ミリ秒) を示します。|
|Last (最後へ)|最新のサンプリング間隔でのカウンターの値 (ミリ秒) を示します。|

## <a name="tasks"></a>タスク

|タスク|関連するトピック|
|-|-|
|**凡例を使用してグラフをカスタマイズする:** グラフ ビューの凡例には、グラフに関連付けられているパフォーマンス カウンターの情報が表示されます。 凡例を使用して、パフォーマンス カウンターの削除、グラフのパフォーマンス カウンターの強調表示、およびプロット オプションのカスタマイズを行うことができます。|-   [グラフ ビューの凡例を使用したロード テストの分析](../test/use-the-graphs-view-legend-to-analyze-load-tests.md)|
|**グラフにカウンターを表示する:** グラフにカウンターを配置することにより、さまざまな種類のデータをロード テストの結果グラフに追加できます。|-   [方法: グラフにカウンターを追加および削除する](../test/how-to-add-and-delete-counters-on-graphs-in-load-test-results.md)|
|**グラフにズーム インする:** ロード テストを完了したら、ズーム バーを使用して、グラフの領域にズーム インしてスクロールできます。 ズーム インすると、ロード テストの実行中に生成されたデータをより詳細に確認できます。|-   [方法: グラフの領域にズーム インする](../test/how-to-zoom-in-on-a-region-of-the-graph-in-load-test-results.md)|
|**グラフを並べて表示する:** ロード テストの結果グラフを複数のパターンで配置できます。 最大で 4 つのグラフを並べて表示できます。||
|**カスタム グラフを作成する:** ロード テストの結果に関する特定の情報を表示するグラフをデザインできます。 カスタム グラフをデザインするには、グラフで表示するロード テストのカウンターを指定します。|-   [方法: カスタム グラフを作成する](../test/how-to-create-custom-graphs-in-load-test-results.md)|
|**グラフのパフォーマンス カウンター データをエクスポートする:** **グラフ** ビューが表示された状態で、**ロード テスト アナライザー** ツール バーの **[グラフ データを Excel にエクスポート]** ボタンを使用すると、グラフのデータを Microsoft Excel にエクスポートできます。||

## <a name="related-tasks"></a>関連タスク

[テーブル ビューでのロード テスト結果とエラーの分析](../test/analyze-load-test-results-and-errors-in-the-tables-view.md)

[方法 : ロード テストの結果にアクセスして分析する](../test/how-to-access-load-test-results-for-analysis.md)

[ロード テストの結果の分析](../test/analyze-load-test-results-using-the-load-test-analyzer.md)

## <a name="see-also"></a>参照

- [方法: グラフにカウンターを追加および削除する](../test/how-to-add-and-delete-counters-on-graphs-in-load-test-results.md)
- [方法: カスタム グラフを作成する](../test/how-to-create-custom-graphs-in-load-test-results.md)
- [方法: グラフの領域にズーム インする](../test/how-to-zoom-in-on-a-region-of-the-graph-in-load-test-results.md)
