---
title: プロファイラーのコマンド ライン - 動的な ASP.NET アプリのインストルメント化、メモリ データの取得
description: Visual Studio プロファイル ツールのコマンドライン ツールを使用して、動的にコンパイルされた ASP.NET アプリケーションの詳細なメモリ アクティビティ データを収集する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 2cdd9903-39db-47e8-93dd-5e6a21bc3435
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- aspnet
ms.openlocfilehash: c26342fb956aa5043f316015f05e18ef70d20559
ms.sourcegitcommit: 8e15b434bf5db3e0f719320ca82682df1a3da110
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/27/2021
ms.locfileid: "98883593"
---
# <a name="how-to-instrument-a-dynamically-compiled-aspnet-web-application-and-collect-memory-data-by-using-the-profiler-command-line"></a>方法: プロファイラーのコマンド ラインを使用して動的にコンパイルされた ASP.NET Web アプリケーションをインストルメント化し、メモリ データを収集する
このトピックでは、コマンドライン ツールの [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] プロファイル ツールを利用し、インストルメンテーション プロファイル方法で、動的にコンパイルされた [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] Web アプリケーションの .NET メモリ割り当てとオブジェクト有効期間に関する詳細データを収集する方法について説明します。

> [!NOTE]
> プロファイル ツールへのパスを取得するには、[コマンド ライン ツールへのパスの指定](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md)に関する記事をご覧ください。 64 ビット コンピューター上では、64 ビット バージョンのツールと 32 ビット バージョンのツールの両方を使用できます。 プロファイラー コマンド ライン ツールを使用するには、コマンド プロンプト ウィンドウの PATH 環境変数にツールのパスを追加するか、コマンド自体にそれを追加します。

 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] Web アプリケーションからパフォーマンス データを収集するには、ターゲット アプリケーションの *web.config* ファイルを変更し、動的にコンパイルされたアプリケーション ファイルをインストルメント化する [VSInstr.exe](../profiling/vsinstr.md) ツールを有効にします。 次に [VSPerfCLREnv.cmd](../profiling/vsperfclrenv.md) ツールを使用し、[!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] Web アプリケーションをホストするサーバーを構成し、適切な環境変数を設定して .NET メモリ プロファイリングを有効にし、コンピューターを再起動します。

 データを収集するには、プロファイラーを起動し、ターゲット アプリケーションを実行します。 プロファイラーをアプリケーションにアタッチしている間はデータ収集を一時停止し、再開できます。適切なデータを収集したら、アプリケーションを閉じ、インターネット インフォメーション サービス (IIS) のワーカー プロセスを閉じ、プロファイラーをシャットダウンします。

 プロファイル作業を完了したら、*web.config* ファイルと Web サーバーを元の状態に復元します。

## <a name="configure-the-aspnet-web-application-and-the-web-server"></a>ASP.NET Web アプリケーションと Web サーバーを構成する

#### <a name="to-configure-the-aspnet-web-application-and-the-web-server"></a>ASP.NET Web アプリケーションと Web サーバーを構成するには

1. ターゲット アプリケーションの *web.config* ファイルを変更します。 「[方法:Web.config ファイルを変更して、動的にコンパイルされた ASP.NET Web アプリケーションをインストルメント化およびプロファイルする](../profiling/how-to-modify-web-config-files-to-instrument-dynamically-compiled-aspnet-apps.md)」をご覧ください。

2. Web アプリケーションをホストするコンピューターでコマンド プロンプト ウィンドウを開きます。

3. プロファイル環境変数を初期化します。 型:

     **VSPerfClrEnv /globaltracegc**

     \- または -

     **VSPerfClrEnv /globaltracegclife**

    - **/globaltracegc** では、メモリの割り当てデータを収集できます。

    - **/globaltracegclife** では、メモリの割り当てデータとオブジェクトの有効期間データを収集できます。

4. コンピューターを再起動します。

## <a name="run-the-profiling-session"></a>プロファイル セッションの実行

#### <a name="to-profile-the-aspnet-web-application"></a>ASP.NET Web アプリケーションをプロファイリングするには

