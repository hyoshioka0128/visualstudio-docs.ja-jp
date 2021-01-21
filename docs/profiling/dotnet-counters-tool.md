---
title: dotnet カウンターを視覚化する | Microsoft Docs
description: Visual Studio パフォーマンス プロファイラーで .NET カウンター ツールを使用する方法について説明します。
ms.date: 12/7/2020
ms.topic: conceptual
helpviewer_keywords:
- dotnet, counters, profiling
author: sagar-shetty
ms.author: sashe
manager: AndSter
ms.workload:
- multiple
ms.openlocfilehash: 7a09cc073b2886ab0d374bccaf8b85f3bb729dd7
ms.sourcegitcommit: 620d30c60da8f9805fce524fe4951cf40f28297d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/05/2021
ms.locfileid: "97905074"
---
# <a name="visualize-dotnet-counters-from-the-visual-studio-profiler"></a>Visual Studio プロファイラーから dotnet カウンターを視覚化する


.NET カウンター ツールを使用すると、Visual Studio プロファイラー内から直接、[dotnet カウンター](/dotnet/core/diagnostics/dotnet-counters)を経時的に視覚化することができます。


> [!NOTE]
> .NET カウンター ツールには、Visual Studio 2019 バージョン 16.7 以降が必要であり、.NET Core 3.0 以降がターゲットとされます。

## <a name="setup"></a>セットアップ

1. Visual Studio でパフォーマンス プロファイラーを開きます (**Alt + F2 キー**、または **[デバッグ] -> [パフォーマンス プロファイラー]** )。

2. **[.NET カウンター]** チェックボックスをオンにします。

   :::image type="content" source="../profiling/media/dotnet-counters-tool-selected.png" alt-text="カウンター ツールが選択されている。":::

3. **[開始]** ボタンをクリックしてツールを実行します。

ツールのパフォーマンスを最適化する方法の詳細については、「[プロファイラー設定の最適化](../profiling/optimize-profiler-settings.md)」を参照してください。


## <a name="understand-your-data"></a>データを理解する

ツールによって最初のデータ収集が行われている間に、[dotnet カウンター](/dotnet/core/diagnostics/dotnet-counters)のライブ値を確認できます。

:::image type="content" source="../profiling/media/dotnet-counters-tool-collecting.png" alt-text=".NET カウンター ツールによって収集が行われている。":::

カウンター名の横にあるチェックボックスをオンにすれば、カウンターのグラフを表示することもできます。 複数のカウンターのグラフを一度に表示できます。


アプリの実行とデータの収集が完了したら、さらに詳細なレポートを目的とした収集を停止することができます。 これを行うには、 **[収集を停止]** ボタンをクリックします。


レポートが読み込まれると、次に示すような完成したレポートが表示されます。

:::image type="content" source="../profiling/media/dotnet-counters-tool-report.png" alt-text=".NET カウンター ツール レポート。":::

このレポートには、次の値が表示されます。

- 最小値 - 選択した時間の範囲内での該当するカウンターの最小値。
- 最大値 - 選択した時間の範囲内での該当するカウンターの最大値。
- 平均値 - 選択した時間の範囲内での該当するカウンターの平均値。

列見出しを右クリックし、見出しを選択すると、テーブル内で列をフィルター処理したり追加したりできます。

:::image type="content" source="../profiling/media/dotnet-counters-tool-columns.png" alt-text=".NET カウンター ツールの列。":::

[カウンター] の横にあるチェックボックスをオンにして、詳細レポート内にグラフを表示することもできます。 テーブル内のデータは、既定では、収集されたトレースの全期間の値となります。 データを特定の時間の範囲にフィルターで絞り込むには、グラフをクリックしてドラッグします。

:::image type="content" source="../profiling/media/dotnet-counters-tool-time-filtering.png" alt-text=".NET カウンター ツールの時間フィルター処理。":::

テーブルは、グラフ内で選択した期間での該当する値に更新されます。 選択した時間の範囲をトレース全体にリセットするには **[選択のクリア]** ボタンを使用します。


## <a name="see-also"></a>関連項目

- [プロファイラー設定の最適化](../profiling/optimize-profiler-settings.md)
- [dotnet カウンター](/dotnet/core/diagnostics/dotnet-counters)
