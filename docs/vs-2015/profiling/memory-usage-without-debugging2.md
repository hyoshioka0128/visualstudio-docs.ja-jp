---
title: デバッグなしのメモリ使用量 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: 24238fc0-40b8-4079-8579-698211db9a26
caps.latest.revision: 18
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 64f739039d17af7fbee9718da93e8610e2619a85
ms.sourcegitcommit: da5ebc29544fdbdf625ab4922c9777faf2bcae4a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/29/2020
ms.locfileid: "82586951"
---
# <a name="memory-usage-without-debugging"></a>デバッグなしのメモリ使用量
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

デバッグなしの**メモリ使用量**ツールを使用して、次のような操作を行えます  
  
- シナリオの開発中に Visual Studio 内でのアプリのメモリ使用量が適切かどうかを監視します。  
  
- アプリのメモリの状態の詳しいスナップショットを作ります。  
  
- スナップショットを比べて、メモリの問題の根本原因を見つけます。  
  
  このトピックでは、メモリ使用量ツールを使って Windows Universal XAML アプリを分析する方法について説明します。 JavaScript と HTML を使用する Windows ユニバーサル アプリでのメモリ使用量を分析する場合、「[メモリ使用量の分析 (JavaScript)](https://msdn.microsoft.com/library/windows/apps/jj819176.aspx)」を参照してください。  
  
## <a name="start-a-memory-usage-diagnostic-session"></a><a name="BKMK_Start_a_Memory_Usage_diagnostic_session"></a>メモリ使用量診断セッションの開始  
  
1. Visual Studio で、C# のユニバーサル Windows プロジェクトを開きます。  
  
2. メニュー バーで、**[デバッグ]、[パフォーマンス プロファイラー...]** の順にクリックします。  
  
3. **[メモリ使用量]** を選択し、ページの下部にある **[開始]** ボタンをクリックします。  
  
     ![メモリ使用量診断セッションの開始](../profiling/media/memuse-start-diagnosticssession.png "MEMUSE_Start_DiagnosticsSession")  
  
## <a name="monitor-memory-use"></a><a name="BKMK_Monitor_memory_use"></a>メモリ使用量の監視  
 **[メモリ使用量]** ツールを使って、問題の検出と修正に使える詳しいレポートを生成できますが、現に開発中のシナリオがメモリに及ぼす影響をリアルタイムで調べることもできます。  
  
 診断セッションを開始すると、アプリが起動し、[**診断ツール**] ウィンドウにアプリのメモリ使用量のタイムライングラフが表示されます。  
  
 ![メモリ使用量の概要ページ](../profiling/media/memuse-reportoverview.png "MEMUSE__ReportOverview")  
  
 タイムライン グラフには、アプリ実行中のメモリの変動が表示されます。 グラフの急な上下動は、通常、何らかのコードがデータを収集または作成し、処理が終わったときにデータを破棄していることを示します。 大きな上下動は、最適化できる可能性がある領域を示しています。 より重大な問題は、使われたまま返されないメモリが増えることです。これは、メモリが効率的に使われていないか、メモリ リークが起きていることを示しているからです。  
  
### <a name="close-a-monitoring-session"></a><a name="BKMK_Close_a_monitoring_session"></a> 監視セッションを閉じる  
 ![コレクションの停止](../profiling/media/memuse-stopcollection.png "MEMUSE__StopCollection")  
  
 レポートを作成せずに監視セッションを停止する場合は、単に診断ウィンドウを閉じます。 メモリのスナップショットを取ったときにレポートを生成するには、**[停止]** をクリックします。  
  
## <a name="take-snapshots-of-the-memory-state-of-your-app"></a><a name="BKMK_Take_snapshots_to_analyze_the_memory_state_of_your_app"></a> アプリのメモリ状態のスナップショットを取る  
 調べる必要があるメモリの問題を見つけた場合は、特定の瞬間にメモリ内のオブジェクトをキャプチャするため、診断セッション中にスナップショットを取ることができます。 アプリではさまざまな型のオブジェクトが大量に使われるため、1 つのシナリオを集中的に分析することをお勧めします。 さらに、メモリの問題が起きる前にアプリのベースライン スナップショットを取り、初めて問題が起きた後でもう 1 回スナップショットを取り、さらにシナリオを反復できる場合は追加のスナップショットを 1 つ以上取ることをお勧めします。  
  
 スナップショットを収集するには、新しい診断セッションを開始します。 メモリのデータをキャプチャしたいときは **[スナップショットの取得]** をクリックします。 レポートを生成するには、**[停止]** をクリックします。  
  
## <a name="memory-usage-overview-page"></a><a name="BKMK_Memory_Usage_overview_page"></a>メモリ使用量の概要ページ  
 データ コレクションを停止すると、メモリ使用量ツールはアプリを停止し、概要レポートが表示されます。  
  
 ![メモリ使用量の概要ページ](../profiling/media/memuse-reportoverview.png "MEMUSE__ReportOverview")  
  
### <a name="memory-usage-snapshot-views"></a><a name="BKMK_Memory_Usage_snapshot_views"></a> メモリ使用量のスナップショット ビュー  
 Visual Studio の新しいウィンドウで詳しいレポートを開くには、スナップショット ビューを使います。 スナップショット ビューには次の 2 種類があります。  
  
- [スナップショットの詳細レポート](../profiling/memory-usage-without-debugging2.md#BKMK_Snapshot_details_reports)には、1 つのスナップショットに含まれる型とインスタンスが表示されます。  
  
- [スナップショットの相違 (diff) レポート](../profiling/memory-usage-without-debugging2.md#BKMK_Snapshot_difference__diff__reports)では、2 つのスナップショットに含まれる型とインスタンスが比較されます。  
  
  ![スナップショット表示のリンク](../profiling/media/memuse-snapshotview-numbered.png "MEMUSE__SnapshotView_Numbered")  
  
  スナップショット ビューの画像に番号を付けて示した項目は、メモリ使用量レポートのビューを開くリンクです。  
  
|||  
|-|-|  
|![ステップ 1](../profiling/media/procguid-1.png "ProcGuid_1")|このリンク テキストは、スナップショット取得時のメモリ内の合計バイト数を示します。<br /><br /> このリンクをクリックすると、スナップショットの詳細レポートが各型のインスタンスの合計サイズ順に並べ替えて表示されます。|  
|![ステップ 2](../profiling/media/procguid-2.png "ProcGuid_2")|このリンク テキストは、スナップショット取得時にメモリに含まれていたオブジェクトの総数を示します。<br /><br /> このリンクをクリックすると、スナップショットの詳細レポートが各型のインスタンス数の順に並べ替えて表示されます。|  
|![ステップ 3](../profiling/media/procguid-3.png "ProcGuid_3")|このリンク テキストは、このスナップショットを取った時点のメモリに含まれていたオブジェクトの合計サイズと前のスナップショットの合計サイズとの差を示します。<br /><br /> このリンク テキストは、このスナップショットのメモリサイズが前のサイズより大きい場合は正の数、小さい場合は負の数になります。 **[ベースライン]** というリンク テキストは、このスナップショットが診断セッションの最初のスナップショットであることを示します。**[相違なし]** は、差がゼロであることを示します。<br /><br /> このリンクをクリックすると、スナップショットの相違レポートが各型のインスタンスの合計サイズの差の順に並べ替えて表示されます。|  
|![ステップ 4](../profiling/media/procguid-4.png "ProcGuid_4")|このリンク テキストは、このスナップショットに含まれるメモリ オブジェクトの総数と前のスナップショットのオブジェクト数との差を示します。<br /><br /> このリンクをクリックすると、スナップショットの相違レポートが各型のインスタンスの総数の差の順に並べ替えて表示されます。|  
  
## <a name="snapshot-reports"></a><a name="BKMK_Snapshot_reports"></a> スナップショットのレポート  
 ![メモリ使用量のスナップショット レポート](../profiling/media/memuse-snapshotreport-all.png "MEMUSE_SnapshotReport_All")  
  
### <a name="snapshot-report-trees"></a><a name="BKMK_Snapshot_report_trees"></a> スナップショットのレポート ツリー  
  
#### <a name="managed-heap"></a><a name="BKMK_Managed_Heap"></a> マネージド ヒープ  
 マネージド ヒープのツリー [[マネージド ヒープ] ツリー (スナップショットの詳細)](../profiling/memory-usage-without-debugging2.md#BKMK_Managed_Heap_tree__Snapshot_details_) と [[マネージド ヒープ] ツリー (スナップショットの相違)](../profiling/memory-usage-without-debugging2.md#BKMK_Managed_Heap_tree__Snapshot_diff_) には、レポートに含まれる型とインスタンスが表示されます。 種類またはインスタンスを選ぶと、選んだ項目の **[ルートのパス]** ツリーと **[参照されたオブジェクト]** ツリーが表示されます。  
  
#### <a name="paths-to-root"></a><a name="BKMK_Paths_to_Root"></a> ルートのパス  
 [[ルートのパス] ツリー (スナップショットの詳細)](../profiling/memory-usage-without-debugging2.md#BKMK_Paths_to_Root_tree__Snapshot_details_) と [[ルートのパス] ツリー (スナップショットの相違)](../profiling/memory-usage-without-debugging2.md#BKMK_Paths_to_Root_tree__Snapshot_diff_) には、種類またはインスタンスを参照するオブジェクトのチェーンが表示されます。 .NET Framework のガベージ コレクターは、オブジェクトへの参照がすべて解放された場合にのみ、オブジェクトのメモリをクリーンアップします。  
  
#### <a name="referenced-objects"></a><a name="BKMK_Referenced_Objects"></a> 参照されたオブジェクト  
 [[参照されたオブジェクト] ツリー (スナップショットの詳細)](../profiling/memory-usage-without-debugging2.md#BKMK_Referenced_Objects_tree__Snapshot_details_) と [[参照されたオブジェクト] ツリー (スナップショットの相違)](../profiling/memory-usage-without-debugging2.md#BKMK_Referenced_Objects_tree__Snapshot_diff_) には、選んだ種類またはインスタンスによって参照されるオブジェクトが表示されます。  
  
### <a name="object-type-and-instance-fields"></a><a name="BKMK_Object_Type_and_Instance_fields"></a> [オブジェクトの種類] フィールドと [オブジェクト インスタンス] フィールド  
 **[オブジェクトの種類]** エントリに子エントリがある場合は、矢印アイコンをクリックして子エントリを表示できます。 **[オブジェクトの種類]** のテキストが青色の場合は、テキストをクリックすればソース コード ファイル内のオブジェクトに移動できます。 ソース ファイルは別のウィンドウで開きます。  
  
 インスタンス名は、メモリ使用量ツールで生成される一意の ID です。  
  
 容易に識別できない種類に気づいた場合や、それがどのようにコードに関わるのかわからない場合は、これはおそらく、.NET Framework、オペレーティング システム、またはコンパイラのオブジェクトであり、オブジェクトの所有権の継承に関わるためにメモリ使用量ツールに表示されているにすぎません。  
  
### <a name="report-tree-filters"></a><a name="BKMK_Report_tree_filters_"></a> レポート ツリーのフィルター  
 ほとんどのアプリには驚くほど多くの型が含まれていますが、そのほとんどはアプリの開発者にとってあまり重要ではありません。 **メモリ使用量**ツールには 2 つのフィルターが定義されており、**[マネージド ヒープ]** ツリーと **[ルートのパス]** ツリーでこれらの型のほとんどを非表示にできます。 型名でツリーをフィルター処理することもできます。  
  
 ![並べ替えとフィルターのオプション](../profiling/media/memuse-sortandfilter.png "MEMUSE_SortAndFilter")  
  
#### <a name="filter"></a><a name="BKMK_Filter"></a>フィルター  
 **[フィルター]** ボックスに文字列を入力して、指定したテキストを含む型だけをツリーに表示するよう制限します。 このフィルターでは、大文字と小文字は区別されず、指定された文字列が型名のどこかに含まれていれば認識されます。  
  
#### <a name="collapse-small-objects"></a><a name="BKMK_Collapse_Small_Objects"></a> 小さいオブジェクトの非表示  
 このフィルターを適用すると、**[サイズ (バイト)]** がスナップショット メモリの合計サイズの 0.5% を下回る型が **[マネージド ヒープ]** リストで非表示になります。  
  
#### <a name="just-my-code"></a><a name="BKMK_Just_My_Code"></a> マイ コードのみ  
 **[マイ コードのみ]** フィルターを適用すると、外部コードによって生成されたほとんどのインスタンスが非表示になります。 外部の型は、オペレーティング システムまたは Framework コンポーネントによって所有されるか、コンパイラによって生成されます。  
  
## <a name="snapshot-details-reports"></a><a name="BKMK_Snapshot_details_reports"></a>スナップショットの詳細レポート  
 診断セッションで得られた 1 つのスナップショットに注目する場合は、スナップショットの詳細レポートを使います。 詳細レポートを開くには、次の画像に示すように、スナップショット ビューに含まれるいずれかのリンクをクリックします。 どちらのリンクからも同じレポートが開きますが、レポート内の **[マネージド ヒープ]** ツリーを最初に表示したときの並べ替え順序だけが異なります。 どちらの場合も、レポートが開いた後で並べ替え順序を変更できます。  
  
 ![スナップショット ビューにあるスナップショット レポートへのリンク](../profiling/media/memuse-snapshotview-snapshotdetailslinks.png "MEMUSE_SnapshotView_SnapshotDetailsLinks")  
  
- **[MB]** リンクをクリックすると、**[包括サイズ (バイト)]** 列でレポートが並べ替えられます。  
  
- [**オブジェクト**のリンクを作成すると、**カウント**列によってレポートが並べ替えられます。  
  
### <a name="managed-heap-tree-snapshot-details"></a><a name="BKMK_Managed_Heap_tree__Snapshot_details_"></a> [マネージド ヒープ] ツリー (スナップショットの詳細)  
 **[マネージド ヒープ]** ツリーには、メモリ内に保持されているオブジェクトの種類が一覧表示されます。 型名を展開すると、サイズ順に、その型の最大のインスタンス 10 個が表示されます。 種類またはインスタンスを選ぶと、選んだ項目の **[ルートのパス]** ツリーと **[参照されたオブジェクト]** ツリーが表示されます。  
  
 ![マネージド ヒープ ツリー](../profiling/media/memuse-snapshotdetails-managedheaptree.png "MEMUSE__SnapshotDetails_ManagedHeapTree")  
  
|||  
|-|-|  
|**オブジェクトの種類**|型またはオブジェクト インスタンスの名前。|  
|**カウント**|型のオブジェクト インスタンス数。 インスタンスの場合、この数は常に 1 です。|  
|**サイズ (バイト)**|型の場合は、メモリのスナップショットに含まれるその型の全インスタンスのサイズ (インスタンスに含まれているオブジェクトのサイズは除く)。<br /><br /> インスタンスの場合は、オブジェクトのサイズ (インスタンスに含まれているオブジェクトのサイズは除く)。 インスタンス。|  
|**包括サイズ (バイト)**|型のインスタンスのサイズまたは単一インスタンスのサイズ (含まれているオブジェクトのサイズを含む)。|  
  
### <a name="paths-to-root-tree-snapshot-details"></a><a name="BKMK_Paths_to_Root_tree__Snapshot_details_"></a> [ルートのパス] ツリー (スナップショットの詳細)  
 **[ルートのパス] ツリー**には、種類またはインスタンスを参照するオブジェクトのチェーンが表示されます。 .NET Framework のガベージ コレクターは、オブジェクトへの参照がすべて解放された場合にのみ、オブジェクトのメモリをクリーンアップします。  
  
 ![型のルートへのパスツリー](../profiling/media/memuse-snapshotdetails-type-pathstoroottree.png "MEMUSE_SnapshotDetails_Type_PathsToRootTree")  
  
 **[ルートのパス]** ツリーに種類が表示されると、その種類への参照を保持する種類のオブジェクト数が **[参照数]** 列に表示されます。 この列は、インスタンスを分析するときには表示されません。  
  
### <a name="referenced-objects-tree-snapshot-details"></a><a name="BKMK_Referenced_Objects_tree__Snapshot_details_"></a> [参照されたオブジェクト] ツリー (スナップショットの詳細)  
 **[参照されたオブジェクト]** ツリーには、選んだ種類またはインスタンスによって参照されるオブジェクトが表示されます。  
  
 ![インスタンスの参照されたオブジェクト ツリー](../profiling/media/memuse-snapshotdetails-referencedobjects-instance.png "MEMUSE_SnapshotDetails_ReferencedObjects_Instance")  
  
|||  
|-|-|  
|**オブジェクトの種類 / インスタンス**|型またはオブジェクト インスタンスの名前。|  
|**サイズ (バイト)**|型の場合は、その型の全インスタンスのサイズ (型に含まれているオブジェクトのサイズは除く)。<br /><br /> インスタンスの場合は、オブジェクトのサイズ (オブジェクトに含まれているオブジェクトのサイズは除く)。|  
|**包括サイズ (バイト)**|型のインスタンスの合計サイズまたはインスタンスのサイズ (含まれているオブジェクトのサイズを含む)。|  
  
## <a name="snapshot-difference-diff-reports"></a><a name="BKMK_Snapshot_difference__diff__reports"></a>スナップショットの相違 (diff) レポート  
 スナップショットの相違 (diff) レポートには、指定したスナップショットとその直前に取られたスナップショットの変更点が表示されます。 相違レポートを開くには、次の画像に示すように、スナップショット ビューに含まれるいずれかのリンクをクリックします。 どちらのリンクからも同じレポートが開きますが、レポート内の **[マネージド ヒープ]** ツリーを最初に表示したときの並べ替え順序だけが異なります。 レポートが開いた後で並べ替え順序を変更できます。  
  
 ![スナップショット ビューにある差分レポートへのリンク](../profiling/media/memuse-snapshotview-snapshotdifflinks.png "MEMUSE_SnapshotView_SnapshotDiffLinks")  
  
- **[MB]** リンクをクリックすると、**[包括サイズ (バイト)]** 列でレポートが並べ替えられます。  
  
- [**オブジェクト**のリンクを作成すると、**カウント**列によってレポートが並べ替えられます。  
  
### <a name="managed-heap-tree-snapshot-diff"></a><a name="BKMK_Managed_Heap_tree__Snapshot_diff_"></a> [マネージド ヒープ] ツリー (スナップショットの相違)  
 **[マネージド ヒープ]** ツリーには、メモリ内に保持されているオブジェクトの種類が一覧表示されます。 型名を展開すると、サイズ順に、その型の最大のインスタンス 10 個が表示されます。 種類またはインスタンスを選ぶと、選んだ項目の **[ルートのパス]** ツリーと **[参照されたオブジェクト]** ツリーが表示されます。  
  
 ![相違レポートにある種類のマネージド ヒープ ツリー](../profiling/media/memuse-snapshotdiff-type-heap.png "MEMUSE_SnapshotDiff_Type_Heap")  
  
 この画像で、**[カウント]**、**[サイズ (バイト)]**、**[包括サイズ (バイト)]** の各列が非表示になっている点にご注意ください。  
  
|||  
|-|-|  
|**オブジェクトの種類**|型またはオブジェクト インスタンスの名前。|  
|**カウント**|指定したスナップショットに含まれる型のインスタンス数。 インスタンスの場合、 **[カウント]** は常に 1 です。|  
|**数の相違**|型の場合は、指定したスナップショットと前のスナップショットとの、型のインスタンス数の差。 インスタンスの場合、このフィールドは空白です。|  
|**サイズ (バイト)**|指定したスナップショットに含まれているオブジェクトのサイズ (オブジェクトに含まれているオブジェクトのサイズは除く)。 型の場合、 **[サイズ (バイト)]** と **[包含サイズ (バイト)]** は型インスタンスの合計サイズです。|  
|**合計サイズの相違 (バイト)**|型の場合は、指定したスナップショットと前のスナップショットとの、その型のインスタンスの合計サイズの差 (インスタンスに含まれているオブジェクトのサイズは除く)。 インスタンスの場合、このフィールドは空白です。|  
|**包括サイズ (バイト)**|指定したスナップショットに含まれているオブジェクトのサイズ (オブジェクトに含まれているオブジェクトのサイズを含む)。|  
|**包括サイズの相違 (バイト)**|型の場合は、指定したスナップショットと前のスナップショットとの、その型の全インスタンスのサイズの差 (オブジェクトに含まれているオブジェクトのサイズを含む)。 インスタンスの場合、このフィールドは空白です。|  
  
### <a name="paths-to-root-tree-snapshot-diff"></a><a name="BKMK_Paths_to_Root_tree__Snapshot_diff_"></a> [ルートのパス] ツリー (スナップショットの相違)  
 **[ルートのパス] ツリー**には、種類またはインスタンスを参照するオブジェクトのチェーンが表示されます。 .NET Framework のガベージ コレクターは、オブジェクトへの参照がすべて解放された場合にのみ、オブジェクトのメモリをクリーンアップします。  
  
 ![差分ビューのインスタンスにあるルートへのパス ツリー](../profiling/media/memuse-snapshotdiff-pathstoroot-instance-all.png "MEMUSE_SnapshotDiff_PathsToRoot_Instance_All")  
  
### <a name="referenced-objects-tree-snapshot-diff"></a><a name="BKMK_Referenced_Objects_tree__Snapshot_diff_"></a> [参照されたオブジェクト] ツリー (スナップショットの相違)  
 **[参照されたオブジェクト]** ツリーには、主要な種類またはインスタンスによって参照されるオブジェクトが表示されます。  
  
 ![インスタンスの参照されたオブジェクト ツリー](../profiling/media/memuse-snapshotdetails-referencedobjects-instance.png "MEMUSE_SnapshotDetails_ReferencedObjects_Instance")  
  
|||  
|-|-|  
|**オブジェクトの種類 / インスタンス**|型またはオブジェクト インスタンスの名前。|  
|**サイズ (バイト)**|インスタンスの場合は、指定したスナップショットに含まれるオブジェクトのサイズ (インスタンスに含まれているオブジェクトのサイズは除く)。<br /><br /> 型の場合は、指定したスナップショットに含まれるその型のインスタンスの合計サイズ (インスタンスに含まれているオブジェクトのサイズは除く)。|  
|**包括サイズ (バイト)**|指定したスナップショットに含まれているオブジェクトのサイズ (オブジェクトに含まれているオブジェクトのサイズを含む)。|  
  
## <a name="see-also"></a>参照  
 [JavaScript メモリ](../profiling/javascript-memory.md)   
 [アプリのパフォーマンスの分析](https://msdn.microsoft.com/library/58acb30b-8428-41a6-b195-b0fdedb89575)   
 [パフォーマンスと診断ツールの実行](https://msdn.microsoft.com/library/788279d8-f56b-40a0-9bef-facc3dfba471)   
 [C++、C#、および Visual Basic を使用した Windows ストアアプリのパフォーマンスのベストプラクティス](https://msdn.microsoft.com/library/windows/apps/hh750313.aspx)   
 [Visual Studio の新しいメモリ使用量ツールでメモリの問題を診断する](https://devblogs.microsoft.com/devops/diagnosing-memory-issues-with-the-new-memory-usage-tool-in-visual-studio/)