1. プロファイラーを起動します。 型:

    **VSPerfCmd** [/start](../profiling/start.md) **:trace** [/output](../profiling/output.md) **:** `OutputFile` [`Options`]

   - **/start:trace** オプションによってプロファイラーが初期化されます。

   - **/start** を使用するには、 **/output:** `OutputFile` オプションを指定する必要があります。 `OutputFile` には、プロファイル データ (.*vsp*) ファイルの名前と場所を指定します。

     **/start:trace** オプションを使用する場合は、次のうちいずれのオプションでも指定できます。

   > [!NOTE]
   > **/user** オプションと **/crosssession** オプションは、通常、ASP.NET アプリケーションで必要です。

   | オプション | 説明 |
   | - | - |
   | [/user](../profiling/user-vsperfcmd.md) **:** [`Domain` **\\** ]`UserName` | [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] ワーカー プロセスを所有するアカウントのドメインおよびユーザー名を指定します (省略可能)。 このオプションは、ログオンしているユーザーとは別のユーザーがプロセスを実行している場合に指定する必要があります。 名前は、Windows タスク マネージャーの **[プロセス]** タブの **[ユーザー名]** 列に表示されます。 |
   | [/crosssession](../profiling/crosssession.md) | 他のセッションにおけるプロセスのプロファイリングを有効にします。 このオプションは、アプリケーションが別のセッションで実行されている場合に必要です。 セッション ID は、Windows タスク マネージャーの **[プロセス]** タブの **[セッション ID]** 列に表示されます。 **/crosssession** の省略形として、 **/CS** を指定することができます。 |
   | [/globaloff](../profiling/globalon-and-globaloff.md) | データ コレクションを一時停止した状態でプロファイラーを起動します。 プロファイリングを再開するには、[/globalon](../profiling/globalon-and-globaloff.md) を使用します。 |
   | [/counter](../profiling/counter.md) **:** `Config` | `Config` で指定されたプロセッサのパフォーマンス カウンターから情報を収集します。 カウンター情報は、プロファイル イベントが発生するたびに、収集されたデータに追加されます。 |
   | [/wincounter](../profiling/wincounter.md) **:** `WinCounterPath` | プロファイリング実行中に収集する Windows パフォーマンス カウンターを指定します。 |
   | [/automark](../profiling/automark.md) **:** `Interval` | **/wincounter** との組み合わせでのみ使用します。 Windows パフォーマンス カウンター コレクション イベントの間隔をミリ秒単位で指定します。 既定値は 500 ミリ秒です。 |
   | [/events](../profiling/events-vsperfcmd.md) **:** `Config` | プロファイリング実行中に収集する ETW (Event Tracing for Windows) イベントを指定します。 ETW イベントは独立した (.*etl*) ファイルに収集されます。 |

2. 一般的な方法で [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] Web アプリケーションを起動します。

## <a name="control-data-collection"></a>データ収集の制御
 ターゲット アプリケーションの実行中に、*VSPerfCmd.exe* のオプションを使用して、プロファイラーのデータ ファイルへのデータ書き込みを開始および停止することにより、データ収集を制御できます。 データ コレクションを制御することにより、アプリケーションの起動や終了など、プログラム実行の特定の部分についてのデータ コレクションを行うことができます。

#### <a name="to-start-and-stop-data-collection"></a>データ収集を開始および停止するには

- 次に示すオプションの組み合わせにより、データ収集を開始および停止します。 個別のコマンド ラインで各オプションを指定します。 データ収集のオンとオフは複数回切り替えることができます。

    |オプション|説明|
    |------------|-----------------|
    |[/globalon /globaloff](../profiling/globalon-and-globaloff.md)|すべてのプロセスのデータ収集を開始 ( **/globalon**) または停止 ( **/globaloff**) します。|
    |[/processon](../profiling/processon-and-processoff.md) **:** `PID` [/processoff](../profiling/processon-and-processoff.md) **:** `PID`|プロセス ID (`PID`) で指定されたプロセスのデータ収集を開始 ( **/processon**) または停止 ( **/processoff**) します。|
    |[/threadon](../profiling/threadon-and-threadoff.md) **:** `TID` [/threadoff](../profiling/threadon-and-threadoff.md) **:** `TID`|スレッド ID (`TID`) で指定されたスレッドのデータ収集を開始 ( **/threadon**) または停止 ( **/threadoff**) します。|

- **VSPerfCmd.exe**[/mark](../profiling/mark.md) オプションを使用して、データ ファイルにプロファイル マークを挿入することもできます。 **/mark** コマンドは、識別子、タイム スタンプ、オプションのユーザー定義文字列を追加します。 マークは、プロファイラー レポートおよびデータ ビューでデータをフィルター処理するために使用できます。

## <a name="end-the-profiling-session"></a>プロファイル セッションの終了
 プロファイル セッションを終了するには、ターゲット [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] Web アプリケーションを閉じ、インターネット インフォメーション サービス (IIS) を停止してプロファイルされたプロセスを停止し、プロファイラーをシャットダウンします。 次に IIS を再起動します。

#### <a name="to-end-a-profiling-session"></a>プロファイル セッションを終了するには

1. [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] Web アプリケーションを終了します。

2. インターネット インフォメーション サービス (IIS) をリセットし、[!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] ワーカー プロセスを閉じます。 種類:

    **IISReset /stop**

3. プロファイラーをシャットダウンします。 型:

    **VSPerfCmd** [/shutdown](../profiling/shutdown.md)

4. IIS を再起動します。 型:

    **IISReset /start**

## <a name="restore-the-application-and-computer-configuration"></a>アプリケーションとコンピューターの構成を復元する
 すべてのプロファイルを完了したら、*web.config* ファイルを置換し、プロファイル環境変数を消去し、コンピューターを再起動してサーバーと [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] アプリケーションを元の状態に復元します。

#### <a name="to-restore-the-application-and-computer-configuration"></a>アプリケーションとコンピューターの構成を復元するには

1. *web.config* ファイルを元のファイルのコピーで置き換えます。

2. (省略可能) プロファイル環境変数を削除します。 型:

     **VSPerfCmd /globaloff**

3. コンピューターを再起動します。

## <a name="see-also"></a>関連項目
- [ASP.NET Web アプリケーションのプロファイリング](../profiling/command-line-profiling-of-aspnet-web-applications.md)
- [.NET メモリのデータ ビュー](../profiling/dotnet-memory-data-views.md)
