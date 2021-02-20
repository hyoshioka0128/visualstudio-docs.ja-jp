---
title: プロファイラーのコマンド ライン - クライアントの .NET コンポーネントのインストルメント化、時間データの取得
description: Visual Studio プロファイル ツールのコマンドライン ツールを使用して、スタンドアロン アプリケーションの .NET Framework コンポーネントのタイミング データを収集する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: b7dcc27b-45c6-4302-9552-6fa5b1e94b56
author: mikejo5000
ms.author: mikejo
manager: jmartens
monikerRange: vs-2017
ms.workload:
- dotnet
ms.openlocfilehash: bcc35a0c83a69a64e4dce3500015024335102b8d
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99942712"
---
# <a name="how-to-instrument-a-stand-alone-net-framework-component-and-collect-timing-data-with-the-profiler-from-the-command-line"></a>方法: コマンド ラインからプロファイラーを使用してスタンドアロンの .NET Framework コンポーネントをインストルメントし、タイミング データを収集する
ここでは、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] プロファイル ツールのコマンド ライン ツールを使用して、.*exe* や .*dll* ファイルなどの .NET Framework コンポーネントをインストルメント化し、詳細なタイミング データを収集する方法について説明します。

> [!NOTE]
> Windows 8 および Windows Server 2012 の強化されたセキュリティ機能によって、Visual Studio プロファイラーがこれらのプラットフォームでデータを収集する方法に大幅な変更が必要になりました。 UWP アプリにも新しい収集手法が必要です。 「[Windows 8 および Windows Server 2012 アプリケーションのパフォーマンス ツール](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)」を参照してください。
>
> プロファイル ツールへのパスを取得するには、[コマンド ライン ツールへのパスの指定](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md)に関する記事をご覧ください。 64 ビット コンピューター上では、64 ビット バージョンのツールと 32 ビット バージョンのツールの両方を使用できます。 プロファイラー コマンド ライン ツールを使用するには、コマンド プロンプト ウィンドウの PATH 環境変数にツールのパスを追加するか、コマンド自体にそれを追加します。
>
> プロファイリングの実行に階層の相互作用データを追加するには、コマンド ライン プロファイリング ツールによる特定の手順が必要です。 [階層相互作用データを収集する](../profiling/adding-tier-interaction-data-from-the-command-line.md)方法に関するページを参照してください。

 インストルメンテーション メソッドを使用して .NET Framework コンポーネントから詳細なタイミング データを収集するには、[VSInstr.exe](../profiling/vsinstr.md) ツールを使用してそのコンポーネントのインストルメント化されたバージョンを生成し、[VSPerfCLREnv.cmd](../profiling/vsperfclrenv.md) ツールを使用して、プロファイル環境変数を初期化します。 次に、プロファイラーを起動します。

 インストルメントされたコンポーネントを実行すると、タイミング データがデータ ファイルに自動的に収集されます。 プロファイル セッション中にデータ収集を一時停止および再開できます。

 プロファイル セッションを終了するには、対象のアプリケーションを終了し、プロファイラーを明示的に終了します。 ほとんどの場合、セッションの最後にプロファイル環境変数を消去することをお勧めします。

## <a name="start-the-profiling-session"></a>プロファイル セッションの開始

#### <a name="to-start-profiling-by-using-the-instrumentation-method"></a>インストルメンテーション メソッドを使用してプロファイルを開始するには

1. コマンド プロンプト ウィンドウを開きます。 必要に応じて、プロファイラー ツール ディレクトリを PATH 環境変数に追加します。 インストール時にはパスは追加されません。

2. **VSInstr** ツールを使用して、対象アプリケーションのインストルメントされたバージョンを生成します。

3. .NET Framework プロファイル環境変数を初期化します。 型:

    **VSPerfClrEnv /traceon**

