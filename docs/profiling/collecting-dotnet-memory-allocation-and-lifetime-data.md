---
title: .NET メモリの割り当てと有効期間データの収集
description: .NET アプリケーションでメモリ関連のパフォーマンスの問題を検出するには、プロファイル ツールを使用してメモリ割り当てとオブジェクト有効期間データを収集します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- .NET memory profiling method
- Profiling Tools,.NET memory method
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- dotnet
ms.openlocfilehash: a9321ce83f65d5a7cac95d793d5f635651bef0e7
ms.sourcegitcommit: 7a5c4f60667b5792f876953d55192b49a73f5fe9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/16/2021
ms.locfileid: "98533798"
---
# <a name="collect-net-framework-memory-allocation-and-lifetime-data"></a>.NET Framework メモリの割り当てと有効期間データの収集

Visual Studio プロファイリング ツールは、.NET Framework メモリ割り当てとオブジェクト有効期間データの収集をサポートしています。アプリケーションのメモリに関連するパフォーマンスの問題を検出できます。

- .NET メモリ割り当てに関するデータには、割り当てられた .NET Framework メモリ オブジェクトのサイズと数が含まれています。

- オブジェクトの有効期間データには、3 つのガベージ コレクション生成で解放される .NET Framework メモリ オブジェクトのサイズと数が含まれています。

> [!NOTE]
> Windows 8 および Windows Server 2012 の強化されたセキュリティ機能によって、Visual Studio プロファイラーがこれらのプラットフォームでデータを収集する方法に大幅な変更が必要になりました。 UWP アプリにも新しい収集手法が必要です。 「[Windows 8 および Windows Server 2012 アプリケーションのパフォーマンス ツール](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)」を参照してください。

データを収集するには、サンプリングまたはインストルメンテーション プロファイリング メソッドを使用します。

- サンプリング メソッドを使用すると、プロファイラーでは、開始またはアタッチされたプロセスで生成されたすべての .NET メモリ割り当てとオブジェクトが追跡されます。

- インストルメンテーション メソッドを使用すると、プロファイラーでは、インストルメント化されたモジュールで生成された .NET メモリ割り当てとオブジェクトのみが追跡されます。

> [!IMPORTANT]
> サンプリング メソッドを使用して .NET メモリ データ (割り当てかオブジェクトの有効期間、またはその両方) を収集している場合、ユーザーが指定したサンプリング イベントはすべて無視され、適切なメモリの割り当てイベントを使用してデータが収集されます。

.NET メモリ割り当てのプロファイリングを有効にすると、割り当てビューも有効になります。 .NET 有効期間データのプロファイリングを有効にすると、オブジェクトの有効期間ビューも有効になります。 詳細については、「[.NET メモリの割り当てビュー](../profiling/dotnet-memory-allocations-view.md)」と「[オブジェクトの有効期間ビュー](../profiling/object-lifetime-view.md)」を参照してください。

プロファイリング ツール コマンドライン ツールを使用して .NET メモリ データを収集する方法の詳細については、「[各種のプロファイル方法を使用したコマンド ラインからのパフォーマンス データの収集](../profiling/using-profiling-methods-to-collect-performance-data-from-the-command-line.md)」の「.NET メモリ メソッドを使用してメモリの割り当てとオブジェクトの有効期間のデータを収集する」を参照してください。

## <a name="to-collect-net-memory-data"></a>.NET メモリ データを収集するには

1. **パフォーマンス エクスプローラー** で、パフォーマンス セッションを右クリックして、 **[プロパティ]** をクリックします。

2. *[パフォーマンス セッション]* **[プロパティ ページ]** ダイアログ ボックスで **[全般]** タブをクリックし、 **[.NET オブジェクトの割り当て情報を収集]** チェック ボックスをオンにします。

3. .NET オブジェクトの有効期間データを収集するには、 **[.NET オブジェクトの有効期間情報も収集]** チェック ボックスをオンにします。

## <a name="common-tasks"></a>一般的なタスク

追加のオプションを、パフォーマンス セッションの [ _パフォーマンス セッション]_ **[プロパティ ページ]** ダイアログ ボックスで指定できます。 このダイアログ ボックスを開くには:

- **パフォーマンス エクスプローラー** で、パフォーマンス セッション名を右クリックして **[プロパティ]** をクリックします。

