---
title: VSPerfCmd:インストルメンテーションを使用して ASP.NET Web アプリのタイミング データを取得する
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- profiling tools,instrumentation method
- instrumentation profiling method
ms.assetid: 29f2fc55-aaf7-4e18-a672-8815455fba73
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- aspnet
ms.openlocfilehash: d764ef32cdcb061992817d433dabb6ae61b64fd9
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "74779650"
---
# <a name="collect-detailed-timing-data-for-an-aspnet-web-application-using-the-profiler-instrumentation-method-from-the-command-line"></a>コマンド ラインからのプロファイラーのインストルメンテーション メソッドを使用した ASP.NET Web アプリケーションの詳細なタイミング データの収集
このセクションでは、**VSPerfCmd** コマンド ライン ツールとインストルメンテーション メソッドを使用して、[!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] Web アプリケーションの詳細なパフォーマンス データを収集する手順とオプションについて説明します。

> [!NOTE]
> **VSPerfCmd** ツールを使用すると、すべてのプロファイル ツール機能にアクセスできます。たとえば、プロファイリングを一時停止したり、再開したり、プロセッサや Windows パフォーマンス カウンターから追加データを収集したりできます。 この機能が不要な場合、**VSPerfASPNETCmd** コマンドライン ツールも利用できます。 [VSPerfCmd](../profiling/vsperfcmd.md) コマンド ライン ツールと比較すると、環境変数を設定する必要がなく、コンピューターを再起動する必要がありません。 詳細については、「[VSPerfASPNETCmd を使用した迅速な Web サイト プロファイリング](../profiling/rapid-web-site-profiling-with-vsperfaspnetcmd.md)」を参照してください。

## <a name="common-tasks"></a>一般的なタスク

|タスク|関連するコンテンツ|
|----------|---------------------|
|**静的にコンパイルされたバイナリをプロファイリングする**|-   [方法: 静的にコンパイルされた ASP.NET アプリケーションをインストルメント化し、詳細なタイミング データを収集する](../profiling/how-to-instrument-statically-compiled-aspnet-and-collect-detailed-timing-data.md)|
|**動的にコンパイルされたバイナリをプロファイリングする**|-   [方法: 動的にコンパイルされた ASP.NET アプリケーションをインストルメント化し、詳細なタイミング データを収集する](../profiling/how-to-instrument-a-dynamically-compiled-aspnet-app-and-collect-timing-data.md)|

## <a name="related-tasks"></a>関連するタスク

### <a name="profile-aspnet-web-applications"></a>ASP.NET Web アプリケーションのプロファイリング

|タスク|関連するコンテンツ|
|----------|---------------------|
|**サンプリング メソッドを使用したプロファイリング**|-   [サンプリングを使用したアプリケーション統計情報の収集](../profiling/collecting-application-statistics-for-aspnet-using-the-profiler-sampling-method.md)|
|**メモリ割り当てとガベージ コレクションのプロファイリング**|-   [メモリ データの収集](../profiling/collecting-memory-data-from-an-aspnet-web-application.md)|
|**リソースの競合とスレッド アクティビティのプロファイリング**|-   [コンカレンシー データの収集](../profiling/collecting-concurrency-data-for-an-aspnet-web-application.md)|

### <a name="profile-by-using-the-instrumentation-method"></a>インストルメンテーション方式を使用したプロファイリング

|タスク|関連するコンテンツ|
|----------|---------------------|
|**スタンドアロン (クライアント) アプリケーションのプロファイリング**|-   [インストルメンテーションを使用した詳細なタイミング データの収集](../profiling/collecting-detailed-timing-data-for-a-stand-alone-application.md)|
|**サービスのプロファイリング**|-   [インストルメンテーションを使用した詳細なタイミング データの収集](../profiling/collecting-detailed-timing-data-for-services-by-using-the-instrumentation-method.md)|

### <a name="analyze-instrumentation-data-views-and-reports"></a>インストルメンテーション データ ビューとレポートの分析
- [インストルメンテーション メソッドのデータ ビュー](../profiling/instrumentation-method-data-views.md)
