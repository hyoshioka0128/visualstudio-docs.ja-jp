---
title: プロファイラーのコマンド ライン - 静的な ASP.NET アプリのインストルメント化、メモリ データの取得
description: Visual Studio プロファイル ツールのコマンドライン ツールを使用して、プリコンパイルされた ASP.NET Web コンポーネントまたは Web サイトのメモリとタイミングのデータを収集する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: ea1dcb7c-1dc3-49ff-9418-8795b5b3d3bc
author: mikejo5000
ms.author: mikejo
manager: jmartens
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: d067e929fe36036457bef59b6ff477180b51c6dd
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99928960"
---
# <a name="how-to-instrument-a-statically-compiled-aspnet-web-application-and-collect-memory-data-by-using-the-profiler-command-line"></a>方法: プロファイラーのコマンド ラインを使用して静的にコンパイルされた ASP.NET Web アプリケーションをインストルメント化し、メモリ データを収集する
この記事では、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] プロファイル ツールのコマンド ライン ツールを使用して、プリコンパイルされた [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] Web コンポーネントまたは Web サイトをインストルメント化し、.NET メモリの割り当て、オブジェクトの有効期間、および詳細なタイミング データを収集する方法について説明します。

> [!NOTE]
> プロファイル ツールへのパスを取得するには、[コマンド ライン ツールへのパスの指定](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md)に関する記事をご覧ください。 64 ビット コンピューター上では、64 ビット バージョンのツールと 32 ビット バージョンのツールの両方を使用できます。 プロファイラー コマンド ライン ツールを使用するには、コマンド プロンプト ウィンドウの PATH 環境変数にツールのパスを追加するか、コマンド自体にそれを追加します。

 インストルメンテーション メソッドを使用して [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] Web コンポーネントからデータを収集するには、[VSInstr.exe](../profiling/vsinstr.md) ツールを使用して、コンポーネントのインストルメントされたバージョンを生成します。 コンポーネントをホストするコンピューターで、コンポーネントのインストルメントされていないバージョンをインストルメントされたバージョンに置き換えます。 次に、[VSPerfCLREnv.cmd](../profiling/vsperfclrenv.md) ツールを使用してグローバル プロファイリング環境変数を初期化し、ホスト コンピューターを再起動します。 次に、プロファイラーを起動します。

 インストルメントされたコンポーネントを実行すると、タイミング データがデータ ファイルに自動的に収集されます。 プロファイル セッション中にデータ収集を一時停止および再開できます。

 プロファイル セッションを終了するには、コンポーネントをホストする [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] ワーカー プロセスを終了し、プロファイラーを明示的に終了します。 ほとんどの場合、セッションの最後にプロファイル環境変数を消去することをお勧めします。

## <a name="start-to-profile"></a>プロファイルの開始

#### <a name="to-instrument-an-aspnet-web-component-and-start-profiling"></a>ASP.NET Web コンポーネントをインストルメントしてプロファイリングを開始するには

1. **VSInstr** ツールを使用して、対象アプリケーションのインストルメントされたバージョンを生成します。 必要に応じて、ASP.NET ホスト コンピューター上のアプリケーション バイナリをインストルメントされたバイナリに置き換えます。

2. コマンド プロンプト ウィンドウを開きます。

3. .NET プロファイル環境変数を初期化します。 コマンド プロンプト ウィンドウで、次のように入力します。

    **VSPerfClrEnv /globaltracegc**

    \- または -

    **VSPerfClrEnv /globaltracegclife**

   - **/globaltracegc** は、.NET メモリの割り当ておよびタイミング データを収集します。

   - **/globaltracegclife** は、.NET メモリの割り当て、オブジェクトの有効期間、および詳細なタイミング データを収集します。

4. コンピューターを再起動します。

5. コマンド プロンプト ウィンドウを開きます。

