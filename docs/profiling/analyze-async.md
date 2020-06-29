---
title: .NET 非同期コードのパフォーマンスを分析する | Microsoft Docs
ms.date: 5/5/2020
ms.topic: conceptual
helpviewer_keywords:
- asynchronous, async, profiling
author: esteban-herrera
ms.author: esherrer
manager: AndSter
ms.workload:
- multiple
ms.openlocfilehash: 49091ba472637d480c04c39f0170c2aee00595d2
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85291003"
---
# <a name="analyze-performance-of-net-asynchronous-code"></a>.NET 非同期コードのパフォーマンスを分析する

.NET Async ツールを使用して、アプリ内の非同期コードのパフォーマンスを分析します。

> [!NOTE]
> .NET Async ツールには、Visual Studio 2019 バージョン 16.7 以降と、**async** および **await** を使用する .NET プロジェクトが必要です。

## <a name="setup"></a>セットアップ

1. **Alt + F2** キーを押して Visual Studio にパフォーマンス プロファイラーを開きます。

1. **[.NET Async]** チェック ボックスをオンにします。

   ![.NET Async ツールが選択されている](../profiling/media/async-tool-selected.png ".NET Async ツールが選択されている")

1. **[開始]** ボタンをクリックしてツールを実行します。

1. ツールの実行が開始されたら、アプリ内でプロファイリングするシナリオを完了します。 次に、 **[収集の停止]** を選択するかアプリを閉じてデータを確認します。

1. 収集が停止すると、プロファイル セッション中に発生したアクティビティのテーブルが表示されます。

   ![.NET Async ツールが停止した](../profiling/media/async-tool-opened.png ".NET Async ツールが停止した")

非同期イベントは、時系列順のアクティビティに整理されます。 それぞれの開始時刻、終了時刻、および期間が表示されます。

[タスク](https://docs.microsoft.com/dotnet/api/system.threading.tasks)に対応する各行には、 **[名前]** 列にラベルが付けられます。 解決できないタスク名に対しては、 **[タスク イン]** ラベルが表示されます。 後ろに、その中でタスクが発生するメソッドの名前が続きます。 収集セッション内で非同期アクティビティが完了しない場合、 **[終了時刻]** 列に **[不完全]** ラベルが表示されます。

特定のタスクまたはアクティビティをさらに詳しく調査するには、行を右クリックします。 次に、 **[ソース ファイルに移動]** を選択して、アクティビティが発生したコード内の場所を確認します。

![[ソース ファイルに移動] が選択されている .NET Async ツール](../profiling/media/async-tool-gotosource.png "[ソース ファイルに移動] が選択されている .NET Async ツール")

## <a name="see-also"></a>関連項目

- [プロファイラー設定の最適化](../profiling/optimize-profiler-settings.md)
