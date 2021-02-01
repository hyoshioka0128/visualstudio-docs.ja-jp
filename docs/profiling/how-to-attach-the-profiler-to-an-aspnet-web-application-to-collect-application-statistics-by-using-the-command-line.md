---
title: ASP.NET にプロファイラーをアタッチし、アプリの統計情報を取得する
description: Visual Studio プロファイル ツールのコマンドライン ツールを使用して、プロファイラーを ASP.NET Web アプリにアタッチし、サンプリング メソッドを使用してパフォーマンス統計情報を取得します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 3725ddbe-ce91-4469-991e-8c5ed048c618
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- aspnet
ms.openlocfilehash: f79591c58865631b20aecb3554e9502a22f6c7b9
ms.sourcegitcommit: 589d96700208bf22c8da9e26a1d2041fbf39b8f9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98801631"
---
# <a name="how-to-attach-the-profiler-to-an-aspnet-web-application-to-collect-application-statistics-by-using-the-command-line"></a>方法: コマンド ラインを使用してプロファイラーを ASP.NET Web アプリケーションにアタッチし、アプリケーションの統計情報を収集する
この記事では、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] プロファイル ツールのコマンドライン ツールを使用してプロファイラーを ASP.NET Web アプリケーションにアタッチし、サンプリング メソッドによってパフォーマンスに関する統計情報を収集する方法について説明します。

> [!NOTE]
> Windows 8 および Windows Server 2012 の強化されたセキュリティ機能によって、Visual Studio プロファイラーがこれらのプラットフォームでデータを収集する方法に大幅な変更が必要になりました。 UWP アプリにも新しい収集手法が必要です。 「[Windows 8 および Windows Server 2012 アプリケーションのパフォーマンス ツール](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)」を参照してください。
>
> プロファイリングの実行に階層の相互作用データを追加するには、コマンド ライン プロファイリング ツールによる特定の手順が必要です。 [階層相互作用データを収集する](../profiling/adding-tier-interaction-data-from-the-command-line.md)方法に関するページを参照してください。
>
> プロファイル ツールへのパスを取得するには、[コマンド ライン ツールへのパスの指定](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md)に関する記事をご覧ください。 64 ビット コンピューター上では、64 ビット バージョンのツールと 32 ビット バージョンのツールの両方を使用できます。 プロファイラー コマンド ライン ツールを使用するには、コマンド プロンプト ウィンドウの PATH 環境変数にツールのパスを追加するか、コマンド自体にそれを追加します。

 ASP.NET Web アプリケーションからパフォーマンス データを収集するには、該当する環境変数を初期化し、ASP.NET Web アプリケーションをホストするコンピューターを再起動してプロファイル用の Web サーバーを構成する必要があります。

 次に、Web サイトをホストする ASP.NET ワーカー プロセスにプロファイラーをアタッチします。 プロファイラーをアプリケーションにアタッチしているときにデータ コレクションを一時停止し、完了後に再開できます。

 プロファイル セッションを終了するには、プロファイリング対象アプリケーションからプロファイラーをデタッチし、プロファイラーを明示的に終了する必要があります。 ほとんどの場合、セッションの最後にプロファイル環境変数を消去することをお勧めします。

## <a name="start-the-profiler-and-attach-to-an-aspnet-web-application"></a>プロファイラーの起動と ASP.NET Web アプリケーションへのアタッチ

#### <a name="to-attach-the-profiler-to-an-aspnet-web-application"></a>プロファイラーを ASP.NET Web アプリケーションにアタッチするには

1. コマンド プロンプト ウィンドウを開きます。

2. プロファイル環境変数を初期化します。 型:

    **VSPerfClrEnv /globalsampleon** **[/samplelineoff]**

   - **/globalsampleon** はサンプリングを有効にします。

   - **/samplelineoff** は特定のソース コード行への収集データの割り当てを無効にします。 このオプションを指定すると、データは関数に対してのみ割り当てられます。

3. コンピューターを再起動します。