4. プロファイラーを起動します。 型:

    **VSPerfCmd /start:trace /output:** `OutputFile` [`Options`]

   - [/start](../profiling/start.md) **:trace** オプションによってプロファイラーが初期化されます。

   - **/start** を使用するには、[/output](../profiling/output.md) **:** `OutputFile` オプションを指定する必要があります。 `OutputFile` には、プロファイル データ (.vsp) ファイルの名前と場所を指定します。

     **/start:trace** オプションでは、次のオプションのいずれかを使用できます。

   | オプション | 説明 |
   | - | - |
   | [/user](../profiling/user-vsperfcmd.md) **:** [`Domain` **\\** ]`UserName` | プロファイリングされたプロセスを所有するアカウントのドメインおよびユーザー名を指定します。 このオプションは、ログオンしているユーザーとは別のユーザーがプロセスを実行している場合にのみ指定する必要があります。 プロセスの所有者は、Windows タスク マネージャーの **[プロセス]** タブの **[ユーザー名]** 列に表示されます。 |
   | [/crosssession](../profiling/crosssession.md) | 他のセッションにおけるプロセスのプロファイリングを有効にします。 このオプションは、ASP.NET アプリケーションが別のセッションで実行されている場合に必要です。 セッション ID は、Windows タスク マネージャーの **[プロセス]** タブの **[セッション ID]** 列に表示されます。 **/crosssession** の省略形として、 **/CS** を指定することができます。 |
   | [/globaloff](../profiling/globalon-and-globaloff.md) | データ コレクションを一時停止した状態でプロファイラーを起動します。 プロファイリングを再開するには、[/globalon](../profiling/globalon-and-globaloff.md) を使用します。 |
   | [/counter](../profiling/counter.md) **:** `Config` | `Config` で指定されたプロセッサのパフォーマンス カウンターから情報を収集します。 カウンター情報は、プロファイル イベントが発生するたびに、収集されたデータに追加されます。 |
   | [/wincounter](../profiling/wincounter.md) **:** `WinCounterPath` | プロファイリング実行中に収集する Windows パフォーマンス カウンターを指定します。 |
   | [/automark](../profiling/automark.md) **:** `Interval` | **/wincounter** との組み合わせでのみ使用します。 Windows パフォーマンス カウンター コレクション イベントの間隔をミリ秒単位で指定します。 既定値は 500 ミリ秒です。 |
   | [/events](../profiling/events-vsperfcmd.md) **:** `Config` | プロファイリング実行中に収集する ETW (Event Tracing for Windows) イベントを指定します。 ETW イベントは独立した (.*etl*) ファイルに収集されます。 |

5. コマンド プロンプト ウィンドウから対象のアプリケーションを開始します。

## <a name="control-data-collection"></a>データ収集の制御
 対象アプリケーションの実行中に、*VSPerfCmd.exe* のオプションを使用して、プロファイラーのデータ ファイルへのデータ書き込みを開始および停止することにより、データ収集を制御できます。 データ コレクションを制御することにより、アプリケーションの起動や終了など、プログラム実行の特定の部分についてのデータ コレクションを行うことができます。

#### <a name="to-start-and-stop-data-collection"></a>データ収集を開始および停止するには

- 次に示すオプションの組み合わせにより、データ収集を開始および停止します。 個別のコマンド ラインで各オプションを指定します。 データ収集のオンとオフは複数回切り替えることができます。

    |オプション|説明|
    |------------|-----------------|
    |[/globalon /globaloff](../profiling/globalon-and-globaloff.md)|すべてのプロセスのデータ収集を開始 ( **/globalon**) または停止 ( **/globaloff**) します。|
    |[/processon](../profiling/processon-and-processoff.md) **:** `PID` [/processoff](../profiling/processon-and-processoff.md) **:** `PID`|プロセス ID (`PID`) で指定されたプロセスのデータ収集を開始 ( **/processon**) または停止 ( **/processoff**) します。|
    |[/threadon](../profiling/threadon-and-threadoff.md) **:** `TID` [/threadoff](../profiling/threadon-and-threadoff.md) **:** `TID`|スレッド ID (`TID`) で指定されたスレッドのデータ収集を開始 ( **/threadon**) または停止 ( **/threadoff**) します。|

## <a name="end-the-profiling-session"></a>プロファイル セッションの終了
 プロファイル セッションを終了するには、インストルメントされたコンポーネントを実行中のアプリケーションを閉じます。 **VSPerfCmd** [/shutdown](../profiling/shutdown.md) オプションを呼び出して、プロファイラーをオフにし、プロファイル データ ファイルを閉じます。 **VSPerfClrEnv /off** コマンドは、プロファイル環境変数を消去します。

#### <a name="to-end-a-profiling-session"></a>プロファイル セッションを終了するには

1. 対象アプリケーションを終了します。

2. プロファイラーをシャットダウンします。 型:

     **VSPerfCmd /shutdown**

3. (省略可能) プロファイル環境変数を削除します。 型:

     **VSPerfClrEnv /off**

## <a name="see-also"></a>関連項目
- [スタンドアロン アプリケーションのプロファイリング](../profiling/command-line-profiling-of-stand-alone-applications.md)
- [インストルメンテーション メソッドのデータ ビュー](../profiling/instrumentation-method-data-views.md)
