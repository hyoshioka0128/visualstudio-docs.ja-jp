---
title: CPU 使用率の分析 | Microsoft Docs
ms.custom: seodec18
ms.date: 11/04/2018
ms.topic: conceptual
ms.assetid: 7501a20d-04a1-480f-a69c-201524aa709d
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 351247f50560896d53267fcf8d7f4a66a81b9461
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "62553621"
---
# <a name="analyze-cpu-usage"></a>CPU 使用率の分析

アプリのパフォーマンスの問題の調査を開始するのに適した方法は、CPU 使用率を理解することです。 **CPU 使用率**パフォーマンス ツールは、C++、C#/Visual Basic、および JavaScript のアプリでコードを実行するのにかかった CPU 時間と割合を示します。

**CPU 使用率**ツールは、開かれた状態の Visual Studio プロジェクトまたはインストール済みの Microsoft Store アプリで実行することができます。または、実行中のアプリまたはプロセスにアタッチすることもできます。 このツールは、ローカルまたはリモートのコンピューターで実行することも、シミュレーターやエミュレーターで実行することもできます。 詳細については、「[デバッガーを使用して、または使用せずにプロファイリング ツールを実行する](../profiling/running-profiling-tools-with-or-without-the-debugger.md)」を参照してください。

**CPU 使用率**ツールは、デバッグを使用して、または使用せずに実行することができます。 デバッガーで、CPU プロファイルをオン/オフにして、CPU 使用率の関数ごとの内訳を確認することができます。 たとえばブレークポイントなどで、実行が一時停止したときに、CPU 使用率の結果を表示できます。

次の手順では、Visual Studio **パフォーマンス プロファイラー**を使用してデバッガーなしで **CPU 使用率**ツールを使用する方法を示します。 例では、ローカル コンピューターでリリース ビルドを使用しています。 リリース ビルドでは、実際のアプリ パフォーマンスの最適なビューが提供されます。 デバッグ ビルドを使用して CPU 使用率を分析するには、[パフォーマンス プロファイリングのビギナーズ ガイド](../profiling/beginners-guide-to-performance-profiling.md)を参照してください。

通常、ローカル コンピューターでは、インストールされているアプリの実行が最適にレプリケートされます。 Windows Phone アプリの場合には、デバイスからのデータを直接収集すると最も正確なデータが得られます。 リモート デバイスからデータを収集するには、リモート デスクトップ接続を介さずに、デバイス上で直接アプリを実行します。

>[!NOTE]
>[パフォーマンス プロファイラー](../profiling/profiling-feature-tour.md)を使用するには、Windows 7 以降が必要です。

## <a name="collect-cpu-usage-data"></a>CPU 使用率のデータの収集

1. Visual Studio プロジェクトで、ソリューション構成を **[リリース]** に設定し、配置ターゲットとして **[ローカル コンピューター]** を選択します。

    ![リリースとローカル コンピューターの選択](../profiling/media/cpuuse_selectreleaselocalmachine.png "リリースとローカル コンピューターの選択")

1. **[デバッグ]**  >  **[パフォーマンス プロファイラー]** の順に選択します。

1. **[使用可能なツール]** の下で、 **[CPU 使用率]** を選択し、 **[開始]** を選択します。

    ![CPU 使用率の選択](../profiling/media/cpuuse_lib_choosecpuusage.png "CPU 使用率の選択")

4. アプリが起動すると、診断セッションが開始され、CPU 使用率データが表示されます。 データの収集が完了したら、 **[コレクションの停止]** を選択します。

   ![CPU 使用率データ コレクションの停止](../profiling/media/cpu_use_wt_stopcollection.png "CPU 使用率データ コレクションの停止")

   CPU 使用率ツールがデータを分析してレポートを表示します。

   ![CPU 使用率レポート](../profiling/media/cpu_use_wt_report.png "CPU 使用率レポート")

## <a name="analyze-the-cpu-usage-report"></a>CPU 使用率レポートの分析

