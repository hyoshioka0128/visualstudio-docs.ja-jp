---
title: プロファイラーを .NET サービスにアタッチし、コンカレンシー データを収集する
ms.custom: seodec18
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: ffbdfe37-8325-44be-bd36-2c8aab2dec7b
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- dotnet
ms.openlocfilehash: 24c49015915b8a1d214a833c38c5550f51c50c13
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85328694"
---
# <a name="how-to-attach-the-profiler-to-a-net-service-to-collect-concurrency-data-by-using-the-command-line"></a>方法: コマンド ラインを使用してプロファイラーを .NET サービスにアタッチし、コンカレンシー データを収集する
この記事では、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] プロファイル ツールのコマンド ライン ツールを使用して、プロファイラーを .NET Framework サービスにアタッチし、サンプリング メソッドによってプロセス データとスレッド コンカレンシー データを収集する方法について説明します。

> [!NOTE]
> Windows 8 および Windows Server 2012 の強化されたセキュリティ機能によって、Visual Studio プロファイラーがこれらのプラットフォームでデータを収集する方法に大幅な変更が必要になりました。 UWP アプリにも新しい収集手法が必要です。 「[Windows 8 および Windows Server 2012 アプリケーションのパフォーマンス ツール](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)」を参照してください。

> [!NOTE]
> プロファイル ツールへのパスを取得するには、[コマンド ライン ツールへのパスの指定](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md)に関する記事をご覧ください。 64 ビット コンピューター上では、64 ビット バージョンのツールと 32 ビット バージョンのツールの両方を使用できます。 プロファイラー コマンド ライン ツールを使用するには、コマンド プロンプト ウィンドウの PATH 環境変数にツールのパスを追加するか、コマンド自体にそれを追加します。

 コンカレンシー データを収集するには、プロファイラーをサービス プロセスにアタッチします。 プロファイラーをサービスにアタッチしている間はデータ コレクションを一時停止し、完了後に再開できます。 プロファイル セッションを終了するには、サービスへのプロファイラーのアタッチを解除し、プロファイラーを明示的に終了する必要があります。 ほとんどの場合、セッションの最後にプロファイル環境変数を消去することをお勧めします。

## <a name="attach-the-profiler"></a>プロファイラーのアタッチ

#### <a name="to-attach-the-profiler-to-a-net-framework-service"></a>プロファイラーを .NET Framework サービスにアタッチするには

1. サービスをインストールします。

2. コマンド ウィンドウを開きます。

3. プロファイル環境変数を初期化します。 型:

     [VSPerfClrEnv](../profiling/vsperfclrenv.md) **/globalsampleon** **[/samplelineoff]**

    - **/globalsampleon** はサンプリングを有効にします。

    - **/samplelineoff** は特定のソース コード行への収集データの割り当てを無効にします。 このオプションを指定すると、データは関数に対してのみ割り当てられます。

4. コンピューターを再起動します。

5. プロファイラーを起動します。 型:

     [VSPerfCmd](../profiling/vsperfcmd.md) **/start:concurrency  /output:** `OutputFile` [`Options`]

     **/start** を使用するには、[/output](../profiling/output.md) **:** `OutputFile` オプションを指定する必要があります。 `OutputFile` には、プロファイル データ (.vsp) ファイルの名前と場所を指定します。

     **/start**では、次のうちいずれかのオプションを指定できます。

    > [!NOTE]
    > **/user** オプションと **/crosssession** オプションは、通常、サービスで必要です。

    |オプション|説明|
    |------------|-----------------|
    |[/user](../profiling/user-vsperfcmd.md) **:** [`Domain` **\\** ]`UserName`|プロファイリングされたプロセスを所有するアカウントのドメインおよびユーザー名を指定します。 このオプションは、ログオンしているユーザーとは別のユーザーがプロセスを実行している場合にのみ指定する必要があります。 プロセスの所有者は、Windows タスク マネージャーの **[プロセス]** タブの **[ユーザー名]** 列に表示されます。|
    |[/crosssession](../profiling/crosssession.md)|他のセッションにおけるプロセスのプロファイリングを有効にします。 このオプションは、サービスが別のセッションで実行されている場合に必要です。 セッション ID は、Windows タスク マネージャーの **[プロセス]** タブの **[セッション ID]** 列に表示されます。 **/crosssession** の省略形として、 **/CS** を指定することができます。|
    |[/wincounter](../profiling/wincounter.md) **:** `WinCounterPath`|プロファイリング実行中に収集する Windows パフォーマンス カウンターを指定します。|
    |[/automark](../profiling/automark.md) **:** `Interval`|**/wincounter** との組み合わせでのみ使用します。 Windows パフォーマンス カウンター コレクション イベントの間隔をミリ秒単位で指定します。 既定値は 500 ミリ秒です。|
    |[/events](../profiling/events-vsperfcmd.md) **:** `Config`|プロファイリング実行中に収集する ETW (Event Tracing for Windows) イベントを指定します。 ETW イベントは独立した (.*etl*) ファイルに収集されます。|