4. プロファイラーを起動します。 **VSPerfCmd** [/start](../profiling/start.md) **:sample** [/output](../profiling/output.md) **:** `OutputFile`[`Options`] と入力します

   - **/start:sample** オプションによってプロファイラーが初期化されます。

   - **/start** を使用するには、 **/output:** `OutputFile` オプションを指定する必要があります。 `OutputFile` には、プロファイル データ (.vsp) ファイルの名前と場所を指定します。

     **/start:sample** オプションを使用する場合は、次のうちいずれかのオプションを指定できます。

   > [!NOTE]
   > **/user** オプションと **/crosssession** オプションは、通常、ASP.NET アプリケーションで必要です。

   | オプション | 説明 |
   | - | - |
   | [/user](../profiling/user-vsperfcmd.md) **:** [`Domain` **\\** ]`UserName` | ASP.NET ワーカー プロセスを所有するアカウントのドメインおよびユーザー名を指定します。 このオプションは、ログオンしているユーザーとは別のユーザーがプロセスを実行している場合に指定する必要があります。 プロセスの所有者は、Windows タスク マネージャーの **[プロセス]** タブの **[ユーザー名]** 列に表示されます。 |
   | [/crosssession](../profiling/crosssession.md) | 他のログオン セッションにおけるプロセスのプロファイリングを有効にします。 このオプションは、ASP.NET アプリケーションが別のセッションで実行されている場合に必要です。 セッション ID は、Windows タスク マネージャーの [プロセス] タブの [セッション ID] 列に表示されます。 **/crosssession** の省略形として、 **/CS** を指定することができます。 |
   | [/wincounter](../profiling/wincounter.md) **:** `WinCounterPath` | プロファイリング実行中に収集する Windows パフォーマンス カウンターを指定します。 |
   | [/automark](../profiling/automark.md) **:** `Interval` | **/wincounter** との組み合わせでのみ使用します。 Windows パフォーマンス カウンター コレクション イベントの間隔をミリ秒単位で指定します。 既定値は 500 ミリ秒です。 |
   | [/events](../profiling/events-vsperfcmd.md) **:** `Config` | プロファイリング実行中に収集する ETW (Event Tracing for Windows) イベントを指定します。 ETW イベントは独立した (.etl) ファイルに収集されます。 |

5. 一般的な方法で ASP.NET Web アプリケーションを起動します。

