---
title: デバッガーを使用して、または使用せずにプロファイリング ツールを実行する | Microsoft Docs
ms.date: 04/02/2020
ms.topic: conceptual
ms.assetid: 3fcdccad-c1bd-4c67-bcec-bf33a8fb5d63
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: cf544b3bec9b492f1d1669549ba5501a52f7d5f2
ms.sourcegitcommit: 9c1cecaff4d9955276eee7865b78d47679dd1e2a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/03/2020
ms.locfileid: "80638808"
---
# <a name="run-profiling-tools-with-or-without-the-debugger"></a>デバッガーを使用して、または使用せずにプロファイリング ツールを実行する

Visual Studio には、パフォーマンス測定とプロファイルのための選り抜きのツールが備わっています。 **CPU 使用率**や**メモリ使用量**など、一部のツールはデバッガーと使用して実行することも、使用せずに実行することもできます。また、リリース ビルド構成かデバッグ ビルド構成で実行できます。 **アプリケーション タイムライン**のような**パフォーマンス プロファイラー** ツールは、デバッグ ビルドまたはリリース ビルドで実行できます。 **診断ツール** ウィンドウや **[イベント]** タブなど、デバッガー統合ツールはデバッギング セッション中のみ実行されます。

>[!NOTE]
>デバッガーなしのパフォーマンス ツールは Windows 7 以降で使用できます。 Windows 8 以降の場合、デバッガー統合プロファイリング ツールを実行する必要があります。

デバッガーなしの**パフォーマンス プロファイラー**とデバッガーが統合されている**診断ツール**では、情報や操作性が異なります。 デバッガー統合ツールの場合、ブレークポイントと変数値が表示されます。 デバッガーなしツールの場合、エンドユーザー体験に近い結果が得られます。

どのツールと結果を使用するか決めるとき、次の点を考慮してください。

- ファイル I/O やネットワーク応答性の問題など、外部パフォーマンス問題は、デバッガー ツールとデバッガーなしツールでは違いがそれほど見えません。
- CPU 負荷の高い呼び出しによって引き起こされる問題については、リリース ビルドとデバッグ ビルドでパフォーマンスが相当違います。 リリース ビルドで問題が存在するかどうかを確認してください。
- デバッグ ビルド中にのみ問題が発生する場合、デバッガーなしツールはおそらく実行する必要がありません。 リリース ビルドの問題の場合、デバッガー ツールがさらなる調査に役立つかどうかを判断します。
- リリース ビルドでは、関数呼び出しと定数のインライン化、不使用のコード パスの除去、変数の保存など、デバッガーでは使用できない方法で最適化が提供されます。 デバッグ ビルドにはそのような最適化がないため、デバッガー統合ツールのパフォーマンス数値は正確性で劣ります。
- デバッガー自体では、例外のインターセプトやモジュール ロード イベントなど、必要なデバッガー操作を行うため、パフォーマンス時間が変わります。
- **パフォーマンス プロファイラー** ツールのリリース ビルド パフォーマンスの数値が最も厳密かつ正確です。 デバッガー統合ツールの結果は、他のデバッグ関連測定値と比較するときに最も役立ちます。

CPU 使用率を確認するには、コマンドライン ツールを使用してリモート マシンでツールを実行します。

## <a name="collect-profiling-data-while-debugging"></a><a name="BKMK_Quick_start__Collect_diagnostic_data"></a> デバッグ中にプロファイリング データを収集する

**[デバッグ]** 、 **[デバッグ開始]** の順に選択するか、**F5** キーを押して Visual Studio でデバッグを開始すると、既定では **[診断ツール]** ウィンドウが表示されます。 手動で開くには、 **[デバッグ]** 、 **[Windows]** 、 **[診断ツールの表示]** の順に選択します。 **[診断ツール]** ウィンドウには、イベント、プロセス メモリ、CPU 使用率に関する情報が表示されます。

![診断ツール](../profiling/media/diagnostictools-update1.png "診断ツール")

- **[メモリ使用量]** または **[CPU 使用率]** を表示するかどうかを選択するには、ツール バーの **[設定]** アイコンを使用します。

- **診断ツールのプロパティ ページ**に表示されるオプションを増やすには、 **[設定]** ドロップダウンで **[設定]** を選択します。

