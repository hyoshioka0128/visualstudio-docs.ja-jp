---
title: .NET Framework メモリの問題を分析する |Microsoft Docs
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
ms.openlocfilehash: e89b3f04a3e0e1dcd0cc29e57e09b1c71fbc2279
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85545549"
---
# <a name="analyze-net-framework-memory-issues"></a>.Net Framework のメモリ分析の問題
Visual Studio マネージド メモリ アナライザーを使用して、.NET Framework コードでのメモリ リークおよび非効率的なメモリの使用を検出します。 対象コードの最低限の .NET Framework バージョンは .NET Framework 4.5 です。  
  
 メモリ分析ツールは、アプリのメモリ内のオブジェクトのコピーである *ヒープデータを使用してダンプファイル* 内の情報を分析します。 ダンプ (.dmp) ファイルは、Visual Studio IDE から収集することも、その他のシステム ツールを使用して収集することもできます。  
  
- 単一のスナップショットを分析することにより、オブジェクト型のメモリ使用に対する相対的な影響を理解し、アプリ内でメモリが効率的に使用されていないコードを検出することができます。  
  
- また、アプリの2つのスナップショットを比較 (*diff*) して、メモリ使用量が時間の経過と共に増加するコード内の領域を見つけることもできます。  
  
  マネージメモリアナライザーのチュートリアルについては、Visual Studio ALM + Team Foundation Server ブログの「Visual Studio 2013 を使用した [実稼働環境での .Net メモリの問題の診断](https://devblogs.microsoft.com/devops/using-visual-studio-2013-to-diagnose-net-memory-issues-in-production/) 」を参照してください。  
  
## <a name="contents"></a><a name="BKMK_Contents"></a> 目次  
 [.NET Framework アプリでのメモリ使用](#BKMK_Memory_use_in__NET_Framework_apps)  
  
 [アプリのメモリの問題を特定する](#BKMK_Identify_a_memory_issue_in_an_app)  
  
 [メモリのスナップショットの収集](#BKMK_Collect_memory_snapshots)  
  
 [メモリ使用量の分析](#BKMK_Analyze_memory_use)  
  
## <a name="memory-use-in-net-framework-apps"></a><a name="BKMK_Memory_use_in__NET_Framework_apps"></a> .NET Framework アプリでのメモリ使用量  
 .NET Framework はガベージ コレクションが実行されるランタイムであるため、ほとんどのアプリでメモリの使用が問題になりません。 ただし、Web サービスや Web アプリケーションなどの長時間実行されるアプリケーションおよびメモリ量に制限があるデバイスでは、メモリ内にオブジェクトが蓄積されると、アプリのパフォーマンスや、そのアプリを実行するデバイスのパフォーマンスに影響することがあります。 メモリが過剰に使用されると、ガベージ コレクターの実行頻度が高すぎる場合や、オペレーティング システムが RAM とディスクとの間でメモリを移動せざるを得ない場合、アプリケーションやコンピューターのリソースが不足する可能性があります。 最悪の場合、"メモリ不足" 例外によってアプリがクラッシュすることもあります。  
  
 .NET *マネージヒープ* は、アプリによって作成された参照オブジェクトが格納される仮想メモリの領域です。 オブジェクトの有効期間はガベージ コレクター (GC) によって管理されます。 ガベージ コレクターは参照を使用して、メモリ ブロックを占有するオブジェクトを追跡します。 参照は、オブジェクトが作成され変数に割り当てられると、作成されます。 単一のオブジェクトに対して、複数の参照を作成することもできます。 たとえば、クラス、コレクション、またはその他のデータ構造にオブジェクトを追加するか、2 つ目の変数にオブジェクトを割り当てると、オブジェクトへの追加の参照が作成されます。 明示的な方法ではありませんが、あるオブジェクトでイベント ハンドラーを別のオブジェクトのイベントに追加した場合も、参照が作成されます。 この場合、ハンドラーが明示的に削除されるか 2 つ目のオブジェクトが破棄されるまで、最初のオブジェクトへの参照が 2 つ目のオブジェクトに保持されます。  
  
 各アプリケーションについて、GC では、アプリケーションから参照されるオブジェクトを追跡する参照ツリーが管理されます。 *参照ツリー*には、グローバルオブジェクトと静的オブジェクト、関連するスレッドスタック、および動的にインスタンス化されたオブジェクトを含む、一連のルートがあります。 オブジェクトへの参照を持つ 1 つ以上の親オブジェクトがある場合、そのオブジェクトではルートが作成されます。 GC は、アプリケーション内の他のオブジェクトまたは変数から参照されていない場合にのみ、そのオブジェクトのメモリを再利用できます。  
  
 ![ページのトップへ](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [目次](#BKMK_Contents)  
  
## <a name="identify-a-memory-issue-in-an-app"></a><a name="BKMK_Identify_a_memory_issue_in_an_app"></a> アプリのメモリの問題を特定する  
 メモリに関する問題の最も可視的な兆候は、アプリのパフォーマンスです (特に、時間の経過に伴ってパフォーマンスが低下する場合)。 特定のアプリの実行中に他のアプリのパフォーマンスが低下した場合も、メモリの問題を示している可能性があります。 メモリに問題があると思われる場合は、タスクマネージャーや [Windows パフォーマンスモニター](https://technet.microsoft.com/library/cc749249.aspx) などのツールを使用してさらに調査してください。 たとえば、考えられるメモリ リークの原因として、説明が付かないような合計メモリ サイズの増加がないか確認します。  
  
 ![[リソース モニター] 内での一貫したメモリの増加](../misc/media/mngdmem-resourcemanagerconsistentgrowth.png "MNGDMEM_ResourceManagerConsistentGrowth")  
  
 また、コードについて認識しているより明らかに大きいメモリ スパイクに気付くことがあります。このような場合は、プロシージャ内での非効率的なメモリの使用を示している可能性があります。  
  
 ![[リソース マネージャー] 内でのメモリの急増](../misc/media/mngdmem-resourcemanagerspikes.png "MNGDMEM_ResourceManagerSpikes")  
  
## <a name="collect-memory-snapshots"></a><a name="BKMK_Collect_memory_snapshots"></a> メモリのスナップショットの収集  
 メモリ分析ツールは、ヒープ情報を含む *ダンプファイル* 内の情報を分析します。 Visual Studio でダンプファイルを作成することも、 [Windows Sysinternals](https://technet.microsoft.com/sysinternals)から[ProcDump](https://technet.microsoft.com/sysinternals/dd996900.aspx)などのツールを使用することもできます。 Visual Studio デバッガーチームのブログで、ダンプの概要 [と作成方法](https://blogs.msdn.microsoft.com/debugger/2009/12/30/what-is-a-dump-and-how-do-i-create-one/) を確認してください。  
  
> [!NOTE]
> ほとんどのツールでは、完全なヒープ メモリ データの有無に関係なくダンプ情報を収集できます。 Visual Studio メモリ アナライザーでは、完全なヒープ情報が求められます。  
  
 **Visual Studio からダンプを収集するには**  
  
1. Visual Studio プロジェクトから開始されたプロセスのダンプ ファイルを作成することも、実行中のプロセスにデバッガーをアタッチすることもできます。 「 [実行中のプロセスへのアタッチ」を](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)参照してください。  
  
2. 実行を停止します。 デバッガーは、[**デバッグ**] メニューの [**すべて中断**] をクリックしたとき、または例外またはブレークポイントで [中断] をクリックすると停止します。  
  
3. [ **デバッグ** ] メニューの [ **名前を付けてダンプを保存**] をクリックします。 [名前を付け**てダンプを保存**] ダイアログボックスで、場所を指定し、[**ファイルの種類**] ボックスの一覧で [**ヒープ付きミニダンプ**] (既定) が選択されていることを確認します。  
  
   **2 つのメモリ スナップショットを比較するには**  
  
   アプリでのメモリ使用量の増加を分析するには、アプリの単一インスタンスから 2 つのダンプ ファイルを収集します。  
  
   ![ページのトップへ](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [目次](#BKMK_Contents)  
  
## <a name="analyze-memory-use"></a><a name="BKMK_Analyze_memory_use"></a> メモリ使用量の分析  
 1つの[スナップショットからメモリデータを分析](#BKMK_Analyze_memory_data_in_from_a_single_snapshot) **&#124;** [オブジェクトの一覧をフィルター処理して、](#BKMK_Filter_the_list_of_objects) [2 つのメモリスナップショットを比較](#BKMK_Compare_two_memory_snapshots) **&#124;**  
  
 ダンプ ファイルでメモリ使用に関する問題を分析するには:  
  
1. Visual Studio で、[ **ファイル**]、[ **開く** ] の順に選択し、ダンプファイルを指定します。  
  
2. [ **ミニダンプファイルの概要** ] ページで、[ **マネージメモリのデバッグ**] を選択します。  
  
    ![ダンプ ファイル概要ページ](../misc/media/mngdmem-dumpfilesummary.png "MNGDMEM_DumpFileSummary")  
  
   メモリ アナライザーによるデバッグ セッションが開始し、ファイルの分析が行われ、[ヒープの表示] ページに結果が表示されます。  
  
   ![ページのトップへ](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [目次](#BKMK_Contents)  
  
### <a name="filter-the-list-of-objects"></a><a name="BKMK_Filter_the_list_of_objects"></a> オブジェクトの一覧をフィルター処理する  
 メモリ アナライザーの既定では、メモリ スナップショット内のオブジェクト一覧がフィルター処理されます。これにより、ユーザー コードの型とインスタンスのみを対象とし、合計ヒープ サイズのパーセンテージで表したしきい値を超える合計包括サイズの型のみが表示されます。 [ **表示設定** ] の一覧では、次のオプションを変更できます。  
  
|名前|説明|  
|-|-|  
|**マイ コードのみを有効にする**|[マイ コードのみ] では、独自に作成した型のみを一覧に表示するために、ほとんどの一般的なシステム オブジェクトが非表示になります。<br /><br /> また、Visual Studio の [ **オプション** ] ダイアログボックスでマイコードのみオプションを設定することもできます。 **[デバッグ]** メニューの **[オプションと設定]** をクリックします。 [**デバッグ**の / **全般**] タブで、[**マイコードのみ**をオンまたはオフにします。|  
|**小さいオブジェクトを折りたたむ**|[**小さいオブジェクトを折りたたむ**。合計包括サイズが合計ヒープサイズの0.5% 未満であるすべての型を非表示にします。|  
  
 **検索**ボックスに文字列を入力して、型の一覧をフィルター処理することもできます。 一覧には、この文字列が名前に含まれる型のみが表示されます。  
  
 ![ページのトップへ](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [目次](#BKMK_Contents)  
  
### <a name="analyze-memory-data-in-from-a-single-snapshot"></a><a name="BKMK_Analyze_memory_data_in_from_a_single_snapshot"></a> 1つのスナップショットからのメモリデータの分析  
 Visual Studio による新しいデバッグ セッションが開始し、ファイルの分析が行われ、[ヒープの表示] ページにメモリ データが表示されます。  
  
 ![オブジェクト型リスト](../misc/media/dbg-mma-objecttypelist.png "DBG_MMA_ObjectTypeList")  
  
 ![ページのトップへ](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [目次](#BKMK_Contents)  
  
#### <a name="object-type-table"></a>オブジェクトの型テーブル  
 最上部のテーブルには、メモリ内に保持されているオブジェクトの型が一覧表示されます。  
  
- **カウント** は、スナップショット内の型のインスタンスの数を示します。  
  
- **Size (バイト)** は、参照を保持しているオブジェクトのサイズを除く、型のすべてのインスタンスのサイズです。 その  
  
- **包括サイズ (バイト)** には、参照されるオブジェクトのサイズが含まれます。  
  
  [**オブジェクトの種類**] 列の [インスタンス] アイコン ([![オブジェクトの種類] 列のインスタンスアイコン](../misc/media/dbg-mma-instancesicon.png "DBG_MMA_InstancesIcon")) をクリックすると、その型のインスタンスの一覧が表示されます。  
  
#### <a name="instance-table"></a>インスタンス テーブル  
 ![インスタンス テーブル](../misc/media/dbg-mma-instancestable.png "DBG_MMA_InstancesTable")  
  
- **Instance** は、オブジェクトのオブジェクト識別子として機能するオブジェクトのメモリ位置です。  
  
- **値は** 、値型の実際の値を示します。 参照される型の名前の上にポインターを合わせると、データヒントでそのデータ値を確認できます。  
  
   ![データのヒントにあるインスタンスの値](../misc/media/dbg-mma-instancevaluesindatatip.png "DBG_MMA_InstanceValuesInDataTip")  
  
- **Size (バイト)** は、オブジェクトのサイズ (参照を保持しているオブジェクトのサイズは除く) です。 その  
  
- **包括サイズ (バイト)** には、参照されるオブジェクトのサイズが含まれます。  
  
  既定では、型とインスタンスは **包括サイズ (バイト)** で並べ替えられます。 並べ替え順序を変更するには、一覧の列ヘッダーを選択します。  
  
#### <a name="paths-to-root"></a>ルートのパス  
  
- [ **オブジェクトの種類** ] テーブルから選択された型の場合、[ **ルートのパス** ] テーブルには、その型のすべてのオブジェクトのルートオブジェクトを表す一意の型階層と、階層内で上位にある型への参照の数が表示されます。  
  
- 型のインスタンスから選択されたオブジェクトの場合、 **ルートへのパス** には、インスタンスへの参照を保持する実際のオブジェクトのグラフが表示されます。 オブジェクトの名前の上にポインターを合わせると、データヒントでそのデータ値を確認できます。  
  
#### <a name="referenced-types--referenced-objects"></a>参照される型/参照されるオブジェクト  
  
- [ **オブジェクトの種類** ] テーブルから選択された型の場合、[参照される **型** ] タブには、選択した型のすべてのオブジェクトに保持されている参照先の型のサイズと数が表示されます。  
  
- 型のインスタンスが選択されている場合、[参照された **オブジェクト** ] には、選択したインスタンスによって保持されているオブジェクトが表示されます。 名前の上にポインターを合わせると、データヒントでそのデータ値を確認できます。  
  
  **循環参照**  
  
  オブジェクトでは、直接的または間接的に 1 つ目のオブジェクトへの参照を保持する 2 つ目のオブジェクトを参照している可能性があります。 メモリアナライザーは、このような状況を検出すると、参照パスの展開を停止し、最初のオブジェクトの一覧に **[Cycle が検出されました]** という注釈を追加して、停止します。  
  
  **ルート型**  
  
  メモリ アナライザーでは、保持されている参照の種類を示す注釈がルート オブジェクトに追加されます。  
  
|注釈|説明|  
|----------------|-----------------|  
|**静的変数** `VariableName`|静的変数。 `VariableName` は変数の名前です。|  
|**終了処理ハンドル**|ファイナライザー キューからの参照。|  
|**ローカル変数**|ローカル変数。|  
|**強力なハンドル**|オブジェクト ハンドル テーブルからの強い参照へのハンドル。|  
|**Io.ピン留めされたハンドル**|オブジェクト ハンドル テーブルからの非同期固定オブジェクト。|  
|**依存ハンドル**|オブジェクト ハンドル テーブルからの依存オブジェクト。|  
|**固定ハンドル**|オブジェクト ハンドル テーブルからの固定された強い参照。|  
|**RefCount ハンドル**|オブジェクト ハンドル テーブルからの参照カウントされたオブジェクト。|  
|**SizedRef ハンドル**|ガベージ コレクション時に、すべてのオブジェクトおよびオブジェクト ルートの集合的なクロージャの概算サイズを保持する強力なハンドル。|  
|**ピンされたローカル変数**|ピンされたローカル変数。|  
  
### <a name="compare-two-memory-snapshots"></a><a name="BKMK_Compare_two_memory_snapshots"></a> 2つのメモリスナップショットの比較  
 メモリ リークの原因である可能性のあるオブジェクトを見つけるために、プロセスに関する 2 つのダンプ ファイルを比較できます。 リークしているオブジェクトの数の増加をわかりやすくするために、1 つ目 (1 回目) と 2 つ目 (2 回目) のファイルを収集する時間間隔は十分長くする必要があります。 2 つのファイルを比較するには:  
  
1. 2番目のダンプファイルを開き、[**ミニダンプファイルの概要**] ページで [**マネージメモリのデバッグ**] を選択します。  
  
2. [メモリ分析レポート] ページで、 **[ベースラインの選択** ] の一覧を開き、[ **参照** ] をクリックして最初のダンプファイルを指定します。  
  
   アナライザーによって、レポートの上部ペインに列が追加されます。このペインには、前のスナップショットの型の **数**、 **サイズ**、および **包括サイズ** の差が表示されます。  
  
   ![種類一覧の相違点列](../misc/media/mngdmem-diffcolumns.png "MNGDMEM_DiffColumns")  
  
   **参照カウントの差分**列も、**ルートテーブルへのパス**に追加されます。  
  
   ![ページのトップへ](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [目次](#BKMK_Contents)  
  
## <a name="see-also"></a>参照  
 [VS ALM TFS ブログ: Visual Studio 2013 を使用した運用環境での .NET メモリの問題の診断](https://devblogs.microsoft.com/devops/using-visual-studio-2013-to-diagnose-net-memory-issues-in-production/)   
 [Channel 9 &#124; Visual Studio TV &#124; マネージメモリ分析](https://channel9.msdn.com/Series/Visual-Studio-2012-Premium-and-Ultimate-Overview/Managed-Memory-Analysis)   
 [Channel 9 &#124; Visual Studio のツールボックス &#124; マネージメモリ分析の Visual Studio 2013](https://channel9.msdn.com/Shows/Visual-Studio-Toolbox/Managed-Memory-Analysis-in-Visual-Studio-2013)