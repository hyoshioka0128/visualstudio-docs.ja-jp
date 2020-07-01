---
title: プロファイラー設定の最適化 | Microsoft Docs
ms.date: 4/29/2020
ms.topic: how-to
helpviewer_keywords:
- Profiler, improve performance
author: Sagar-S-S
ms.author: sashe
manager: AndSter
ms.workload:
- multiple
ms.openlocfilehash: 1ef802958817b43dd66973db66a80d328454aa83
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/24/2020
ms.locfileid: "85329262"
---
# <a name="optimizing-profiler-settings"></a>プロファイラー設定の最適化

Visual Studio のパフォーマンス プロファイラーと [診断ツール] ウィンドウには、ツールの全体的なパフォーマンスに影響を与えるさまざまな設定が多数あります。 一部の設定を変更すると、ツールで結果を処理するときに、分析が迅速に実行されたり、待機時間が増加したりする可能性があります。 特定の設定の概要とパフォーマンスに与える影響の概要を以下に示します。

## <a name="symbol-settings"></a>[シンボルの設定]

デバッガー オプションのシンボル設定 ( **[デバッグ] > [オプション] > [シンボル]** ) は、ツールで結果を生成するのにかかる時間に大きく影響します。 シンボル サーバーを有効にするか **_NT_SYMBOL_PATH** を使用すると、レポートに読み込まれる各モジュールのシンボルがプロファイラーで要求されます。 現時点では、シンボルの自動読み込みの設定に関係なく、プロファイラーでは、常にすべてのシンボルが自動的に読み込まれます。

![シンボル読み込みページ](../profiling/media/symbolloading.png "シンボル読み込み")

**[出力]** ウィンドウの **[診断ツール]** 見出しの下で、シンボル読み込みの進行状況を確認できます。

![シンボル読み込みの進行状況](../profiling/media/symbolloadingprogress.png "シンボル読み込みの進行状況")

ダウンロードが完了すると、シンボルがキャッシュされます。これにより、今後の分析が高速化されますが、それでもファイルを読み込んで分析する必要があります。 シンボルの読み込みによって分析が遅くなっている場合は、シンボル サーバーをオフにしてシンボル キャッシュをクリアしてみてください。 代わりに、自分のプロジェクト用にローカルに構築されたシンボルを使用してください。

## <a name="show-external-code"></a>[外部コードの表示]

**パフォーマンス プロファイラー**と **[診断ツール]** ウィンドウ内のツールの多くには、ユーザー コードと外部コードという概念があります。 ユーザー コードは、開いているソリューションまたは開いているワークスペースによって作成されたコードです。 外部コードはそれ以外のすべてです。 **[外部コードの表示]** 設定を無効のままにするか **[マイコードのみ表示]** を有効にすることで、ツールで外部コードを単一の第 1 レベルのフレームに集約でき、結果を表示するために必要な処理量を大幅に減らすことができます。 これにより、ユーザーは、処理されるデータを最小限に抑えながら、どの外部コードの呼び出しによって処理が遅くなっているかを確認できます。 可能であれば **[外部コードの表示]** を無効のままにし、分析対象の diagsession に対してソリューションまたはワークスペースを開いていることを確認します。

## <a name="trace-duration"></a>トレース実行時間

プロファイルの実行時間を短くすると、データの量が少なくなり、分析が迅速に行われます。 通常は、トレースを 5 分以内のパフォーマンス データに制限することをお勧めします。 [CPU 使用率](../profiling/cpu-usage.md)ツールなどの一部のツールでは、ツールの実行中にデータ収集を一時停止して、分析するシナリオに対して収集されるデータの量を制限できます。

## <a name="sampling-frequency"></a>サンプリング頻度

[CPU 使用率](../profiling/cpu-usage.md)ツールや [NET オブジェクト割り当て](../profiling/dotnet-alloc-tool.md)ツールなどの特定のツールでは、サンプリング頻度を調整できます。 このサンプリング頻度を高くすると、より正確に測定できますが、生成されるデータの量が増加します。 通常、特定の問題を調査する場合を除き、この設定は既定のレートのままにしておくことが最善です。

![ハブのプロパティ ページ ダイアログ](../profiling/media/diaghubpropertiespage.png "ハブのプロパティ ページ ダイアログ")

## <a name="see-also"></a>関連項目

- [デバッガーを使用した、または使用しないプロファイリング ツールの実行](../profiling/running-profiling-tools-with-or-without-the-debugger.md)
- [複数のプロファイラー ツールの同時使用](../profiling/use-multiple-profiler-tools-simultaneously.md)
- [パフォーマンス収集方法について](../profiling/understanding-performance-collection-methods-perf-profiler.md)
