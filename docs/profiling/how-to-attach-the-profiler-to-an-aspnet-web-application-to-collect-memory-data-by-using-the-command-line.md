---
title: プロファイラーを ASP.NET にアタッチし、メモリ データを収集する
description: Visual Studio プロファイル ツールを使用して、ASP.NET Web アプリケーションにプロファイラーをアタッチし、.NET Framework のメモリ割り当ての数とサイズに関するデータを取得します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: d608f85a-41ae-4ca7-85e6-b96624dbc83c
author: mikejo5000
ms.author: mikejo
manager: jmartens
monikerRange: vs-2017
ms.workload:
- aspnet
ms.openlocfilehash: eb90141f10787b820fcb31ee0337f6cd8402f084
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99877084"
---
# <a name="how-to-attach-the-profiler-to-an-aspnet-web-application-to-collect-memory-data-by-using-the-command-line"></a>方法: コマンド ラインを使用してプロファイラーを ASP.NET Web アプリケーションにアタッチし、メモリ データを収集する
この記事では、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] プロファイル ツールのコマンド ライン ツールを使用して、[!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] Web アプリケーションにプロファイラーをアタッチし、.NET Framework のメモリ割り当ての数とサイズに関するデータを収集する方法について説明します。 .NET Framework メモリ オブジェクトの有効期間に関するデータも収集できます。

> [!NOTE]
> プロファイル ツールへのパスを取得するには、[コマンド ライン ツールへのパスの指定](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md)に関する記事をご覧ください。 64 ビット コンピューター上では、64 ビット バージョンのツールと 32 ビット バージョンのツールの両方を使用できます。 プロファイラー コマンド ライン ツールを使用するには、コマンド プロンプト ウィンドウの PATH 環境変数にツールのパスを追加するか、コマンド自体にそれを追加します。

 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] Web アプリケーションからパフォーマンス データを収集するには、[VSPerfCLREnv.cmd](../profiling/vsperfclrenv.md) ツールを使用して、[!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] Web アプリケーションをホストするコンピューター上で該当する環境変数を初期化する必要があります。 次に、コンピューターを再起動して、Web サーバーをプロファイリング用に構成します。

 次に、[VSPerfCmd.exe](../profiling/vsperfcmd.md) ツールを使用して、Web サイトをホストする [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] ワーカー プロセスにプロファイラーをアタッチします。 プロファイラーをアプリケーションにアタッチしているときにデータ コレクションを一時停止し、完了後に再開できます。

 プロファイル セッションを終了するには、アプリケーションへのプロファイラーのアタッチを解除し、プロファイラーを明示的に終了する必要があります。 ほとんどの場合、セッションの最後にプロファイル環境変数を消去することをお勧めします。

## <a name="attach-the-profiler"></a>プロファイラーのアタッチ

#### <a name="to-attach-the-profiler-to-an-aspnet-web-application"></a>プロファイラーを ASP.NET Web アプリケーションにアタッチするには

1. コマンド プロンプト ウィンドウを開きます。

