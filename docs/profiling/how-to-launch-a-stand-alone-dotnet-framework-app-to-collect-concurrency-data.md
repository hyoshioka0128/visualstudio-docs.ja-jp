---
title: プロファイラーのコマンド ライン - クライアントの .NET アプリを開き、コンカレンシー データを取得する
description: Visual Studio プロファイル ツールのコマンドライン ツールを使用して、.NET のスタンドアロン アプリを起動し、プロセスおよびスレッドのコンカレンシー データを収集する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 17a48848-bd3e-44ef-9971-e39836ff1df2
author: mikejo5000
ms.author: mikejo
manager: jmartens
monikerRange: vs-2017
ms.workload:
- dotnet
ms.openlocfilehash: 81311e9dea2c5367b44cdf2cc8e2327a8aff5617
ms.sourcegitcommit: 20f546a0b13b56e7b0da21abab291d42a5ba5928
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/23/2021
ms.locfileid: "104884110"
---
# <a name="how-to-launch-a-stand-alone-net-framework-application-with-the-profiler-to-collect-concurrency-data-by-using-the-command-line"></a>方法: コマンド ラインを使用してプロファイラーによってスタンドアロンの .NET Framework アプリケーションを起動し、コンカレンシー データを収集する
ここでは、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] プロファイリング ツールのコマンド ライン ツールを使用して、.NET Framework のスタンドアロン (クライアント) アプリケーションを起動し、プロセスおよびスレッドのコンカレンシー データを収集する方法について説明します

> [!NOTE]
> プロファイル ツールへのパスを取得するには、[コマンド ライン ツールへのパスの指定](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md)に関する記事をご覧ください。 64 ビット コンピューター上では、64 ビット バージョンのツールと 32 ビット バージョンのツールの両方を使用できます。 プロファイラー コマンド ライン ツールを使用するには、コマンド プロンプト ウィンドウの PATH 環境変数にツールのパスを追加するか、コマンド自体にそれを追加します。

 プロファイラーをアプリケーションにアタッチしている間はデータ収集を一時停止し、完了後に再開できます。 プロファイル セッションを終了するには、アプリケーションへのプロファイラーのアタッチを解除し、プロファイラーを明示的に終了する必要があります。

## <a name="start-the-application-with-the-profiler"></a>プロファイラーによるアプリケーションの起動
 プロファイラーを使用して対象の .NET Framework アプリケーションを起動するには、*VSPerfClrEnv.exe* を使用して、.NET Framework プロファイル変数を設定します。 次に、VSPerfCmd の **/start** オプションおよび **/launch** オプションを使用して、プロファイラーを初期化し、アプリケーションを起動します。 **/start** と **/launch**、およびそれぞれのオプションは、1 つのコマンド ラインで指定できます。 また、 **/globaloff** オプションをコマンド ラインに追加すると、対象アプリケーションの起動時にデータ コレクションを一時停止できます。 次に、別のコマンド ラインで **/globalon** を使用して、データ収集を開始できます。

#### <a name="to-start-an-application-with-the-profiler"></a>プロファイラーを使用してアプリケーションを起動するには

1. コマンド プロンプト ウィンドウを開きます。

