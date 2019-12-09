---
title: プロファイラーのコマンド ライン:.NET サービスのインストルメント化、メモリデータの取得
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 2fa072fc-05fe-4420-99c0-51d2ea3ac4ce
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- dotnet
ms.openlocfilehash: 8697f1451e3d528ff27beb2467ff7758e04267cc
ms.sourcegitcommit: 00b71889bd72b6a566586885bdb982cfe807cf54
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2019
ms.locfileid: "74775497"
---
# <a name="how-to-instrument-a-net-framework-service-and-collect-memory-data-by-using-the-profiler-command-line"></a>方法: プロファイラーのコマンド ラインを使用して .NET Framework サービスをインストルメントし、メモリ データを収集する
この記事では、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] プロファイル ツールのコマンド ライン ツールを使用して .NET Framework サービスをインストルメント化し、メモリ使用量データを収集する方法について説明します。 メモリ割り当てデータを収集することも、メモリ割り当てデータとオブジェクト有効期間データの両方を収集することもできます。

> [!NOTE]
> Windows 8 および Windows Server 2012 の強化されたセキュリティ機能によって、Visual Studio プロファイラーがこれらのプラットフォームでデータを収集する方法に大幅な変更が必要になりました。 UWP アプリにも新しい収集手法が必要です。 「[Windows 8 および Windows Server 2012 アプリケーションのパフォーマンス ツール](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)」を参照してください。
>
> [!NOTE]
> コンピューターの起動後にサービスを再起動できない場合、インストルメンテーション メソッドを使用してサービスをプロファイリングすることはできません。このようなサービスが起動されるのは、オペレーティング システムの起動時です。
>
> プロファイル ツールへのパスを取得するには、[コマンド ライン ツールへのパスの指定](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md)に関する記事をご覧ください。 64 ビット コンピューター上では、64 ビット バージョンのツールと 32 ビット バージョンのツールの両方を使用できます。 プロファイラー コマンド ライン ツールを使用するには、コマンド プロンプト ウィンドウの PATH 環境変数にツールのパスを追加するか、コマンド自体にそれを追加します。

## <a name="start-the-profiling-session"></a>プロファイル セッションの開始
 .NET Framework サービスからパフォーマンス データを収集するには、[VSPerfCLREnv.cmd](../profiling/vsperfclrenv.md) ツールを使用して適切な環境変数を初期化し、[VSInstr.exe](../profiling/vsinstr.md) ツールを使用してサービス バイナリ ファイルのインストルメントされたコピーを作成します。

 サービスをホストするコンピューターをプロファイリング用に構成するには再起動が必要です。 サービス コントロール マネージャーからサービスを手動で起動することも必要です。 その後、プロファイラーを起動し、.NET Framework サービスを起動します。

 インストルメントされたコンポーネントを実行すると、メモリ データがデータ ファイルに自動的に収集されます。 プロファイル セッション中にデータ収集を一時停止および再開できます。

 プロファイル セッションを終了するには、サービスを終了し、プロファイラーを明示的に終了します。 ほとんどの場合、セッションの最後にプロファイル環境変数を消去することをお勧めします。

#### <a name="to-begin-profiling-a-net-framework-service"></a>.NET Framework サービスのプロファイリングを開始するには

1. コマンド プロンプト ウィンドウを開きます。

2. **VSInstr** ツールを使用して、サービス バイナリのインストルメントされたバージョンを生成します。

3. サービス コントロール マネージャーを使用して、元のバイナリをインストルメントされたバージョンに置き換えます。 サービスの [スタートアップの種類] が [手動] に設定されていることを確認します。

