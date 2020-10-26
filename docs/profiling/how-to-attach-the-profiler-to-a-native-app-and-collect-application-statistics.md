---
title: ネイティブ アプリにプロファイラーをアタッチし、アプリの統計情報を収集する
ms.custom: seodec18
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: df44fe42-281b-4398-b3fc-277b62ae41f1
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- cplusplus
ms.openlocfilehash: 9d463413833ad476b8d6ad90369f53267e3f7cff
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85328673"
---
# <a name="how-to-attach-the-profiler-to-a-native-stand-alone-application-and-collect-application-statistics-by-using-the-command-line"></a>方法: コマンド ラインを使用してスタンドアロンのネイティブ アプリケーションにプロファイラーをアタッチし、アプリケーション統計情報を収集する
この記事では、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] プロファイル ツールのコマンド ライン ツールを使用して、実行中のスタンドアロンのネイティブ (クライアント) アプリケーションにプロファイラーをアタッチし、サンプリング メソッドを使用してパフォーマンスに関する統計情報を収集する方法について説明します。

> [!NOTE]
> Windows 8 および Windows Server 2012 の強化されたセキュリティ機能によって、Visual Studio プロファイラーがこれらのプラットフォームでデータを収集する方法に大幅な変更が必要になりました。 UWP アプリにも新しい収集手法が必要です。 「[Windows 8 および Windows Server 2012 アプリケーションのパフォーマンス ツール](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)」を参照してください。
>
> プロファイル ツールへのパスを取得するには、[コマンド ライン ツールへのパスの指定](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md)に関する記事をご覧ください。 64 ビット コンピューター上では、64 ビット バージョンのツールと 32 ビット バージョンのツールの両方を使用できます。 プロファイラー コマンド ライン ツールを使用するには、コマンド プロンプト ウィンドウの PATH 環境変数にツールのパスを追加するか、コマンド自体にそれを追加します。

 プロファイラーをアプリケーションにアタッチしているときにデータ コレクションを一時停止し、完了後に再開できます。 プロファイル セッションを終了するには、アプリケーションへのプロファイラーのアタッチを解除し、プロファイラーを明示的に終了する必要があります。

## <a name="attach-the-profiler"></a>プロファイラーのアタッチ
 プロファイラーを対象のアプリケーションにアタッチするには、**VSPerfCmd/start** オプションと **/attach** オプションを使用してプロファイラーを初期化し、対象のアプリケーションにアタッチします。 **/start** と **/attach**、およびそれぞれのオプションは、1 つのコマンド ラインで指定できます。 **/globaloff** オプションを追加して、対象アプリケーションの起動時にデータ収集を一時停止することもできます。 次に、 **/globalon** を使用してデータの収集を開始します。

#### <a name="to-attach-the-profiler-to-a-running-net-framework-application"></a>実行中の .NET Framework アプリケーションにプロファイラーをアタッチするには

1. コマンド プロンプト ウィンドウを開きます。

2. プロファイラーを起動します。 型:

    **VSPerfCmd /start:sample /output:** `OutputFile` [`Options`]

   - [/start](../profiling/start.md) **:sample** オプションによってプロファイラーが初期化されます。

   - **/start** を使用するには、[/output](../profiling/output.md) **:** `OutputFile` オプションを指定する必要があります。 `OutputFile` には、プロファイル データ (.vsp) ファイルの名前と場所を指定します。

     **/start:sample** オプションを使用する場合は、次のうちいずれかのオプションを指定できます。

   | オプション | 説明 |
   | - | - |
   | [/user](../profiling/user-vsperfcmd.md) **:** [`Domain` **\\** ]`UserName` | プロファイリングされたプロセスを所有するアカウントのドメインおよびユーザー名を指定します。 このオプションは、ログオンしているユーザーとは別のユーザーがプロセスを実行している場合にのみ指定する必要があります。 プロセスの所有者は、Windows タスク マネージャーの [プロセス] タブの [ユーザー名] 列に表示されます。 |
   | [/crosssession](../profiling/crosssession.md) | 他のセッションにおけるプロセスのプロファイリングを有効にします。 このオプションは、ASP.NET アプリケーションが別のセッションで実行されている場合に必要です。 セッション ID は、Windows タスク マネージャーの [プロセス] タブの [セッション ID] 列に表示されます。 **/crosssession** の省略形として、 **/CS** を指定することができます。 |
   | [/wincounter](../profiling/wincounter.md) **:** `WinCounterPath` | プロファイリング実行中に収集する Windows パフォーマンス カウンターを指定します。 |
   | [/automark](../profiling/automark.md) **:** `Interval` | **/wincounter** との組み合わせでのみ使用します。 Windows パフォーマンス カウンター コレクション イベントの間隔をミリ秒単位で指定します。 既定値は 500 ミリ秒です。 |
   | [/events](../profiling/events-vsperfcmd.md) **:** `Config` | プロファイリング実行中に収集する ETW (Event Tracing for Windows) イベントを指定します。 ETW イベントは独立した (.*etl*) ファイルに収集されます。 |