診断レポートは、**合計 CPU** の高い順に並べ替えられます。 並べ替え順序または並べ替え列を変更するには、列ヘッダーを選択します。 表示するスレッドを選択または選択解除するには、 **[フィルター]** ドロップダウンを使用します。特定のスレッドまたはノードを検索するには、 **[検索]** ボックスを使用します。

::: moniker range=">=vs-2019"
Visual Studio 2019 以降、 **[ホット パスの展開]** ボタンと **[ホット パスの表示]** ボタンをクリックすることで、最も高い割合で CPU を使用している関数の呼び出しを呼び出しツリー ビューに表示できます。
::: moniker-end

### <a name="cpu-usage-data-columns"></a><a name="BKMK_Call_tree_data_columns"></a> CPU 使用率データの列

|||
|-|-|
|**合計 CPU [ユニット、%]**|![合計 % のデータ演算式](../profiling/media/cpu_use_wt_totalpercentequation.png "CPU_USE_WT_TotalPercentEquation")<br /><br /> 選択した時間範囲において、関数の呼び出し、および関数が呼び出した関数で使用された CPU 時間 (ミリ秒) と割合です。 これは、特定の時間範囲におけるアプリの合計 CPU アクティビティと、利用可能な合計 CPU とを比較する **CPU 使用率**タイムライン グラフとは異なります。|
|**セルフ CPU [ユニット、%]**|![自己 % 演算式](../profiling/media/cpu_use_wt_selflpercentequation.png "CPU_USE_WT_SelflPercentEquation")<br /><br /> 選択した時間範囲において、関数の呼び出し (関数が呼び出した関数を除く) で使用された CPU 時間 (ミリ秒) と使用率 (パーセンテージ) です。|
|**Module**|関数を含むモジュールの名前です。

### <a name="the-cpu-usage-call-tree"></a><a name="BKMK_The_CPU_Usage_call_tree"></a> CPU 使用率コール ツリー

コール ツリーを表示するには、レポートの親ノードを選択します。 **[CPU 使用率]** ページが開き、**呼び出し元/呼び出し先**ビューが表示されます。 **[現在のビュー]** ドロップダウンで **[コール ツリー]** を選択します。

#### <a name="call-tree-structure"></a><a name="BKMK_Call_tree_structure"></a> コール ツリーの構造

::: moniker range=">=vs-2019"
![コール ツリーの構造](../profiling/media/vs-2019/cpu-use-wt-getmaxnumbercalltree-annotated.png "コール ツリーの構造")
::: moniker-end
::: moniker range="vs-2017"
![コール ツリーの構造](../profiling/media/cpu_use_wt_getmaxnumbercalltree_annotated.png "コール ツリーの構造")
::: moniker-end

|||
|-|-|
|![ステップ 1](../profiling/media/procguid_1.png "ProcGuid_1")|CPU 使用率コール ツリーのトップ レベルのノードは擬似ノードです。|
|![ステップ 2](../profiling/media/procguid_2.png "ProcGuid_2")|ほとんどのアプリでは、 **[外部コードの表示]** オプションが無効になっていると、2 番目のレベルのノードが、 **[外部コード]** ノードになります。 ノードには、アプリの開始と停止、UI の描画、スレッドの制御、およびアプリへの他の低レベル サービスの提供を行うシステムとフレームワーク コードが含まれています。|
|![ステップ 3](../profiling/media/procguid_3.png "ProcGuid_3")|セカンド レベル ノードの子はユーザー コード メソッドおよび非同期ルーチンで、セカンド レベル システムとフレームワーク コードによって呼び出される、または作成されます。|
|![ステップ 4](../profiling/media/procguid_4.png "ProcGuid_4")|メソッドの子ノードには、親メソッドを呼び出すためだけのデータが含まれます。 **[外部コードの表示]** がオフのとき、アプリ メソッドには **[外部コード]** ノードが含まれる場合もあります。|

#### <a name="external-code"></a><a name="BKMK_External_Code"></a> 外部コード