2. プロファイル環境変数を初期化します。 型:

    **VSPerfClrEnv** { **/globalsamplegc** &#124; **/globalsamplegclife**} **[/samplelineoff]**

   - オプションの **/globalsamplegc** と **/globalsamplegclife** では、収集するメモリ データの型を指定します。

        次のいずれかのオプションを 1 つのみ指定します。

       |オプション|説明|
       |------------|-----------------|
       |**/globalsamplegc**|メモリの割り当てデータを収集できます。|
       |**/globalsamplegclife**|メモリの割り当てデータとオブジェクトの有効期間データを収集できます。|

   - オプションの **/samplelineoff** は特定のソース コード行への収集データの割り当てを無効にします。 このオプションを指定すると、データは関数レベルで割り当てられます。

3. コンピューターを再起動して、新しい環境構成を設定します。

4. コマンド プロンプト ウィンドウを開きます。 必要に応じて、プロファイラー パスの環境変数を設定します。

5. プロファイラーを起動します。 型:

    **VSPerfCmd**  [/start](../profiling/start.md) **:sample**  [/output](../profiling/output.md) **:** `OutputFile` [`Options`]

   - **/start:sample** オプションによってプロファイラーが初期化されます。

   - **/start** を使用するには、 **/output:** `OutputFile` オプションを指定する必要があります。 `OutputFile` には、プロファイル データ (.vsp) ファイルの名前と場所を指定します。

     **/start:sample** オプションを使用する場合は、次のうちいずれかのオプションを指定できます。

   > [!NOTE]
   > **/user** オプションと **/crosssession** オプションは、通常、ASP.NET アプリケーションで必要です。

   | オプション | 説明 |
   | - | - |
   | [/user](../profiling/user-vsperfcmd.md) **:** [`Domain` **\\** ]`UserName` | ASP.NET ワーカー プロセスを所有するアカウントのドメインおよびユーザー名を指定します。 このオプションは、ログオンしているユーザーとは別のユーザーがプロセスを実行している場合に指定する必要があります。 プロセスの所有者は、Windows タスク マネージャーの [プロセス] タブの [ユーザー名] 列に表示されます。 |
   | [/crosssession](../profiling/crosssession.md) | 他のログオン セッションにおけるプロセスのプロファイリングを有効にします。 このオプションは、ASP.NET アプリケーションが別のセッションで実行されている場合に必要です。 セッション ID は、Windows タスク マネージャーの [プロセス] タブの [セッション ID] 列に表示されます。 **/crosssession** の省略形として、 **/CS** を指定することができます。 |
   | [/waitstart](../profiling/waitstart.md) [ **:** `Interval`] | プロファイラーがエラーを返すまでプロファイラーの初期化を待機する秒数を指定します。 `Interval` を指定しなかった場合、プロファイラーは無期限に待機します。 既定では、 **/start** が直ちに返されます。 |
   | [/wincounter](../profiling/wincounter.md) **:** `WinCounterPath` | プロファイリング実行中に収集する Windows パフォーマンス カウンターを指定します。 |
   | [/automark](../profiling/automark.md) **:** `Interval` | **/wincounter** との組み合わせでのみ使用します。 Windows パフォーマンス カウンター コレクション イベントの間隔をミリ秒単位で指定します。 既定値は 500 ミリ秒です。 |
   | [/events](../profiling/events-vsperfcmd.md) **:** `Config` | プロファイリング実行中に収集する ETW (Event Tracing for Windows) イベントを指定します。 ETW イベントは独立した (.etl) ファイルに収集されます。 |

6. 一般的な方法で [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] Web アプリケーションを起動します。

7. プロファイラーを [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] ワーカー プロセスにアタッチします。 型:

    **VSPerfCmd**  [/attach](../profiling/attach.md) **:** {`PID`&#124;`ProcName`} [[/targetclr](../profiling/targetclr.md) **:** `Version`]

   - プロセス ID `(PID)` には、[!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] ワーカー プロセスのプロセス ID またはプロセス名を指定します。 Windows タスク マネージャーで、実行中のすべてのプロセスのプロセス ID を参照できます。

   - **/targetclr:** `Version` には、アプリケーションに複数のバージョンのランタイムが読み込まれている場合に、プロファイリングを行う共通言語ランタイム (CLR) のバージョンを指定します。

## <a name="control-data-collection"></a>データ収集の制御
 アプリケーションの実行中に、**VSPerfCmd.exe** オプションを使用して、プロファイラーのデータ ファイルへのデータ書き込みを開始および停止することにより、データ収集を制御できます。 データ コレクションを制御することにより、アプリケーションの起動や終了など、プログラム実行の特定の部分についてのデータ コレクションを行うことができます。

#### <a name="to-start-and-stop-data-collection"></a>データ収集を開始および停止するには

- 次に示す **VSPerfCmd** のオプションの組み合わせにより、データ収集を開始および停止します。 個別のコマンド ラインで各オプションを指定します。 データ収集のオンとオフは複数回切り替えることができます。

    |オプション|説明|
    |------------|-----------------|
    |[/globalon /globaloff](../profiling/globalon-and-globaloff.md)|すべてのプロセスのデータ収集を開始 ( **/globalon**) または停止 ( **/globaloff**) します。|
    |[/processon](../profiling/processon-and-processoff.md) **:** `PID` [/processoff](../profiling/processon-and-processoff.md) **:** `PID`|`PID` で指定されたプロセスのデータ収集を開始 ( **/processon**) または停止 ( **/processoff**) します。|
    |**/attach:** {`PID`&#124;`ProcName`} [/detach](../profiling/detach.md)[ **:** {`PID`&#124;:`ProcName`}]|**/attach** は、プロセス ID またはプロセス名で指定したプロセスのデータ収集を開始します。 **/detach** は、指定されたプロセスのデータ収集を停止します。特定のプロセスが指定されていない場合は、すべてのプロセスのデータ収集を停止します。|

## <a name="end-the-profiling-session"></a>プロファイル セッションの終了
 プロファイル セッションを終了するには、プロファイラーを Web アプリケーションからデタッチする必要があります。 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] ワーカー プロセスを再起動するか、**VSPerfCmd /detach** オプションを呼び出すことによって、サンプリング メソッドを使用してプロファイリングが実行されているアプリケーションからのデータ収集を停止できます。 次に、**VSPerfCmd** [/shutdown](../profiling/shutdown.md) オプションを呼び出して、プロファイラーをオフにし、プロファイル データ ファイルを閉じます。 **VSPerfClrEnv /globaloff** コマンドによってプロファイル環境変数は消去されますが、コンピューターを再起動するまでシステム構成はリセットされません。

#### <a name="to-end-a-profiling-session"></a>プロファイル セッションを終了するには

1. 対象アプリケーションからプロファイラーをデタッチするには、次のいずれかの手順を実行します。

   - **VSPerfCmd** [/detach](../profiling/detach.md) と入力します

      \- または -

   - [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] ワーカー プロセスを終了します。 型:

     **IISReset /stop**

2. プロファイラーをシャットダウンします。 型:

    **VSPerfCmd /shutdown**

3. (省略可能) プロファイル環境変数を削除します。 型:

    **VSPerfCmd /globaloff**

4. コンピューターを再起動します。 必要に応じて、インターネット インフォメーション サービス (IIS: Internet Information Services) を再起動します。 型:

    **IISReset /start**

## <a name="see-also"></a>関連項目
- [ASP.NET Web アプリケーションのプロファイリング](../profiling/command-line-profiling-of-aspnet-web-applications.md)
- [.NET メモリのデータ ビュー](../profiling/dotnet-memory-data-views.md)