6. 起動の必要なサービスがあれば起動します。

7. プロファイラーをサービスにアタッチします。 型:

     **VSPerfCmd /attach:** `PID` [[/targetclr](../profiling/targetclr.md) **:** `Version`]

    - `PID` には、サービスのプロセス ID またはプロセス名を指定します。 Windows タスク マネージャーで、実行中のすべてのプロセスのプロセス ID を参照できます。

    - **targetclr:** `Version` には、アプリケーションに複数のバージョンのランタイムが読み込まれている場合に、プロファイリングを行う共通言語ランタイム (CLR) のバージョンを指定します。 任意。

## <a name="control-data-collection"></a>データ収集の制御
 サービスの実行中は、*VSPerfCmd.exe* のオプションを使用してファイルへのデータ書き込みを開始または停止することにより、データ収集を制御できます。 データ収集を制御することにより、アプリケーションの起動やシャットダウンなど、プログラム実行の特定の部分についてのデータ収集を行うことができます。

#### <a name="to-start-and-stop-data-collection"></a>データ収集を開始および停止するには

- 次に示す **VSPerfCmd** のオプションの組み合わせにより、データ収集を開始および停止します。 個別のコマンド ラインで各オプションを指定します。 データ収集のオンとオフは複数回切り替えることができます。

    |オプション|説明|
    |------------|-----------------|
    |[/globalon /globaloff](../profiling/globalon-and-globaloff.md)|すべてのプロセスのデータ収集を開始 ( **/globalon**) または停止 ( **/globaloff**) します。|
    |[/processon](../profiling/processon-and-processoff.md) **:** `PID` [/processoff](../profiling/processon-and-processoff.md) **:** `PID`|プロセス ID (`PID`) で指定されたプロセスのデータ コレクションを開始 ( **/processon**) または停止 ( **/processoff**) します。|
    |**/attach:** {`PID`&#124;`ProcName`} [/detach](../profiling/detach.md)[:{`PID`&#124;`ProcName`}]|**/attach** は、プロセス ID またはプロセス名で指定したプロセスのデータ収集を開始します。 **/detach** は、指定されたプロセスのデータ コレクションを停止します。特定のプロセスが指定されていない場合は、すべてのプロセスのデータ コレクションを停止します。|

- **VSPerfCmd.exe**[/mark](../profiling/mark.md) オプションを使用して、データ ファイルにプロファイル マークを挿入することもできます。 **/mark** コマンドは、識別子、タイム スタンプ、およびオプションのユーザー定義文字列を追加します。 マークは、プロファイラー レポートおよびデータ ビューでデータをフィルター処理するために使用できます。 次に示す VSPerfCmd のオプションの組み合わせにより、データ収集を開始および停止します。 個別のコマンド ラインで各オプションを指定します。 データ収集のオンとオフは複数回切り替えることができます。

## <a name="end-the-profiling-session"></a>プロファイル セッションの終了
 プロファイル セッションを終了するには、プロファイラーがデータ収集を停止している必要があります。 サービスを停止するか **VSPerfCmd /detach** オプションを呼び出すことによって、コンカレンシー メソッドを使用してプロファイリングが実行されているアプリケーションからのデータ収集を停止できます。 次に、**VSPerfCmd /shutdown** オプションを呼び出して、プロファイラーをオフにし、プロファイル データ ファイルを閉じます。 **VSPerfClrEnv /globaloff** コマンドによってプロファイル環境変数は消去されますが、コンピューターを再起動するまでシステム構成はリセットされません。

#### <a name="to-end-a-profiling-session"></a>プロファイル セッションを終了するには

1. 対象アプリケーションからプロファイラーをデタッチするには、次のいずれかの操作を行います。

    - サービスを停止します。

         \- または -

    - **VSPerfCmd /detach** と入力します

2. プロファイラーをシャットダウンします。 型:

     **VSPerfCmd**  [Shutdown](../profiling/shutdown.md)
