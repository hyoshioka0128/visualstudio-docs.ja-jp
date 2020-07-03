---
title: プロファイラーのコマンド ライン - サービスのタイミングの詳細を取得するためのインストルメント化
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 6116e1df-ed3e-4b0d-ac7f-22f7d7ac00ea
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 502ae620dc8641fabc8a5f6225b5673d5530c7f0
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/24/2020
ms.locfileid: "85331792"
---
# <a name="collect-detailed-timing-data-for-services-by-using-the-instrumentation-method-from-the-profiler-command-line"></a>プロファイラーのコマンド ラインからインストルメンテーション メソッドを使用した、サービスの詳細なタイミング データの収集
このセクションでは、コマンド ラインからインストルメンテーション メソッドを使用して、Windows サービスの詳細なパフォーマンス データを収集する手順とオプションについて説明します。

## <a name="common-tasks"></a>一般的なタスク

|タスク|関連するコンテンツ|
|----------|---------------------|
|**.NET サービスをプロファイリングする**|-   [方法: .NET サービスをインストルメントし、詳細なタイミング データを収集する](../profiling/how-to-instrument-a-dotnet-service-and-collect-detailed-timing-data-by-using-the-profiler-command-line.md)|
|**階層の相互作用データを追加する**|-   [階層相互作用データを収集する](../profiling/adding-tier-interaction-data-from-the-command-line.md)|
|**C/C++ サービスをプロファイリングする**|-   [方法: ネイティブ サービスをインストルメントし、詳細なタイミング データを収集する](../profiling/how-to-instrument-a-native-service-and-collect-detailed-timing-data-by-using-the-profiler-command-line.md)|

## <a name="related-tasks"></a>関連するタスク

### <a name="profile-windows-services"></a>Windows サービスのプロファイリング

|タスク|関連するコンテンツ|
|----------|---------------------|
|**サンプリング メソッドを使用したプロファイリング**|-   [サンプリングを使用したアプリケーション統計情報の収集](../profiling/collecting-application-statistics-for-services-by-using-the-profiler-sampling-method.md)|
|**.NET のメモリ割り当てとガベージ コレクションのプロファイリング**|-   [.NET メモリ データの収集](../profiling/collecting-memory-data-from-dotnet-framework-services-by-using-the-profiler-command-line.md)|
|**リソースの競合とスレッド アクティビティのプロファイリング**|-   [コンカレンシー データの収集](../profiling/collecting-concurrency-data-for-a-service-by-using-the-profiler-command-line.md)|

### <a name="profile-by-using-the-instrumentation-method"></a>インストルメンテーション方式を使用したプロファイリング

|タスク|関連するコンテンツ|
|----------|---------------------|
|**スタンドアロン (クライアント) アプリケーションのプロファイリング**|-   [インストルメンテーションを使用した詳細なタイミング データの収集](../profiling/collecting-detailed-timing-data-for-a-stand-alone-application.md)|
|**ASP.NET Web アプリケーションのプロファイリング**|-   [インストルメンテーションを使用した詳細なタイミング データの収集](../profiling/collecting-detailed-timing-data-aspnet-profiler-instrumentation-method.md)|

### <a name="analyze-instrumentation-data-views-and-reports"></a>インストルメンテーション データ ビューとレポートの分析
- [インストルメンテーション メソッドのデータ ビュー](../profiling/instrumentation-method-data-views.md)
