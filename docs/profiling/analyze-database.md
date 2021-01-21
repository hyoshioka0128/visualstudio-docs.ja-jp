---
title: .NET Core プロジェクトのデータベース使用状況を分析する |Microsoft Docs
ms.date: 5/5/2020
ms.topic: conceptual
helpviewer_keywords:
- database, profiling
author: esteban-herrera
ms.author: esherrer
manager: AndSter
ms.workload:
- multiple
ms.openlocfilehash: 0aeb2341d905be8f34d47c477f35861b8575dc69
ms.sourcegitcommit: 13cf7569f62c746708a6ced1187d8173eda7397c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/25/2020
ms.locfileid: "91352317"
---
# <a name="analyze-database-performance-using-the-database-tool"></a>データベース ツールを使用してデータベースのパフォーマンスを分析する

データベース ツールを使用して、診断セッション中にアプリによって実行されたデータベース クエリを記録します。 その後、個々のクエリに関する情報を分析して、アプリのパフォーマンスを向上させるための場所を見つけることができます。

> [!NOTE]
> データベース ツールでは、Visual Studio 2019 バージョン 16.3 以降と、[ADO.NET]( https://docs.microsoft.com/dotnet/framework/data/adonet/ado-net-overview) または [Entity Framework Core](/ef/core/) のいずれかを使用する Windows 上の .NET Core プロジェクトが必要です。

## <a name="setup"></a>セットアップ

1. **Alt + F2** キーを押して Visual Studio にパフォーマンス プロファイラーを開きます。

1. **[データベース]** チェック ボックスをオンにします。

   ![[データベース] ツールが選択されている](./media/db-launch.png "[データベース] ツールが選択されている")

   > [!NOTE]
   > ツールを選択できない場合は、他のすべてのツールのチェック ボックスをオフにします。これは一部のツールは単独で実行される必要があるためです。 ツールを一緒に実行することの詳細については、「[コマンド ラインからのプロファイリング ツールの使用](../profiling/using-the-profiling-tools-from-the-command-line.md)」を参照してください。
   >
   > それでもツールを使用できない場合は、プロジェクトが前述の要件を満たしていることを確認します。 プロジェクトが最も正確なデータを取得するためのリリース モードになっていることを確認します。

1. **[開始]** ボタンを選択してツールを実行します。

1. ツールの実行が開始されたら、アプリ内でプロファイリングするシナリオを完了します。 次に、 **[収集の停止]** を選択するかアプリを閉じてデータを確認します。

1. 収集が停止すると、プロファイル セッション中に実行されたクエリのテーブルが表示されます。

   ![[データベース] ツールが停止した](./media/db-after.png "[データベース] ツールが停止した")

クエリは時系列で整理されていますが、任意の列で並べ替えることができます。 列のタイトルを右クリックすることで、さらに多くの列を表示できます。 **[期間]** 列を選択すると、最も長い時間がかかったものを先頭に、最も短い時間がかかったものを最後にする順序でクエリが並べられます。

調査するクエリが見つかったら、そのクエリを右クリックします。 次に、 **[ソース ファイルに移動]** を選択して、そのクエリを実行しているコードを確認します。

![[ソース ファイルに移動] が選択されている](./media/db-gotosource.png "[ソース ファイルに移動] が選択されている")

グラフで時間の範囲を選択した場合、クエリ テーブルには、その時間の範囲中に発生したクエリのみが表示されます。 この動作は、[CPU 使用率ツール](./cpu-usage.md?view=vs-2019&preserve-view=true)も実行する場合に特に便利です。

## <a name="see-also"></a>関連項目

- [プロファイラー設定の最適化](../profiling/optimize-profiler-settings.md)