---
title: プロファイラーのコマンド ライン:静的な ASP.NET アプリのインストルメント化、タイミング データの取得
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: b260ce68-76e6-4c3b-8062-3c00bd5cf7b8
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- aspnet
ms.openlocfilehash: 7d743dd854bd11449161c47cc896d0735849e1dd
ms.sourcegitcommit: 00b71889bd72b6a566586885bdb982cfe807cf54
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2019
ms.locfileid: "74778857"
---
# <a name="how-to-instrument-a-statically-compiled-aspnet-web-application-and-collect-detailed-timing-data-with-the-profiler-by-using-the-command-line"></a>方法: プロファイラーのコマンド ラインを使用して、静的にコンパイルされた ASP.NET Web アプリケーションをインストルメント化し、詳細なタイミング データを収集する
この記事では、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] プロファイル ツールのコマンド ライン ツールを使用して、プリコンパイルされた [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] Web コンポーネントまたは Web サイトをインストルメント化し、詳細なタイミング データを収集する方法について説明します。

> [!NOTE]
> プロファイル ツールへのパスを取得するには、[コマンド ライン ツールへのパスの指定](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md)に関する記事をご覧ください。 64 ビット コンピューター上では、64 ビット バージョンのツールと 32 ビット バージョンのツールの両方を使用できます。 プロファイラー コマンド ライン ツールを使用するには、コマンド プロンプト ウィンドウの PATH 環境変数にツールのパスを追加するか、コマンド自体にそれを追加します。
>
> プロファイリングの実行に階層の相互作用データを追加するには、コマンド ライン プロファイリング ツールによる特定の手順が必要です。 「[Visual Studio IDE を使用した階層相互作用データの収集](../profiling/adding-tier-interaction-data-from-the-command-line.md)」をご覧ください。

 インストルメンテーション メソッドを使用して [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] Web コンポーネントから詳細なタイミング データを収集するには、[VSInstr.exe](../profiling/vsinstr.md) ツールを使用して、コンポーネントのインストルメントされたバージョンを生成します。 コンポーネントをホストするコンピューターで、コンポーネントのインストルメントされていないバージョンをインストルメントされたバージョンに置き換えます。 次に、[VSPerfCLREnv.cmd](../profiling/vsperfclrenv.md) ツールを使用してグローバル プロファイリング環境変数を初期化し、ホスト コンピューターを再起動します。 次に、プロファイラーを起動します。

 インストルメントされたコンポーネントを実行すると、タイミング データがデータ ファイルに自動的に収集されます。 プロファイル セッション中にデータ収集を一時停止および再開できます。

 プロファイル セッションを終了するには、コンポーネントをホストする [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] ワーカー プロセスを終了し、プロファイラーを明示的に終了します。 ほとんどの場合、セッションの最後にプロファイル環境変数を消去することをお勧めします。

## <a name="start-to-profile"></a>プロファイルの開始

#### <a name="to-instrument-an-aspnet-web-component-and-start-profiling"></a>ASP.NET Web コンポーネントをインストルメント化してプロファイリングを開始するには

1. コマンド プロンプト ウィンドウを開きます。

2. **VSInstr** ツールを使用して、対象アプリケーションのインストルメントされたバージョンを生成します。 必要に応じて、ASP.NET ホスト コンピューター上のアプリケーション バイナリをインストルメントされたバイナリに置き換えます。

3. .NET プロファイル環境変数を初期化します。 [コマンド プロンプト] ウィンドウに次のように入力します。

    **VSPerfClrEnv /globaltraceon**

4. コンピューターを再起動します。

5. コマンド プロンプト ウィンドウを開きます。 必要に応じて、プロファイラー ツールのパスを設定します。

