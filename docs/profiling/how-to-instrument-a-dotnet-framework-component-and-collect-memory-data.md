---
title: プロファイラーのコマンド ライン:クライアントの .NET コンポーネントのインストルメント化、メモリ データの取得
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: d09cc46a-70f5-48f9-aa24-89913e67b359
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- dotnet
ms.openlocfilehash: 76d216c4f112f88001b0314a23f22e689f729106
ms.sourcegitcommit: 00b71889bd72b6a566586885bdb982cfe807cf54
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2019
ms.locfileid: "74775902"
---
# <a name="how-to-instrument-a-stand-alone-net-framework-component-and-collect-memory-data-with-the-profiler-by-using-the-command-line"></a>方法: プロファイラーのコマンド ラインを使用してスタンドアロンの .NET Framework コンポーネントをインストルメントし、メモリ データを収集する
この記事では、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] プロファイル ツールのコマンド ライン ツールを使用して、スタンドアロン アプリケーションの .NET Framework コンポーネント (.exe ファイル、.dll ファイルなど) をインストルメント化し、プロファイラーを使用してメモリ情報を収集する方法について説明します。

> [!NOTE]
> プロファイル ツールへのパスを取得するには、[コマンド ライン ツールへのパスの指定](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md)に関する記事をご覧ください。 64 ビット コンピューター上では、64 ビット バージョンのツールと 32 ビット バージョンのツールの両方を使用できます。 プロファイラー コマンド ライン ツールを使用するには、コマンド プロンプト ウィンドウの PATH 環境変数にツールのパスを追加するか、コマンド自体にそれを追加します。

 インストルメンテーション メソッドを使用して .NET Framework コンポーネントからメモリ データを収集するには、[VSInstr.exe](../profiling/vsinstr.md) ツールを使用してそのコンポーネントのインストルメントされたバージョンを生成し、[VSPerfCLREnv.cmd](../profiling/vsperfclrenv.md) ツールを使用して、プロファイル環境変数を初期化します。 その後、*VSPerfCmd.exe* ツールを使用してプロファイラーを起動します。

 インストルメントされたコンポーネントを実行すると、メモリ データがデータ ファイルに自動的に収集されます。 プロファイル セッション中にデータ収集を一時停止および再開できます。

 プロファイル セッションを終了するには、対象のアプリケーションを終了し、プロファイラーを明示的に終了します。 ほとんどの場合、セッションの最後にプロファイル環境変数を消去することをお勧めします。

## <a name="start-the-application-with-the-profiler"></a>プロファイラーによるアプリケーションの起動

#### <a name="to-attach-the-profiler-to-a-running-net-framework-application"></a>実行中の .NET Framework アプリケーションにプロファイラーをアタッチするには

1. コマンド プロンプト ウィンドウを開きます。

2. **VSInstr** ツールを使用して、対象アプリケーションのインストルメントされたバージョンを生成します。