6. プロファイラーを起動します。 コマンド プロンプト ウィンドウで、次のように入力します。

    **VSPerfCmd /start:trace /output:** `OutputFile` [`Options`]

   - [/start](../profiling/start.md) **:trace** オプションによってプロファイラーが初期化されます。

   - **/start** を使用するには、[/output](../profiling/output.md) **:** `OutputFile` オプションを指定する必要があります。 `OutputFile` には、プロファイル データ (.vsp) ファイルの名前と場所を指定します。

     **/start:trace** オプションを使用する場合は、次のうちいずれのオプションでも指定できます。

   > [!NOTE]
   > **/user** オプションと **/crosssession** オプションは、通常、ASP.NET アプリケーションで必要です。

   | オプション | 説明 |
   | - | - |
   | [/user](../profiling/user-vsperfcmd.md) **:** [`Domain` **\\** ]`UserName` | ASP.NET ワーカー プロセスを所有するアカウントのドメインおよびユーザー名を指定します (省略可能)。 このオプションは、ログオンしているユーザーとは別のユーザーがプロセスを実行している場合に指定する必要があります。この名前は、Windows タスク マネージャーの **[プロセス]** タブの **[ユーザー名]** 列に表示されます。 |
   | [/crosssession](../profiling/crosssession.md) | 他のセッションにおけるプロセスのプロファイリングを有効にします。 このオプションは、アプリケーションが別のセッションで実行されている場合に必要です。 セッション ID は、Windows タスク マネージャーの **[プロセス]** タブの [セッション ID] 列に表示されます。 **/crosssession** の省略形として、 **/CS** を指定することができます。 |
   | [/wincounter](../profiling/wincounter.md) **:** `WinCounterPath` | プロファイリング実行中に収集する Windows パフォーマンス カウンターを指定します。 |
   | [/automark](../profiling/automark.md) **:** `Interval` | **/wincounter** との組み合わせでのみ使用します。 Windows パフォーマンス カウンター コレクション イベントの間隔をミリ秒単位で指定します。 既定値は 500 ミリ秒です。 |
   | [/events](../profiling/events-vsperfcmd.md) **:** `Config` | プロファイリング実行中に収集する ETW (Event Tracing for Windows) イベントを指定します。 ETW イベントは独立した (.etl) ファイルに収集されます。 |
   | [/globaloff](../profiling/globalon-and-globaloff.md) | データ収集を一時停止してプロファイラーを起動するには、 **/globaloff** オプションを **/start** コマンド ラインに追加します。 プロファイリングを再開するには、 **/globalon** を使用します。 |

7. インストルメント化されたコンポーネントを含む Web サイトを開きます。

## <a name="control-data-collection"></a>データ収集の制御
 対象アプリケーションの実行中は、*VSPerfCmd.exe* のオプションを使用してファイルへのデータ書き込みを開始および停止することにより、データ収集を制御できます。 データ コレクションを制御することにより、アプリケーションの起動や終了など、プログラム実行の特定の部分についてのデータ コレクションを行うことができます。

#### <a name="to-start-and-stop-data-collection"></a>データ収集を開始および停止するには

- 次に示すオプションの組み合わせにより、データ収集を開始および停止します。 個別のコマンド ラインで各オプションを指定します。 データ収集のオンとオフは複数回切り替えることができます。

    |オプション|説明|
    |------------|-----------------|
    |[/globalon /globaloff](../profiling/globalon-and-globaloff.md)|すべてのプロセスのデータ収集を開始 ( **/globalon**) または停止 ( **/globaloff**) します。|
    |[/processon](../profiling/processon-and-processoff.md) **:** `PID` [/processoff](../profiling/processon-and-processoff.md) **:** `PID`|プロセス ID (`PID`) で指定されたプロセスのデータ収集を開始 ( **/processon**) または停止 ( **/processoff**) します。|
    |[/threadon](../profiling/threadon-and-threadoff.md) **:** `TID` [/threadoff](../profiling/threadon-and-threadoff.md) **:** `TID`|スレッド ID (`TID`) で指定されたスレッドのデータ収集を開始 ( **/threadon**) または停止 ( **/threadoff**) します。|

## <a name="end-the-profiling-session"></a>プロファイル セッションの終了
 プロファイル セッションを終了するには、[!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] Web アプリケーションを終了し、インターネット インフォメーション サービス (IIS) の **IISReset** コマンド使用して [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] ワーカー プロセスを終了します。 **VSPerfCmd** [/shutdown](../profiling/shutdown.md) オプションを呼び出して、プロファイラーをオフにし、プロファイル データ ファイルを閉じます。 **VSPerfClrEnv /globaloff** コマンドは、プロファイル環境変数を消去します。 新しい環境設定を適用するには、コンピューターを再起動する必要があります。

#### <a name="to-end-a-profiling-session"></a>プロファイル セッションを終了するには

1. [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] Web アプリケーションを終了します。

2. [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] ワーカー プロセスを終了します。 型:

    **IISReset /stop**

3. プロファイラーをシャットダウンします。 型:

    **VSPerfCmd /shutdown**

4. (省略可能) プロファイル環境変数を削除します。 型:

    **VSPerfCmd /globaloff**

5. コンピューターを再起動します。 必要に応じて、IIS を再起動します。 型:

    **IISReset /start**

## <a name="see-also"></a>関連項目
- [ASP.NET Web アプリケーションのプロファイリング](../profiling/command-line-profiling-of-aspnet-web-applications.md)
- [.NET メモリのデータ ビュー](../profiling/dotnet-memory-data-views.md)
