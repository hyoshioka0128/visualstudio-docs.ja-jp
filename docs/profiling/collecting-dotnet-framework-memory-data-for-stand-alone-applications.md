---
title: プロファイラーのコマンド ラインを使って .NET Framework メモリ データを取得する
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 7bce69e2-407c-4342-8516-641586968928
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- dotnet
ms.openlocfilehash: 62a55c36cd634b9451ad3796e5866d1e3a89b6a2
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/24/2020
ms.locfileid: "85331720"
---
# <a name="collect-net-framework-memory-data-by-using-the-profiler-command-line"></a>プロファイラーのコマンド ラインを使用して .NET Framework メモリ データを収集する

このセクションでは、コマンド ラインからサンプリング メソッドを使用して、.NET クライアント (スタンドアロン) アプリケーションのメモリ割り当てとオブジェクト有効期間データを収集する手順とオプションについて説明します。

## <a name="common-tasks"></a>一般的なタスク

|タスク|関連コンテンツ|
|----------|---------------------|
|**アプリケーションの起動と .NET メモリのプロファイリング**|-   [方法: プロファイラーによって .NET Framework アプリケーションを起動し、メモリ データを収集する](../profiling/how-to-launch-a-stand-alone-dotnet-framework-app-to-collect-memory-data.md)|
|**プロファイラーを NET アプリケーションにアタッチする**|-   [方法: プロファイラーを .NET Framework アプリケーションにアタッチし、メモリ データを収集する](../profiling/how-to-attach-the-profiler-to-a-dotnet-framework-app-to-collect-memory-data.md)|
|**アプリケーションをインストルメント化して .NET メモリ データを収集する**|-   [方法: プロファイラーを使用してスタンドアロンの .NET Framework コンポーネントをインストルメント化し、メモリ データを収集する](../profiling/how-to-instrument-a-dotnet-framework-component-and-collect-memory-data.md)|

## <a name="related-tasks"></a>関連タスク

### <a name="profile-stand-alone-applications"></a>スタンドアロン アプリケーションのプロファイリング

|タスク|関連コンテンツ|
|----------|---------------------|
|**サンプリング メソッドを使用したプロファイリング**|-   [サンプリングを使用したアプリケーション統計情報の収集](../profiling/collecting-application-statistics-for-stand-alone-applications.md)|
|**インストルメンテーション方式を使用したプロファイリング**|-   [インストルメンテーションを使用した詳細なタイミング データの収集](../profiling/collecting-detailed-timing-data-for-a-stand-alone-application.md)|
|**リソースの競合とスレッド アクティビティのプロファイリング**|-   [コンカレンシー データの収集](../profiling/collecting-concurrency-data-for-stand-alone-applications.md)|
|**階層の相互作用データを追加する**|-   [階層相互作用データを収集する](../profiling/adding-tier-interaction-data-from-the-command-line.md)|

### <a name="profile-net-memory-data"></a>.NET メモリ データのプロファイリング

|タスク|関連コンテンツ|
|----------|---------------------|
|**ASP.NET アプリケーションのプロファイリング**|-   [メモリ データの収集](../profiling/collecting-memory-data-from-an-aspnet-web-application.md)|
|**サービスのプロファイリング**|-   [.NET メモリ データの収集](../profiling/collecting-memory-data-from-dotnet-framework-services-by-using-the-profiler-command-line.md)|

### <a name="analyze-net-memory-data-views-and-reports"></a>.NET メモリ データ ビューとレポートの分析
- [.NET メモリのデータ ビュー](../profiling/dotnet-memory-data-views.md)

## <a name="reference"></a>リファレンス
- [コマンド ライン プロファイリング ツール リファレンス](../profiling/command-line-profiling-tools-reference.md)