6. プロファイラーを起動します。 型:

    **VSPerfCmd /start:trace /output:** `OutputFile` [`Options`]

   - [/start](../profiling/start.md) **:trace** オプションによってプロファイラーが初期化されます。

   - **/start** を使用するには、[/output](../profiling/output.md) **:** `OutputFile` オプションを指定する必要があります。 `OutputFile` には、プロファイル データ (.vsp) ファイルの名前と場所を指定します。

     **/start:trace** オプションを使用する場合は、次のうちいずれのオプションでも指定できます。

   > [!NOTE]
   > **/user** オプションと **/crosssession** オプションは、通常、ASP.NET アプリケーションで必要です。

   | オプション | 説明 |
   | - | - |
   | [/user](../profiling/user-vsperfcmd.md) **:** [`Domain` **\\** ]`UserName` | ASP.NET ワーカー プロセスを所有するアカウントのドメインおよびユーザー名を指定します。 このオプションは、ログオンしているユーザーとは別のユーザーがプロセスを実行している場合に指定する必要があります。 プロセスの所有者は、Windows タスク マネージャーの **[プロセス]** タブの **[ユーザー名]** 列に表示されます。 |
   | [/crosssession](../profiling/crosssession.md) | 他のログオン セッションにおけるプロセスのプロファイリングを有効にします。 このオプションは、ASP.NET アプリケーションが別のセッションで実行されている場合に必要です。 セッション ID は、Windows タスク マネージャーの **[プロセス]** タブの [セッション ID] 列に表示されます。 **/crosssession** の省略形として、 **/CS** を指定することができます。 |
   | [/wincounter](../profiling/wincounter.md) **:** `WinCounterPath` | プロファイリング実行中に収集する Windows パフォーマンス カウンターを指定します。 |
   | [/automark](../profiling/automark.md) **:** `Interval` | **/wincounter** との組み合わせでのみ使用します。 Windows パフォーマンス カウンター コレクション イベントの間隔をミリ秒単位で指定します。 既定値は 500 ミリ秒です。 |
   | [/events](../profiling/events-vsperfcmd.md) **:** `Config` | プロファイリング実行中に収集する ETW (Event Tracing for Windows) イベントを指定します。 ETW イベントは独立した (.*etl*) ファイルに収集されます。 |
   | [/globaloff](../profiling/globalon-and-globaloff.md) | データ収集を一時停止してプロファイラーを起動するには、 **/globaloff** オプションを **/start** コマンド ラインに追加します。 プロファイリングを再開するには、 **/globalon** を使用します。 |

7. インストルメントされたコンポーネントを含む Web サイトを開きます。

## <a name="control-data-collection"></a>データ収集の制御
 対象アプリケーションの実行中に、*VSPerfCmd.exe* のオプションを使用してファイルへのデータ書き込みを開始および停止することにより、データ収集を制御できます。 データ コレクションを制御することにより、アプリケーションの起動や終了など、プログラム実行の特定の部分についてのデータ コレクションを行うことができます。

#### <a name="to-start-and-stop-data-collection"></a>データ収集を開始および停止するには

- 次に示すオプションの組み合わせにより、データ収集を開始および停止します。 個別のコマンド ラインで各オプションを指定します。 データ収集のオンとオフは複数回切り替えることができます。

    |オプション|説明|
    |------------|-----------------|
    |[/globalon /globaloff](../profiling/globalon-and-globaloff.md)|すべてのプロセスのデータ収集を開始 ( **/globalon**) または停止 ( **/globaloff**) します。|
    |[/processon](../profiling/processon-and-processoff.md) **:** `PID` [/processoff](../profiling/processon-and-processoff.md) **:** `PID`|プロセス ID (`PID`) で指定されたプロセスのデータ収集を開始 ( **/processon**) または停止 ( **/processoff**) します。|
    |[/threadon](../profiling/threadon-and-threadoff.md) **:** `TID` [/threadoff](../profiling/threadon-and-threadoff.md) **:** `TID`|スレッド ID (`TID`) で指定されたスレッドのデータ収集を開始 ( **/threadon**) または停止 ( **/threadoff**) します。|

## <a name="end-the-profiling-session"></a>プロファイル セッションの終了
 プロファイル セッションを終了するには、[!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] Web アプリケーションを終了し、インターネット インフォメーション サービス (IIS) の **IISReset** コマンド使用して [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] ワーカー プロセスを終了します。 **VSPerfCmd** [/shutdown](../profiling/shutdown.md) オプションを呼び出して、プロファイラーをオフにし、プロファイル データ ファイルを閉じます。

 **VSPerfClrEnv /globaloff** コマンドは、プロファイル環境変数を消去します。 新しい環境設定を適用するには、コンピューターを再起動する必要があります。

#### <a name="to-end-a-profiling-session"></a>プロファイル セッションを終了するには

1. [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] Web アプリケーションを終了します。

2. [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] ワーカー プロセスを終了します。 型:

    **IISReset /stop**

3. プロファイラーをシャットダウンします。 型:

    **VSPerfCmd /shutdown**

4. (省略可能) プロファイル環境変数を削除します。 型:

    **VSPerfCmd /globaloff**

5. コンピューターを再起動します。

## <a name="see-also"></a>関連項目
- [ASP.NET Web アプリケーションのプロファイリング](../profiling/command-line-profiling-of-aspnet-web-applications.md)
- [インストルメンテーション メソッドのデータ ビュー](../profiling/instrumentation-method-data-views.md)
