---
title: プロファイラーのコマンド ライン - クライアントの .NET Framework アプリを開く、メモリ データの取得
description: Visual Studio プロファイル ツールのコマンドライン ツールを使用して、.NET Framework スタンドアロン アプリを起動し、メモリ アクティビティ データを収集する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 3bc53041-91b7-4ad0-8413-f8bf2c4b3f5e
author: mikejo5000
ms.author: mikejo
manager: jmartens
monikerRange: vs-2017
ms.workload:
- dotnet
ms.openlocfilehash: acfa657552cb070fe8b98ff4dc761ab6913a6c93
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99860816"
---
# <a name="how-to-launch-a-stand-alone-net-framework-application-with-the-profiler-to-collect-memory-data-by-using-the-command-line"></a>方法: コマンド ラインを使用してプロファイラーによってスタンドアロンの .NET Framework アプリケーションを起動し、メモリ データを収集する
ここでは、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] プロファイリング ツールのコマンド ライン ツールを使用して、.NET Framework のスタンドアロン (クライアント) アプリケーションを起動し、メモリ データを収集する方法について説明します。

 プロファイル セッションには、3 つの部分があります。

- プロファイラーを使用してアプリケーションを起動する。

- プロファイル データを収集する。

- プロファイル セッションを終了する。

> [!NOTE]
> プロファイル ツールへのパスを取得するには、[コマンド ライン ツールへのパスの指定](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md)に関する記事をご覧ください。 64 ビット コンピューター上では、64 ビット バージョンのツールと 32 ビット バージョンのツールの両方を使用できます。 プロファイラー コマンド ライン ツールを使用するには、コマンド プロンプト ウィンドウの PATH 環境変数にツールのパスを追加するか、コマンド自体にそれを追加します。

## <a name="start-the-application-with-the-profiler"></a>プロファイラーによるアプリケーションの起動
 プロファイラーを使用して対象アプリケーションを起動するには、**VSPerfCmd.exe/start** オプションと **/launch** オプションを使用して、プロファイラーを初期化し、アプリケーションを起動します。 **/start** と **/launch**、およびそれぞれのオプションは、1 つのコマンド ラインで指定できます。

 **/globaloff** オプションを追加して、対象アプリケーションの起動時にデータ収集を一時停止することもできます。 次に、 **/globalon** を使用してデータの収集を開始します。

#### <a name="to-start-an-application-by-using-the-profiler"></a>プロファイラーを使用してアプリケーションを起動するには

1. コマンド プロンプト ウィンドウを開きます。

2. プロファイラーを起動します。 型:

    **VSPerfCmd /start:sample /output:** `OutputFile` [`Options`]

   - [/start](../profiling/start.md) **:sample** オプションによってプロファイラーが初期化されます。

   - **/start** を使用するには、[/output](../profiling/output.md) **:** `OutputFile` オプションを指定する必要があります。 `OutputFile` には、プロファイル データ (.vsp) ファイルの名前と場所を指定します。

     **/start:sample** オプションを使用する場合は、次のうちいずれかのオプションを指定できます。

   | オプション | 説明 |
   | - | - |
   | [/wincounter](../profiling/wincounter.md) **:** `WinCounterPath` | プロファイリング実行中に収集する Windows パフォーマンス カウンターを指定します。 |
   | [/automark](../profiling/automark.md) **:** `Interval` | **/wincounter** との組み合わせでのみ使用します。 Windows パフォーマンス カウンター コレクション イベントの間隔をミリ秒単位で指定します。 既定値は 500 ミリ秒です。 |

