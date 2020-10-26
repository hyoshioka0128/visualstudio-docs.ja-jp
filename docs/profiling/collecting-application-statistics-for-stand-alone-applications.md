---
title: プロファイラーのコマンド ラインを使ってスタンドアロン アプリの統計情報を収集する
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- sampling profiling method
- profilng tools,sampling method
ms.assetid: be2dbdd0-fc88-45f9-a1d5-bcb4f64e17ad
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 589dae38917e43f9b832fb2d3475bf63546a2e31
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85331882"
---
# <a name="collect-application-statistics-for-stand-alone-applications-by-using-the-profiler-command-line"></a>プロファイラーのコマンド ラインを使用したスタンドアロン アプリケーションのアプリケーション統計情報の収集
このセクションでは、コマンド ラインからサンプリング メソッドを使用して、クライアント (スタンドアロン) アプリケーションのパフォーマンスの統計情報を収集する手順とオプションについて説明します。

> [!NOTE]
> Windows 8 および Windows Server 2012 の強化されたセキュリティ機能によって、Visual Studio プロファイラーがこれらのプラットフォームでデータを収集する方法に大幅な変更が必要になりました。 UWP アプリにも新しい収集手法が必要です。 「[Windows 8 および Windows Server 2012 アプリケーションのパフォーマンス ツール](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)」を参照してください。

## <a name="common-tasks"></a>一般的なタスク

|タスク|関連コンテンツ|
|----------|---------------------|
|**プロファイリングを使用してアプリケーションを起動する**|-   [方法: スタンドアロン アプリケーションを起動し、アプリケーション統計情報を収集する](../profiling/how-to-launch-a-stand-alone-app-and-collect-application-statistics.md)|
|**実行中の .NET Framework アプリケーションにプロファイラーをアタッチする**|-   [方法: .NET Framework のアプリケーションにプロファイラーをアタッチし、アプリケーションの統計情報を収集する](../profiling/how-to-attach-the-profiler-to-a-dotnet-app-and-collect-application-statistics.md)|
|**実行中の C/C++ アプリケーションにプロファイラーをアタッチする**|-   [方法: プロファイラーをネイティブ アプリケーションにアタッチし、アプリケーション統計情報を収集する](../profiling/how-to-attach-the-profiler-to-a-native-app-and-collect-application-statistics.md)|
|**階層の相互作用データを追加する**|-   [階層相互作用データの収集](../profiling/adding-tier-interaction-data-from-the-command-line.md)|

## <a name="related-tasks"></a>関連タスク

### <a name="profile-stand-alone-applications"></a>スタンドアロン アプリケーションのプロファイリング

|タスク|関連コンテンツ|
|----------|---------------------|
|**アプリケーションをインストルメント化する**|-   [インストルメンテーションを使用した詳細なタイミング データの収集](../profiling/collecting-detailed-timing-data-for-a-stand-alone-application.md)|
|**.NET のメモリ割り当てとガベージ コレクション データの収集**|-   [.NET Framework メモリ データの収集](../profiling/collecting-dotnet-framework-memory-data-for-stand-alone-applications.md)|
|**リソース競合とスレッド実行データの収集**|-   [コンカレンシー データの収集](../profiling/collecting-concurrency-data-for-stand-alone-applications.md)|

### <a name="profile-by-using-the-sampling-method"></a>サンプリング メソッドを使用したプロファイリング

|タスク|関連コンテンツ|
|----------|---------------------|
|**ASP.NET Web アプリケーションのプロファイリング**|-   [サンプリングを使用したアプリケーション統計情報の収集](../profiling/collecting-application-statistics-for-aspnet-using-the-profiler-sampling-method.md)|
|**サービスのプロファイリング**|-   [サンプリングを使用したアプリケーション統計情報の収集](../profiling/collecting-application-statistics-for-services-by-using-the-profiler-sampling-method.md) サンプリング メソッドを使用して Windows サービスからパフォーマンスの統計情報を収集する方法について説明します。|

### <a name="analyze-sampling-data-views-and-reports"></a>サンプリング データ ビューとレポートの分析
- [サンプリング メソッドのデータ ビュー](../profiling/profiler-sampling-method-data-views.md)