2. プロファイラーを起動します。 型:

    [VSPerfCmd](../profiling/vsperfcmd.md) **/start:concurrency**[ **,** {**ResourceOnly**&#124;**ThreadOnly**}] **/output:** `OutputFile` [`Options`]

   - [/start](../profiling/start.md) オプションによってプロファイラーが初期化されます。

     | コマンド | 説明 |
     |-------------------------------------| - |
     | **/start:concurrency** | リソース競合データとスレッド実行データの両方の収集を有効にします。 |
     | **/start:concurrency,resourceonly** | リソース競合データの収集のみを有効にします。 |
     | **/start:concurrency,threadonly** | スレッド実行データの収集のみを有効にします。 |

   - **/start** を使用するには、[/output](../profiling/output.md) **:** `OutputFile` オプションを指定する必要があります。 `OutputFile` には、プロファイル データ (.vsp) ファイルの名前と場所を指定します。

     **/start:concurrency** オプションを使用する場合は、次のうちいずれかのオプションを指定できます。

   | オプション | 説明 |
   | - | - |
   | [/user](../profiling/user-vsperfcmd.md) **:** [`domain\`]`username` | プロファイラーへのアクセスを許可するアカウントのオプションのドメインとユーザー名を指定します。 |
   | [/crosssession](../profiling/crosssession.md) | 他のログオン セッションにおけるプロセスのプロファイリングを有効にします。 |
   | [/wincounter](../profiling/wincounter.md) **:** `WinCounterPath` | プロファイリング実行中に収集する Windows パフォーマンス カウンターを指定します。 |
   | [/automark](../profiling/automark.md) **:** `Interval` | **/wincounter** との組み合わせでのみ使用します。 Windows パフォーマンス カウンター コレクション イベントの間隔をミリ秒単位で指定します。 既定値は 500 ミリ秒です。 |
   | [/events](../profiling/events-vsperfcmd.md) **:** `Config` | プロファイリング実行中に収集する ETW (Event Tracing for Windows) イベントを指定します。 ETW イベントは独立した (.*etl*) ファイルに収集されます。 |

3. 対象アプリケーションを起動します。 型:

    **VSPerfCmd**  [/launch](../profiling/launch.md) **:** `AppName` [`Options`] [`Sample Event`]

    **/launch** オプションを使用する場合は、次のうちどのオプションでも指定できます。

   |オプション|説明|
   |------------|-----------------|
   |[/args](../profiling/args.md) **:** `Arguments`|対象アプリケーションへ渡されるコマンド ライン引数を格納する文字列を指定します。|
   |[/console](../profiling/console.md)|対象のコマンド ライン アプリケーションを別のウィンドウで起動でします。|
   |[/targetclr](../profiling/targetclr.md) **:** `Version`|アプリケーションに複数バージョンのランタイムが読み込まれている場合に、プロファイリングを行う共通言語ランタイム (CLR: Common Language Runtime) のバージョンを指定します。|

## <a name="control-data-collection"></a>データ収集の制御
 対象アプリケーションの実行中は、*VSPerfCmd.exe* のオプションを使用してファイルへのデータ書き込みを開始および停止することにより、データ収集を制御できます。 データ収集を制御することにより、アプリケーションの起動やシャットダウンなど、プログラム実行の特定の部分についてのデータ収集を行うことができます。

#### <a name="to-start-and-stop-data-collection"></a>データ収集を開始および停止するには

1. 次の *VSPerfCmd.exe* オプションの組み合わせにより、データ収集を開始し、停止します。 個別のコマンド ラインで各オプションを指定します。 データ収集のオンとオフは複数回切り替えることができます。

    |オプション|説明|
    |------------|-----------------|
    |[/globalon /globaloff](../profiling/globalon-and-globaloff.md)|すべてのプロセスのデータ収集を開始 ( **/globalon**) または停止 ( **/globaloff**) します。|
    |[/processon](../profiling/processon-and-processoff.md) **:** `PID` [/processoff](../profiling/processon-and-processoff.md) **:** `PID`|プロセス ID (`PID`) で指定されたプロセスのデータ収集を開始 ( **/processon**) または停止 ( **/processoff**) します。|
    |[/attach](../profiling/attach.md) **:** {`PID`&#124;`ProcName`} [/detach](../profiling/detach.md)[ **:** {`PID`&#124;`ProcName`}]|**/attach** は、プロセス ID (`PID`) またはプロセス名 (ProcName) で指定したプロセスのデータ収集を開始します。 **/detach** は、指定されたプロセスのデータ収集を停止します。特定のプロセスが指定されていない場合は、すべてのプロセスのデータ収集を停止します。|

## <a name="end-the-profiling-session"></a>プロファイル セッションの終了
 プロファイル セッションを終了するには、プロファイラーがデータ収集を停止している必要があります。 コンカレンシー データの収集を停止するには **VSPerfCmd /detach** オプションを呼び出して、プロファイリング対象のアプリケーションを終了する必要があります。 次に、**VSPerfCmd /shutdown** オプションを呼び出して、プロファイラーをオフにし、プロファイル データ ファイルを閉じます。 **VSPerfClrEnv /off** コマンドは、プロファイル環境変数を消去します。

#### <a name="to-end-a-profiling-session"></a>プロファイル セッションを終了するには

1. 対象アプリケーションからプロファイラーをデタッチするには、次のいずれかの操作を行います。

    - 対象アプリケーションを終了します。

         \- または -

    - **VSPerfCmd /detach** と入力します

2. プロファイラーをシャットダウンします。

     **VSPerfCmd**  [/shutdown](../profiling/shutdown.md)

## <a name="see-also"></a>関連項目
- [コンカレンシー データの収集](../profiling/collecting-concurrency-data-for-stand-alone-applications.md)
