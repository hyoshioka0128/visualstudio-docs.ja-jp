---
title: デバッガーを使用して、または使用せずにプロファイリング ツールを実行する | Microsoft Docs
ms.date: 5/26/2020
ms.topic: conceptual
ms.assetid: 3fcdccad-c1bd-4c67-bcec-bf33a8fb5d63
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 45632967c39348e8dc78dc3e2fb95227dcd86d7d
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85285910"
---
# <a name="run-profiling-tools-with-or-without-the-debugger"></a>デバッガーを使用して、または使用せずにプロファイリング ツールを実行する

Visual Studio には、パフォーマンス測定とプロファイルのための選り抜きのツールが備わっています。 CPU 使用率やメモリ使用量など、一部のツールはデバッガーと使用して実行することも、使用せずに実行することもできます。また、リリース ビルド構成かデバッグ ビルド構成で実行できます。 アプリケーション タイムラインのようなパフォーマンス プロファイラー ツールは、デバッグ ビルドまたはリリース ビルドで実行できます。 診断ツール ウィンドウや [イベント] タブなど、デバッガー統合ツールはデバッギング セッション中のみ実行されます。

>[!NOTE]
>デバッガーなしのパフォーマンス ツールは Windows 7 以降で使用できます。 Windows 8 以降の場合、デバッガー統合プロファイリング ツールを実行する必要があります。

デバッガーなしのパフォーマンス プロファイラーとデバッガーが統合されている診断ツールでは、情報や操作性が異なります。 デバッガー統合ツールの場合、ブレークポイントと変数値が表示されます。 デバッガーなしツールの場合、エンドユーザー体験に近い結果が得られます。

どのツールと結果を使用するか決めるとき、以下を考慮してください。

- ファイル I/O やネットワーク応答性の問題など、外部パフォーマンス問題は、デバッガー ツールとデバッガーなしツールでは違いがそれほど見えません。
- CPU 負荷の高い呼び出しによって引き起こされる問題については、リリース ビルドとデバッグ ビルドでパフォーマンスが相当違います。 リリース ビルドで問題が存在するかどうかを確認してください。
- デバッグ ビルド中にのみ問題が発生する場合、デバッガーなしツールはおそらく実行する必要がありません。 リリース ビルドの問題の場合、デバッガー ツールがさらなる調査に役立つかどうかを判断します。
- リリース ビルドでは、関数呼び出しと定数のインライン化、不使用のコード パスの除去、変数の保存など、デバッガーでは使用できない方法で最適化が提供されます。 デバッグ ビルドにはそのような最適化がないため、デバッガー統合ツールのパフォーマンス数値は正確性で劣ります。
- デバッガー自体では、例外のインターセプトやモジュール ロード イベントなど、必要なデバッガー操作を行うため、パフォーマンス時間が変わります。
- パフォーマンス プロファイラー ツールのリリース ビルド パフォーマンスの数値が最も厳密かつ正確です。 デバッガー統合ツールの結果は、他のデバッグ関連測定値と比較するときに最も役立ちます。

## <a name="collect-profiling-data-while-debugging"></a><a name="BKMK_Quick_start__Collect_diagnostic_data"></a> デバッグ中にプロファイリング データを収集する

**[デバッグ]**  >  **[デバッグ開始]** の順に選択するか、**F5** キーを押して Visual Studio でデバッグを開始すると、既定では **[診断ツール]** ウィンドウが表示されます。 手動で開くには、 **[デバッグ]** 、 **[Windows]** 、 **[診断ツールの表示]** の順に選択します。 **[診断ツール]** ウィンドウには、イベント、プロセス メモリ、CPU 使用率に関する情報が表示されます。

![[診断ツール] ウィンドウのスクリーンショット](../profiling/media/diagnostictoolswindow.png "[診断ツール] ウィンドウ")

- **[メモリ使用量]** 、 **[UI 分析]** 、 **[CPU 使用率]** を表示するかどうかを選択するには、ツール バーの **[設定]** アイコンを使用します。

- **診断ツールのプロパティ ページ**に表示されるオプションを増やすには、 **[設定]** ドロップダウン リストで **[設定]** を選択します。

