---
title: コマンド ラインのプロファイル方法を使ってパフォーマンス データを取得する
description: プロファイル対象のアプリケーションの種類などの要因によって、選択する Visual Studio プロファイル ツールのコマンド ライン ツールやオプションがどのように変わるかについて学習します。
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 5613fafc-f298-4e7a-9a2d-a853b61cdf9c
author: mikejo5000
ms.author: mikejo
manager: jmartens
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: ebcd3fdbc09029309d1b06efc75417add223ce04
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99917587"
---
# <a name="use-profiling-methods-to-collect-performance-data-from-the-command-line"></a>各種のプロファイル方法を使用したコマンド ラインからのパフォーマンス データの収集
使用する [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] プロファイル ツールのコマンド ライン ツールおよびオプションは、プロファイル対象のアプリケーションの種類、使用するプロファイル方法、ターゲット アプリケーションが、ネイティブ コードと .NET Framework コードのどちらで記述されているかなどの要因によって決まります。

 このトピックでは、コマンド ラインの手順について、使用するプロファイル方法ごとに説明します。

## <a name="use-the-sampling-method-to-collect-performance-statistics"></a>サンプリング メソッドを使用してパフォーマンス統計情報を収集する
 プロファイリング ツールのサンプリング メソッドでは、プロファイリングの実行中、指定した間隔でパフォーマンス データを収集します。 サンプリング データは、CPU 制約によるパフォーマンス上の問題を把握するのに役立ち、アプリケーションのパフォーマンスを調べるための最初の方法として適しています。

 プロファイラーとアプリケーションを同時に開始することも、実行中のアプリケーションのインスタンスにプロファイラーをアタッチすることもできます。

|タスク|ターゲット アプリケーションの種類|
|----------|-----------------------------|
|**アプリケーションを起動する**|-   [スタンドアロン アプリケーション](../profiling/how-to-launch-a-stand-alone-app-and-collect-application-statistics.md)|
|**実行中のプロセスにアタッチする**|-   [スタンドアロンの .NET Framework アプリケーション](../profiling/how-to-attach-the-profiler-to-a-dotnet-app-and-collect-application-statistics.md)<br />-   [スタンドアロンのネイティブ アプリケーション](../profiling/how-to-attach-the-profiler-to-a-native-app-and-collect-application-statistics.md)<br />-   [ASP.NET Web アプリケーション](../profiling/how-to-attach-the-profiler-to-an-aspnet-web-application-to-collect-application-statistics-by-using-the-command-line.md)<br />-   [.NET サービス](../profiling/how-to-attach-the-profiler-to-a-dotnet-service-to-collect-application-statistics-by-using-the-command-line.md)<br />-   [ネイティブ サービス](../profiling/how-to-attach-the-profiler-to-a-native-service-to-collect-application-statistics-by-using-the-command-line.md)|

## <a name="use-the-instrumentation-method-to-collect-detailed-timing-data"></a>インストルメンテーション メソッドを使用して詳しいタイミング データを収集する
 プロファイリング ツールのインストルメンテーション メソッドでは、パフォーマンス情報を記録するためのソフトウェア プローブを含むアプリケーション バイナリのコピーからパフォーマンス データを収集します。 インストルメント化された各関数の開始時と終了時、およびインストルメント化された関数から他の関数を呼び出すたびに、インストルメンテーション データが収集されます。 インストルメンテーション メソッドは、ディスクの使用率などの I/O の問題に関連するパフォーマンス上の問題を検出するのに役立ちます。

 [VInstr.exe](../profiling/vsinstr.md) ツールを使用すると、インストルメント化されたバイナリを作成できます。 プロファイラーを初期化すると、ターゲット アプリケーションの実行時にインストルメント化されたバイナリからデータが自動的に収集されます。

 **ターゲット アプリケーションの種類**

- [スタンドアロンの .NET Framework コンポーネント](../profiling/how-to-instrument-a-dotnet-framework-component-and-collect-timing-data.md)

- [スタンドアロンのネイティブ コンポーネント](../profiling/how-to-instrument-a-native-component-and-collect-timing-data.md)

- [静的にコンパイルされた ASP.NET Web アプリケーション](../profiling/how-to-instrument-statically-compiled-aspnet-and-collect-detailed-timing-data.md)

- [動的にコンパイルされた ASP.NET Web アプリケーション](../profiling/how-to-instrument-a-dynamically-compiled-aspnet-app-and-collect-timing-data.md)

- [.NET サービス](../profiling/how-to-instrument-a-dotnet-service-and-collect-detailed-timing-data-by-using-the-profiler-command-line.md)

- [ネイティブ サービス](../profiling/how-to-instrument-a-native-service-and-collect-detailed-timing-data-by-using-the-profiler-command-line.md)