- Visual Studio Enterprise を実行している場合は、Visual Studio の **[ツール]** 、 **[オプション]** 、 **[IntelliTrace]** で IntelliTrace を有効または無効にすることができます。

診断セッションは、デバッグを停止すると終了します。

### <a name="the-events-tab"></a>[イベント] タブ

デバッグ セッション中、 **[診断ツール]** ウィンドウの **[イベント]** タブに、発生した診断イベントが一覧表示されます。 カテゴリ プレフィックスの**ブレークポイント**や**ファイル**などで、カテゴリの一覧を簡単にスキャンしたり、不要なカテゴリをスキップしたりできます。

**[フィルター]** ドロップダウンを使用して、特定のイベント カテゴリを選択または選択解除して表示または非表示にするイベントをフィルター処理します。

![診断イベント フィルター](../profiling/media/diagnosticeventfilter.png "診断イベント フィルター")

イベントの一覧で特定の文字列を見つけるには、検索ボックスを使用します。 下は文字列 "name" の検索結果です。4 つのイベントに一致しました。

![診断イベント検索](../profiling/media/diagnosticseventsearch.png "診断イベント検索")

詳細については、次を参照してください。[検索とフィルター処理、診断ツール ウィンドウの [イベント] タブ](https://devblogs.microsoft.com/devops/searching-and-filtering-the-events-tab-of-the-diagnostic-tools-window/)します。

## <a name="collect-profiling-data-without-debugging"></a>デバッグなしでプロファイリング データを収集する

デバッグなしでパフォーマンス データを収集するには、**パフォーマンス プロファイラー** ツールを実行できます。 一部のプロファイリング ツールを実行するには管理者権限が必要です。 管理者として Visual Studio を開くこともできますし、診断セッションを開始するときに管理者としてツールを実行することもできます。

1. Visual Studio プロジェクトでプロジェクトを開き、ソリューション構成を **[リリース]** に設定し、配置ターゲットとして **[ローカル Windows デバッガー]** (または **[ローカル コンピューター]** ) を選択します。

1. **[デバッグ]**  >  **[パフォーマンス プロファイラー]** の順に選択するか、**Alt**+**F2** を押します。

1. 診断の起動ページで、実行するツールを 1 つ以上選択します。 プロジェクトの種類、オペレーティング システム、およびプログラミング言語に適用されるツールのみが表示されます。 **[すべてのツールの表示]** を選択すると、この診断セッションで無効になっているツールも表示されます。 次に、選択したツールが C# UWP アプリを検索する方法を示します。

   ![診断ツールの選択](../profiling/media/diag_selecttool.png "DIAG_SelectTool")

1. 診断セッションを開始するには、 **[開始]** を選択します。

   セッションを実行している間に、ツールによっては診断ツール ページにリアルタイム データのグラフが表示されます。

    ![[パフォーマンスと診断のハブ] でデータを収集](../profiling/media/pdhub_collectdata.png "ハブのデータの収集")

1. 診断セッションを終了するには、 **[コレクションの停止]** を選択します。

   分析されたデータは **[レポート]** ページに表示されます。

レポートを保存し、診断ツールの起動ページの **[最近開いたセッション]** 一覧から開くことができます。

![保存済みの診断セッション ファイルを開く](../profiling/media/pdhub_openexistingdiagsession.png "PDHUB_OpenExistingDiagSession")

### <a name="the-profiling-report"></a>プロファイリング レポート
 ![診断ツール レポート](../profiling/media/diag_report.png "DIAG_Report")

|||
|-|-|
|![ステップ 1](../profiling/media/procguid_1.png "ProcGuid_1")|タイムラインは、プロファイル セッションの長さ、アプリケーションのアクティブ化ライフサイクル イベント、ユーザー マークを示します。|
|![ステップ 2](../profiling/media/procguid_2.png "ProcGuid_2")|青いバーをドラッグしてタイムラインの領域を選択することにより、レポートをタイムラインの一部だけに制限できます。|
|![ステップ 3](../profiling/media/procguid_3.png "ProcGuid_3")|各診断ツールにはマスター グラフが 1 つ以上表示されます。 診断セッション ツールの複数のツールがある場合、マスター グラフが全部表示されます。|
|![ステップ 4](../profiling/media/procguid_4.png "ProcGuid_4")|各ツールの個々のグラフを折りたたんだり、展開したりできます。|
|![手順 5](../profiling/media/procguid_6.png "ProcGuid_6")|データにツールが複数含まれるとき、タブの下でツールの詳細が収集されます。|
|![手順 6](../profiling/media/procguid_6a.png "ProcGuid_6a")|レポートの下半分には、各ツールの詳細が 1 つ以上表示されます。 タイムラインのリージョンを選択することで表示を絞り込むことができます。|

## <a name="run-diagnostic-sessions-on-installed-or-running-apps"></a>インストール済みのアプリまたは実行中のアプリで診断セッションを実行する

Visual Studio プロジェクトからのアプリの起動以外に、別のターゲットに対して診断セッションを実行することもできます。 たとえば、Windows アプリ ストアからインストールされたアプリのパフォーマンス問題を診断できます。 パフォーマンス プロファイラーで、 **[ターゲットの変更]** の下にあるドロップダウン リストを選択します。

![診断ツールの分析ターゲットを選択](../profiling/media/pdhub_chooseanalysistarget.png "PDHUB_ChooseAnalysisTarget")

既にインストール済みのアプリを起動することも、既に実行中のアプリやプロセスに診断ツールをアタッチすることもできます。

分析ターゲットとして**実行可能ファイル**を選択する場合は、ローカル マシンまたはリモート マシン上の *.exe* へのパスを入力できます。 どちらの場合も、 *.exe* はローカルで実行されます。 ただし、Visual Studio でソリューションを開くことによって、アプリのプロファイリングを行うことをお勧めします。

UWP アプリの場合は、 **[実行中のアプリ]** または **[インストール済みのアプリ]** を選択するとき、指定された配置ターゲット上で検出されたアプリの一覧の中からアプリを選択します。 このターゲットはローカル コンピューターまたはリモート コンピューターにすることができます。 リモート マシンで UWP アプリをプロファイリングするには、 **[リモート接続]** ダイアログ ボックスで **[ユニバーサル (暗号化されていないプロトコル)]** を選択する必要があります。

![診断用の実行中またはインストール済みのアプリを選択](../profiling/media/pdhub_selectrunningapp.png "PDHUB_SelectRunningApp")

> [!NOTE]
> プロファイリング ツールをリモートで使用する必要があるその他のシナリオについては、「[コマンド ラインからアプリケーションのパフォーマンスを測定する](../profiling/profile-apps-from-command-line.md)」を参照してください。 コマンドライン ツールは、CPU 使用率と .NET オブジェクト割り当てツールで使用できます。

## <a name="see-also"></a>関連項目

次は診断開発チームのブログ投稿と MSDN 記事です。
- [MSDN マガジン:Visual Studio 2015 でのデバッグ中のパフォーマンス分析](https://msdn.microsoft.com/magazine/dn973013.aspx)

- [MSDN マガジン:IntelliTrace を使用して迅速に問題を診断する](https://msdn.microsoft.com/magazine/dn973014.aspx)

- [ブログの投稿:Visual Studio 2015 でのメモリ使用量ツールを使用したイベント ハンドラーのリークの診断](https://devblogs.microsoft.com/devops/diagnosing-event-handler-leaks-with-the-memory-usage-tool-in-visual-studio-2015/)

- [ビデオ:Microsoft Visual Studio Ultimate 2015 での IntelliTrace を使用したデバッグ履歴](https://channel9.msdn.com/Events/Ignite/2015/BRK3716)

- [ビデオ:Visual Studio 2015 を使用したパフォーマンスに関する問題のデバッグ](https://channel9.msdn.com/Events/Build/2015/3-731)

- [パフォーマンスのヒント:Visual Studio を使用したデバッグ中のパフォーマンス概要の参照](https://devblogs.microsoft.com/devops/perftips-performance-information-at-a-glance-while-debugging-with-visual-studio/)

- [Visual Studio 2015 の診断ツール [デバッガー] ウィンドウ](https://devblogs.microsoft.com/devops/diagnostic-tools-debugger-window-in-visual-studio-2015/)

- [IntelliTrace in Visual Studio Enterprise 2015 (Visual Studio Enterprise2015 の IntelliTrace)](https://devblogs.microsoft.com/devops/intellitrace-in-visual-studio-ultimate-2015/)