3. プロファイラーを対象のアプリケーションにアタッチします。 型:

    **VSPerfCmd**  [/attach](../profiling/attach.md) **:** {`PID`&#124;`ProcName`} [`Sample Event`]

    `PID` には、対象アプリケーションのプロセス ID を指定します。 `ProcessName` には、プロセスの名前を指定します。 `ProcessName` を指定して、同じ名前の複数のプロセスが実行中である場合、結果は予測できません。 Windows タスク マネージャーで、実行中のすべてのプロセスのプロセス ID を参照できます。

    既定では、パフォーマンス データはプロセッサのクロック サイクル数 10,000,000 (停止なし) ごとにサンプリングされます。 このため、1 GHz のプロセッサにおける 1 秒あたりのサンプリング回数は約 100 回です。 次のオプションのいずれかを指定して、クロック サイクルの間隔の変更、または別のサンプリング イベントの指定ができます。

   |サンプリング イベント|説明|
   |------------------|-----------------|
   |[/timer](../profiling/timer.md) **:** `Interval`|サンプリングの間隔を、`Interval` で指定された停止なしのクロック サイクル数に変更します。|
   |[/pf](../profiling/pf.md)[ **:** `Interval`]|サンプリング イベントをページ フォールトに変更します。 `Interval` を指定した場合は、サンプル間のページ フォールト数が設定されます。 既定値は 10 です。|
   |[/sys](../profiling/sys-vsperfcmd.md) [ **:** `Interval`]|サンプリング イベントを、プロセスからオペレーティング システムのカーネルへのシステム コール (syscall) に変更します。 `Interval` を指定した場合は、サンプル間の呼び出し回数が設定されます。 既定値は 10 です。|
   |[/counter](../profiling/counter.md) **:** `Config`|サンプリング イベントと間隔を、プロセッサのパフォーマンス カウンターと、`Config` で指定した間隔に、それぞれ変更します。|

## <a name="control-data-collection"></a>データ収集の制御
 対象アプリケーションの実行中に、*VSPerfCmd.exe* のオプションを使用してプロファイラー データ ファイルへのデータの書き込みを開始したり、停止したりできます。 データ収集を制御することにより、アプリケーションの起動やシャットダウンなど、プログラム実行の特定の部分についてのデータ収集を行うことができます。

#### <a name="to-start-and-stop-data-collection"></a>データ収集を開始および停止するには

- 次に示す **VSPerfCmd** のオプションの組み合わせにより、データ収集を開始および停止します。 個別のコマンド ラインで各オプションを指定します。 データ収集のオンとオフは複数回切り替えることができます。

    |オプション|説明|
    |------------|-----------------|
    |[/globalon /globaloff](../profiling/globalon-and-globaloff.md)|すべてのプロセスのデータ収集を開始 ( **/globalon**) または停止 ( **/globaloff**) します。|
    |[/processon](../profiling/processon-and-processoff.md) **:** `PID` [/processoff](../profiling/processon-and-processoff.md) **:** `PID`|`PID` で指定されたプロセスのデータ収集を開始 ( **/processon**) または停止 ( **/processoff**) します。|
    |[/attach](../profiling/attach.md) **:** `PID` [/detach](../profiling/detach.md)|**/attach** は、`PID` で指定されたプロセスのデータ収集を開始します。 **/detach** は、すべてのプロセスのデータ収集を停止します。|

## <a name="end-the-profiling-session"></a>プロファイル セッションの終了
 プロファイル セッションを終了するには、プロファイラーをプロファイリング対象のすべてのプロセスからデタッチし、プロファイラーを明示的に終了する必要があります。 サンプリング メソッドを使用してプロファイリングを実行したアプリケーションからプロファイラーをデタッチするには、アプリケーションを終了するか、**VSPerfCmd /detach** オプションを呼び出します。 次に、**VSPerfCmd /shutdown** オプションを呼び出して、プロファイラーをオフにし、プロファイル データ ファイルを閉じます。 **VSPerfClrEnv /off** コマンドは、プロファイル環境変数を消去します。

#### <a name="to-end-a-profiling-session"></a>プロファイル セッションを終了するには

1. 対象アプリケーションからプロファイラーをデタッチするには、次のいずれかの手順を実行します。

    - **VSPerfCmd /detach** と入力します

         \- または -

    - 対象アプリケーションを終了します。

2. プロファイラーをシャットダウンします。 型:

     **VSPerfCmd**  [/shutdown](../profiling/shutdown.md)

3. (省略可能) プロファイル環境変数を削除します。 型:

     **VSPerfClrEnv /off**

## <a name="see-also"></a>関連項目
- [スタンドアロン アプリケーションのプロファイリング](../profiling/command-line-profiling-of-stand-alone-applications.md)
- [サンプリング メソッドのデータ ビュー](../profiling/profiler-sampling-method-data-views.md)