## <a name="use-net-memory-methods-to-collect-memory-allocation-and-object-lifetime-data"></a>.NET メモリ メソッドを使用してメモリの割り当てとオブジェクトの有効期間のデータを収集する
 プロファイル ツールの .NET メモリ メソッドを使用すると、.NET Framework メモリの割り当てデータおよび .NET Framework のオブジェクトの有効期間に関する情報を収集できます。

 プロファイラーを使用してターゲット アプリケーションを開始できるほか、実行中のアプリケーションのインスタンスにプロファイラーをアタッチすることもできます。また、.NET Framework メモリ データと共に詳しいタイミング情報を収集するためのインストルメント化されたバージョンのアプリケーションを作成することもできます。

|タスク|ターゲット アプリケーションの種類|
|----------|-----------------------------|
|**アプリケーションを起動する**|-   [スタンドアロンの .NET Framework アプリケーション](../profiling/how-to-launch-a-stand-alone-dotnet-framework-app-to-collect-memory-data.md)|
|**実行中のプロセスにアタッチする**|-   [スタンドアロンの .NET Framework アプリケーション](../profiling/how-to-attach-the-profiler-to-a-dotnet-framework-app-to-collect-memory-data.md)<br />-   [ASP.NET Web アプリケーション](../profiling/how-to-attach-the-profiler-to-an-aspnet-web-application-to-collect-memory-data-by-using-the-command-line.md)<br />-   [.NET サービス](../profiling/how-to-attach-the-profiler-to-a-dotnet-service-to-collect-memory-data-by-using-the-command-line.md)|
|**モジュールをインストルメント化する**|-   [スタンドアロンの .NET Framework コンポーネント](../profiling/how-to-instrument-a-dotnet-framework-component-and-collect-memory-data.md)<br />-   [静的にコンパイルされた ASP.NET Web アプリケーション](../profiling/how-to-instrument-a-statically-compiled-aspnet-app-and-collect-memory-data.md)<br />-   [動的にコンパイルされた ASP.NET Web アプリケーション](../profiling/how-to-instrument-a-dynamically-compiled-aspnet-web-application-and-collect-memory-data.md)<br />-   [.NET サービス](../profiling/how-to-instrument-a-dotnet-framework-service-and-collect-memory-data-by-using-the-profiler-command-line.md)|

## <a name="use-the-concurrency-method-to-collect-resource-contention-and-thread-activity-data"></a>コンカレンシー メソッドを使用してリソースの競合およびスレッド アクティビティのデータを収集する
 プロファイリング ツールのコンカレンシー メソッドを使用すると、マルチスレッド アプリケーションのリソースの競合およびスレッドとプロセスのアクティビティ データを収集できます。

 プロファイラーを使用してアプリケーションを開始することも、実行中のアプリケーションのインスタンスにプロファイラーをアタッチすることもできます。

|タスク|ターゲット アプリケーションの種類|
|----------|-----------------------------|
|**アプリケーションを起動する**|-   [スタンドアロンの .NET Framework アプリケーション](../profiling/how-to-launch-a-stand-alone-dotnet-framework-app-to-collect-concurrency-data.md)<br />-   [スタンドアロンのネイティブ アプリケーション](../profiling/how-to-launch-a-stand-alone-native-application-to-collect-concurrency-data.md)|
|**実行中のプロセスにアタッチする**|-   [スタンドアロンの .NET Framework アプリケーション](../profiling/how-to-attach-the-profiler-to-a-dotnet-app-and-collect-concurrency-data.md)<br />-   [スタンドアロンのネイティブ アプリケーション](../profiling/how-to-attach-the-profiler-to-a-native-app-and-collect-concurrency-data.md)<br />-   [ASP.NET Web アプリケーション](../profiling/how-to-attach-the-profiler-to-an-aspnet-web-application-to-collect-concurrency-data-by-using-the-command-line.md)<br />-   [.NET サービス](../profiling/how-to-attach-the-profiler-to-a-dotnet-service-to-collect-concurrency-data-by-using-the-command-line.md)<br />-   [ネイティブ サービス](../profiling/how-to-attach-the-profiler-to-a-native-service-to-collect-concurrency-data-by-using-the-command-line.md)|

## <a name="add-tier-interaction-data-to-a-profiling-run"></a>プロファイリングの実行に階層の相互作用データを追加する
 プロファイリングの実行に階層の相互作用データを追加するには、コマンド ライン プロファイリング ツールによる特定の手順が必要です。 「[階層相互作用データの収集](../profiling/adding-tier-interaction-data-from-the-command-line.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [スタンドアロン アプリケーションのプロファイリング](../profiling/command-line-profiling-of-stand-alone-applications.md)
- [ASP.NET Web アプリケーションのプロファイリング](../profiling/command-line-profiling-of-aspnet-web-applications.md)
- [サービスのプロファイリング](../profiling/command-line-profiling-of-services.md)