6. プロファイラーを ASP.NET ワーカー プロセスにアタッチします。 **VSPerfCmd** [/attach](../profiling/attach.md) **:** {`PID`&#124;`ProcName`} [`Sample Event`] [[/targetclr](../profiling/targetclr.md) **:** `Version`] と入力します

   - `PID` は ASP.NET ワーカー プロセスのプロセス ID を指定します。`ProcName` はワーカー プロセスの名前を指定します。 Windows タスク マネージャーで、実行中のすべてのプロセスのプロセス ID と名前を参照できます。

   - 既定では、パフォーマンス データはプロセッサのクロック サイクル数 10,000,000 (停止なし) ごとにサンプリングされます。 このため、1 GHz のプロセッサにおける 1 秒あたりのサンプリング回数は約 100 回です。 次の **VSPerfCmd** オプションのいずれかを指定して、クロック サイクルの間隔の変更、または別のサンプリング イベントの指定ができます。

   |サンプリング イベント|説明|
   |------------------|-----------------|
   |[/timer](../profiling/timer.md) **:** `Interval`|サンプリングの間隔を、`Interval` で指定された停止なしのクロック サイクル数に変更します。|
   |[/pf](../profiling/pf.md)[ **:** `Interval`]|サンプリング イベントをページ フォールトに変更します。 `Interval` を指定した場合は、サンプル間のページ フォールト数が設定されます。 既定値は 10 です。|
   |[/sys](../profiling/sys-vsperfcmd.md)[`:``Interval`]|サンプリング イベントを、プロセスからオペレーティング システムのカーネルへのシステム コール (syscall) に変更します。 `Interval` を指定した場合は、サンプル間の呼び出し回数が設定されます。 既定値は 10 です。|
   |[/counter](../profiling/counter.md) **:** `Config`|サンプリング イベントと間隔を、プロセッサのパフォーマンス カウンターと、`Config` で指定した間隔に、それぞれ変更します。|
   |[/targetclr](../profiling/targetclr.md) **:** `Version`|アプリケーションに複数バージョンのランタイムが読み込まれている場合に、プロファイリングを行う共通言語ランタイム (CLR: Common Language Runtime) のバージョンを指定します。|

   - **targetclr:** `Version` には、アプリケーションに複数バージョンのランタイムが読み込まれている場合に、プロファイリングを行う CLR のバージョンを指定します。 任意。

## <a name="control-data-collection"></a>データ収集の制御
 アプリケーションの実行中は、*VSPerfCmd.exe* のオプションを使用してファイルへのデータ書き込みを開始または停止することにより、データ収集を制御できます。 データ コレクションを制御することにより、アプリケーションの起動や終了など、プログラム実行の特定の部分についてのデータ コレクションを行うことができます。

#### <a name="to-start-and-stop-data-collection"></a>データ収集を開始および停止するには

- 次に示す **VSPerfCmd** のオプションの組み合わせにより、データ収集を開始および停止します。 個別のコマンド ラインで各オプションを指定します。 データ収集のオンとオフは複数回切り替えることができます。

    |オプション|説明|
    |------------|-----------------|
    |[/globalon /globaloff](../profiling/globalon-and-globaloff.md)|すべてのプロセスのデータ収集を開始 ( **/globalon**) または停止 ( **/globaloff**) します。|
    |[/processon](../profiling/processon-and-processoff.md) **:** `PID` **/processoff:** `PID`|`PID` で指定されたプロセスのデータ収集を開始 ( **/processon**) または停止 ( **/processoff**) します。|
    |[/attach](../profiling/attach.md) **:** {`PID`&#124;`ProcName`} [/detach](../profiling/detach.md)[ **:** {`PID`&#124;`ProcName`}]|**/attach** は、`PID` またはプロセス名 (ProcName) で指定したプロセスのデータ収集を開始します。 **/detach** は、指定されたプロセスのデータ収集を停止します。特定のプロセスが指定されていない場合は、すべてのプロセスのデータ収集を停止します。|

## <a name="end-the-profiling-session"></a>プロファイル セッションの終了
 プロファイル セッションを終了するには、[!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] Web アプリケーションを終了し、インターネット インフォメーション サービス (IIS) の **IISReset** コマンド使用して [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] ワーカー プロセスを終了します。 **VSPerfCmd** [/shutdown](../profiling/shutdown.md) オプションを呼び出して、プロファイラーをオフにし、プロファイル データ ファイルを閉じます。

 **VSPerfClrEnv /globaloff** コマンドは、プロファイル環境変数を消去します。 新しい環境設定を適用するには、コンピューターを再起動する必要があります。

 **VSPerfClrEnv /globaloff** コマンドによってプロファイル環境変数は消去されますが、コンピューターを再起動するまでシステム構成はリセットされません。

#### <a name="to-end-a-profiling-session"></a>プロファイル セッションを終了するには

1. 対象アプリケーションからプロファイラーをデタッチするには、次のいずれかの操作を行います。

   - **VSPerfCmd /detach** と入力します

      \- または -

   - [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] ワーカー プロセスを終了します。

2. プロファイラーをシャットダウンします。 **VSPerfCmd** [/shutdown](../profiling/shutdown.md) と入力します

3. (省略可能) プロファイル環境変数を削除します。 型:

    **VSPerfCmd /globaloff**

4. コンピューターを再起動します。

## <a name="see-also"></a>関連項目
- [ASP.NET Web アプリケーションのプロファイリング](../profiling/command-line-profiling-of-aspnet-web-applications.md)
- [サンプリング メソッドのデータ ビュー](../profiling/profiler-sampling-method-data-views.md)