コードによって実行されるシステムおよびフレームワークの関数は、*外部コード*と呼ばれます。 外部コード関数は、アプリの開始と停止、UI の描画、スレッドの制御、およびアプリへの他の低レベル サービスの提供を行います。 外部コードを確認することはほとんどないため、CPU 使用率コール ツリーはユーザー メソッドの外部関数を 1 つの **[外部コード]** ノードにまとめます。

外部コードの呼び出しパスを表示するには、診断レポートのメイン ページ (右側のウィンドウ) で、 **[フィルター]** ドロップダウンから **[外部コードの表示]** を選択し、 **[適用]** を選択します。 **[CPU 使用率]** ページの **[コール ツリー]** ビューで外部コードの呼び出しが展開されます。 ( **[フィルター]** ドロップダウンは、詳細ビューではなくメインの診断ページで使用できます。)

![外部コードの表示](../profiling/media/cpu_use_wt_filterview.png "[外部コードの表示]")

多くの外部コードの呼び出しチェーンは複雑な入れ子になっているため、チェーンの幅が **[関数名]** 列の表示幅に収まりきらない可能性があります。 その場合、関数名が **...** として表示されます。

![コール ツリーの入れ子式の外部コード](../profiling/media/cpu_use_wt_showexternalcodetoowide.png "コール ツリーの入れ子式の外部コード")

探している関数名を検索するには、検索ボックスを使用します。 選択した行をポイントするか、水平スクロール バーを使用してデータを表示します。

::: moniker range=">=vs-2019"
![入れ子式の外部コードの検索](../profiling/media/vs-2019/cpu-use-wt-showexternalcodetoowide-found.png "入れ子式の外部コードの検索")
::: moniker-end
::: moniker range="vs-2017"
![入れ子式の外部コードの検索](../profiling/media/cpu_use_wt_showexternalcodetoowide_found.png "入れ子式の外部コードの検索")
::: moniker-end

### <a name="asynchronous-functions-in-the-cpu-usage-call-tree"></a><a name="BKMK_Asynchronous_functions_in_the_CPU_Usage_call_tree"></a> CPU 使用率コール ツリー内の非同期関数

 コンパイラが非同期メソッドを検出すると、メソッドの実行を制御するために非表示のクラスを作成します。 概念的に、クラスはステート マシンです。 クラスには、元のメソッドを非同期に呼び出すコンパイラにより生成された関数と、それらを実行するために必要なコールバック、スケジューラ、反復子があります。 親メソッドによって元のメソッドが呼び出されると、コンパイラは親の実行コンテキストからメソッドを削除し、アプリの実行を制御するシステムとフレームワーク コードのコンテキストにある非表示のクラスのメソッドを実行します。 非同期のメソッドは、多くの場合、1 つ以上の異なるスレッドで実行されます (必ずそうなるわけではありません)。 このコードは、**CPU 使用率**コール ツリーで、ツリーのトップ ノードのすぐ下にある **[外部コード]** ノードの子として表示されます。

次の例では、 **[外部コード]** の下にある最初の 2 つのノードは、ステート マシン クラスのコンパイラ生成メソッドです。 3 番目のノードは、元のメソッドへの呼び出しです。

![非同期ノード](media/cpu_use_wt_getmaxnumberasync_selected.png "非同期ノード")

生成されたメソッドを展開して、詳細を表示します。

![拡張非同期ノード](media/cpu_use_wt_getmaxnumberasync_expandedcalltree.png "拡張非同期ノード")

- `MainPage::GetMaxNumberAsyncButton_Click` は単に、タスクの値のリストを管理し、結果の最大値を計算し、出力を表示します。

- `MainPage+<GetMaxNumberAsyncButton_Click>d__3::MoveNext` は、 `GetNumberAsync`の呼び出しをラップする 48 個のタスクをスケジュールして起動するために必要なアクティビティを表示します。

- `MainPage::<GetNumberAsync>b__b` は `GetNumber`を呼び出すタスクのアクティビティを表示します。
