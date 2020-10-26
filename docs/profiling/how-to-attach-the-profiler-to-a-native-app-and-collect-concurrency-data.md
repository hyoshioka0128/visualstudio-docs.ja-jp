---
title: プロファイラーをネイティブ アプリケーションにアタッチし、コンカレンシー データを収集する
ms.custom: seodec18
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 12d3e0f3-4b74-4e66-8fbf-8ac99bd4f91c
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- cplusplus
ms.openlocfilehash: dcc125f795a29f53abb07920aa11c9a5e6ee966b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85329521"
---
# <a name="how-to-attach-the-profiler-to-a-native-stand-alone-application-and-collect-concurrency-data-by-using-the-command-line"></a>方法: コマンド ラインを使用してスタンドアロンのネイティブ アプリケーションにプロファイラーをアタッチし、コンカレンシー データを収集する
この記事では、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] プロファイル ツールのコマンド ライン ツールを使用して、実行中のスタンドアロンのネイティブ (C/C++) アプリケーションにプロファイラーをアタッチし、スレッド競合データを収集する方法について説明します。

> [!NOTE]
> プロファイル ツールへのパスを取得するには、[コマンド ライン ツールへのパスの指定](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md)に関する記事をご覧ください。 64 ビット コンピューター上では、64 ビット バージョンのツールと 32 ビット バージョンのツールの両方を使用できます。 プロファイラー コマンド ライン ツールを使用するには、コマンド プロンプト ウィンドウの PATH 環境変数にツールのパスを追加するか、コマンド自体にそれを追加します。

 プロファイラーをアプリケーションにアタッチしている間はデータ収集を一時停止し、完了後に再開できます。 プロファイル セッションを終了するには、アプリケーションへのプロファイラーのアタッチを解除し、プロファイラーを明示的に終了する必要があります。

## <a name="attach-the-profiler-to-a-running-native-application"></a>実行中のネイティブ アプリケーションにプロファイラーをアタッチする

#### <a name="to-attach-the-profiler-to-a-running-native-application"></a>実行中のネイティブ アプリケーションにプロファイラーをアタッチするには

1. コマンド プロンプトに次のコマンドを入力します。

     [VSPerfCmd](../profiling/vsperfcmd.md) **/start:concurrency**

     **/start:concurrency** オプションと共に、次の表の任意のオプションを指定できます。

    |オプション|説明|
    |------------|-----------------|
    |[/user](../profiling/user-vsperfcmd.md) **:** [`Domain\`]`Username`|プロファイラーへのアクセスを許可するアカウントのオプションのドメインとユーザー名を指定します。|
    |[/crosssession](../profiling/crosssession.md)|他のログオン セッションにおけるプロセスのプロファイリングを有効にします。|
    |[/wincounter](../profiling/wincounter.md) **:** `WinCounterPath`|プロファイリング実行中に収集する Windows パフォーマンス カウンターを指定します。|
    |[/automark](../profiling/automark.md) **:** `Interval`|**/wincounter** との組み合わせでのみ使用します。 Windows パフォーマンス カウンター コレクション イベントの間隔をミリ秒単位で指定します。 既定値は 500 です。|
    |[/events](../profiling/events-vsperfcmd.md) **:** `Config`|プロファイリング実行中に収集する ETW (Event Tracing for Windows) イベントを指定します。 ETW イベントは独立した (.etl) ファイルに収集されます。|

2. 次のコマンドを入力して、対象アプリケーションにプロファイラーをアタッチします。

     **VSPerfCmd**  [/attach](../profiling/attach.md) **:** {`PID`&#124;`ProcName`}

     `PID` には、対象アプリケーションのプロセス ID を指定します。 Windows タスク マネージャーで、実行中のすべてのプロセスのプロセス ID を参照できます。

## <a name="control-data-collection"></a>データ収集の制御
 対象アプリケーションの実行中は、*VSPerfCmd.exe* のオプションを使用してファイルへのデータ書き込みを開始および停止することにより、データ収集を制御できます。 データ収集を制御することにより、アプリケーションの起動や終了など、プログラム実行の特定部分のデータを収集できます。

#### <a name="to-start-and-stop-data-collection"></a>データ収集を開始および停止するには

- 次の表に示すオプションの組み合わせにより、データ収集を開始および停止します。 個別のコマンド ラインで各オプションを指定します。 データ収集のオンとオフは複数回切り替えることができます。

    |オプション|説明|
    |------------|-----------------|
    |[/globalon /globaloff](../profiling/globalon-and-globaloff.md)|すべてのプロセスのデータ収集を開始 ( **/globalon**) または停止 ( **/globaloff**) します。|
    |[/processon](../profiling/processon-and-processoff.md) **:** `PID` [/processoff](../profiling/processon-and-processoff.md) **:** `PID`|プロセス ID (`PID`) で指定されたプロセスのデータ収集を開始 ( **/processon**) または停止 ( **/processoff**) します。|
    |[/attach](../profiling/attach.md) **:** {`PID`&#124;`ProcName`} [/detach](../profiling/detach.md)[ **:** {`PID`&#124;`ProcName`}]|**/attach** は、プロセス ID (`PID`) またはプロセス名 (*ProcName*) で指定したプロセスのデータ収集を開始します。 **/detach** は、指定されたプロセスのデータ コレクションを停止します。プロセスが指定されていない場合は、すべてのプロセスのデータ コレクションを停止します。|

## <a name="end-the-profiling-session"></a>プロファイル セッションの終了
 プロファイル セッションを終了するには、プロファイラーがデータ収集を停止している必要があります。 アプリケーションを終了するか **VSPerfCmd /detach** オプションを呼び出すことによって、サンプリング メソッドを使用してプロファイリングが実行されているアプリケーションからのデータ収集を停止できます。 次に、**VSPerfCmd /shutdown** オプションを呼び出して、プロファイラーをオフにし、プロファイル データ ファイルを閉じます。

#### <a name="to-end-a-profiling-session"></a>プロファイル セッションを終了するには

1. 対象のアプリケーションを終了するか次のコマンドを入力し、アプリケーションからプロファイラーをデタッチします。

     **VSPerfCmd /detach**

2. 次のコマンドを入力してプロファイラーを終了します。

     **VSPerfCmd**  [/shutdown](../profiling/shutdown.md)