3. 対象アプリケーションを起動します。 型:

    **VSPerfCmd**  [/launch](../profiling/launch.md) **:** `appName` **/gc:** {**allocation**&#124;**lifetime**}[`Options`]

   - [/gc](../profiling/gc-vsperfcmd.md) **:** `Keyword` オプションは、.NET Framework メモリ データを収集するために必要です。 keyword パラメーターは、メモリの割り当てデータを収集するのか、メモリの割り当てデータとオブジェクトの有効期間データの両方を収集するのかを指定します。

     |キーワード|説明|
     |-------------|-----------------|
     |**allocation**|メモリの割り当てデータのみを収集します。|
     |**lifetime**|.NET メモリの割り当てデータとオブジェクトの有効期間データの両方を収集します。|

     **/launch** オプションを使用する場合は、次のうちどのオプションでも指定できます。

   |オプション|説明|
   |------------|-----------------|
   |[/args](../profiling/args.md) **:** `Arguments`|対象アプリケーションへ渡されるコマンド ライン引数を格納する文字列を指定します。|
   |[/console](../profiling/console.md)|対象のコマンド ライン アプリケーションを別のウィンドウで起動でします。|
   |[/events](../profiling/events-vsperfcmd.md) **:** `Config`|プロファイリング実行中に収集する ETW (Event Tracing for Windows) イベントを指定します。 ETW イベントは独立した (.etl) ファイルに収集されます。|
   |[/targetclr](../profiling/targetclr.md) **:** `Version`|アプリケーションに複数バージョンのランタイムが読み込まれている場合に、プロファイリングを行う共通言語ランタイム (CLR: Common Language Runtime) のバージョンを指定します。|

## <a name="control-data-collection"></a>データ収集の制御
 対象アプリケーションの実行中に、*VSPerfCmd.exe* のオプションを使用してファイルへのデータ書き込みを開始および停止することにより、データ収集を制御できます。 データ コレクションを制御することにより、アプリケーションの起動や終了など、プログラム実行の特定の部分についてのデータ コレクションを行うことができます。

#### <a name="to-start-and-stop-data-collection"></a>データ収集を開始および停止するには

- 次に示すオプションの組み合わせにより、データ収集を開始および停止します。 個別のコマンド ラインで各オプションを指定します。 データ収集のオンとオフは複数回切り替えることができます。

    |オプション|説明|
    |------------|-----------------|
    |[/globalon /globaloff](../profiling/globalon-and-globaloff.md)|すべてのプロセスのデータ収集を開始 ( **/globalon**) または停止 ( **/globaloff**) します。|
    |[/processon](../profiling/processon-and-processoff.md) **:** `PID` [processoff](../profiling/processon-and-processoff.md) **:** `PID`|プロセス ID (`PID`) で指定されたプロセスのデータ収集を開始 ( **/processon**) または停止 ( **/processoff**) します。|
    |[/attach](../profiling/attach.md) **:** `PID` [/detach](../profiling/detach.md)|**/attach** は、`PID` (プロセス ID) で指定したプロセスのデータ収集を開始します。 **/detach** は、すべてのプロセスのデータ収集を停止します。|

- **VSPerfCmd.exe**[/mark](../profiling/mark.md) オプションを使用して、データ ファイルにプロファイル マークを挿入することもできます。 **/mark** コマンドは、識別子、タイム スタンプ、およびオプションのユーザー定義文字列を追加します。 マークは、データをフィルター処理するために使用できます。

## <a name="end-the-profiling-session"></a>プロファイル セッションの終了
 プロファイル セッションを終了するには、プロファイラーをプロファイリング対象のすべてのプロセスからデタッチし、プロファイラーを明示的に終了する必要があります。 サンプリング メソッドを使用してプロファイリングを実行したアプリケーションからプロファイラーをデタッチするには、アプリケーションを終了するか、**VSPerfCmd /detach** オプションを呼び出します。 次に、**VSPerfCmd /shutdown** オプションを呼び出して、プロファイラーをオフにし、プロファイル データ ファイルを閉じます。 **VSPerfClrEnv /off** コマンドは、プロファイル環境変数を消去します。

#### <a name="to-end-a-profiling-session"></a>プロファイル セッションを終了するには

1. 対象アプリケーションからプロファイラーをデタッチするには、次のいずれかの手順を実行します。

    - 対象アプリケーションを終了します。

         \- または -

    - **VSPerfCmd /detach** と入力します

2. プロファイラーをシャットダウンします。 型:

     **VSPerfCmd**  [/shutdown](../profiling/shutdown.md)

## <a name="see-also"></a>関連項目
- [スタンドアロン アプリケーションのプロファイリング](../profiling/command-line-profiling-of-stand-alone-applications.md)
- [.NET メモリのデータ ビュー](../profiling/dotnet-memory-data-views.md)
