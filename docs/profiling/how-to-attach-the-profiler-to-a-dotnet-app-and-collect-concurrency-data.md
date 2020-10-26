---
title: プロファイラーを .NET アプリにアタッチし、コンカレンシー データを収集する | Microsoft Docs
ms.custom: seodec18
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: fdd41576-797e-4312-8520-fee7bb767e4a
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- dotnet
ms.openlocfilehash: ab5ae5059b5315d37f6b471c31026e6fe6609e8b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85330151"
---
# <a name="how-to-attach-the-profiler-to-a-net-framework-stand-alone-application-to-collect-concurrency-data-by-using-the-command-line"></a>方法: コマンド ラインを使用してプロファイラーをスタンドアロンの .NET Framework アプリケーションにアタッチし、コンカレンシー データを収集する
この記事では、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] プロファイル ツールのコマンド ライン ツールを使用して、実行中の .NET Framework のスタンドアロン (クライアント) アプリケーションにプロファイラーをアタッチし、プロセスとスレッドのコンカレンシー データを収集する方法について説明します。

> [!NOTE]
> プロファイル ツールへのパスを取得するには、「[チュートリアル:プロファイラー API の使用](../profiling/walkthrough-using-profiler-apis.md)」をご覧ください。 64 ビット コンピューター上では、64 ビット バージョンのツールと 32 ビット バージョンのツールの両方を使用できます。 プロファイラー コマンド ライン ツールを使用するには、コマンド プロンプト ウィンドウの PATH 環境変数にツールのパスを追加するか、コマンド自体にそれを追加します。 詳細については、「[コマンド ライン ツールへのパスの指定](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md)」をご覧ください。

 プロファイラーをアプリケーションにアタッチしている間はデータ収集を一時停止し、完了後に再開できます。 プロファイル セッションを終了するには、アプリケーションへのプロファイラーのアタッチを解除し、プロファイラーを明示的に終了する必要があります。

## <a name="attach-the-profiler"></a>プロファイラーのアタッチ

#### <a name="to-attach-the-profiler-to-a-running-net-framework-application"></a>実行中の .NET Framework アプリケーションにプロファイラーをアタッチするには

1. コマンド プロンプト ウィンドウを開きます。

2. プロファイラーを起動します。 型:

     [VSPerfCmd](../profiling/vsperfcmd.md) **/start:concurrency  /output:** `OutputFile` [`Options`]

     **/start** を使用するには、[/output](../profiling/output.md) **:** `OutputFile` オプションを指定する必要があります。 `OutputFile` には、プロファイル データ (.vsp) ファイルの名前と場所を指定します。

     **/start:concurrency** オプションを使用する場合は、次のうちいずれかのオプションを指定できます。

    |オプション|説明|
    |------------|-----------------|
    |[/wincounter](../profiling/wincounter.md) **:** `WinCounterPath`|プロファイリング実行中に収集する Windows パフォーマンス カウンターを指定します。|
    |[/automark](../profiling/automark.md) **:** `Interval`|**/wincounter** との組み合わせでのみ使用します。 Windows パフォーマンス カウンター コレクション イベントの間隔をミリ秒単位で指定します。 既定値は 500 ミリ秒です。|
    |[/events](../profiling/events-vsperfcmd.md) **:** `Config`|プロファイリング実行中に収集する ETW (Event Tracing for Windows) イベントを指定します。 ETW イベントは独立した (.etl) ファイルに収集されます。|

3. 一般的な方法で対象のアプリケーションを起動します。

4. プロファイラーを対象のアプリケーションにアタッチします。 型:

     **VSPerfCmd /attach:** `PID` **[/lineoff]** [ **/targetclr:** `Version`]

    - `PID` には、対象アプリケーションのプロセス ID を指定します。 Windows タスク マネージャーで、実行中のすべてのプロセスのプロセス ID を参照できます。

    - [/lineoff](../profiling/lineoff.md) を指定すると、行番号データの収集が無効になります。

    - [/targetclr](../profiling/targetclr.md) **:** `Version` には、アプリケーションに複数のバージョンのランタイムが読み込まれている場合に、プロファイリングを行う共通言語ランタイム (CLR) のバージョンを指定します。 任意。

## <a name="control-data-collection"></a>データ収集の制御
 対象アプリケーションの実行中は、*VSPerfCmd.exe* のオプションを使用してファイルへのデータ書き込みを開始および停止することにより、データ収集を制御できます。 データ収集を制御することにより、アプリケーションの起動や終了など、プログラム実行の特定の部分についてのデータ収集を行うことができます。

#### <a name="to-start-and-stop-data-collection"></a>データ収集を開始および停止するには

- 次の *VSPerfCmd.exe* オプションの組み合わせにより、データ収集を開始し、停止します。 個別のコマンド ラインで各オプションを指定します。 データ収集のオンとオフは複数回切り替えることができます。

    |オプション|説明|
    |------------|-----------------|
    |[/globalon /globaloff](../profiling/globalon-and-globaloff.md)|すべてのプロセスのデータ収集を開始 ( **/globalon**) または停止 ( **/globaloff**) します。|
    |[/processon](../profiling/processon-and-processoff.md) **:** `PID` [/processoff](../profiling/processon-and-processoff.md) **:** `PID`|プロセス ID (`PID`) で指定されたプロセスのデータ収集を開始 ( **/processon**) または停止 ( **/processoff**) します。|
    |[/attach](../profiling/attach.md) **:** {`PID`&#124;`ProcName`} [/detach](../profiling/detach.md)[ **:** {`PID`&#124;`ProcName`}]|**/attach** は、プロセス ID (`PID`) またはプロセス名 (ProcName) で指定したプロセスのデータ収集を開始します。 **/detach** は、指定されたプロセスのデータ収集を停止します。特定のプロセスが指定されていない場合は、すべてのプロセスのデータ収集を停止します。|

## <a name="end-the-profiling-session"></a>プロファイル セッションの終了
 プロファイル セッションを終了するには、プロファイラーがデータ収集を停止している必要があります。 アプリケーションを終了するか **VSPerfCmd /detach** オプションを呼び出すことによって、コンカレンシー メソッドを使用してプロファイリングが実行されているアプリケーションからのデータ収集を停止できます。 次に、**VSPerfCmd /shutdown** オプションを呼び出して、プロファイラーをオフにし、プロファイル データ ファイルを閉じます。 **VSPerfClrEnv /off** コマンドは、プロファイル環境変数を消去します。

#### <a name="to-end-a-profiling-session"></a>プロファイル セッションを終了するには

1. 対象アプリケーションからプロファイラーをデタッチするには、次のいずれかの操作を行います。

    - **VSPerfCmd /detach** と入力します

         \- または -

    - 対象アプリケーションを終了します。

2. プロファイラーをシャットダウンします。 型:

     VSPerfCmd[/shutdown](../profiling/shutdown.md)
