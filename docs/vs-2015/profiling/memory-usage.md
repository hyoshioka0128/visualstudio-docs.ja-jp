---
title: メモリ使用量 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: bbb58d6c-3362-4ca3-8e87-64b2d4415bf6
caps.latest.revision: 17
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 0feabad8dfa3b086c9ed5a1a58e231719774f9cc
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "74298363"
---
# <a name="memory-usage"></a>メモリ使用量
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

デバッガーに統合された **メモリ使用量** 診断ツールを使用したデバッグ中に、メモリリークおよび非効率的なメモリを見つけます。 メモリ使用量ツールを使用すると、マネージド メモリ ヒープ、およびネイティブ メモリ ヒープの 1 つまたは複数の *スナップショット* を取得できます。 .NET アプリ、ネイティブ アプリ、または混在モード (.NET とネイティブ) アプリのスナップショットを収集できます。  
  
- 単一のスナップショットを分析することにより、オブジェクト型のメモリ使用に対する相対的な影響を理解し、アプリ内でメモリが効率的に使用されていないコードを検出することができます。  
  
- アプリの 2 つのスナップショットを比較 (diff) することにより、コード内で時間の経過に伴ってメモリ使用量が増加している箇所を検出することもできます。  
  
  次の図は、Visual Studio 2015 Update 1 の [ **診断ツール** ] ウィンドウを示しています。  
  
  ![DiagnosticTools&#45;Update1](../profiling/media/diagnostictools-update1.png "DiagnosticTools-Update1")  
  
  **メモリ使用量** ツールでメモリのスナップショットをいつでも収集できますが、Visual Studio デバッガーを使用すると、パフォーマンスの問題を調査中にアプリケーションの実行方法を制御することができます。 ブレークポイントの設定、ステップ実行、すべて中断、その他のデバッガー アクションは、パフォーマンスの調査を最も関連性の高いコード パスに集中させるのに役立ちます。 アプリの実行中にこれらのアクションを実行することで、目的としていないコードからのノイズを除去することができ、問題の診断にかかる時間を大幅に短縮できます。  
  
  さらに、デバッガーの外部のメモリ ツールも使用できます。 「 [デバッグなしのメモリ使用量](https://msdn.microsoft.com/library/8883bc5f-df86-4f84-aa2b-a21150f499b0)」を参照してください。  
  
> [!NOTE]
> **カスタム アロケーター サポート** ネイティブ メモリ プロファイラーは、実行時に生成された割り当て [ETW](https://msdn.microsoft.com/library/windows/desktop/bb968803\(v=vs.85\).aspx) イベント データを収集して機能します。  CRT および Windows SDK のアロケーターには、割り当てデータをキャプチャできるように、ソース レベルで注釈が付けられています。  独自のアロケーターを作成する場合、新しく割り当てられたヒープ メモリへのポインターを返すすべての関数は、 [__declspec](https://msdn.microsoft.com/library/832db681-e8e1-41ca-b78c-cd9d265cdb87)(アロケーター) で修飾できます。myMalloc での例を次に示します。  
>   
> `__declspec(allocator) void* myMalloc(size_t size)`  
  
## <a name="analyze-memory-use-with-the-debugger"></a>デバッガーのメモリ使用量の分析  
  
> [!NOTE]
> メモリ データの収集はネイティブ アプリや混在モードのアプリのパフォーマンスに影響する可能性があるため、既定でメモリのスナップショットは無効になっています。 ネイティブ アプリや混在モードのアプリのスナップショットを有効にするには、デバッグ セッションを開始します (ショートカット キー: **F5**)。 **[診断ツール]** ウィンドウが表示されたら、[メモリ使用量] タブを選択し、 **[スナップショットを有効にする]** を選択します。  
>   
> ![スナップショットを有効にする](../profiling/media/dbgdiag-mem-mixedtoolbar-enablesnapshot.png "DBGDIAG_MEM_MixedToolbar_EnableSnapshot")  
>   
> デバッグを停止 (ショートカット キー: **Shift + F5**) してから再開します。  
  
 メモリの状態をキャプチャする場合は常に、 **[メモリ使用量]** 概要ツールバーで **[スナップショットの取得]** を選択します。  
  
 ![スナップショットの取得](../profiling/media/dbgdiag-mem-mixedtoolbar-takesnapshot.png "DBGDIAG_MEM_MixedToolbar_TakeSnapshot")  
  
> [!TIP]
> - メモリ比較のベースラインを作成するには、デバッグ セッションの開始時に、スナップショットを取得することを検討します。  
>   - アプリがメモリの割り当てと割り当て解除を頻繁に行う場合、目的とする操作のメモリ プロファイルを取得するのは容易ではないため、操作の最初と最後にブレークポイントを設定するか、操作をステップ実行して、メモリが変更される正確なポイントを見つけます。  
  
## <a name="viewing-memory-snapshot-details"></a>メモリのスナップショットの詳細表示  
 メモリ使用量の概要テーブルの行には、デバッグ セッション中に取得したスナップショットが一覧表示されます。  
  
 行の列は、プロジェクトのプロパティで選択したデバッグ モード (.NET、ネイティブ、または混合 (.NET とネイティブの両方)) によって決まります。  
  
- **[管理オブジェクト]** および **[ネイティブ割り当て]** 列には、スナップショット取得時の .NET メモリおよびネイティブ メモリ内のオブジェクト数が表示されます。  
  
- **[マネージド ヒープ サイズ]** および **[ネイティブ ヒープ サイズ]** 列には、.NET ヒープおよびネイティブ ヒープのバイト数が表示されます。  
  
- 複数のスナップショットを取得した場合、概要テーブルのセルには、行のスナップショットと前のスナップショットの間の値の変化が含まれます。  
  
   ![メモリの概要テーブル セル](../profiling/media/dbgdiag-mem-summarytablecell.png "DBGDIAG_MEM_SummaryTableCell")  
  
  **詳細レポートの表示方法:**  
  
- 選択したスナップショットのみの詳細を表示するには、現在のリンクを選択します。  
  
- 現在のスナップショットと前のスナップショットの相違点の詳細を表示するには、変更リンクを選択します。  
  
  レポートが新しいウィンドウに表示されます。  
  
## <a name="memory-usage-details-reports"></a>メモリ使用量の詳細レポート  
  
### <a name="managed-types-reports"></a>マネージド型レポート  
 メモリ使用量の概要テーブルで、 **[マネージド オブジェクト]** または **[マネージド ヒープ サイズ]** セルの現在のリンクを選択します。  
  
 ![デバッガーのマネージド型のレポート &#45; ルートへのパス](../profiling/media/dbgdiag-mem-managedtypesreport-pathstoroot.png "DBGDIAG_MEM_ManagedTypesReport_PathsToRoot")  
  
 上のウィンドウには、型で参照されているすべてのオブジェクトのサイズ (**包括サイズ**) を含む、スナップショット内の型の総数およびサイズが表示されます。  
  
 下のウィンドウの **[ルートのパス]** ツリーには、上ウィンドウで選択されている型を参照するオブジェクトが表示されます。 .NET Framework のガベージ コレクターがオブジェクトのメモリをクリーンアップするのは、そのオブジェクトを参照する最後の型が解放されたときに限られます。  
  
 **[参照される型]** ツリーには、上のウィンドウで選択されている型に保持されている参照が表示されます。  
  
 ![マネージド参照型のレポート ビュー](../profiling/media/dbgdiag-mem-managedtypesreport-referencedtypes.png "DBGDIAG_MEM_ManagedTypesReport_ReferencedTypes")  
  
 上のウィンドウで選択した型のインスタンスを表示するには、![インスタンス アイコン](../profiling/media/dbgdiag-mem-instanceicon.png "DBGDIAG_MEM_InstanceIcon") アイコンを選択します。  
  
 ![インスタンス ビュー](../profiling/media/dbgdiag-mem-managedtypesreport-instances.png "DBGDIAG_MEM_ManagedTypesReport_Instances")  
  
 **[インスタンス]** ビューには、上のウィンドウのスナップショットで選択されているインスタンスが表示されます。 [ルートのパス] および [参照されたオブジェクト] ウィンドウには、選択したインスタンスを参照するオブジェクト、および選択したインスタンスが参照する型が表示されます。 スナップショットが取得された時点でデバッガーを停止すると、[値] セルの上にマウス カーソルを移動して、ツール ヒントにオブジェクトの値を表示することができます。  
  
### <a name="native-type-reports"></a>ネイティブ型のレポート  
 **[診断ツール]** ウィンドウのメモリ使用量の概要テーブルで、 **[ネイティブ割り当て]** または **[ネイティブ ヒープ サイズ]** セルの現在のリンクを選択します。  
  
 ![ネイティブ型のビュー](../profiling/media/dbgdiag-mem-native-typesview.png "DBGDIAG_MEM_Native_TypesView")  
  
 **[型ビュー]** には、スナップショットの型の数およびサイズが表示されます。  
  
- 選択した型のインスタンス アイコン (![[オブジェクト型] 列の [インスタンス] アイコン](../misc/media/dbg-mma-instancesicon.png "DBG_MMA_InstancesIcon")) を選択し、スナップショットの選択した型のオブジェクトに関する情報を表示します。  
  
     **[インスタンス]** ビューには、選択した型の各インスタンスが表示されます。 インスタンスを選択すると呼び出し履歴が表示され、その結果、 **[割り当て呼び出し履歴]** ウィンドウにそのインスタンスが作成されます。  
  
     ![インスタンス ビュー](../profiling/media/dbgdiag-mem-native-instances.png "DBGDIAG_MEM_Native_Instances")  
  
- **[表示モード]** の一覧で **[スタック ビュー]** を選択し、選択した型の割り当て履歴を表示します。  
  
     ![スタック ビュー](../profiling/media/dbgdiag-mem-native-stacksview.png "DBGDIAG_MEM_Native_StacksView")  
  
### <a name="change-diff-reports"></a>変更 (Diff) レポート  
  
- **[診断ツール]** ウィンドウの **[メモリ使用量]** タブで、概要テーブルのセルにある変更リンクを選択します。  
  
   ![変更 &#40;差分&#41;f レポートを選択します](../profiling/media/dbgdiag-mem-choosediffreport.png "DBGDIAG_MEM_ChooseDiffReport")  
  
- マネージド レポート、もしくはネイティブ レポートの **[比較対象]** 一覧でスナップショットを選択します。  
  
   ![比較対象の一覧からスナップショットを選択](../profiling/media/dbgdiag-mem-choosecompareto.png "DBGDIAG_MEM_ChooseCompareTo")  
  
  変更レポートを実行すると、基本のスナップショット値と比較のスナップショットの差分を表示する列 ( **(Diff)** のマークが付けられる) が、基本レポートに追加されます。 ネイティブ型の差分レポート ビューは次のようになります。  
  
  ![ネイティブ型の差分ビュー](../profiling/media/dbgdiag-mem-native-typesviewdiff.png "DBGDIAG_MEM_Native_TypesViewDiff")  
  
## <a name="blogs-and-videos"></a>ブログとビデオ  
 [Visual Studio 2015 の診断ツール [デバッガー] ウィンドウ](https://devblogs.microsoft.com/devops/diagnostic-tools-debugger-window-in-visual-studio-2015/)  
  
 [ブログ: Visual Studio 2015 のデバッグ中のメモリ使用量ツール](https://devblogs.microsoft.com/devops/memory-usage-tool-while-debugging-in-visual-studio-2015/)  
  
 [Visual C++ ブログ: VS2015 プレビューでのネイティブ メモリ診断](https://devblogs.microsoft.com/cppblog/native-memory-diagnostics-in-vs2015-preview/)  
  
 [Visual C++ ブログ: Visual Studio 2015 CTP のネイティブ メモリ診断ツール](https://devblogs.microsoft.com/cppblog/native-memory-diagnostic-tools-for-visual-studio-14-ctp/)