4. プロファイル環境変数を初期化します。 型:

    **VSPerfClrEnv** { **/globaltracegc** &#124; **/globaltracegclife**}

   - **/globaltracegc** および **/globaltracegclife** を使用すると、メモリの割り当てデータとオブジェクトの有効期間データを収集できます。

       |オプション|説明|
       |------------|-----------------|
       |**/globaltracegc**|メモリの割り当てデータのみを収集します。|
       |**/globaltracegclife**|メモリの割り当ておよびオブジェクトの有効期間データを収集します。|

5. コンピューターを再起動します。

6. コマンド プロンプト ウィンドウを開きます。

7. プロファイラーを起動します。 型:

    **VSPerfCmd**  [/start](../profiling/start.md) **:trace**  [/output](../profiling/output.md) **:** `OutputFile` [`Options`]

   - **/start: contention** オプションによってプロファイラーが初期化されます。

   - **/start** を使用するには、 **/output:** `OutputFile` オプションを指定する必要があります。 `OutputFile` には、プロファイル データ (.vsp) ファイルの名前と場所を指定します。

     **/start:sample** オプションを使用する場合は、次のうちいずれかのオプションを指定できます。

   > [!NOTE]
   > **/user** オプションと **/crosssession** オプションは、通常、サービスで必要です。

   | オプション | 説明 |
   | - | - |
   | [/user](../profiling/user-vsperfcmd.md) **:** [`Domain` **\\** ]`UserName` | ASP.NET ワーカー プロセスを所有するアカウントのドメインおよびユーザー名を指定します。 このオプションは、ログオンしているユーザーとは別のユーザーがプロセスを実行している場合に指定する必要があります。 プロセスの所有者は、Windows タスク マネージャーの [プロセス] タブの [ユーザー名] 列に表示されます。 |
   | [/crosssession](../profiling/crosssession.md) | 他のログオン セッションにおけるプロセスのプロファイリングを有効にします。 このオプションは、ASP.NET アプリケーションが別のセッションで実行されている場合に必要です。 セッション ID は、Windows タスク マネージャーの **[プロセス]** タブの **[セッション ID]** 列に表示されます。 **/crosssession** の省略形として、 **/CS** を指定することができます。 |
   | [/waitstart](../profiling/waitstart.md)[ **:** `Interval`] | プロファイラーがエラーを返すまでプロファイラーの初期化を待機する秒数を指定します。 `Interval` を指定しなかった場合、プロファイラーは無期限に待機します。 既定では、 **/start** が直ちに返されます。 |
   | [/globaloff](../profiling/globalon-and-globaloff.md) | データ収集を一時停止してプロファイラーを起動するには、 **/globaloff** オプションを **/start** コマンド ラインに追加します。 プロファイリングを再開するには、 **/globalon** を使用します。 |
   | [/counter](../profiling/counter.md) **:** `Config` | Config で指定されたプロセッサのパフォーマンス カウンターから情報を収集します。カウンター情報は、プロファイル イベントが発生するたびに、収集されたデータに追加されます。 |
   | [/wincounter](../profiling/wincounter.md) **:** `WinCounterPath` | プロファイリング実行中に収集する Windows パフォーマンス カウンターを指定します。 |
   | [/automark](../profiling/automark.md) **:** `Interval` | **/wincounter** との組み合わせでのみ使用します。 Windows パフォーマンス カウンター コレクション イベントの間隔をミリ秒単位で指定します。 既定値は 500 ミリ秒です。 |
   | [/events](../profiling/events-vsperfcmd.md) **:** `Config` | プロファイリング実行中に収集する ETW (Event Tracing for Windows) イベントを指定します。 ETW イベントは独立した (.*etl*) ファイルに収集されます。 |

8. 起動の必要なサービスがあれば起動します。

9. プロファイラーをサービスにアタッチします。 型:

     **VSPerfCmd /attach:** `PID`&#124;`ProcessName`

    - サービスのプロセス ID またはプロセス名を指定します。 Windows タスク マネージャーで、実行中のすべてのプロセスのプロセス ID と名前を参照できます。

## <a name="control-data-collection"></a>データ収集の制御
 サービスの実行中は、*VSPerfCmd.exe* のオプションを使用してファイルへのデータ書き込みを開始または停止することにより、データ収集を制御できます。 データ コレクションを制御することにより、アプリケーションの起動や終了など、プログラム実行の特定の部分についてのデータ コレクションを行うことができます。

#### <a name="to-start-and-stop-data-collection"></a>データ コレクションを開始および停止するには

- 次に示す **VSPerfCmd** のオプションの組み合わせにより、データ収集を開始および停止します。 個別のコマンド ラインで各オプションを指定します。 データ収集のオンとオフは複数回切り替えることができます。

    |オプション|説明|
    |------------|-----------------|
    |[/globalon /globaloff](../profiling/globalon-and-globaloff.md)|すべてのプロセスのデータ収集を開始 ( **/globalon**) または停止 ( **/globaloff**) します。|
    |[/processon](../profiling/processon-and-processoff.md) **:** `PID` [/processoff](../profiling/processon-and-processoff.md) **:** `PID`|プロセス ID (`PID`) で指定されたプロセスのデータ収集を開始 ( **/processon**) または停止 ( **/processoff**) します。|
    |[/threadon](../profiling/threadon-and-threadoff.md) **:** `TID` [/threadoff](../profiling/threadon-and-threadoff.md) **:** `TID`|スレッド ID (`TID`) で指定されたスレッドのデータ収集を開始 ( **/threadon**) または停止 ( **/threadoff**) します。|

## <a name="end-the-profiling-session"></a>プロファイル セッションの終了
 プロファイル セッションを終了するには、インストルメントされたコンポーネントを実行しているアプリケーションを終了し、**VSPerfCmd** [/shutdown](../profiling/shutdown.md) オプションを開始してプロファイラーをオフにした後、プロファイル データ ファイルを閉じます。 **VSPerfClrEnv /globaloff** コマンドは、プロファイル環境変数を消去します。

#### <a name="to-end-a-profiling-session"></a>プロファイル セッションを終了するには

1. サービス コントロール マネージャーからサービスを停止します。

2. プロファイラーをシャットダウンします。 型:

     **VSPerfCmd /shutdown**

3. すべてのプロファイリングを完了したら、プロファイル環境変数を消去します。 型:

     **VSPerfClrEnv /globaloff**

     インストルメントされたモジュールを元のモジュールに置き換えます。 必要に応じて、サービスの [スタートアップの種類] を再構成します。

4. コンピューターを再起動します。

## <a name="see-also"></a>関連項目
- [サービスのプロファイリング](../profiling/command-line-profiling-of-services.md)
- [.NET メモリのデータ ビュー](../profiling/dotnet-memory-data-views.md)
