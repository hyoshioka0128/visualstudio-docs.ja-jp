---
title: Analyze .NET Framework memory issues | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
f1_keywords:
- vs.diagnostics.managedmemoryanalysis
ms.assetid: 43341928-9930-48cf-a57f-ddcc3984b787
caps.latest.revision: 9
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: e94edbeac381ac634171507766126ab954153eb1
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74295894"
---
# <a name="analyze-net-framework-memory-issues"></a>.Net Framework のメモリ分析の問題
Visual Studio マネージド メモリ アナライザーを使用して、.NET Framework コードでのメモリ リークおよび非効率的なメモリの使用を検出します。 対象コードの最低限の .NET Framework バージョンは .NET Framework 4.5 です。  
  
 The memory analysis tool analyzes information in *dump files with heap data* that a copy of the objects in an app's memory. ダンプ (.dmp) ファイルは、Visual Studio IDE から収集することも、その他のシステム ツールを使用して収集することもできます。  
  
- 単一のスナップショットを分析することにより、オブジェクト型のメモリ使用に対する相対的な影響を理解し、アプリ内でメモリが効率的に使用されていないコードを検出することができます。  
  
- You can also compare (*diff*) two snapshots of an app to find areas in your code that cause the memory use to increase over time.  
  
  For a walkthrough of the managed memory analyzer, see [Using Visual Studio 2013 to Diagnose .NET Memory Issues in Production](https://devblogs.microsoft.com/devops/using-visual-studio-2013-to-diagnose-net-memory-issues-in-production/) on the Visual Studio ALM + Team Foundation Server blog .  
  
## <a name="BKMK_Contents"></a> 目次  
 [Memory use in .NET Framework apps](#BKMK_Memory_use_in__NET_Framework_apps)  
  
 [Identify a memory issue in an app](#BKMK_Identify_a_memory_issue_in_an_app)  
  
 [Collect memory snapshots](#BKMK_Collect_memory_snapshots)  
  
 [Analyze memory use](#BKMK_Analyze_memory_use)  
  
## <a name="BKMK_Memory_use_in__NET_Framework_apps"></a> Memory use in .NET Framework apps  
 .NET Framework はガベージ コレクションが実行されるランタイムであるため、ほとんどのアプリでメモリの使用が問題になりません。 ただし、Web サービスや Web アプリケーションなどの長時間実行されるアプリケーションおよびメモリ量に制限があるデバイスでは、メモリ内にオブジェクトが蓄積されると、アプリのパフォーマンスや、そのアプリを実行するデバイスのパフォーマンスに影響することがあります。 メモリが過剰に使用されると、ガベージ コレクターの実行頻度が高すぎる場合や、オペレーティング システムが RAM とディスクとの間でメモリを移動せざるを得ない場合、アプリケーションやコンピューターのリソースが不足する可能性があります。 最悪の場合、"メモリ不足" 例外によってアプリがクラッシュすることもあります。  
  
 The .NET *managed heap* is a region of virtual memory where reference objects created by an app are stored. オブジェクトの有効期間はガベージ コレクター (GC) によって管理されます。 ガベージ コレクターは参照を使用して、メモリ ブロックを占有するオブジェクトを追跡します。 参照は、オブジェクトが作成され変数に割り当てられると、作成されます。 単一のオブジェクトに対して、複数の参照を作成することもできます。 たとえば、クラス、コレクション、またはその他のデータ構造にオブジェクトを追加するか、2 つ目の変数にオブジェクトを割り当てると、オブジェクトへの追加の参照が作成されます。 明示的な方法ではありませんが、あるオブジェクトでイベント ハンドラーを別のオブジェクトのイベントに追加した場合も、参照が作成されます。 この場合、ハンドラーが明示的に削除されるか 2 つ目のオブジェクトが破棄されるまで、最初のオブジェクトへの参照が 2 つ目のオブジェクトに保持されます。  
  
 各アプリケーションについて、GC では、アプリケーションから参照されるオブジェクトを追跡する参照ツリーが管理されます。 The *reference tree* has a set of roots, which includes global and static objects, as well as associated thread stacks and dynamically instantiated objects. オブジェクトへの参照を持つ 1 つ以上の親オブジェクトがある場合、そのオブジェクトではルートが作成されます。 GC は、アプリケーション内の他のオブジェクトまたは変数から参照されていない場合にのみ、そのオブジェクトのメモリを再利用できます。  
  
 ![Back to top](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [Contents](#BKMK_Contents)  
  
## <a name="BKMK_Identify_a_memory_issue_in_an_app"></a> Identify a memory issue in an app  
 メモリに関する問題の最も可視的な兆候は、アプリのパフォーマンスです (特に、時間の経過に伴ってパフォーマンスが低下する場合)。 特定のアプリの実行中に他のアプリのパフォーマンスが低下した場合も、メモリの問題を示している可能性があります。 If you suspect a memory issue, use a tool like Task Manager or [Windows Performance Monitor](https://technet.microsoft.com/library/cc749249.aspx) to investigate further. たとえば、考えられるメモリ リークの原因として、説明が付かないような合計メモリ サイズの増加がないか確認します。  
  
 ![Consistent memory growth in Resource Monitor](../misc/media/mngdmem-resourcemanagerconsistentgrowth.png "MNGDMEM_ResourceManagerConsistentGrowth")  
  
 また、コードについて認識しているより明らかに大きいメモリ スパイクに気付くことがあります。このような場合は、プロシージャ内での非効率的なメモリの使用を示している可能性があります。  
  
 ![Memory spikes in Resource Manager](../misc/media/mngdmem-resourcemanagerspikes.png "MNGDMEM_ResourceManagerSpikes")  
  
## <a name="BKMK_Collect_memory_snapshots"></a> Collect memory snapshots  
 The memory analysis tool analyzes information in *dump files* that contain heap information. You can create dump files in Visual Studio, or you can use a tool like [ProcDump](https://technet.microsoft.com/sysinternals/dd996900.aspx) from [Windows Sysinternals](https://technet.microsoft.com/sysinternals). See [What is a dump, and how do I create one?](https://blogs.msdn.microsoft.com/debugger/2009/12/30/what-is-a-dump-and-how-do-i-create-one/) on the Visual Studio Debugger Team blog.  
  
> [!NOTE]
> ほとんどのツールでは、完全なヒープ メモリ データの有無に関係なくダンプ情報を収集できます。 Visual Studio メモリ アナライザーでは、完全なヒープ情報が求められます。  
  
 **To collect a dump from Visual Studio**  
  
1. Visual Studio プロジェクトから開始されたプロセスのダンプ ファイルを作成することも、実行中のプロセスにデバッガーをアタッチすることもできます。 See [Attach to Running Processes](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md).  
  
2. 実行を停止します。 The debugger stops when you choose **Break All** on the **Debug** menu, or at an exception or at a breakpoint  
  
3. On the **Debug** menu, choose **Save Dump As**. In the **Save Dump As** dialog box, specify a location and make sure that **Minidump with Heap** (the default) is selected in the **Save as type** list.  
  
   **To compare two memory snapshots**  
  
   アプリでのメモリ使用量の増加を分析するには、アプリの単一インスタンスから 2 つのダンプ ファイルを収集します。  
  
   ![Back to top](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [Contents](#BKMK_Contents)  
  
## <a name="BKMK_Analyze_memory_use"></a> Analyze memory use  
 [Filter the list of objects](#BKMK_Filter_the_list_of_objects) **&#124;** [Analyze memory data in from a single snapshot](#BKMK_Analyze_memory_data_in_from_a_single_snapshot) **&#124;** [Compare two memory snapshots](#BKMK_Compare_two_memory_snapshots)  
  
 ダンプ ファイルでメモリ使用に関する問題を分析するには:  
  
1. In Visual Studio, choose **File**, **Open** and specify the dump file.  
  
2. On the **Minidump File Summary** page, choose **Debug Managed Memory**.  
  
    ![Dump file summary page](../misc/media/mngdmem-dumpfilesummary.png "MNGDMEM_DumpFileSummary")  
  
   メモリ アナライザーによるデバッグ セッションが開始し、ファイルの分析が行われ、[ヒープの表示] ページに結果が表示されます。  
  
   ![Back to top](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [Contents](#BKMK_Contents)  
  
### <a name="BKMK_Filter_the_list_of_objects"></a> Filter the list of objects  
 メモリ アナライザーの既定では、メモリ スナップショット内のオブジェクト一覧がフィルター処理されます。これにより、ユーザー コードの型とインスタンスのみを対象とし、合計ヒープ サイズのパーセンテージで表したしきい値を超える合計包括サイズの型のみが表示されます。 You can change these options in the **View Settings** list:  
  
|||  
|-|-|  
|**マイ コードのみを有効にする**|[マイ コードのみ] では、独自に作成した型のみを一覧に表示するために、ほとんどの一般的なシステム オブジェクトが非表示になります。<br /><br /> You can also set the Just My Code option in the Visual Studio **Options** dialog box. **[デバッグ]** メニューの **[オプションと設定]** をクリックします。 In the **Debugging**/**General** tab, choose or clear **Just My Code**.|  
|**Collapse Small Objects**|**Collapse Small Objects** hides all types whose total inclusive size is less than 0.5 percent of the total heap size.|  
  
 You can also filter the type list by entering a string in the **Search** box. 一覧には、この文字列が名前に含まれる型のみが表示されます。  
  
 ![Back to top](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [Contents](#BKMK_Contents)  
  
### <a name="BKMK_Analyze_memory_data_in_from_a_single_snapshot"></a> Analyze memory data in from a single snapshot  
 Visual Studio による新しいデバッグ セッションが開始し、ファイルの分析が行われ、[ヒープの表示] ページにメモリ データが表示されます。  
  
 ![The Object Type list](../misc/media/dbg-mma-objecttypelist.png "DBG_MMA_ObjectTypeList")  
  
 ![Back to top](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [Contents](#BKMK_Contents)  
  
#### <a name="object-type-table"></a>オブジェクトの型テーブル  
 最上部のテーブルには、メモリ内に保持されているオブジェクトの型が一覧表示されます。  
  
- **Count** shows the number of instances of the type in the snapshot.  
  
- **Size (Bytes)** is the size of the all instances of the type, excluding the size of objects it holds references to. 次に、  
  
- **Inclusive Size (Bytes)** includes the sizes of referenced objects.  
  
  You can choose the instances icon (![The instance icon in the Object Type column](../misc/media/dbg-mma-instancesicon.png "DBG_MMA_InstancesIcon")) in the **Object Type** column to view a list of the instances of the type.  
  
#### <a name="instance-table"></a>インスタンス テーブル  
 ![Instances table](../misc/media/dbg-mma-instancestable.png "DBG_MMA_InstancesTable")  
  
- **Instance** is the memory location of the object that serves as the object identifier of the object  
  
- **Value** shows the actual value of value types. 参照される型の名前の上にポインターを合わせると、データヒントでそのデータ値を確認できます。  
  
   ![Instance values in a data tip](../misc/media/dbg-mma-instancevaluesindatatip.png "DBG_MMA_InstanceValuesInDataTip")  
  
- **Size (Bytes)** is the size of the object, excluding the size of objects it holds references to. 次に、  
  
- **Inclusive Size (Bytes)** includes the sizes of referenced objects.  
  
  By default, types and instances are sorted by **Inclusive Size (Bytes)** . 並べ替え順序を変更するには、一覧の列ヘッダーを選択します。  
  
#### <a name="paths-to-root"></a>ルートのパス  
  
- For a type selected from the **Object Type** table, the **Paths to Root** table shows the unique type hierarchies that lead to root objects for all objects of the type, along with the number of references to the type that is above it in the hierarchy.  
  
- For an object selected from the instance of a type, **Paths to Root** shows a graph of the actual objects that hold a reference to the instance. オブジェクトの名前の上にポインターを合わせると、データヒントでそのデータ値を確認できます。  
  
#### <a name="referenced-types--referenced-objects"></a>参照される型/参照されるオブジェクト  
  
- For a type selected from the **Object Type** table, the **Referenced Types** tab shows the size and number of referenced types held by all objects of the selected type.  
  
- For a selected instance of a type, **Referenced Objects** shows the objects that are held by the selected instance. 名前の上にポインターを合わせると、データヒントでそのデータ値を確認できます。  
  
  **Circular references**  
  
  オブジェクトでは、直接的または間接的に 1 つ目のオブジェクトへの参照を保持する 2 つ目のオブジェクトを参照している可能性があります。 When the memory analyzer encounters this situation, it stops expanding the reference path and adds a **[Cycle Detected]** annotation to the listing of the first object and stops.  
  
  **Root types**  
  
  メモリ アナライザーでは、保持されている参照の種類を示す注釈がルート オブジェクトに追加されます。  
  
|注釈|説明|  
|----------------|-----------------|  
|**Static variable** `VariableName`|静的変数。 `VariableName` は変数の名前です。|  
|**Finalization Handle**|ファイナライザー キューからの参照。|  
|**Local Variable**|ローカル変数。|  
|**Strong Handle**|オブジェクト ハンドル テーブルからの強い参照へのハンドル。|  
|**Async. Pinned Handle**|オブジェクト ハンドル テーブルからの非同期固定オブジェクト。|  
|**Dependent Handle**|オブジェクト ハンドル テーブルからの依存オブジェクト。|  
|**Pinned Handle**|オブジェクト ハンドル テーブルからの固定された強い参照。|  
|**RefCount Handle**|オブジェクト ハンドル テーブルからの参照カウントされたオブジェクト。|  
|**SizedRef Handle**|ガベージ コレクション時に、すべてのオブジェクトおよびオブジェクト ルートの集合的なクロージャの概算サイズを保持する強力なハンドル。|  
|**Pinned local variable**|ピンされたローカル変数。|  
  
### <a name="BKMK_Compare_two_memory_snapshots"></a> Compare two memory snapshots  
 メモリ リークの原因である可能性のあるオブジェクトを見つけるために、プロセスに関する 2 つのダンプ ファイルを比較できます。 リークしているオブジェクトの数の増加をわかりやすくするために、1 つ目 (1 回目) と 2 つ目 (2 回目) のファイルを収集する時間間隔は十分長くする必要があります。 2 つのファイルを比較するには:  
  
1. Open the second dump file, and then choose **Debug Managed Memory** on the **Minidump File Summary** page.  
  
2. On the memory analysis report page, open the **Select baseline** list, and then choose **Browse** to specify the first dump file.  
  
   The analyzer adds columns to the top pane of the report that display the difference between the **Count**, **Size**, and **Inclusive Size** of the types to those values in the earlier snapshot.  
  
   ![Diff columns in the type list](../misc/media/mngdmem-diffcolumns.png "MNGDMEM_DiffColumns")  
  
   A **Reference Count Diff** column is also added to the **Paths to Root** table.  
  
   ![Back to top](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [Contents](#BKMK_Contents)  
  
## <a name="see-also"></a>参照  
 [VS ALM TFS Blog: Using Visual Studio 2013 to Diagnose .NET Memory Issues in Production](https://devblogs.microsoft.com/devops/using-visual-studio-2013-to-diagnose-net-memory-issues-in-production/)   
 [Channel 9 &#124; Visual Studio TV &#124; Managed Memory Analysis](https://channel9.msdn.com/Series/Visual-Studio-2012-Premium-and-Ultimate-Overview/Managed-Memory-Analysis)   
 [Channel 9 &#124; Visual Studio Toolbox &#124; Managed Memory Analysis in Visual Studio 2013](https://channel9.msdn.com/Shows/Visual-Studio-Toolbox/Managed-Memory-Analysis-in-Visual-Studio-2013)
