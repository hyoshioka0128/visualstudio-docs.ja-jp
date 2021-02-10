---
title: プロファイラーを .NET サービスにアタッチし、メモリ データを収集する
description: Visual Studio プロファイル ツールのコマンド ライン ツールを使用して、プロファイラーを .NET Framework サービスにアタッチし、メモリ データを収集します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: aeac39af-ad99-479f-aa36-4104356ca512
author: mikejo5000
ms.author: mikejo
manager: jmartens
monikerRange: vs-2017
ms.workload:
- dotnet
ms.openlocfilehash: 22db478d5d88f8e3311b7b3ddb883768d5ad9af6
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99958792"
---
# <a name="how-to-attach-the-profiler-to-a-net-framework-service-to-collect-memory-data-by-using-the-command-line"></a>方法: コマンド ラインを使用してプロファイラーを .NET Framework サービスにアタッチし、メモリ データを収集する
この記事では、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] プロファイル ツールのコマンド ライン ツールを使用してプロファイラーを .NET Framework サービスにアタッチし、メモリ データを収集する方法について説明します。 メモリ割り当ての数およびサイズに関するデータだけでなく、メモリ オブジェクトの有効期間に関するデータも収集できます。

> [!NOTE]
> Windows 8 および Windows Server 2012 の強化されたセキュリティ機能によって、Visual Studio プロファイラーがこれらのプラットフォームでデータを収集する方法に大幅な変更が必要になりました。 UWP アプリにも新しい収集手法が必要です。 「[Windows 8 および Windows Server 2012 アプリケーションのパフォーマンス ツール](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)」を参照してください。
>
> [!NOTE]
> プロファイル ツールへのパスを取得するには、[コマンド ライン ツールへのパスの指定](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md)に関する記事をご覧ください。 64 ビット コンピューター上では、64 ビット バージョンのツールと 32 ビット バージョンのツールの両方を使用できます。 プロファイラー コマンド ライン ツールを使用するには、コマンド プロンプト ウィンドウの PATH 環境変数にツールのパスを追加するか、コマンド自体にそれを追加します。

 .NET Framework サービスからメモリ データを収集するには、[VSPerfCLREnv.cmd](../profiling/vsperfclrenv.md) ツールを使用して、サービスをホストするコンピューター上で該当する環境変数を初期化する必要があります。 コンピューターをプロファイリング用に構成するには再起動が必要です。

 次に、[VSPerfCmd](../profiling/vsperfcmd.md) ツールを使用してプロファイラーをサービス プロセスにアタッチします。 プロファイラーをサービスにアタッチしている間はデータ コレクションを一時停止し、完了後に再開できます。

 プロファイル セッションを終了するには、プロファイラーをサービスからデタッチし、プロファイラーを明示的に終了する必要があります。 ほとんどの場合、セッションの最後にプロファイル環境変数を消去することをお勧めします。

## <a name="attach-the-profiler"></a>プロファイラーのアタッチ

#### <a name="to-attach-the-profiler-to-a-net-framework-service"></a>プロファイラーを .NET Framework サービスにアタッチするには

1. インストールの必要なサービスがあればインストールします。

2. コマンド プロンプト ウィンドウを開きます。

3. プロファイル環境変数を初期化します。 型:

    **VSPerfClrEnv** { **/globalsamplegc /globalsamplegclife**} **[/samplelineoff]**

   - オプションの **/globalsamplegclife** と **/globalsamplegclife** では、収集するメモリ データの型を指定します。 次のいずれかのオプションを 1 つのみ指定します。

     **/globalsamplegc** メモリの割り当てデータの収集を有効にします。

     **/globalsamplegclife** メモリの割り当てデータとオブジェクトの有効期間データの両方の収集を有効にします。

   - **/samplelineoff** オプションを指定すると、ソース コードの行番号データの収集が無効になります。

4. コンピューターを再起動して、新しい環境構成を設定します。

5. 起動の必要なサービスがあれば起動します。

6. コマンド プロンプト ウィンドウを開きます。 必要に応じて、プロファイラー パスを PATH 環境変数に追加します。

