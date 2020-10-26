---
title: '[タスク] ウィンドウの使用 | Microsoft Docs'
ms.date: 03/18/2018
ms.topic: conceptual
f1_keywords:
- vs.debug.paralleltasks
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugger, parallel tasks window
ms.assetid: bd5e0612-a0dc-41cf-a7af-1e87d0d5c35f
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b32dc6372a6ce4983e9bd11e05a4a662d0ad44ba
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62901598"
---
# <a name="using-the-tasks-window-c-visual-basic-c"></a>[タスク] ウィンドウの使用 (C#、Visual Basic、C++)

**[タスク]** ウィンドウは **[スレッド]** ウィンドウに似ていますが、このウィンドウには、各スレッドではなく <xref:System.Threading.Tasks.Task?displayProperty=fullName>、[task_handle](/cpp/parallel/concrt/reference/task-group-class)、または [WinJS.Promise](/previous-versions/windows/apps/br211867(v=win.10)) オブジェクトに関する情報が表示されます。 スレッドと同様、タスクは、同時に実行できる非同期操作を表します。ただし、複数のタスクが同じスレッドで実行される場合もあります。

マネージド コードでは、<xref:System.Threading.Tasks.Task?displayProperty=fullName> オブジェクトを操作するときや、**await** および **async** (VisualBasic では **Await** および **Async**) キーワードを操作するとき、 **[タスク]** ウィンドウを使用できます。 マネージド コードでのタスクの詳細については、[並列プログラミング](/dotnet/standard/parallel-programming/index)に関するページを参照してください。

ネイティブ コードでは、[タスク グループ](/cpp/parallel/concrt/task-parallelism-concurrency-runtime)、[並列アルゴリズム](/cpp/parallel/concrt/parallel-algorithms)、[非同期エージェント](/cpp/parallel/concrt/asynchronous-agents)、および[軽量タスク](/cpp/parallel/concrt/task-scheduler-concurrency-runtime)を操作するときに **[タスク]** ウィンドウを使用できます。 ネイティブ コードのタスクの詳細については、「[コンカレンシー ランタイム](/cpp/parallel/concrt/concurrency-runtime)」を参照してください。

JavaScript では、promise `.then` コードを操作するときに [タスク] ウィンドウを使用できます。 詳細については、[JavaScript での非同期プログラミング (UWP アプリ)](/previous-versions/windows/apps/hh700330(v=win.10)) に関するページを参照してください。

**[タスク]** ウィンドウは、デバッガーを中断するといつでも使用できます。 アクセスするには、 **[デバッグ]** メニューの **[ウィンドウ]** をクリックし、 **[タスク]** をクリックします。 次の図は、既定のモードの **[タスク]** ウィンドウを示しています。

![[タスク] ウィンドウ](../debugger/media/parallel_tasks_window.png "Parallel_Tasks_Window")

> [!NOTE]
> マネージド コードでは、マネージド スレッドがスリープまたは結合状態のときに、状態が [TaskStatus.Created](<xref:System.Threading.Tasks.TaskStatus.Created>)、[TaskStatus.WaitingForActivation](<xref:System.Threading.Tasks.TaskStatus.WaitingForActivation>) または [TaskStatus.WaitingToRun](<xref:System.Threading.Tasks.TaskStatus.WaitingToRun>) の <xref:System.Threading.Tasks.Task> は **[タスク]** ウィンドウに表示されないことがあります。

## <a name="tasks-column-information"></a>[タスク] ウィンドウの列の情報

**[タスク]** ウィンドウの列には、次の情報が表示されます。

