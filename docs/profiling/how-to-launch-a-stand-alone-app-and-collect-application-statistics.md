---
title: Profiler コマンド ライン:スタンドアロン アプリを起動させ、アプリの統計を取得する
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 52dcee2b-f178-4a76-bddc-e36c50bfcb78
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: fb6228592115091dc538dbe59c227a180e75aa10
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "74775419"
---
# <a name="how-to-launch-a-stand-alone-application-with-the-profiler-and-collect-application-statistics-by-using-the-command-line"></a>方法: コマンド ラインを使用してプロファイラーでスタンドアロン アプリケーションを起動し、アプリケーション統計情報を収集する
ここでは、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] プロファイリング ツールのコマンド ライン ツールを使用してスタンドアロン (クライアント) アプリケーションを起動し、サンプリング メソッドによってパフォーマンスに関する統計情報を収集する方法について説明します。

> [!NOTE]
> Windows 8 および Windows Server 2012 の強化されたセキュリティ機能によって、Visual Studio プロファイラーがこれらのプラットフォームでデータを収集する方法に大幅な変更が必要になりました。 UWP アプリにも新しい収集手法が必要です。 「[Windows 8 および Windows Server 2012 アプリケーションのパフォーマンス ツール](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)」を参照してください。
>
> プロファイリングの実行に階層の相互作用データを追加するには、コマンド ライン プロファイル ツールによる特定の手順が必要です。 「[階層相互作用データの収集](../profiling/adding-tier-interaction-data-from-the-command-line.md)」を参照してください。

 プロファイラー コマンド ライン ツールを使用するには、コマンド プロンプト ウィンドウの PATH 環境変数にそのパスを追加するか、コマンド自体にこのパスを追加します。 Visual Studio がインストールされているコンピューターで、Visual Studio のコマンド ウィンドウからプロファイリング ツールを実行できます。

1. Visual Studio がインストールされているコンピューターでプロファイリング ツールを実行している場合、Visual Studio のコマンド ウィンドウによって正しいパスが設定されます。 **[ツール]** メニューで **[Visual Studio コマンド プロンプト]** を選択します。

> [!NOTE]
> プロファイル ツールへのパスを取得するには、[コマンド ライン ツールへのパスの指定](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md)に関する記事をご覧ください。 64 ビット コンピューター上では、64 ビット バージョンのツールと 32 ビット バージョンのツールの両方を使用できます。 プロファイラー コマンド ライン ツールを使用するには、コマンド プロンプト ウィンドウの PATH 環境変数にツールのパスを追加するか、コマンド自体にそれを追加します。

## <a name="start-the-application-with-the-profiler"></a>プロファイラーによるアプリケーションの起動
 プロファイラーを使用して対象のアプリケーションを起動するには、VSPerfCmd の **/start** オプションと **/launch** オプションを使用して、プロファイラーを初期化し、アプリケーションを起動します。 **/start** と **/launch**、およびそれぞれのオプションは、1 つのコマンド ラインで指定できます。

 **/globaloff** オプションを追加して、対象アプリケーションの起動時にデータ収集を一時停止することもできます。 次に、 **/globalon** を使用してデータの収集を開始します。

#### <a name="to-start-an-application-by-using-the-profiler"></a>プロファイラーを使用してアプリケーションを起動するには

1. コマンド プロンプト ウィンドウを開きます。

2. プロファイラーを起動します。 型:

    **VSPerfCmd /start:sample /output:** `OutputFile` [`Options`]

   - [/start](../profiling/start.md) **:sample** オプションによってプロファイラーが初期化されます。

   - **/start** を使用するには、[/output](../profiling/output.md) **:** `OutputFile` オプションを指定する必要があります。 `OutputFile` には、プロファイル データ (.vsp) ファイルの名前と場所を指定します。

     **/start:sample** オプションを使用する場合は、次のうちいずれかのオプションを指定できます。

   | オプション | 説明 |
   | - | - |
   | [/wincounter](../profiling/wincounter.md) **:** `WinCounterPath` | プロファイリング実行中に収集する Windows パフォーマンス カウンターを指定します。 |
   | [/automark](../profiling/automark.md) **:** `Interval` | **/wincounter** との組み合わせでのみ使用します。 Windows パフォーマンス カウンター コレクション イベントの間隔をミリ秒単位で指定します。 既定値は 500 ミリ秒です。 |
   | [/events](../profiling/events-vsperfcmd.md) **:** `Config` | プロファイリング実行中に収集する ETW (Event Tracing for Windows) イベントを指定します。 ETW イベントは独立した (.*etl*) ファイルに収集されます。 |

