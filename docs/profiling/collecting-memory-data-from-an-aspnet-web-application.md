---
title: プロファイラーのコマンド ラインを使って ASP.NET Web アプリのメモリ データを取得する
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- .NET memory profiling method
- profiling tools,.NET memory method
ms.assetid: 57acf2b0-327a-4c0e-8078-ac2f6d99457d
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- aspnet
ms.openlocfilehash: 646445613aa9d03d2134094ebf0f694cef2f91ef
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85331703"
---
# <a name="collect-memory-data-from-an-aspnet-web-application-by-using-the-profiler-command-line"></a>プロファイラーのコマンド ラインを使用した ASP.NET Web アプリケーションからのメモリ データの収集
このセクションでは、**VSPerfCmd** コマンドライン ツールを使用し、ASP.NET Web アプリケーションのメモリ割り当てとオブジェクト有効期間データを収集する手順とオプションについて説明します。

> [!NOTE]
> **VSPerfCmd** ツールを使用すると、すべてのプロファイル ツール機能にアクセスできます。たとえば、プロファイリングを一時停止したり、再開したり、プロセッサや Windows パフォーマンス カウンターから追加データを収集したりできます。 この機能が不要な場合、**VSPerfASPNETCmd** コマンドライン ツールも利用できます。 [VSPerfCmd](../profiling/vsperfcmd.md) コマンド ライン ツールと比較すると、環境変数を設定する必要がなく、コンピューターを再起動する必要がありません。 詳細については、「[VSPerfASPNETCmd を使用した迅速な Web サイト プロファイリング](../profiling/rapid-web-site-profiling-with-vsperfaspnetcmd.md)」を参照してください。

## <a name="common-tasks"></a>一般的なタスク

|タスク|関連コンテンツ|
|----------|---------------------|
|**プロファイラーを実行中の ASP.NET アプリケーションにアタッチする**|-   [方法: プロファイラーを ASP.NET Web アプリケーションにアタッチし、メモリ データを収集する](../profiling/how-to-attach-the-profiler-to-an-aspnet-web-application-to-collect-memory-data-by-using-the-command-line.md)|
|**静的にコンパイルされたバイナリをインストルメント化する**|-   [方法: 静的にコンパイルされた ASP.NET アプリケーションをインストルメント化し、メモリ データを収集する](../profiling/how-to-instrument-a-statically-compiled-aspnet-app-and-collect-memory-data.md)|
|**動的にコンパイルされたバイナリをインストルメント化する**|-   [方法: 動的にコンパイルされた ASP.NET アプリケーションをインストルメント化し、メモリ データを収集する](../profiling/how-to-instrument-a-dynamically-compiled-aspnet-web-application-and-collect-memory-data.md)|

## <a name="related-tasks"></a>関連タスク

### <a name="profile-aspnet-web-applications"></a>ASP.NET Web アプリケーションのプロファイリング

|タスク|関連コンテンツ|
|----------|---------------------|
|**サンプリング メソッドを使用したプロファイリング**|-   [サンプリングを使用したアプリケーション統計情報の収集](../profiling/collecting-application-statistics-for-aspnet-using-the-profiler-sampling-method.md)|
|**インストルメンテーション方式を使用したプロファイリング**|-   [インストルメンテーションを使用した詳細なタイミング データの収集](../profiling/collecting-detailed-timing-data-aspnet-profiler-instrumentation-method.md)|
|**リソースの競合とスレッド アクティビティのプロファイリング**|-   [コンカレンシー データの収集](../profiling/collecting-concurrency-data-for-an-aspnet-web-application.md)|

### <a name="profile-net-framework-memory-data"></a>.NET Framework メモリ データのプロファイリング

|タスク|関連コンテンツ|
|----------|---------------------|
|**スタンドアロン (クライアント) アプリケーションのプロファイリング**|-   [.NET Framework メモリ データの収集](../profiling/collecting-dotnet-framework-memory-data-for-stand-alone-applications.md)|
|**サービスのプロファイリング**|-   [.NET メモリ データの収集](../profiling/collecting-memory-data-from-dotnet-framework-services-by-using-the-profiler-command-line.md)|

### <a name="analyze-net-memory-data-views-and-reports"></a>.NET メモリ データ ビューとレポートの分析
- [.NET メモリのデータ ビュー](../profiling/dotnet-memory-data-views.md)

## <a name="reference"></a>リファレンス
- [コマンド ライン プロファイリング ツール リファレンス](../profiling/command-line-profiling-tools-reference.md)