|列名|説明|
|-----------------|-----------------|
|**フラグ**|どのタスクにフラグが設定されているかを示します。タスクのフラグを設定または解除することができます。|
|**アイコン**|黄色の矢印は現在のタスクを示します。 現在のタスクは、現在のスレッドの最上位のタスクです。<br /><br /> 白い矢印は中断しているタスク、つまりデバッガーを呼び出したときに現在のタスクだったタスクを示します。<br /><br /> 一時停止アイコンはユーザーによって凍結されているタスクを示します。 一覧でタスクを右クリックして、タスクを凍結したり凍結解除したりすることができます。|
|**ID**|タスクに対してシステムで指定された番号です。 ネイティブ コードでは、タスクのアドレスになります。|
|**状態**|タスクの現在の状態 (スケジュール、アクティブ、ブロック、デッドロック、待機中、または完了)。 スケジュール状態のタスクは、まだ実行されていないため、まだ呼び出し履歴、割り当てられたスレッド、関連情報がないタスクです。<br /><br /> アクティブなタスクは、デバッガーを中断する前にコードを実行していたタスクです。<br /><br /> 待機中またはブロック タスクは、イベントがシグナル状態になるか、ロックが解放されるか、別のタスクが終了するのを待機しているためにブロックされているものです。<br /><br /> デッドロック状態のタスクは、スレッドが別のスレッドでデッドロックされた待機中のタスクです。<br /><br /> ブロックに関する詳細情報を表示するには、デッドロックまたは待機中のタスクの **[状態]** セルの上にカーソルを置きます。 **警告:** **[タスク]** ウィンドウでは、待機チェーン トラバーサル (WCT) でサポートされる同期プリミティブを使用する、ブロックされているタスクに関してのみ、デッドロックが報告されます。 たとえば、WCT を使用する、デッドロック状態の <xref:System.Threading.Tasks.Task> オブジェクトに対して、デバッガーからは**待機中デッドロック**が報告されます。 同時実行ランタイムによって管理されるデッドロック状態のタスクに対して、デバッガーからは **待機中** が報告されます。 WCT の詳細については、「[Wait Chain Traversal](/windows/desktop/Debug/wait-chain-traversal)」 (待機チェーン トラバーサル) を参照してください。|
|**開始時刻**|タスクがアクティブになった時間です。|
|**期間**|タスクがアクティブになっている秒数です。|
|**完了時間**|タスクが完了した時間です。|
|**場所**|タスクの呼び出し履歴内の現在の位置です。 タスクのすべての呼び出し履歴を表示するには、このセルの上にカーソルを置きます。 スケジュール状態のタスクについては、このセルには値が表示されません。|
|**Task**|最初のメソッドと、作成時にタスクに渡された引数です。|
|**AsyncState**|タスクの状態です (マネージド コードの場合)。 既定では、この列は非表示になっています。 この列を表示するには、いずれかの列ヘッダーのコンテキスト メニューを開きます。 **[列]** 、 **[AsyncState]** の順にクリックします。|
|**親**|このタスクを作成したタスクの ID です。 この列が空白のタスクには親はありません。 これは、マネージド プログラムの場合にのみ適用されます。|
|**スレッドの割り当て**|タスクを実行しているスレッドの ID と名前です。|
|**AppDomain**|マネージド コード用の情報で、タスクを実行しているアプリケーション ドメインを示します。|
|**task_group**|ネイティブ コード用の情報で、タスクのスケジュールを設定した [task_group](/cpp/parallel/concrt/reference/task-group-class) オブジェクトのアドレスを示します。 非同期エージェントおよび軽量タスクでは、この列は 0 に設定されます。|
|**Process**|タスクが実行されているプロセスの ID です。|

 ビューに列を追加するには、列見出しを右クリックし、追加する列を選択します (列を削除するには選択を解除します)。また、列を左右にドラッグして列の順序を変更することもできます。 列のショートカット メニューを次の図に示します。

 ![[タスク] ウィンドウのショートカット ビュー メニュー](../debugger/media/parallel_tasks_contextmenu.png "Parallel_Tasks_ContextMenu")

## <a name="sorting-tasks"></a>タスクの並べ替え
 列を基準にタスクを並べ替えるには、列ヘッダーをクリックします。 たとえば、 **[ID]** 列ヘッダーをクリックすると、タスクをタスク ID 順に並べ替えることができます (例: 1、2、3、4、5)。 並べ替え順序を逆にするには、もう一度列ヘッダーをクリックします。 現在の並べ替え列と並べ替え順序は、列に矢印で示されます。

