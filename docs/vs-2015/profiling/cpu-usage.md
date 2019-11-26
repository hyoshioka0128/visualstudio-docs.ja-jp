---
title: CPU 使用率 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 7501a20d-04a1-480f-a69c-201524aa709d
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: f699666216d38c34583ebeb15e2bb6ba4953b671
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74300760"
---
# <a name="cpu-usage"></a>CPU 使用率
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

アプリのパフォーマンスの問題を調査する必要がある場合、まず CPU の使用方法の理解から始めることができます。 **CPU 使用率**ツールは、CPU が Visual C++、Visual C#/Visual Basic、JavaScript のコードを実行するとき、どこで時間を費やしているかを示します。  
  
 Visual Studio 2015 Update 1 以降、デバッガーを終了することなく CPU 使用率の関数ごとの内訳を確認できます。 デバッグ中に CPU プロファイリングのオンとオフを切り替えたり、ブレークポイントなど、実行が停止しているときに結果を表示できます。 詳細については、「 [Profile Your CPU in the Debugger in Visual Studio 2015](https://devblogs.microsoft.com/devops/profile-your-cpu-in-the-debugger-in-visual-studio-2015/)」を参照してください。  
  
 Windows ストア アプリのパフォーマンス分析に関するチュートリアルについては、「 [ストア アプリにおける CPU 使用率の分析](https://msdn.microsoft.com/library/windows/apps/dn641982.aspx)」を参照してください。  
  
 パフォーマンスと診断ハブでは、診断セッションの実行と管理のために他の多くのオプションを提供しています。 たとえば、 **CPU 使用率** ツールをローカルまたはリモートのコンピューターで、あるいはシミュレーターやエミュレーターで実行できます。 Visual Studio で開いているプロジェクトのパフォーマンスを分析したり、実行中のアプリにアタッチしたり、Windows ストアからインストールされたアプリを開始したりできます。 詳細については、「[デバッグなしでプロファイリングツールを実行](https://msdn.microsoft.com/library/e97ce1a4-62d6-4b8e-a2f7-61576437ff01)する」を参照してください。  
  
## <a name="BKMK_Collect_CPU_usage_data"></a> CPU 使用率のデータの収集  
  
1. Visual Studio で、ソリューション構成を **[リリース]** に設定して配置ターゲットを選択します。  
  
    ![リリースおよびローカルコンピューターの選択](../profiling/media/cpuuse-selectreleaselocalmachine.png "CPUUSE_SelectReleaseLocalMachine")  
  
   - アプリを **[リリース]** モードで実行すると、アプリの実際のパフォーマンスをよりよく把握できます。  
  
   - アプリをローカル コンピューターで実行すると、インストールされているアプリの実行に最も近い状態で再現できます。  
  
   - リモート デバイスからデータを収集している場合は、アプリはリモート デスクトップ接続を使用しないで、デバイス上で直接実行してください。  
  
   - Windows Phone アプリの場合には、 **[デバイス]** からのデータを直接収集すると最も正確なデータが得られます。  
  
2. **[デバッグ]** メニューの **[パフォーマンス プロファイラー...]** をクリックします。  
  
3. **[CPU 使用率]** 、 **[開始]** を選択します。  
  
    ![CPU 使用率の選択](../profiling/media/cpuuse-lib-choosecpuusage.png "CPUUSE_LIB_ChooseCpuUsage")  
  
4. アプリが起動したら、 **[最大数を取得]** をクリックします。 出力の表示後に約 1 秒待ってから、 **[非同期の最大数の取得]** を選択します。 ボタン クリックごとに合間を開けることで、診断レポートの中でボタン クリックのルーチンを分離しやすくなります。  
  
5. 2 番目の出力行が表示された後、パフォーマンスと診断ハブで **[コレクションの停止]** をクリックします。  
  
   ![CpuUsage データコレクションの停止](../profiling/media/cpu-use-wt-stopcollection.png "CPU_USE_WT_StopCollection")  
  
   CPU 使用率ツールがデータを分析してレポートを表示します。  
  
   ![CpuUsage レポート](../profiling/media/cpu-use-wt-report.png "CPU_USE_WT_Report")  
  
## <a name="analyze-the-cpu-usage-report"></a>CPU 使用率レポートの分析  
  
### <a name="BKMK_The_CPU_Usage_call_tree"></a> CPU 使用率コール ツリー  
 コール ツリー情報を理解するには、 `GetMaxNumberButton_Click` セグメントを再度選択し、コール ツリーの詳細を確認します。  
  
#### <a name="BKMK_Call_tree_structure"></a> コール ツリーの構造  
 ![Getmaxnumber ボタン&#95;[コールツリー]](../profiling/media/cpu-use-wt-getmaxnumbercalltree-annotated.png "CPU_USE_WT_GetMaxNumberCallTree_annotated")  
  
|||  
|-|-|  
|![ステップ 1](../profiling/media/procguid-1.png "ProcGuid_1")|CPU 使用率コール ツリーのトップ レベルのノードは擬似ノードです。|  
|![ステップ 2](../profiling/media/procguid-2.png "ProcGuid_2")|ほとんどのアプリでは、 **[外部コードの表示]** オプションをオフにすると、セカンド レベルのノードは **[外部コード]** ノードとなります。このノードに含まれるシステムおよびフレームワーク コードは、アプリの開始と停止、UI の描画、スレッド スケジュールの制御、およびアプリへの他の低レベル サービスの提供を行います。|  
|![ステップ 3](../profiling/media/procguid-3.png "ProcGuid_3")|セカンド レベル ノードの子はユーザー コード メソッドおよび非同期ルーチンで、セカンド レベル システムとフレームワーク コードによって呼び出される、または作成されます。|  
|![ステップ 4](../profiling/media/procguid-4.png "ProcGuid_4")|メソッドの子ノードには、親メソッドの呼び出しのみのデータが含まれます。 **[外部コードの表示]** がオフのとき、アプリ メソッドには **[外部コード]** ノードが含まれる場合もあります。|  
  
#### <a name="BKMK_External_Code"></a> 外部コード  
 外部コードとは、書き記したコードによって実行されるシステムおよびフレームワーク コンポーネント内の関数です。 外部コードには、アプリの開始と停止、UI の描画、スレッドの制御、およびアプリへの他の低レベル サービスの提供を行う関数が含まれます。 外部コードを確認することはほとんどないため、CPU 使用率コール ツリーはユーザー メソッドの外部関数を 1 つの **[外部コード]** ノードにまとめます。  
  
 外部コードのコール パスを表示する場合、 **[フィルター ビュー]** リストから **[外部コードの表示]** をクリックし、 **[適用]** をクリックします。  
  
 ![[フィルタービュー]、[外部コードの表示] の順に選択します。](../profiling/media/cpu-use-wt-filterview.png "CPU_USE_WT_FilterView")  
  
 多くの外部コードの呼び出しチェーンは複雑な入れ子になっているため、関数名列の幅は、一部の大型コンピューター モニターを除いてディスプレイの幅に収まりきらない可能性があります。 その場合、関数名は **[…]** と表示されます。  
  
 ![コールツリー内の入れ子になった外部コード](../profiling/media/cpu-use-wt-showexternalcodetoowide.png "CPU_USE_WT_ShowExternalCodeTooWide")  
  
 検索ボックスを使って目的のノードを探した後、水平スクロール バーを使ってデータを表示させます。  
  
 ![入れ子になった外部コードの検索](../profiling/media/cpu-use-wt-showexternalcodetoowide-found.png "CPU_USE_WT_ShowExternalCodeTooWide_Found")  
  
### <a name="BKMK_Call_tree_data_columns"></a> コール ツリー データの列  
  
|||  
|-|-|  
|**合計 CPU (%)**|![合計 % のデータ演算式](../profiling/media/cpu-use-wt-totalpercentequation.png "CPU_USE_WT_TotalPercentEquation")<br /><br /> 選択した時間の範囲内で、関数への呼び出しおよび関数が呼び出した関数によって使用されたアプリの CPU アクティビティの割合です。 これは、特定の時間範囲におけるアプリの合計アクティビティと、利用可能な合計 CPU 能力とを比較する **[CPU 使用率]** タイムライン グラフとは異なります。|  
|**セルフ CPU (%)**|![自己 % 演算式](../profiling/media/cpu-use-wt-selflpercentequation.png "CPU_USE_WT_SelflPercentEquation")<br /><br /> 選択した時間の範囲内で、関数への呼び出しによって使用されたアプリの CPU アクティビティの割合で、関数が呼び出した関数によるアクティビティは除外されます。|  
|**合計 CPU (ミリ秒)**|選択した時間の範囲内で、関数への呼び出しおよび関数が呼び出した関数によって使用されたミリ秒です。|  
|**セルフ CPU (ミリ秒)**|選択した時間の範囲内で、関数への呼び出しおよび関数が呼び出した関数によって使用されたミリ秒です。|  
|**モジュール**|関数が含まれるモジュールの名前、または [外部コード] ノード内の関数が含まれるモジュールの数です。|  
  
### <a name="BKMK_Asynchronous_functions_in_the_CPU_Usage_call_tree"></a> CPU 使用率コール ツリー内の非同期関数  
 コンパイラが非同期メソッドを検出すると、メソッドの実行を制御するために非表示のクラスを作成します。 概念的に言って、クラスとはコンパイラによって生成された関数のリストを含んだステート マシンです。これらの関数は、元のメソッドの操作を非同期で呼び出したり、それに必要なコールバック、スケジューラ、および反復子を正しく呼び出したりします。 元のメソッドが親メソッドによって呼び出されると、ランタイムは親の実行コンテキストからメソッドを削除し、アプリの実行を制御するシステムとフレームワーク コードのコンテキストにある非表示のクラスのメソッドを実行します。 非同期のメソッドは、多くの場合、1 つ以上の異なるスレッドで実行されます (必ずそうなるわけではありません)。 このコードは、CPU 使用率コール ツリーで、ツリーのトップ ノードのすぐ下にある **[外部コード]** ノードの子として表示されます。  
  
 これをこの例で表示するには、タイムラインで `GetMaxNumberAsyncButton_Click` セグメントを再度選択します。  
  
 ![Getmaxnumber Asyncbutton&#95;[レポートの選択] をクリック](../profiling/media/cpu-use-wt-getmaxnumberasync-selected.png "CPU_USE_WT_GetMaxNumberAsync_Selected")  
  
 **[外部コード]** の下にある最初の 2 つのノードは、ステート マシン クラスのコンパイラ生成メソッドです。 3 つ目は、元のメソッドへの呼び出しです。 生成されたメソッドを展開すると詳細が表示されます。  
  
 ![展開された Getmaxnumber Asyncbutton&#95;呼び出しツリーのクリック](../profiling/media/cpu-use-wt-getmaxnumberasync-expandedcalltree.png "CPU_USE_WT_GetMaxNumberAsync_ExpandedCallTree")  
  
- `MainPage::GetMaxNumberAsyncButton_Click` の機能は少なく、タスクの値のリストを管理し、結果の最大値を計算し、出力を表示します。  
  
- `MainPage+<GetMaxNumberAsyncButton_Click>d__3::MoveNext` は、 `GetNumberAsync`の呼び出しをラップする 48 個のタスクをスケジュールして起動するために必要なアクティビティを表示します。  
  
- `MainPage::<GetNumberAsync>b__b` は `GetNumber` を呼び出すタスクのアクティビティを表示します。