- Visual Studio Enterprise を実行している場合は、 **[ツール]**  >  **[オプション]**  >  **[IntelliTrace]** に移動して IntelliTrace を有効または無効にすることができます。

診断セッションは、デバッグを停止すると終了します。

### <a name="the-events-tab"></a>[イベント] タブ

デバッグ セッション中、[診断ツール] ウィンドウの [イベント] タブに、発生した診断イベントが一覧表示されます。 *Breakpoint* や *File* などのカテゴリ プレフィックスを使用すると、カテゴリの一覧を簡単にスキャンしたり、不要なカテゴリをスキップしたりできます。

**[フィルター]** ドロップダウン リストを使用して、特定のイベント カテゴリを選択または選択解除して表示または非表示にするイベントをフィルター処理します。

![診断イベント フィルターのスクリーンショット](../profiling/media/diagnosticeventfilter.png "診断イベント フィルター")

イベントの一覧で特定の文字列を見つけるには、検索ボックスを使用します。 4 つのイベントに一致した文字列 *name* の検索結果を次に示します。

![診断イベント検索のスクリーンショット](../profiling/media/diagnosticseventsearch.png "診断イベント検索")

詳細については、次を参照してください。[検索とフィルター処理、診断ツール ウィンドウの [イベント] タブ](https://devblogs.microsoft.com/devops/searching-and-filtering-the-events-tab-of-the-diagnostic-tools-window/)します。

## <a name="collect-profiling-data-without-debugging"></a>デバッグなしでプロファイリング データを収集する

デバッグなしでパフォーマンス データを収集するには、パフォーマンス プロファイラー ツールを実行できます。

1. Visual Studio プロジェクトでプロジェクトを開き、ソリューション構成を  **[リリース]** に設定し、配置ターゲットとして  **[ローカル Windows デバッガー]**  (または  **[ローカル コンピューター]** ) を選択します。

1. **[デバッグ]**  >  **[パフォーマンス プロファイラー]** の順に選択するか、**Alt**+**F2** を押します。

1. 診断ツールの起動ページで、実行するツールを 1 つ以上選択します。 プロジェクトの種類、オペレーティング システム、およびプログラミング言語に適用されるツールのみが表示されます。 **[すべてのツールの表示]** を選択すると、この診断セッションで無効になっているツールも表示されます。

   ![診断ツールのスクリーンショット](../profiling/media/diaghubsummarypage.png "DIAG_SelectTool")

1. 診断セッションを開始するには、 **[開始]** を選択します。

   セッションの実行中、一部のツールには、診断ツール ページにリアルタイム データのグラフと、データ収集を一時停止および再開するためのコントロールが表示されます。

    ![[パフォーマンスと診断] ハブでのデータ収集のスクリーンショット](../profiling/media/diaghubcollectdata.png "ハブのデータの収集")

1. 診断セッションを終了するには、 **[コレクションの停止]** を選択します。

   分析されたデータは、 **[レポート]** ページに表示されます。

レポートを保存し、診断ツールの起動ページの **[最近開いたセッション]** 一覧から開くことができます。

![診断ツールの [最近開いたセッション] リストのスクリーンショット](../profiling/media/diaghubopenexistingdiagsession.png "PDHUB_OpenExistingDiagSession")

## <a name="collect-profiling-data-from-the-command-line"></a>コマンド ラインからプロファイル データを収集する

コマンド ラインからパフォーマンス データを測定するには、Visual Studio またはリモート ツールに含まれている VSDiagnostics.exe を使用できます。 これは、Visual Studio がインストールされていないシステムでパフォーマンス トレースをキャプチャする場合や、パフォーマンス トレースのコレクションのスクリプトを作成する場合に便利です。 VSDiagnostics.exe を使用すると、ツールが停止するまでプロファイル データをキャプチャして保存する診断セッションが開始されます。 その時点で、そのデータは .diagsession ファイルにエクスポートされます。このファイルは、Visual Studio で開いて結果を分析できます。

### <a name="launch-an-application"></a>アプリケーションを起動する

1. コマンド プロンプトを開き、VSDiagnostics.exe のあるディレクトリに移動します。

   ```
   <Visual Studio Install Folder>\Team Tools\DiagnosticsHub\Collector\
   ```

2. 次のコマンドで VSDiagnostics.exe を起動します。

   ```
   VSDiagnostics.exe start <id> /launch:<appToLaunch> /loadConfig:<configFile>
   ```

   次の引数を含める必要があります。

   - \<id\>:収集セッションを識別します。 ID は常に 1 - 255 の数字です。
   - \<appToLaunch\>:起動およびプロファイルする実行可能ファイル。
   - \<configFile\>:起動する収集エージェントの構成ファイル。

3. 収集を停止して結果を表示するには、この記事で後述する「収集を停止する」セクションの手順を実行します。

### <a name="attach-to-an-existing-application"></a>既存のアプリケーションにアタッチする

1. メモ帳などのアプリケーションを開き、**タスク マネージャー**を開いて、そのプロセス ID (PID) を取得します。 タスク マネージャーの  **[詳細]**   タブで PID を見つけます。
2. コマンド プロンプトを開き、実行可能な収集エージェントがあるディレクトリに移動します。 通常は、以下のとおりです。

   ```
   <Visual Studio installation folder>\2019\Preview\Team Tools\DiagnosticsHub\Collector\
   ```

3. 次のコマンドを入力して、VSDiagnostics.exe ファイルを起動します。

   ```
   VSDiagnostics.exe start <id> /attach:<pid> /loadConfig:<configFile>
   ```

   次の引数を含める必要があります。

   - \<id\>:収集セッションを識別します。 ID は常に 1 - 255 の数字です。
   - \<pid\>:プロファイルするプロセスの PID。この場合は、手順 1 で見つけた PID です。
   - \<configFile\>:起動する収集エージェントの構成ファイル。 詳細については、 [エージェントの構成ファイル](../profiling/profile-apps-from-command-line.md)に関するセクションを参照してください。

4. 収集を停止して結果を表示するには、次のセクションの手順を実行します。

### <a name="stop-collection"></a>収集を停止する

1. 次のコマンドを入力して、収集セッションを停止し、ファイルに出力を送信します。

   ```
   VSDiagnostics.exe stop <id> /output:<path to file>
   ```

2. 前のコマンドから出力されたファイルに移動し、Visual Studio でそれを開いて、収集された情報を調べます。

## <a name="agent-configuration-files"></a>エージェントの構成ファイル

収集エージェントは、測定対象が何かに応じて、さまざまな種類のデータを収集する交換可能なコンポーネントです。
便宜上、その情報をエージェント構成ファイルに保管することができます。 構成ファイルは、少なくとも .dll ファイルの名前とその COM CLSID を含む .json ファイルです。 以下は、次のフォルダー内にある構成ファイルの例です。

```
<Visual Studio installation folder>\Team Tools\DiagnosticsHub\Collector\AgentConfigs\
```

エージェントの構成ファイルをダウンロードして表示するには、以下のリンクを参照してください。

- https://aka.ms/vs/diaghub/agentconfig/cpubase
- https://aka.ms/vs/diaghub/agentconfig/cpuhigh
- https://aka.ms/vs/diaghub/agentconfig/cpulow
- https://aka.ms/vs/diaghub/agentconfig/database
- https://aka.ms/vs/diaghub/agentconfig/dotnetasyncbase
- https://aka.ms/vs/diaghub/agentconfig/dotnetallocbase
- https://aka.ms/vs/diaghub/agentconfig/dotnetalloclow

 [CPU 使用率](../profiling/cpu-usage.md)プロファイル ツールについて収集されたデータに対応する CpuUsage 構成 (Base/High/Low)。
DotNetObjectAlloc 構成 (Base/Low)。 [.NET オブジェクト割り当てツール](../profiling/dotnet-alloc-tool.md)について収集されたデータに対応します。

Base/Low/High 構成はサンプリング レートを表します。 たとえば、Low は 100 サンプル/秒、High は 4,000 サンプル/秒です。
VSDiagnostics.exe ツールを収集エージェントで使用するには、適切なエージェントの DLL と COM CLSID の両方が必要です。 エージェントには、その他の構成オプションがある場合もあります。 構成ファイルなしでエージェントを使用する場合は、次のコマンドでこの形式を使用してください。

```
VSDiagnostics.exe start <id> /attach:<pid> /loadAgent:<agentCLSID>;<agentName>[;<config>]
```
