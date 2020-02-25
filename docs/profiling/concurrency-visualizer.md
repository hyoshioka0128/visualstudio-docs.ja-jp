---
title: コンカレンシー ビジュアライザー | Microsoft Docs
ms.date: 07/11/2017
ms.topic: conceptual
f1_keywords:
- vs.cv.performance.viewnavigation
- vs.cv.overview
- vs.cv.performance.gettingstarted
- vs.cv.gettingstarted
helpviewer_keywords:
- Concurrency Visualizer, Concurrency Visualizer
ms.assetid: ae5879a0-1e1a-455a-ba72-148e57f59289
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d3b4e151db08ad5490ed6238223d553f9e76aa0f
ms.sourcegitcommit: 41f4f55af0176bed1ed949426929d4bdb53105a7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/13/2020
ms.locfileid: "77192404"
---
# <a name="concurrency-visualizer"></a>コンカレンシー ビジュアライザー

> [!NOTE]
> コンカレンシー ビジュアライザーは、Visual Studio に対する任意の拡張機能です。 コンカレンシー ビジュアライザーとコンカレンシー ビジュアライザー コレクション ツールは、以下のリンクからダウンロードします。
>
> - [Visual Studio 2019 用コンカレンシー ビジュアライザー](https://marketplace.visualstudio.com/items?itemName=Diagnostics.DiagnosticsConcurrencyVisualizer2019#overview)拡張機能をダウンロードします。
> - [Visual Studio 2017 用コンカレンシー ビジュアライザー](https://marketplace.visualstudio.com/items?itemName=VisualStudioProductTeam.ConcurrencyVisualizer2017#overview)拡張機能をダウンロードします。
> - [Visual Studio 2015 用コンカレンシー ビジュアライザー](https://marketplace.visualstudio.com/items?itemName=Diagnostics.ConcurrencyVisualizerforVisualStudio2015)拡張機能をダウンロードします。
> - [Concurrency Visualizer Collection Tools for Visual Studio 2015](https://www.microsoft.com/download/details.aspx?id=49103) をダウンロードします。
>
> [コンカレンシー ビジュアライザーのコマンド ライン ユーティリティ (CVCollectionCmd)](../profiling/concurrency-visualizer-command-line-utility-cvcollectioncmd.md) を使用して、コマンド ラインからトレースを収集することで、Visual Studio 2015 用のコンカレンシー ビジュアライザーでトレースを表示できます。 このツールは、Visual Studio がインストールされていないコンピューターで使用できます。

コンカレンシー ビジュアライザーを使用すると、マルチスレッド アプリがどのように動作するかを確認することができます。 コンカレンシー ビジュアライザーのビューには、プログラム内のスレッドとシステム間の時間的な関係をまとめて示す、グラフィカルな表形式のテキスト データが表示されます。 コンカレンシー ビジュアライザーを使用すると、パフォーマンスのボトルネック、十分に活用されていない CPU、スレッドの競合、コア間のスレッドの移行、同期の遅延、DirectX のアクティビティ、重複 I/O の領域などの情報を検索できます。 これらのビューでは、グラフィカルな出力を呼び出し履歴とソース コードにリンクすることで、アクション可能なデータを使用できるようになります。

> [!NOTE]
> コンカレンシー ビジュアライザーでは、Web プロジェクトはサポートされません。

コンカレンシー ビジュアライザーは、[Windows イベント トレーシング](/windows/win32/etw/event-tracing-portal)の機能に依存しています。

## <a name="related-topics"></a>関連トピック

|Title|説明|
|-----------|-----------------|
|[使用状況ビュー](../profiling/utilization-view.md)|すべてのプロセッサのシステム アクティビティを表示して分析する方法について説明します。|
|[スレッド ビュー](../profiling/threads-view-parallel-performance.md)|プログラム内のスレッド間の対話を分析する方法について説明します。|
|[コア ビュー](../profiling/cores-view.md)|コア間のスレッドの移行を分析する方法について説明します。|
|[適切に動作しないマルチスレッド アプリケーションの一般的なパターン](../profiling/common-patterns-for-poorly-behaved-multithreaded-applications.md)|いくつかの一般的なパターンについて説明し、それらがどのようにコンカレンシー ビジュアライザーに表示されるかを示します。|
|[Visual Studio での並行開発に関するブログ](https://blogs.msdn.microsoft.com/visualizeparallel/)|コンカレンシー ビジュアライザーのヒントとベスト プラクティスについて説明します。|
|[パフォーマンス レポートのビュー](../profiling/performance-report-views.md)|Visual Studio プロファイリング ツールのレポートおよびビューに関するリファレンス情報を提供します。|
|[コンカレンシー ビジュアライザー SDK](../profiling/concurrency-visualizer-sdk.md)|ソース コードをインストルメント化してコンカレンシー ビジュアライザーに追加情報を表示する方法について説明します。|
|[コンカレンシー ビジュアライザー コマンドライン ユーティリティ (CVCollectionCmd)](../profiling/concurrency-visualizer-command-line-utility-cvcollectioncmd.md)|コンカレンシー ビジュアライザーのコマンド ライン ユーティリティ (CVCollectionCmd.exe) を使用して、Visual Studio がインストールされていないコンピューター上でトレースを収集および処理する方法について説明します。|

## <a name="see-also"></a>関連項目

- [Visual Studio のプロファイル](../profiling/index.yml)
- [プロファイル ツールの概要](../profiling/profiling-feature-tour.md)
