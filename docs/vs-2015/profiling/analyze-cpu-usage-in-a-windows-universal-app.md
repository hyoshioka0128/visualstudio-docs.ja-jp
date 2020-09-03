---
title: Windows ユニバーサル アプリでの CPU 使用率の分析 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: c122b08e-e3bf-43e6-bd6c-e776e178fd9a
caps.latest.revision: 21
author: MikeJo5000
ms.author: mikejo
manager: jillfra
robots: noindex,nofollow
ms.openlocfilehash: def581f547db19a8db4cebc4d63739ff09bb5fab
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85531665"
---
# <a name="analyze-cpu-usage-in-a-windows-universal-app"></a>Windows ユニバーサル アプリでの CPU 使用率の分析
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Windows および Windows Phone] (../Image/windows_and_phone_content.png "windows_and_phone_content")  
  
 アプリのパフォーマンスの問題を調査する必要がある場合、まず CPU の使用状況を理解することから始めることができます。 **CPU 使用率** ツールは、CPU がコードを実行する際、どこで時間を費やしているかを示します。 特定のシナリオに重点を置いて、1つの診断セッションで CPU 使用率を [XAML UI 応答性](https://msdn.microsoft.com/library/4ff84cd1-4e63-4fda-b34f-3ef862a6e480) ツール、 [Cpu 使用率ツール](../profiling/cpu-usage.md) ツール、または両方のツールで実行できます。  
  
> [!NOTE]
> **CPU 使用率**ツールは、Windows Phone Silverlight 8.1 アプリには使用できません。  
  
 このチュートリアルでは、簡単な Windows Universal XAML アプリの CPU 使用率の収集と分析について説明します。  
  
## <a name="create-the-cpuusedemo-project"></a><a name="BKMK_Create_the_CpuUseDemo_project"></a> CpuUseDemo プロジェクトの作成  
 **CpuUseDemo** とは、CPU 使用率のデータを収集して分析する方法を説明するために作成されたアプリです。 ボタンは、関数に対する複数の呼び出しの中から最大の値を選択するメソッドを呼び出して数字を生成します。 呼び出された関数は、非常に多くの乱数値を作成した後、最後の値を返します。 データはテキスト ボックスに表示されます。  
  
1. **BlankApp** テンプレートを使って **CpuUseDemo** という名前の新しい C# Windows Universal アプリ プロジェクトを作成します。  
  
     ![CpuUseDemoProject の作成](../profiling/media/cpu-use-newproject.png "CPU_USE_NewProject")  
  
2. MainPage.xaml を[このコード](#BKMK_MainPage_xaml)で置き換えます。  
  
3. MainPage.xaml.cs を[このコード](#BKMK_MainPage_xaml_cs)で置き換えます。  
  
4. アプリをビルドして、試してみてください。アプリは、CPU 使用率データ分析の一般的なケースを示すのに十分です。  
  
## <a name="collect-cpu-usage-data"></a><a name="BKMK_Collect_CPU_usage_data"></a> CPU 使用率データの収集  
 ![シミュレーターでアプリのリリース ビルドを実行する](../profiling/media/cpu-use-wt-setsimulatorandretail.png "CPU_USE_WT_SetSimulatorAndRetail")  
  
1. Visual Studio で、配置ターゲットを [**シミュレーター**] に設定し、ソリューション構成を [**リリース**] に設定します。  
  
   - シミュレーターでアプリを実行すると、アプリと Visual Studio IDE との間で簡単に切り替えることができます。  
  
   - このアプリを [**リリース**] モードで実行すると、アプリの実際のパフォーマンスをよりよく把握できます。  
  
2. **[デバッグ]** メニューの **[パフォーマンス プロファイラー...]** をクリックします。  
  
3. パフォーマンスと診断ハブで、[**CPU 使用率**] をクリックしてから、[**開始**] をクリックします。  
  
    ![CpuUsage 診断セッションの開始](../profiling/media/cpu-use-wt-perfdiaghub.png "CPU_USE_WT_PerfDiagHub")  
  
4. アプリが起動したら、[ **最大数を取得**] をクリックします。 出力の表示後に約 1 秒待ってから、[ **非同期の最大数の取得**] を選択します。 ボタンのクリック間隔を空けると、診断レポートにおいてボタン クリックのルーチンを分離しやすくなります。  
  
5. 2 番目の出力行が表示された後、パフォーマンスと診断ハブで **[コレクションの停止]** をクリックします。  
  
   ![CpuUsage データ コレクションの停止](../profiling/media/cpu-use-wt-stopcollection.png "CPU_USE_WT_StopCollection")  
  
   CPU 使用率ツールがデータを分析してレポートを表示します。  
  
   ![CpuUsage レポート](../profiling/media/cpu-use-wt-report.png "CPU_USE_WT_Report")  
  
## <a name="analyze-the-cpu-usage-report"></a><a name="BKMK_Analyze_the_CPU_Usage_report"></a> CPU 使用率レポートの分析  
  
### <a name="cpu-utilization-timeline-graph"></a><a name="BKMK_CPU_utilization_timeline_graph"></a> CPU 使用状況タイムライン グラフ  
 ![Cpu 使用率 &#40;% &#41; タイムライングラフ](../profiling/media/cpu-use-wt-timelinegraph.png "CPU_USE_WT_TimelineGraph")  
  
 CPU 使用状況グラフは、デバイスにあるすべてのプロセッサー コアのすべての CPU 時間に対するアプリの CPU アクティビティの割合を示します。 このレポートのデータはデュアル コアのコンピューターで収集されました。 2 つの急激な増加は、2 つのボタン クリックの CPU アクティビティを表します。 `GetMaxNumberButton_Click` はシングル コアで同期的に実行されるため、メソッドのグラフの高さが 50% を超えていないのは理にかなっています。 また、`GetMaxNumberAsycButton_Click` は非同期的に両方のコアで実行されるため、グラフの急激な増加が両方のコアでほぼすべての CPU リソースを活用しているように見えるのも適切と言えます。  
  
#### <a name="select-timeline-segments-to-view-details"></a><a name="BKMK_Select_timeline_segments_to_view_details"></a> 詳細を確認するためにタイムライン セグメントを選択する  
 [**診断セッション**] タイムラインの選択バーを使用して、GetMaxNumberButton_Click のデータに注目します。  
  
 ![Getmaxnumber ボタン&#95;クリックして選択](../profiling/media/cpu-use-wt-getmaxnumberreport.png "CPU_USE_WT_GetMaxNumberReport")  
  
 [**診断セッション**] タイムラインでは、選択したセグメントで使用した時間 (このレポートでは 2 秒余り) が表示され、選択で実行されたメソッドを対象にコール ツリーをフィルターします。  
  
 次に `GetMaxNumberAsyncButton_Click` セグメントを選択します。  
  
 ![Getmaxnumber Asyncbutton&#95;クリックしてレポートを選択](../profiling/media/cpu-use-wt-getmaxnumberasync-selected.png "CPU_USE_WT_GetMaxNumberAsync_Selected")  
  
 このメソッドは `GetMaxNumberButton_Click` よりも 1 秒早く完了しますが、コール ツリー エントリの意味はそれほど明確ではありません。  
  
### <a name="the-cpu-usage-call-tree"></a><a name="BKMK_The_CPU_Usage_call_tree"></a> CPU 使用率コール ツリー  
 コール ツリー情報を理解するには、 `GetMaxNumberButton_Click` セグメントを再度選択し、コール ツリーの詳細を確認します。  
  
#### <a name="call-tree-structure"></a><a name="BKMK_Call_tree_structure"></a> コール ツリーの構造  
 ![Getmaxnumber ボタン&#95;[コールツリー]](../profiling/media/cpu-use-wt-getmaxnumbercalltree-annotated.png "CPU_USE_WT_GetMaxNumberCallTree_annotated")  
  
|Image|説明|  
|-|-|  
|![ステップ 1](../profiling/media/procguid-1.png "ProcGuid_1")|CPU 使用率コール ツリーのトップ レベルのノードは擬似ノードです。|  
|![ステップ 2](../profiling/media/procguid-2.png "ProcGuid_2")|ほとんどのアプリでは、 **[外部コードの表示]** オプションをオフにすると、セカンド レベルのノードは **[外部コード]** ノードとなります。このノードに含まれるシステムおよびフレームワーク コードは、アプリの開始と停止、UI の描画、スレッド スケジュールの制御、およびアプリへの他の低レベル サービスの提供を行います。|  
|![ステップ 3](../profiling/media/procguid-3.png "ProcGuid_3")|セカンド レベル ノードの子はユーザー コード メソッドおよび非同期ルーチンで、セカンド レベル システムとフレームワーク コードによって呼び出される、または作成されます。|  
|![ステップ 4](../profiling/media/procguid-4.png "ProcGuid_4")|メソッドの子ノードには、親メソッドの呼び出しのみのデータが含まれます。 **[外部コードの表示]** がオフのとき、アプリ メソッドには **[外部コード]** ノードが含まれる場合もあります。|  
  
#### <a name="external-code"></a><a name="BKMK_External_Code"></a> 外部コード  
 外部コードは、作成したコードによって実行されるシステムおよびフレームワーク コンポーネント内の関数で構成されます。 外部コードには、アプリの開始と停止、UI の描画、スレッドの制御、およびアプリへの他の低レベル サービスの提供を行う関数が含まれます。 ほとんどの場合、外部コードに関心がなく、CPU 使用率コールツリーはユーザーメソッドの外部関数を1つの **[外部コード]** ノードに収集します。  
  
 外部コードのコール パスを表示する場合、 **[フィルター ビュー]** リストから **[外部コードの表示]** をクリックし、 **[適用]** をクリックします。  
  
 ![[フィルター表示]、[外部コードの表示] の順に選択](../profiling/media/cpu-use-wt-filterview.png "CPU_USE_WT_FilterView")  
  
 多くの外部コードの呼び出しチェーンは複雑な入れ子になっているため、関数名列の幅は、一部の大型コンピューター モニターを除いてディスプレイの幅に収まりきらない可能性があります。 この場合、関数名は **[...]** と表示されます。  
  
 ![コール ツリーの入れ子式の外部コード](../profiling/media/cpu-use-wt-showexternalcodetoowide.png "CPU_USE_WT_ShowExternalCodeTooWide")  
  
 検索ボックスを使って目的のノードを探した後、水平スクロール バーを使ってデータを表示させます。  
  
 ![入れ子式の外部コードの検索](../profiling/media/cpu-use-wt-showexternalcodetoowide-found.png "CPU_USE_WT_ShowExternalCodeTooWide_Found")  
  
### <a name="call-tree-data-columns"></a><a name="BKMK_Call_tree_data_columns"></a> コール ツリー データの列  
  
|プロパティ|説明|  
|-|-|  
|**合計 CPU (%)**|![合計 % のデータ演算式](../profiling/media/cpu-use-wt-totalpercentequation.png "CPU_USE_WT_TotalPercentEquation")<br /><br /> 選択した時間範囲におけるアプリの CPU アクティビティのうち、関数の呼び出し、および関数が呼び出した関数が使用した割合です。 これは、特定の時間範囲におけるアプリの合計アクティビティと、利用可能な合計 CPU 能力とを比較する [ **CPU 使用率** ] タイムライン グラフとは異なります。|  
|**セルフ CPU (%)**|![自己 % 演算式](../profiling/media/cpu-use-wt-selflpercentequation.png "CPU_USE_WT_SelflPercentEquation")<br /><br /> 選択した時間範囲におけるアプリの CPU アクティビティのうち、関数の呼び出しが使用した割合です。ただし、関数から呼び出された関数のアクティビティは除きます。|  
|**合計 CPU (ミリ秒)**|選択した時間範囲内で、関数への呼び出しおよび関数が呼び出した関数によって使用されたミリ秒です。|  
|**セルフ CPU (ミリ秒)**|選択した時間範囲内で、関数への呼び出しおよび関数が呼び出した関数によって使用されたミリ秒です。|  
|**[Module]**|関数が含まれるモジュールの名前です。あるいは、[外部コード] ノード内の関数が含まれるモジュールの数です。|  
  
### <a name="asynchronous-functions-in-the-cpu-usage-call-tree"></a><a name="BKMK_Asynchronous_functions_in_the_CPU_Usage_call_tree"></a> CPU 使用率コールツリー内の非同期関数  
 コンパイラが非同期メソッドを検出すると、メソッドの実行を制御するために非表示のクラスを作成します。 概念的に言って、クラスとはコンパイラによって生成された関数のリストを含んだステート マシンです。これらの関数は、元のメソッドの操作を非同期で呼び出したり、それに必要なコールバック、スケジューラ、および反復子を正しく呼び出したりします。 元のメソッドが親メソッドによって呼び出されると、ランタイムは親の実行コンテキストからメソッドを削除し、アプリの実行を制御するシステムとフレームワーク コードのコンテキストにある非表示のクラスのメソッドを実行します。 非同期のメソッドは、多くの場合、1 つ以上の異なるスレッドで実行されます (必ずそうなるわけではありません)。 このコードは、CPU 使用率コール ツリーで、ツリーのトップ ノードのすぐ下にある **[外部コード]** ノードの子として表示されます。  
  
 これをこの例で表示するには、タイムラインで `GetMaxNumberAsyncButton_Click` セグメントを再度選択します。  
  
 ![Getmaxnumber Asyncbutton&#95;クリックしてレポートを選択](../profiling/media/cpu-use-wt-getmaxnumberasync-selected.png "CPU_USE_WT_GetMaxNumberAsync_Selected")  
  
 **[外部コード]** の下にある最初の 2 つのノードは、ステート マシン クラスのコンパイラ生成メソッドです。 3 つ目は、元のメソッドへの呼び出しです。 生成されたメソッドを展開すると詳細が表示されます。  
  
 ![拡張された Getmaxnumber Asyncbutton&#95;[コールツリー]](../profiling/media/cpu-use-wt-getmaxnumberasync-expandedcalltree.png "CPU_USE_WT_GetMaxNumberAsync_ExpandedCallTree")  
  
- `MainPage::GetMaxNumberAsyncButton_Click` の機能は少なく、タスクの値のリストを管理し、結果の最大値を計算し、出力を表示します。  
  
- `MainPage+<GetMaxNumberAsyncButton_Click>d__3::MoveNext` は、 `GetNumberAsync`の呼び出しをラップする 48 個のタスクをスケジュールして起動するために必要なアクティビティを表示します。  
  
- `MainPage::<GetNumberAsync>b__b` は `GetNumber`を呼び出すタスクのアクティビティを表示します。  
  
## <a name="next-steps"></a><a name="BKMK_Next_steps"></a> 次のステップ  
 CpuUseDemo アプリには目立った機能がないかもしれませんが、非同期操作やパフォーマンスと診断ハブの他のツールで試行錯誤することによって、ユーティリティを拡張することができます。  
  
- `MainPage::<GetNumberAsync>b__b` は、GetNumber メソッドの実行よりも、[外部コード] でより多くの時間を費やします。 この時間の大半は、非同期操作のオーバーヘッドです。 `NUM_TASKS` で、タスクの数を増やし (MainPage.xaml.cs の `GetNumber` 定数で設定)、イテレーションの数を減らしてみます (`MIN_ITERATIONS` の値を変更)。 コレクション シナリオを実行し、`MainPage::<GetNumberAsync>b__b` の CPU アクティビティを元の CPU 使用率の診断セッションのものと比較します。 タスクを減らし、イテレーションを増やしてみます。  
  
- ユーザーは多くの場合、アプリの実際のパフォーマンスは気にしていませんが、アプリの見かけ上のパフォーマンスや応答性は気にします。 XAML UI 応答性ツールは、見かけ上の応答性に影響するアクティビティの詳細を UI スレッドに表示します。  
  
     診断とパフォーマンス ハブで新しいセッションを作成し、XAML UI 応答性ツールと CPU 使用率ツールの両方を追加します。 コレクション シナリオを実行します。 ここまで読み進めることができた場合、レポートには既にわかっていること以外の情報はないでしょう。しかし、2 つのメソッドの **UI スレッド使用状況**のタイムライン グラフの違いは歴然としています。 複雑な実世界のアプリでは、ツールを組み合わせて使用することは非常に役立ちます。  
  
## <a name="mainpagexaml"></a><a name="BKMK_MainPage_xaml"></a> Mainpage.xaml  
  
```csharp  
<Page  
    x:Class="CpuUseDemo.MainPage"  
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
    xmlns:local="using:CpuUseDemo"  
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"  
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"  
    mc:Ignorable="d">  
  
    <Page.Resources>  
        <Style TargetType="TextBox">  
            <Setter Property="FontFamily"  Value="Lucida Console" />  
        </Style>  
    </Page.Resources>  
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">  
        <Grid.RowDefinitions>  
            <RowDefinition Height="Auto" />  
            <RowDefinition Height="*" />  
        </Grid.RowDefinitions>  
        <StackPanel Grid.Row="0" Orientation="Horizontal"  Margin="0,40,0,0">  
            <Button Name="GetMaxNumberButton" Click="GetMaxNumberButton_Click"  Content="Get Max Number" />  
            <Button Name="GetMaxNumberAsyncButton" Click="GetMaxNumberAsyncButton_Click"  Content="Get Max Number Async" />  
        </StackPanel>  
        <StackPanel Grid.Row="1">  
            <TextBox Name="TextBox1" AcceptsReturn="True" />  
        </StackPanel>  
    </Grid>  
  
</Page>  
  
```  
  
## <a name="mainpagexamlcs"></a><a name="BKMK_MainPage_xaml_cs"></a> MainPage.xaml.cs  
  
```csharp  
using System;  
using System.Collections.Generic;  
using System.IO;  
using System.Linq;  
using System.Runtime.InteropServices.WindowsRuntime;  
using Windows.Foundation;  
using Windows.Foundation.Collections;  
using Windows.UI.Xaml;  
using Windows.UI.Xaml.Controls;  
using Windows.UI.Xaml.Controls.Primitives;  
using Windows.UI.Xaml.Data;  
using Windows.UI.Xaml.Input;  
using Windows.UI.Xaml.Media;  
using Windows.UI.Xaml.Navigation;  
using Windows.Foundation.Diagnostics;  
using System.Threading;  
using System.Threading.Tasks;  
using System.Collections.Concurrent;  
  
// The Blank Page item template is documented at http://go.microsoft.com/fwlink/?LinkId=234238  
  
namespace CpuUseDemo  
{  
    /// <summary>  
    /// An empty page that can be used on its own or navigated to within a Frame.  
    /// </summary>  
    public sealed partial class MainPage : Page  
    {  
        public MainPage()  
        {  
            this.InitializeComponent();  
        }  
  
        const int NUM_TASKS = 48;  
        const int MIN_ITERATIONS = int.MaxValue / 1000;  
        const int MAX_ITERATIONS = MIN_ITERATIONS + 10000;  
  
        long m_totalIterations = 0;  
        readonly object m_totalItersLock = new object();  
  
        private void GetMaxNumberButton_Click(object sender, RoutedEventArgs e)  
        {  
            GetMaxNumberAsyncButton.IsEnabled = false;  
            lock (m_totalItersLock)  
            {  
                m_totalIterations = 0;  
            }  
            List<int> tasks = new List<int>();  
            for (var i = 0; i < NUM_TASKS; i++)  
            {  
                var result = 0;  
                result = GetNumber();  
                tasks.Add(result);  
            }  
            var max = tasks.Max();  
            var s = GetOutputString("GetMaxNumberButton_Click", NUM_TASKS, max, m_totalIterations);  
            TextBox1.Text += s;  
            GetMaxNumberAsyncButton.IsEnabled = true;  
        }  
  
        private async void GetMaxNumberAsyncButton_Click(object sender, RoutedEventArgs e)  
        {  
            GetMaxNumberButton.IsEnabled = false;  
            GetMaxNumberAsyncButton.IsEnabled = false;  
            lock (m_totalItersLock)  
            {  
                m_totalIterations = 0;  
            }  
            var tasks = new ConcurrentBag<Task<int>>();  
            for (var i = 0; i < NUM_TASKS; i++)  
            {  
                tasks.Add(GetNumberAsync());  
            }  
            await Task.WhenAll(tasks.ToArray());  
            var max = 0;  
            foreach (var task in tasks)  
            {  
                max = Math.Max(max, task.Result);  
            }  
            var func = "GetMaxNumberAsyncButton_Click";  
            var outputText = GetOutputString(func, NUM_TASKS, max, m_totalIterations);  
            TextBox1.Text += outputText;  
            this.GetMaxNumberButton.IsEnabled = true;  
            GetMaxNumberAsyncButton.IsEnabled = true;  
        }  
  
        private int GetNumber()  
        {  
            var rand = new Random();  
            var iters = rand.Next(MIN_ITERATIONS, MAX_ITERATIONS);  
            var result = 0;  
            lock (m_totalItersLock)  
            {  
                m_totalIterations += iters;  
            }  
            // we're just spinning here  
            // and using Random to frustrate compiler optimizations  
            for (var i = 0; i < iters; i++)  
            {  
                result = rand.Next();  
            }  
            return result;  
        }  
  
        private Task<int> GetNumberAsync()  
        {  
            return Task<int>.Run(() =>  
            {  
                return GetNumber();  
            });  
        }  
  
        string GetOutputString(string func, int cycles, int max, long totalIters)  
        {  
            var fmt = "{0,-35}Tasks:{1,3}    Maximum:{2, 12}    Iterations:{3,12}\n";  
            return String.Format(fmt, func, cycles, max, totalIters);  
        }  
  
    }  
}  
  
```
