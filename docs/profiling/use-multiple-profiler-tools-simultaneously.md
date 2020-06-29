---
title: 複数のプロファイラー ツールの同時使用 | Microsoft Docs
ms.date: 4/29/2020
ms.topic: conceptual
helpviewer_keywords:
- Profiler, multiple tools
author: Sagar-S-S
ms.author: sashe
manager: AndSter
ms.workload:
- multiple
ms.openlocfilehash: 7844d81af02211d1c9f4e444c6367152e73392e9
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85290971"
---
# <a name="using-multiple-profiler-tools-simultaneously"></a>複数のプロファイラー ツールの同時使用

パフォーマンス プロファイラーは、パフォーマンスの問題を把握するために同じセッション内で複数のツールを使用できるという考え方で設計されています。 パフォーマンス プロファイラーのほとんどのツールでは、[CPU 使用率](../profiling/cpu-usage.md)、[.NET Async ツール](../profiling/analyze-async.md)、[データベース](../profiling/analyze-database.md) ツールなどの同時実行がサポートされています。 同じ診断セッション内でツールを同時に実行するには、ツールの横にあるチェック ボックスをオンにしてから、診断セッションを開始します。

![ハブのすべてのツールがオンになっているダイアログ](../profiling/media/diaghuballtoolsselected.png "ハブのすべてのツールがオンになっているダイアログ")

>[!NOTE]
>[.NET オブジェクト割り当て](../profiling/dotnet-alloc-tool.md)ツールなどの特定のツールは、オーバーヘッドの高さやその他の技術的な制限により、他のツールと一緒に実行することはできません。

## <a name="time-filtering"></a>時間フィルター処理 

分析時に複数のツール間で時間フィルター操作が適用されるため、1 つのツールの情報を使用して時間範囲を絞り込んで、別のツールのデータをフィルター処理できます。 この機能は、トレース内の特定のポイントを分析し、アプリケーションの状態を把握するのに役立ちます。

![ハブの時間フィルター処理ダイアログ](../profiling/media/diaghubtimefiltering.png "ハブの時間フィルター処理ダイアログ")

## <a name="see-also"></a>関連項目

- [プロファイラー設定の最適化](../profiling/optimize-profiler-settings.md)
- [デバッガーを使用した、または使用しないプロファイリング ツールの実行](../profiling/running-profiling-tools-with-or-without-the-debugger.md)
- [パフォーマンス収集方法について](../profiling/understanding-performance-collection-methods-perf-profiler.md)
