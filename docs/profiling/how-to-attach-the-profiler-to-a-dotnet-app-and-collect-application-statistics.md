---
title: プロファイラーを NET Framework のスタンドアロン アプリにアタッチし、アプリの統計を取得する
ms.custom: seodec18
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: b62fcbc1-791f-474e-890a-a6c332e0c9ea
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- dotnet
ms.openlocfilehash: 9084f2d1dd784172735c66d38da785dffb74d82c
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "74779182"
---
# <a name="how-to-attach-the-profiler-to-a-net-framework-stand-alone-application-and-collect-application-statistics-by-using-the-command-line"></a>方法: コマンド ラインを使用して .NET Framework のスタンドアロン アプリケーションにプロファイラーをアタッチし、アプリケーションの統計情報を収集する
この記事では、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] プロファイル ツールのコマンド ライン ツールを使用して、実行中の .NET Framework スタンドアロン (クライアント) アプリケーションにプロファイラーをアタッチし、サンプリング メソッドを使用してパフォーマンスに関する統計情報を収集する方法について説明します。

> [!NOTE]
> Windows 8 および Windows Server 2012 の強化されたセキュリティ機能によって、Visual Studio プロファイラーがこれらのプラットフォームでデータを収集する方法に大幅な変更が必要になりました。 UWP アプリにも新しい収集手法が必要です。 「[Windows 8 および Windows Server 2012 アプリケーションのパフォーマンス ツール](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)」を参照してください。
>
> プロファイル ツールへのパスを取得するには、[コマンド ライン ツールへのパスの指定](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md)に関する記事をご覧ください。 64 ビット コンピューター上では、64 ビット バージョンのツールと 32 ビット バージョンのツールの両方を使用できます。 プロファイラー コマンド ライン ツールを使用するには、コマンド プロンプト ウィンドウの PATH 環境変数にツールのパスを追加するか、コマンド自体にそれを追加します。
>
> プロファイリングの実行に階層の相互作用データを追加するには、コマンド ライン プロファイリング ツールによる特定の手順が必要です。 [階層相互作用データを収集する](../profiling/adding-tier-interaction-data-from-the-command-line.md)方法に関するページを参照してください。

 .NET Framework アプリケーションからパフォーマンス データを収集するには、該当する環境変数を初期化してから対象アプリケーションを起動する必要があります。 プロファイラーをアプリケーションにアタッチしているときにデータ コレクションを一時停止し、完了後に再開できます。

 プロファイル セッションを終了するには、アプリケーションへのプロファイラーのアタッチを解除し、プロファイラーを明示的に終了する必要があります。 ほとんどの場合、プロファイル セッションの最後にプロファイル環境変数を消去することをお勧めします。

## <a name="attach-the-profiler"></a>プロファイラーのアタッチ

#### <a name="to-attach-the-profiler-to-a-running-net-framework-application"></a>実行中の .NET Framework アプリケーションにプロファイラーをアタッチするには

1. コマンド プロンプト ウィンドウを開きます。

2. プロファイル環境変数を初期化します。 型:

    **VSPerfClrEnv /sampleon** **[/samplelineoff]**

   - **/samplelineoff** オプションを指定すると、ソース コードの行番号データの収集が無効になります。

3. プロファイラーを起動します。 型:

    **VSPerfCmd /start:sample /output:** `OutputFile` [`Options`]

   - [/start](../profiling/start.md) **:sample** オプションによってプロファイラーが初期化されます。

   - **/start** を使用するには、[/output](../profiling/output.md) **:** `OutputFile` オプションを指定する必要があります。 `OutputFile` には、プロファイル データ (.vsp) ファイルの名前と場所を指定します。

     **/start:sample** オプションを使用する場合は、次のうちいずれかのオプションを指定できます。

   | オプション | 説明 |
   | - | - |
   | [/user](../profiling/user-vsperfcmd.md) **:** [`Domain` **\\** ]`UserName` | プロファイリングされるプロセスを所有するアカウントのドメインおよびユーザー名を指定します (省略可能)。 このオプションは、ログオンしているユーザーとは別のユーザーとしてアプリケーションが開始された場合にのみ指定する必要があります。 |
   | [/crosssession](../profiling/crosssession.md) | 他のログオン セッションにおけるプロセスのプロファイリングを有効にします。 **/crosssession** の省略形として、 **/CS** を指定することができます。 このオプションは、アプリケーションが別のセッションで実行されている場合に必要です。 |
   | [/wincounter](../profiling/wincounter.md) **:** `WinCounterPath` | プロファイリング実行中に収集する Windows パフォーマンス カウンターを指定します。 |
   | [/automark](../profiling/automark.md) **:** `Interval` | **/wincounter** との組み合わせでのみ使用します。 Windows パフォーマンス カウンター コレクション イベントの間隔をミリ秒単位で指定します。 既定値は 500 ミリ秒です。 |
   | [/events](../profiling/events-vsperfcmd.md) **:** `Config` | プロファイリング実行中に収集する ETW (Event Tracing for Windows) イベントを指定します。 ETW イベントは独立した (.*etl*) ファイルに収集されます。 |