## <a name="grouping-tasks"></a>タスクのグループ化
 リスト ビューの任意の列に基づいてタスクをグループ化することができます。 たとえば、 **[状態]** 列の列ヘッダーを右クリックしてから、 **[状態でグループ化]**  >  **[[*status*]]** の順にクリックすると、状態が同じであるすべてのタスクをグループ化できます。 たとえば、待機中のタスクをすばやく表示して、ブロックされている理由を集中的に確認することができます。 また、デバッグ セッションでは関係のないグループを折りたたむこともできます。 他の列を基準にしても、同じようにしてグループ化できます。 グループに対しては、グループ ヘッダーの横にあるボタンをクリックするだけで、まとめてフラグを設定したり解除したりすることができます。 次の図は、グループ化されたモードの **[タスク]** ウィンドウを示しています。

 ![[タスク] ウィンドウのグループ化されたモード](../debugger/media/parallel_tasks_groupedmode.png "Parallel_Tasks_GroupedMode")

## <a name="parent-child-view"></a>親子ビュー
 (このビューは、マネージド コードでのみ使用できます)。 **[状態]** 列ヘッダーを右クリックしてから、 **[グループ化]**  >  **[親]** の順にクリックすることで、タスクの一覧を階層ビューに切り替えることができます。そこでは、すべての子タスクが、表示と非表示を切り替えることができるサブノードとして親の下に表示されます。

## <a name="flagging-tasks"></a>タスクに対するフラグの設定
 タスクが実行中のスレッドにフラグを設定することができます。そのためには、タスク一覧の項目を選択し、コンテキスト メニューから **[割り当てられたスレッドにフラグを設定]** を選ぶか、最初の列のフラグ アイコンをクリックします。 複数のタスクにフラグを設定してそれらだけを集中して確認する場合、フラグ列で並べ替えを行うことで、フラグを設定したすべてのタスクが上に表示されるようにすることができます。 **[並列スタック]** ウィンドウを使用して、フラグを設定したタスクだけを表示することもできます。 これにより、デバッグには関係のないタスクを除外することができます。 フラグはデバッグ セッション間で保持されません。

## <a name="freezing-and-thawing-tasks"></a>タスクの凍結と凍結解除
 タスク一覧の項目を右クリックして **[割り当てられたスレッドを凍結]** をクリックすると、タスクを実行しているスレッドを凍結することができます (タスクが既に凍結されている場合は、コマンドは **[割り当てられたスレッドの凍結を解除]** になります)。スレッドを凍結すると、現在のブレークポイントの後のコードのステップ実行でそのスレッドが実行されなくなります。 **[これ以外のすべてのスレッドを凍結]** コマンドでは、タスク一覧の項目を実行しているものを除くすべてのスレッドが凍結されます。

 各タスクのその他のメニュー項目を次の図に示します。

 ![[タスク] ウィンドウのショートカット スレッド メニュー](../debugger/media/parallel_tasks_contextmenu2.png "Parallel_Tasks_ContextMenu2")

## <a name="switching-the-active-task-or-frame"></a>アクティブなタスクまたはフレームの切り替え

**[タスクに切り替え]** コマンドでは、現在のタスクがアクティブなタスクになります。 **[フレームに切り替え]** コマンドでは、選択されたスタック フレームがアクティブなスタック フレームになります。 デバッガー コンテキストは、現在のタスクまたは選択されたスタック フレームに切り替わります。

## <a name="see-also"></a>関連項目

- [デバッガーでのはじめに](../debugger/debugger-feature-tour.md)
- [マネージド コードをデバッグする](../debugger/debugging-managed-code.md)
- [並列プログラミング](/dotnet/standard/parallel-programming/index)
- [コンカレンシー ランタイム](/cpp/parallel/concrt/concurrency-runtime)
- [[並列スタック] ウィンドウの使用](../debugger/using-the-parallel-stacks-window.md)
- [チュートリアル: 並列アプリケーションのデバッグ](../debugger/walkthrough-debugging-a-parallel-application.md)