3. 対象アプリケーションを起動します。 **VSPerfCmd /launch:** `appName` [`Options`] [`Sample Event`] と入力します。

    **/launch** オプションを使用する場合は、次のうちから 1 つ以上のオプションを指定できます。

   |オプション|説明|
   |------------|-----------------|
   |[/args](../profiling/args.md) **:** `Arguments`|対象アプリケーションへ渡されるコマンド ライン引数を格納する文字列を指定します。|
   |[/console](../profiling/console.md)|対象のコマンド ライン アプリケーションを別のウィンドウで起動でします。|

    既定では、パフォーマンス データはプロセッサのクロック サイクル数 10,000,000 (停止なし) ごとにサンプリングされます。 このため、1 GHz のプロセッサでは 10 ミリ秒ごとに約 1 回です。 次のオプションのいずれかを指定すると、クロック サイクルの間隔の変更や、別のサンプリング イベントの指定ができます。

   |サンプリング イベント|説明|
   |------------------|-----------------|
   |[/timer](../profiling/timer.md) **:** `Interval`|サンプリングの間隔を、`Interval` で指定された停止なしのクロック サイクル数に変更します。|
   |[/pf](../profiling/pf.md)[ **:** `Interval`]|サンプリング イベントをページ フォールトに変更します。 `Interval` を指定した場合は、サンプル間のページ フォールト数が設定されます。 既定値は 10 です。|
   |[/sys](../profiling/sys-vsperfcmd.md)[ **:** `Interval`]|サンプリング イベントを、プロセスからオペレーティング システムのカーネルへのシステム コール (syscall) に変更します。 `Interval` を指定した場合は、サンプル間の呼び出し回数が設定されます。 既定値は 10 です。|
   |[/counter](../profiling/counter.md) **:** `Config`|サンプリング イベントと間隔を、プロセッサのパフォーマンス カウンターと、`Config` で指定した間隔に、それぞれ変更します。|

## <a name="control-data-collection"></a>データ収集の制御
 対象アプリケーションの実行中に、*VSPerfCmd.exe* のオプションを使用して、プロファイラーのデータ ファイルへのデータ書き込みを開始および停止することにより、データ収集を制御できます。 データ コレクションを制御することにより、アプリケーションの起動や終了など、プログラム実行の特定の部分についてのデータ コレクションを行うことができます。

#### <a name="to-start-and-stop-data-collection"></a>データ収集を開始および停止するには

- 次に示すオプションの組み合わせにより、データ収集を開始および停止します。 個別のコマンド ラインで各オプションを指定します。 データ収集のオンとオフは複数回切り替えることができます。

    |オプション|説明|
    |------------|-----------------|
    |[/globalon /globaloff](../profiling/globalon-and-globaloff.md)|すべてのプロセスのデータ収集を開始 ( **/globalon**) または停止 ( **/globaloff**) します。|
    |[/processon](../profiling/processon-and-processoff.md) **:** `PID`  [/processoff](../profiling/processon-and-processoff.md) **:** `PID`|プロセス ID (`PID`) で指定されたプロセスのデータ収集を開始 ( **/processon**) または停止 ( **/processoff**) します。|
    |[/attach](../profiling/attach.md) **:** {`PID`&#124;`ProcName`} [/detach](../profiling/detach.md)[ **:** {`PID`&#124;`ProcName`}]|**/attach** は、`PID` またはプロセス名 (ProcName) で指定したプロセスのデータ収集を開始します。 **/detach** は、指定されたプロセスのデータ収集を停止します。特定のプロセスが指定されていない場合は、すべてのプロセスのデータ収集を停止します。|

## <a name="end-the-profiling-session"></a>プロファイル セッションの終了
 プロファイル セッションを終了するには、プロファイリングされたプロセスへのプロファイラーのアタッチを解除し、プロファイラーを明示的に終了する必要があります。 サンプリング メソッドを使用してプロファイリングを実行したアプリケーションからプロファイラーをデタッチするには、アプリケーションを終了するか、**VSPerfCmd /detach** オプションを呼び出します。 次に、**VSPerfCmd /shutdown** オプションを呼び出して、プロファイラーをオフにし、プロファイル データ ファイルを閉じます。 **VSPerfClrEnv /off** コマンドは、プロファイル環境変数を消去します。

#### <a name="to-end-a-profiling-session"></a>プロファイル セッションを終了するには

1. 対象アプリケーションからプロファイラーをデタッチするには、次のいずれかの手順を実行します。

    - 対象アプリケーションを終了します。

         \- または -

    - **VSPerfCmd /detach** と入力します

2. プロファイラーをシャットダウンします。 型:

     **VSPerfCmd**  [/shutdown](../profiling/shutdown.md)

## <a name="see-also"></a>関連項目
- [スタンドアロン アプリケーションのプロファイリング](../profiling/command-line-profiling-of-stand-alone-applications.md)
- [サンプリング メソッドのデータ ビュー](../profiling/profiler-sampling-method-data-views.md)