4. 必要な場合、通常の方法で対象のアプリケーションを起動します。

5. プロファイラーを対象のアプリケーションにアタッチします。 型:

    **VSPerfCmd /attach:** {`PID`&#124;`ProcessName`} [`Sample Event`] [ **/targetclr:** `Version`]

   - `PID` には、対象アプリケーションのプロセス ID を指定します。 `ProcessName` には、プロセスの名前を指定します。 `ProcessName` を指定して、同じ名前の複数のプロセスが実行中である場合、結果は予測できません。 Windows タスク マネージャーで、実行中のすべてのプロセスのプロセス ID を参照できます。

   - [/targetclr](../profiling/targetclr.md) **:** `Version` には、アプリケーションに複数のバージョンのランタイムが読み込まれている場合に、プロファイリングを行う共通言語ランタイム (CLR) のバージョンを指定します。 任意。

   - 既定では、パフォーマンス データはプロセッサのクロック サイクル数 10,000,000 (停止なし) ごとにサンプリングされます。 このため、1 GHz のプロセッサでは 10 ミリ秒ごとに約 1 回です。 次のオプションのいずれかを指定すると、クロック サイクルの間隔の変更や、別のサンプリング イベントの指定ができます。[/targetclr](../profiling/targetclr.md) **:** `Version` には、アプリケーションに複数バージョンのランタイムが読み込まれている場合に、プロファイリングを行う CLR のバージョンを指定します。 任意。

   |||
   |-|-|
   |サンプリング イベント|説明|
   |[/timer](../profiling/timer.md) **:** `Interval`|サンプリングの間隔を、`Interval` で指定された停止なしのクロック サイクル数に変更します。|
   |[/pf](../profiling/pf.md) [ **:** `Interval`]|サンプリング イベントをページ フォールトに変更します。 `Interval` を指定した場合は、サンプル間のページ フォールト数が設定されます。 既定値は 10 です。|
   |[/sys](../profiling/sys-vsperfcmd.md) [ **:** `Interval`]|サンプリング イベントを、プロセスからオペレーティング システムのカーネルへのシステム コール (syscall) に変更します。 `Interval` を指定した場合は、サンプル間の呼び出し回数が設定されます。 既定値は 10 です。|
   |[/counter](../profiling/counter.md) **:** `Config`|サンプリング イベントと間隔を、プロセッサのパフォーマンス カウンターと、`Config` で指定した間隔に、それぞれ変更します。|

## <a name="control-data-collection"></a>データ収集の制御
 対象アプリケーションの実行中に、*VSPerfCmd.exe* のオプションを使用して、プロファイラーのデータ ファイルへのデータ書き込みを開始および停止することにより、データ収集を制御できます。 データ コレクションを制御することにより、アプリケーションの起動や終了など、プログラム実行の特定の部分についてのデータ コレクションを行うことができます。

#### <a name="to-start-and-stop-data-collection"></a>データ収集を開始および停止するには

- 次に示すオプションの組み合わせにより、データ収集を開始および停止します。 個別のコマンド ラインで各オプションを指定します。 データ収集のオンとオフは複数回切り替えることができます。

    |オプション|説明|
    |------------|-----------------|
    |[/globalon /globaloff](../profiling/globalon-and-globaloff.md)|すべてのプロセスのデータ収集を開始 ( **/globalon**) または停止 ( **/globaloff**) します。|
    |[/processon](../profiling/processon-and-processoff.md) **:** `PID` [/processoff](../profiling/processon-and-processoff.md) **:** `PID`|`PID` で指定されたプロセスのデータ収集を開始 ( **/processon**) または停止 ( **/processoff**) します。|
    |[/attach](../profiling/attach.md) **:** {`PID`&#124;`ProcName`} [/detach](../profiling/detach.md)[ **:** {`PID`&#124;`ProcName`}]|**/attach** は、`PID` またはプロセス名 (ProcName) で指定したプロセスのデータ収集を開始します。 **/detach** は、指定されたプロセスのデータ収集を停止します。特定のプロセスが指定されていない場合は、すべてのプロセスのデータ収集を停止します。|

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
