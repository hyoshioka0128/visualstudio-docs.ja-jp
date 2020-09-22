---
title: プロファイラーのコマンド ラインを使用した ASP.NET Web アプリケーションからのメモリ データの収集 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- .NET memory profiling method
- profiling tools,.NET memory method
ms.assetid: 57acf2b0-327a-4c0e-8078-ac2f6d99457d
caps.latest.revision: 18
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 0f7c759d4c2c4760be6782a518f4cdf209e828d4
ms.sourcegitcommit: fb8babf5cd72f1fc2f97ffe4ad7b62d91f325f61
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2020
ms.locfileid: "90842317"
---
# <a name="collecting-memory-data-from-an-aspnet-web-application-by-using-the-profiler-command-line"></a>プロファイラーのコマンド ラインを使用した ASP.NET Web アプリケーションからのメモリ データの収集
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このセクションでは、**VSPerfCmd** コマンドライン ツールを使用し、ASP.NET Web アプリケーションのメモリ割り当てとオブジェクト有効期間データを収集する手順とオプションについて説明します。  
  
> [!NOTE]
> **VSPerfCmd** ツールを使用すると、すべてのプロファイル ツール機能にアクセスできます。たとえば、プロファイリングを一時停止したり、再開したり、プロセッサや Windows パフォーマンス カウンターから追加データを収集したりできます。 この機能が不要な場合、**VSPerfASPNETCmd** コマンドライン ツールも利用できます。 [VSPerfCmd](../profiling/vsperfcmd.md) コマンド ライン ツールと比較すると、環境変数を設定する必要がなく、コンピューターを再起動する必要がありません。 詳細については、「 [VSPerfASPNETCmd を使用した迅速な Web サイトプロファイリング](../profiling/rapid-web-site-profiling-with-vsperfaspnetcmd.md)」を参照してください。  
  
## <a name="common-tasks"></a>一般的なタスク  
  
|タスク|関連するコンテンツ|  
|----------|---------------------|  
|**プロファイラーを実行中の ASP.NET アプリケーションにアタッチする**|-   [方法: プロファイラーを ASP.NET Web アプリケーションにアタッチし、メモリ データを収集する](../profiling/how-to-attach-the-profiler-to-an-aspnet-web-application-to-collect-memory-data-by-using-the-command-line.md)|  
|**静的にコンパイルされたバイナリをインストルメント化する**|-   [方法: 静的にコンパイルされた ASP.NET アプリケーションをインストルメント化し、メモリ データを収集する](../profiling/how-to-instrument-a-statically-compiled-aspnet-web-application-and-collect-memory-data-by-using-the-profiler-command-line.md)|  
|**動的にコンパイルされたバイナリをインストルメント化する**|-   [方法: 動的にコンパイルされた ASP.NET アプリケーションをインストルメントし、メモリデータを収集する](../profiling/how-to-instrument-a-dynamically-compiled-aspnet-web-application-and-collect-memory-data-by-using-the-profiler-command-line.md)|  
  
## <a name="related-tasks"></a>Related Tasks  
  
### <a name="profiling-aspnet-web-applications"></a>ASP.NET Web アプリケーションのプロファイリング  
  
|タスク|関連するコンテンツ|  
|----------|---------------------|  
|**サンプリング メソッドを使用したプロファイリング**|-   [サンプリングを使用したアプリケーション統計情報の収集](../profiling/collecting-application-statistics-for-aspnet-web-applications-using-the-profiler-sampling-method-from-the-command-line.md)|  
|**インストルメンテーション方式を使用したプロファイリング**|-   [インストルメンテーションを使用した詳細なタイミングデータの収集](/visualstudio/profiling/collecting-detailed-timing-data-aspnet-profiler-instrumentation-method?view=vs-2015)|  
|**リソースの競合とスレッド アクティビティのプロファイリング**|-   [同時実行データの収集](../profiling/collecting-concurrency-data-for-an-aspnet-web-application-using-the-profiler-command-line.md)|  
  
### <a name="profiling-net-framework-memory-data"></a>.NET Framework メモリ データのプロファイリング  
  
|タスク|関連するコンテンツ|  
|----------|---------------------|  
|**スタンドアロン (クライアント) アプリケーションのプロファイリング**|-   [.NET Framework メモリ データの収集](../profiling/collecting-dotnet-framework-memory-data-for-stand-alone-applications-by-using-the-profiler-command-line.md)|  
|**サービスのプロファイリング**|-   [.NET メモリデータの収集](../profiling/collecting-memory-data-from-dotnet-framework-services-by-using-the-profiler-command-line.md)|  
  
### <a name="analyzing-net-memory-data-views-and-reports"></a>.NET メモリ データ ビューとレポートの分析  
 [.NET メモリデータビュー](../profiling/dotnet-memory-data-views.md)  
  
## <a name="reference"></a>リファレンス  
 [コマンドラインプロファイルツールリファレンス](../profiling/command-line-profiling-tools-reference.md)
