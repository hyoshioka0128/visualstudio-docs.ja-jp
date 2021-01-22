---
title: サンプリングを使用したパフォーマンス統計情報の収集
description: プロファイル ツールのサンプリング メソッドを使用して、プロセッサ使用率の問題を見つけます。 これはほとんどのパフォーマンス調査を開始するために推奨されるメソッドです。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- Profiling Tools,sampling
- sampling profiling method
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: e5a58ec02fa6bff0dd06ce08b933a381bca37a80
ms.sourcegitcommit: 7a5c4f60667b5792f876953d55192b49a73f5fe9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/16/2021
ms.locfileid: "98533733"
---
# <a name="collect-performance-statistics-by-using-sampling"></a>サンプリングを使用したパフォーマンス統計情報の収集

既定では、Visual Studio Profiling Tools のサンプリング メソッドは、10,000,000 プロセッサ サイクルごと (1 GHz コンピューターで約 100 分の 1 秒ごと) にプロファイリング情報を収集します。 このサンプリング メソッドはプロセッサ使用率の問題を検出するのに役立ち、ほとんどのパフォーマンス調査を開始するときに推奨される方法です。

> [!NOTE]
> Windows 8 および Windows Server 2012 の強化されたセキュリティ機能によって、Visual Studio プロファイラーがこれらのプラットフォームでデータを収集する方法に大幅な変更が必要になりました。 UWP アプリにも新しい収集手法が必要です。 ｢[Windows 8 および Windows Server 2012 アプリケーションのパフォーマンス ツール](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)」を参照してください。

サンプリング メソッドは、次のいずれかの手順を使用して指定できます。

- プロファイリング ウィザードの最初のページで **[CPU サンプリング (推奨)]** をクリックします。
- **パフォーマンス エクスプローラー** のツールバーで、 **[メソッド]** 一覧の **[サンプリング]** をクリックします。
- パフォーマンス セッションの [プロパティ] ダイアログ ボックスの **[全般]** ページで、 **[サンプリング]** をクリックします。

## <a name="common-tasks"></a>一般的なタスク

追加のオプションを、パフォーマンス セッションの [ _パフォーマンス セッション]_ **[プロパティ ページ]** ダイアログ ボックスで指定できます。 このダイアログ ボックスを開くには:

- **パフォーマンス エクスプローラー** で、パフォーマンス セッション名を右クリックして **[プロパティ]** をクリックします。

  次の表の各タスクでは、サンプリング メソッドを使用してプロファイリングを実行する際に、 _[パフォーマンス セッション]_ **[プロパティ ページ]** ダイアログ ボックスで指定できるオプションについて説明しています。

|タスク|関連コンテンツ|
|----------|---------------------|
|**[全般]** ページで、.NET のメモリ割り当ておよび有効期間データ コレクションを追加し、生成されるプロファイリング データ (.vsp) ファイルの名前付けの詳細を指定します。|- [.NET メモリの割り当ておよび有効期間データの収集](../profiling/collecting-dotnet-memory-allocation-and-lifetime-data.md)<br />- [方法: パフォーマンス データ ファイル名のオプションを設定する](../profiling/how-to-set-performance-data-file-name-options.md)|
|**[サンプリング]** ページで、サンプリング速度を変更するか、プロセッサのクロック サイクルのサンプリング イベントを別のプロセッサ パフォーマンス カウンターを変更するか、または両方を変更します。|- [方法 : サンプリング イベントを選択する](../profiling/how-to-choose-sampling-events.md)|
|コード ソリューション内に複数の .exe プロジェクトがある場合は、 **[起動]** ページで、開始するアプリケーションおよび開始順序を指定します。|- [階層相互作用データの収集](../profiling/collecting-tier-interaction-data.md)|
|**[階層の相互作用]** ページで、実行するプロファイルで収集されるデータに ADO.NET 呼び出し情報を追加します。|- [階層相互作用データの収集](../profiling/collecting-tier-interaction-data.md)|
|**[Windows イベント]** ページで、サンプリング データと共に収集する 1 つ以上の ETW (Windows イベント トレーシング) イベントを指定します。|- [方法: ETW (Event Tracing for Windows) データを収集する](../profiling/how-to-collect-event-tracing-for-windows-etw-data.md)|
|**[Windows カウンター]** ページで、プロファイリング データをマークとして追加するオペレーティング システムのパフォーマンス カウンターを 1 つ以上指定します。|- [方法 : Windows カウンター データを収集する](../profiling/how-to-collect-windows-counter-data.md)|
|アプリケーション モジュールで複数のバージョンを使用する場合は、 **[詳細]** ページで、プロファイリングする .NET Framework ランタイムのバージョンを指定します。 既定では、最初に読み込まれたバージョンがプロファイリングされます。|- [方法: side-by-side 実行でプロファイリングするように .NET Framework ランタイムを指定する](../profiling/how-to-specify-the-dotnet-framework-runtime.md)|