3. .NET Framework プロファイル環境変数を初期化します。 型:

    **VSPerfClrEnv** { **/tracegc** &#124; **/tracegclife**}

   - **/tracegc** オプションと **/tracegclife** オプションは環境変数を初期化し、メモリの割り当てデータのみを収集するか、メモリの割り当てデータとオブジェクトの有効期間データの両方を収集します。

       |オプション|説明|
       |------------|-----------------|
       |**/tracegc**|メモリの割り当てデータのみを収集できます。|
       |**/tracegclife**|メモリの割り当てデータとオブジェクトの有効期間データを収集できます。|

4. プロファイラーを起動します。 型:

    **VSPerfCmd /start:trace /output:** `OutputFile` [`Options`]

   - [/start](../profiling/start.md) **:trace** オプションによってプロファイラーが初期化されます。

   - **/start** を使用するには、[/output](../profiling/output.md) **:** `OutputFile` オプションを指定する必要があります。 `OutputFile` には、プロファイル データ (.*vsp*) ファイルの名前と場所を指定します。

     **/start:trace** オプションを使用する場合は、次のうちいずれのオプションでも指定できます。

   | オプション | 説明 |
   | - | - |
   | [/user](../profiling/user-vsperfcmd.md) **:** [`Domain` **\\** ]`UserName` | プロファイリングされたプロセスを所有するアカウントのドメインおよびユーザー名を指定します。 このオプションは、ログオンしているユーザーとは別のユーザーがプロセスを実行している場合にのみ指定する必要があります。 プロセスの所有者は、Windows タスク マネージャーの **[プロセス]** タブの [ユーザー名] 列に表示されます。 |
   | [/crosssession](../profiling/crosssession.md) | 他のセッションにおけるプロセスのプロファイリングを有効にします。 このオプションは、アプリケーションが別のセッションで実行されている場合に必要です。 セッション ID は、Windows タスク マネージャーの **[プロセス]** タブの **[セッション ID]** 列に表示されます。 **/crosssession** の省略形として、 **/CS** を指定することができます。 |
   | [/globaloff](../profiling/globalon-and-globaloff.md) | データ収集を一時停止してプロファイラーを起動するには、 **/globaloff** オプションを **/start** コマンド ラインに追加します。 プロファイリングを再開するには、 **/globalon** を使用します。 |
   | [/wincounter](../profiling/wincounter.md) **:** `WinCounterPath` | プロファイリング実行中に収集する Windows パフォーマンス カウンターを指定します。 |
   | [/automark](../profiling/automark.md) **:** `Interval` | **/wincounter** との組み合わせでのみ使用します。 Windows パフォーマンス カウンター コレクション イベントの間隔をミリ秒単位で指定します。 既定値は 500 ミリ秒です。 |
   | [/counter](../profiling/counter.md) **:** `Config` | Config で指定されたプロセッサのパフォーマンス カウンターから情報を収集します。カウンター情報は、プロファイル イベントが発生するたびに、収集されたデータに追加されます。 |
   | [events](../profiling/events-vsperfcmd.md) **:** `Config` | プロファイリング実行中に収集する ETW (Event Tracing for Windows) イベントを指定します。 ETW イベントは独立した (.*etl*) ファイルに収集されます。 |

5. コマンド プロンプト ウィンドウから対象のアプリケーションを開始します。

## <a name="control-data-collection"></a>データ収集の制御
 対象アプリケーションの実行中は、*VSPerfCmd.exe* のオプションを使用してファイルへのデータ書き込みを開始および停止することにより、データ収集を制御できます。 データ コレクションを制御することにより、アプリケーションの起動や終了など、プログラム実行の特定の部分についてのデータ コレクションを行うことができます。

#### <a name="to-start-and-stop-data-collection"></a>データ コレクションを開始および停止するには

- 次に示す **VSPerfCmd** のオプションの組み合わせにより、データ収集を開始および停止します。 個別のコマンド ラインで各オプションを指定します。 データ収集のオンとオフは複数回切り替えることができます。

    |オプション|説明|
    |------------|-----------------|
    |[/globalon](../profiling/globalon-and-globaloff.md) [/globaloff](../profiling/globalon-and-globaloff.md)|すべてのプロセスのデータ収集を開始 ( **/globalon**) または停止 ( **/globaloff**) します。|
    |[/processon](../profiling/processon-and-processoff.md) **:** `PID` [/processoff](../profiling/processon-and-processoff.md) **:** `PID`|プロセス ID (`PID`) で指定されたプロセスのデータ収集を開始 ( **/processon**) または停止 ( **/processoff**) します。|
    |[/threadon](../profiling/threadon-and-threadoff.md) **:** `TID` [/threadoff](../profiling/threadon-and-threadoff.md) **:** `TID`|スレッド ID (`TID`) で指定されたスレッドのデータ収集を開始 ( **/threadon**) または停止 ( **/threadoff**) します。|

## <a name="end-the-profiling-session"></a>プロファイル セッションの終了
 プロファイル セッションを終了するには、インストルメントされたコンポーネントを実行しているアプリケーションを終了し、**VSPerfCmd** [/shutdown](../profiling/shutdown.md) オプションを呼び出してプロファイラーをオフにした後、プロファイル データ ファイルを閉じます。 **VSPerfClrEnv /off** コマンドは、プロファイル環境変数を消去します。

#### <a name="to-end-a-profiling-session"></a>プロファイル セッションを終了するには

1. 対象アプリケーションを終了します。

2. プロファイラーをシャットダウンします。 型:

     **VSPerfCmd /shutdown**

3. (省略可能) プロファイル環境変数を削除します。 型:

     **VSPerfCmd /off**

## <a name="see-also"></a>関連項目
- [スタンドアロン アプリケーションのプロファイリング](../profiling/command-line-profiling-of-stand-alone-applications.md)
- [.NET メモリのデータ ビュー](../profiling/dotnet-memory-data-views.md)