次の表の各タスクでは、.NET メモリ データを収集する際に、 _[パフォーマンス セッション]_ **[プロパティ ページ]** ダイアログ ボックスで指定できるオプションについて説明しています。

|タスク|関連コンテンツ|
|----------|---------------------|
|**[全般]** ページで、生成されるプロファイリング データ (.vsp) ファイルの名前付けの詳細を指定します。|- [.NET メモリの割り当てと有効期間データの収集](../profiling/collecting-dotnet-memory-allocation-and-lifetime-data.md)<br />- [方法: パフォーマンス データ ファイル名のオプションを設定する](../profiling/how-to-set-performance-data-file-name-options.md)|
|コード ソリューション内に複数の .exe プロジェクトがある場合は、 **[起動]** ページで、開始するアプリケーションを選択します。|- [階層相互作用データを収集する](../profiling/collecting-tier-interaction-data.md)|
|**[階層の相互作用]** ページで、プロファイリング実行に ADO.NET 呼び出しデータを追加します。|- [階層相互作用データを収集する](../profiling/collecting-tier-interaction-data.md)|
|**[Windows イベント]** ページで、サンプリング データと共に収集する 1 つ以上の ETW (Windows イベント トレーシング) イベントを指定します。|- [方法: ETW (Event Tracing for Windows) データを収集する](../profiling/how-to-collect-event-tracing-for-windows-etw-data.md)|
|**[Windows カウンター]** ページで、プロファイリング データをマークとして追加するオペレーティング システムのパフォーマンス カウンターを 1 つ以上指定します。|- [方法: Windows カウンター データを収集する](../profiling/how-to-collect-windows-counter-data.md)|
|アプリケーション モジュールで複数のバージョンを使用する場合は、 **[詳細]** ページで、プロファイリングする .NET Framework ランタイムのバージョンを指定します。 既定では、最初に読み込まれたバージョンがプロファイリングされます。|- [方法: .NET Framework ランタイムを指定する](../profiling/how-to-specify-the-dotnet-framework-runtime.md)|

## <a name="instrumentation-tasks"></a>インストルメンテーション タスク

次の表のタスクは、インストルメンテーション メソッドでのプロファイリングに固有の **[プロパティ ページ]** ダイアログ ボックスのオプションです。

|タスク|関連するコンテンツ|
|----------|---------------------|
|**[バイナリ]** ページで、モジュールのインストルメント化されたコピーの場所を指定します。 既定では、元のバイナリはバックアップ フォルダーに移動されます。|- [方法: インストルメント化されたバイナリの再配置](../profiling/how-to-relocate-instrumented-binaries.md)|
|**[インストルメンテーション]** ページで、プロファイリングのオーバーヘッドを低減するために小規模関数を除外し、ASP.NET Web ページで JavaScript コードをプロファイルし、インストルメンテーション処理の前と後にコマンド プロンプトで実行するコマンドを指定します。|- [方法: インストルメンテーションで短い関数を除外または含める](../profiling/how-to-exclude-or-include-short-functions-from-instrumentation.md)<br />- [方法: Web ページ内の JavaScript コードをプロファイリングする](../profiling/how-to-profile-javascript-code-in-web-pages.md)<br />- [方法: インストルメント前のコマンドおよびインストルメント後のコマンドを指定する](../profiling/how-to-specify-pre-and-post-instrument-commands.md)|
|**[CPU カウンター]** ページで、プロファイリング データを追加するプロセッサのパフォーマンス カウンターを 1 つ以上指定します。|- [方法: CPU カウンター データを収集する](../profiling/how-to-collect-cpu-counter-data.md)|
|**[詳細]** ページで、追加する VSInstr.exe オプションをすべて指定します (特定の関数を含めるオプションや特定の関数を除外するオプションなど)。 VSInstr オプションの詳細については、「[VSInstr](../profiling/vsinstr.md)」を参照してください。|- [方法: 追加のインストルメンテーション オプションを指定する](../profiling/how-to-specify-additional-instrumentation-options.md)<br />- [方法: インストルメンテーションを特定の関数に制限する](../profiling/how-to-limit-instrumentation-to-specific-functions.md)|

## <a name="see-also"></a>関連項目

[パフォーマンス セッションの構成](../profiling/configuring-performance-sessions.md)
[方法: 収集方法を選択する](../profiling/how-to-choose-collection-methods.md)
[パフォーマンス セッションのプロパティ](../profiling/performance-session-properties.md)
