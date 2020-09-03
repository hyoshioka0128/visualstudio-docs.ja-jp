---
title: ASP.NET Web アプリの統計情報を収集する | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- profiling tools, sampling method
- sampling profling method
ms.assetid: f8383ab1-eb49-4d3f-8608-d8b4d51a81be
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- aspnet
ms.openlocfilehash: 8f353f551b3b524cfa49fb2cb638c261dcde660d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85331921"
---
# <a name="collect-statistics-for-aspnet-web-apps"></a>ASP.NET Web アプリの統計情報を収集する

このセクションでは、**VSPerfASPNETCmd** および **VSPerfCmd** コマンドライン ツールとサンプリング プロファイル メソッドを使用して、ASP.NET Web アプリケーションのパフォーマンスの統計情報を収集する手順とオプションについて説明します。

> [!NOTE]
> Windows 8 および Windows Server 2012 の強化されたセキュリティ機能によって、Visual Studio プロファイラーがこれらのプラットフォームでデータを収集する方法に大幅な変更が必要になりました。 UWP アプリにも新しい収集手法が必要です。 ｢[Windows 8 および Windows Server 2012 アプリケーションのパフォーマンス ツール](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)」を参照してください。

> [!NOTE]
> **VSPerfCmd** ツールを使用すると、プロファイルの一時停止や再開など、すべてのプロファイル ツール機能にアクセスし、プロセッサと Windows パフォーマンス カウンターからその他のデータも収集できますが、この機能が不要な場合は **VSPerfASPNETCmd** コマンド ライン ツールを使用することをお勧めします。 **VSPerfASPNETCmd** コマンド ライン ツールは、スタンドアロン プロファイラーを使用して ASP.NET Web サイトのプロファイリングを実行するときに推奨される方法です。 [VSPerfCmd](../profiling/vsperfcmd.md) コマンド ライン ツールと比較すると、環境変数を設定する必要がなく、コンピューターを再起動する必要がありません。 詳細については、「[VSPerfASPNETCmd を使用した迅速な Web サイト プロファイリング](../profiling/rapid-web-site-profiling-with-vsperfaspnetcmd.md)」を参照してください。

## <a name="common-tasks"></a>一般的なタスク

|タスク|関連コンテンツ|
|----------|---------------------|
|**プロファイラーを ASP.NET アプリケーションにアタッチする**|-   [方法: コマンド ラインを使用してプロファイラーを ASP.NET Web アプリケーションにアタッチし、アプリケーションの統計情報を収集する](../profiling/how-to-attach-the-profiler-to-an-aspnet-web-application-to-collect-application-statistics-by-using-the-command-line.md)|

## <a name="related-tasks"></a>関連タスク

### <a name="profile-aspnet-web-applications"></a>ASP.NET Web アプリケーションのプロファイリング

|タスク|関連コンテンツ|
|----------|---------------------|
|**インストルメンテーション方式を使用したプロファイリング**|-   [インストルメンテーションを使用した詳細なタイミング データの収集](../profiling/collecting-detailed-timing-data-aspnet-profiler-instrumentation-method.md)|
|**メモリ割り当てとガベージ コレクションのプロファイリング**|-   [メモリ データの収集](../profiling/collecting-memory-data-from-an-aspnet-web-application.md)|
|**リソースの競合とスレッド アクティビティのプロファイリング**|-   [コンカレンシー データの収集](../profiling/collecting-concurrency-data-for-an-aspnet-web-application.md)|

### <a name="sample-method"></a>サンプル メソッド

|タスク|関連コンテンツ|
|----------|---------------------|
|**スタンドアロン (クライアント) アプリケーションのプロファイリング**|-   [サンプリングを使用したアプリケーション統計情報の収集](../profiling/collecting-application-statistics-for-stand-alone-applications.md)|
|-   **サービスのプロファイリング**|-   [サンプリングを使用したアプリケーション統計情報の収集](../profiling/collecting-application-statistics-for-services-by-using-the-profiler-sampling-method.md)|

### <a name="analyze-sampling-data-views-and-reports"></a>サンプリング データ ビューとレポートの分析
- [サンプリング メソッドのデータ ビュー](../profiling/profiler-sampling-method-data-views.md)