7. プロファイラーを起動します。 型:

    **VSPerfCmd**  [/start](../profiling/start.md) **:sample**  [/output](../profiling/output.md) **:** `OutputFile` [`Options`]

   - **/start:sample** オプションによってプロファイラーが初期化されます。

   - **/start** を使用するには、 **/output:** `OutputFile` オプションを指定する必要があります。 `OutputFile` には、プロファイル データ (.vsp) ファイルの名前と場所を指定します。

     **/start:sample** オプションを使用する場合は、次の 1 つ以上のオプションを指定できます。

   > [!NOTE]
   > **/user** オプションと **/crosssession** オプションは、通常、サービスで必要です。

   | オプション | 説明 |
   | - | - |
   | [/user](../profiling/user-vsperfcmd.md) **:** [`Domain` **\\** ]`UserName` | プロセスを所有するアカウントのドメインおよびユーザー名を指定します。 このオプションは、ログオンしているユーザーとは別のユーザーがプロセスを実行している場合に指定する必要があります。 プロセスの所有者は、Windows タスク マネージャーの [プロセス] タブの [ユーザー名] 列に表示されます。 |
   | [/crosssession](../profiling/crosssession.md) | 他のログオン セッションにおけるプロセスのプロファイリングを有効にします。 このオプションは、ASP.NET アプリケーションが別のセッションで実行されている場合に必要です。 セッション ID は、Windows タスク マネージャーの [プロセス] タブの [セッション ID] 列に表示されます。 **/crosssession** の省略形として、 **/CS** を指定することができます。 |
   | [/user](../profiling/user-vsperfcmd.md) **:** [`Domain` **\\** ]`UserName` | サービスが実行されるログオン アカウントのドメインおよびユーザー名を指定します (省略可能)。 ログオン アカウントは、Windows サービス コントロール マネージャーのサービスの [ログオン方法] 列に表示されます。 |
   | [/crosssession&#124;cs](../profiling/crosssession.md) | 他のログオン セッションにおけるプロセスのプロファイリングを有効にします。 |
   | [/wincounter](../profiling/wincounter.md) **:** `WinCounterPath` | プロファイリング実行中に収集する Windows パフォーマンス カウンターを指定します。 |
   | [/automark](../profiling/automark.md) **:** `Interval` | **/wincounter** との組み合わせでのみ使用します。 Windows パフォーマンス カウンター コレクション イベントの間隔をミリ秒単位で指定します。 既定値は 500 ミリ秒です。 |
   | [/events](../profiling/events-vsperfcmd.md) **:** `Config` | プロファイリング実行中に収集する ETW (Event Tracing for Windows) イベントを指定します。 ETW イベントは独立した (.etl) ファイルに収集されます。 |

8. プロファイラーをサービスにアタッチします。 型:

    **VSPerfCmd**  [/attach](../profiling/attach.md) **:** {`PID`&#124;`ProcName`} [[/targetclr](../profiling/targetclr.md) **:** `Version`]

   - サービスのプロセス ID またはプロセス名を指定します。 Windows タスク マネージャーで、実行中のすべてのプロセスのプロセス ID と名前を参照できます。

   - **targetclr:** `Version` には、アプリケーションに複数のバージョンのランタイムが読み込まれている場合に、プロファイリングを行う共通言語ランタイム (CLR) のバージョンを指定します。 任意。

## <a name="control-data-collection"></a>データ収集の制御
 サービスの実行中に、*VSPerfCmd.exe* のオプションを使用して、プロファイラー データ ファイルへのデータ書き込みを停止または開始できます。 データ コレクションを制御することにより、アプリケーションの起動や終了など、プログラム実行の特定の部分についてのデータ コレクションを行うことができます。

#### <a name="to-start-and-stop-data-collection"></a>データ収集を開始および停止するには

- 次に示す **VSPerfCmd** のオプションの組み合わせにより、データ収集を開始および停止します。 個別のコマンド ラインで各オプションを指定します。 データ収集のオンとオフは複数回切り替えることができます。

    |オプション|説明|
    |------------|-----------------|
    |[/globalon /globaloff](../profiling/globalon-and-globaloff.md)|すべてのプロセスのデータ収集を開始 ( **/globalon**) または停止 ( **/globaloff**) します。|
    |[/processon](../profiling/processon-and-processoff.md) **:** `PID` [/processoff](../profiling/processon-and-processoff.md) **:** `PID`|プロセス ID (`PID`) で指定されたプロセスのデータ コレクションを開始 ( **/processon**) または停止 ( **/processoff**) します。|
    |**/attach:** {`PID`&#124;`ProcName`} [/detach](../profiling/detach.md)[:{`PID`&#124;`ProcName`}]|**/attach** は、プロセス ID またはプロセス名で指定したプロセスのデータ収集を開始します。 **/detach** は、指定されたプロセスのデータ収集を停止します。特定のプロセスが指定されていない場合は、すべてのプロセスのデータ収集を停止します。|

## <a name="end-the-profiling-session"></a>プロファイル セッションの終了
 プロファイル セッションを終了するには、プロファイラーがデータ収集を停止している必要があります。 サービスを停止するか **VSPerfCmd /detach** オプションを呼び出すことによって、サンプリング メソッドを使用してプロファイリングが実行されているアプリケーションからのデータ コレクションを停止できます。 次に、**VSPerfCmd** [/shutdown](../profiling/shutdown.md) オプションを呼び出して、プロファイラーをオフにし、プロファイル データ ファイルを閉じます。 **VSPerfClrEnv /globaloff** コマンドによってプロファイル環境変数は消去されますが、コンピューターを再起動するまでシステム構成はリセットされません。

#### <a name="to-end-a-profiling-session"></a>プロファイル セッションを終了するには

1. 対象アプリケーションからプロファイラーをデタッチするには、次のいずれかの操作を行います。

    - サービスを停止します。

         \- または -

    - **VSPerfCmd /detach** と入力します

2. プロファイラーをシャットダウンします。 型:

     **VSPerfCmd /shutdown**

3. (省略可能) プロファイル環境変数を削除します。 型:

     **VSPerfClrEnv /globaloff**

4. コンピューターを再起動します。

## <a name="see-also"></a>関連項目
- [サービスのプロファイリング](../profiling/command-line-profiling-of-services.md)
- [.NET メモリのデータ ビュー](../profiling/dotnet-memory-data-views.md)
