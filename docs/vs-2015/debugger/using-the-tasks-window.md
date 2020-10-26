---
title: '[タスク] ウィンドウの使用 | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.paralleltasks
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- debugger, parallel tasks window
ms.assetid: bd5e0612-a0dc-41cf-a7af-1e87d0d5c35f
caps.latest.revision: 23
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 267a04e0d717bde311423aae7f35fba07ca6f39b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65684038"
---
# <a name="using-the-tasks-window"></a>[タスク] ウィンドウの使用
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

**[タスク]** ウィンドウは **[スレッド]** ウィンドウに似ていますが、このウィンドウには、各スレッドではなく <xref:System.Threading.Tasks.Task?displayProperty=fullName>、[task_handle](https://msdn.microsoft.com/library/b4af5b28-227d-4488-8194-0a0d039173b7)、または [WinJS.Promise](https://msdn.microsoft.com/library/windows/apps/br211867.aspx) オブジェクトに関する情報が表示されます。 スレッドと同様、タスクは、同時に実行できる非同期操作を表します。ただし、複数のタスクが同じスレッドで実行される場合もあります。 詳細については、「 [JavaScript での非同期プログラミング (Windows ストアアプリ)](https://msdn.microsoft.com/library/windows/apps/hh700330.aspx) 」を参照してください。  
  
 マネージド コードでは、<xref:System.Threading.Tasks.Task?displayProperty=fullName> オブジェクトを操作するときや、**await** および **async** (VisualBasic では **Await** および **Async**) キーワードを操作するとき、 **[タスク]** ウィンドウを使用できます。 マネージド コードでのタスクの詳細については、[並列プログラミング](https://msdn.microsoft.com/library/4d83c690-ad2d-489e-a2e0-b85b898a672d)に関するページを参照してください。  
  
 ネイティブ コードでは、[タスク グループ](https://msdn.microsoft.com/library/42f05ac3-2098-494a-ba84-737fcdcad077)、[並列アルゴリズム](https://msdn.microsoft.com/library/045dca7b-4d73-4558-a44c-383b88a28473)、[非同期エージェント](https://msdn.microsoft.com/library/6cf6ccc6-87f1-4e14-af15-ea8ba58fef1a)、および[軽量タスク](https://msdn.microsoft.com/library/9aba278c-e0c9-4ede-b7c6-fedf7a365d90)を操作するときに **[タスク]** ウィンドウを使用できます。 ネイティブ コードのタスクの詳細については、「[コンカレンシー ランタイム](https://msdn.microsoft.com/library/874bc58f-8dce-483e-a3a1-4dcc9e52ed2c)」を参照してください。  
  
 JavaScript では、promise.then コードを操作するときに [タスク] ウィンドウを使用できます。  
  
 **[タスク]** ウィンドウは、デバッガーを中断するといつでも使用できます。 アクセスするには、 **[デバッグ]** メニューの **[ウィンドウ]** をクリックし、 **[タスク]** をクリックします。 次の図は、既定のモードの **[タスク]** ウィンドウを示しています。  
  
 ![並列タスク ウィンドウ](../debugger/media/parallel-tasks-window.png "Parallel_Tasks_Window")  
  
> [!NOTE]
> マネージド コードでは、マネージド スレッドがスリープ状態または結合状態のとき、状態が <xref:System.Threading.Tasks.Task>、<xref:System.Threading.Tasks.TaskStatus>、または <xref:System.Threading.Tasks.TaskStatus> の <xref:System.Threading.Tasks.TaskStatus> は [タスク] ウィンドウに表示されないことがあります。  
  
## <a name="tasks-column-information"></a>[タスク] ウィンドウの列の情報  
 **[タスク]** ウィンドウの列には、次の情報が表示されます。  
  
|列名|説明|  
|-----------------|-----------------|  
|**フラグ**|どのタスクにフラグが設定されているかを示します。タスクのフラグを設定または解除することができます。|  
|**アイコン**|黄色の矢印は現在のタスクを示します。 現在のタスクは、現在のスレッドの最上位のタスクです。<br /><br /> 白い矢印は中断しているタスク、つまりデバッガーを呼び出したときに現在のタスクだったタスクを示します。<br /><br /> 一時停止アイコンはユーザーによって凍結されているタスクを示します。 一覧でタスクを右クリックして、タスクを凍結したり凍結解除したりすることができます。|  
|**ID**|タスクに対してシステムで指定された番号です。 ネイティブ コードでは、タスクのアドレスになります。|  
|**状態**|タスクの現在の状態 (スケジュール、アクティブ、デッドロック、待機中、または完了) です。 スケジュール状態のタスクは、まだ実行されていないため、まだ呼び出し履歴、割り当てられたスレッド、関連情報がないタスクです。<br /><br /> アクティブなタスクは、デバッガーを中断する前にコードを実行していたタスクです。<br /><br /> 待機中のタスクは、イベントがシグナル状態になるか、ロックが解放されるか、別のタスクが終了するのを待機しているためにブロックされているタスクです。<br /><br /> デッドロック状態のタスクは、スレッドが別のスレッドでデッドロックされた待機中のタスクです。<br /><br /> デッドロックまたは待機中のタスクの **状態** セルにマウスポインターを合わせると、ブロックに関する詳細情報が表示されます。 **警告:** **[タスク]** ウィンドウでは、待機チェーン トラバーサル (WCT) でサポートされる同期プリミティブを使用する、ブロックされているタスクに関してのみ、デッドロックが報告されます。 たとえば、WCT を使用するデッドロックされたオブジェクトの場合、 <xref:System.Threading.Tasks.Task> デバッガーは **待機中のデッドロック**を報告します。 同時実行ランタイムによって管理されるデッドロック状態のタスクに対して、デバッガーからは **待機中** が報告されます。 WCT の詳細については、「[Wait Chain Traversal](https://msdn.microsoft.com/library/ms681622\(VS.85\).aspx)」 (待機チェーン トラバーサル) を参照してください。|  
|**開始時刻**|タスクがアクティブになった時間です。|  
|**期間**|タスクがアクティブになっている秒数です。|  
|**完了時間**|タスクが完了した時間です。|  
|**場所**|タスクの呼び出し履歴内の現在の位置です。 タスクのすべての呼び出し履歴を表示するには、このセルの上にカーソルを置きます。 スケジュール状態のタスクについては、このセルには値が表示されません。|  
|**Task**|最初のメソッドと、作成時にタスクに渡された引数です。|  
|**親**|このタスクを作成したタスクの ID です。 この列が空白のタスクには親はありません。 これは、マネージド プログラムの場合にのみ適用されます。|  
|**スレッドの割り当て**|タスクを実行しているスレッドの ID と名前です。|  
|**リターン状態**|タスクが完了したときのステータスです。 戻り値の状態は、[ **成功**]、[ **キャンセル**]、および [ **エラー**] です。|  
|**AppDomain**|マネージド コード用の情報で、タスクを実行しているアプリケーション ドメインを示します。|  
|**task_group**|ネイティブ コード用の情報で、タスクのスケジュールを設定した [task_group](https://msdn.microsoft.com/library/b4af5b28-227d-4488-8194-0a0d039173b7) オブジェクトのアドレスを示します。 非同期エージェントおよび軽量タスクでは、この列は 0 に設定されます。|  
|プロセス|タスクが実行されているプロセスの ID です。|  
|Async State (非同期状態)|タスクの状態です (マネージド コードの場合)。 既定では、この列は非表示になっています。 この列を表示するには、いずれかの列ヘッダーのコンテキスト メニューを開きます。 **[列]** 、 **[AsyncState]** の順にクリックします。|  
  
 ビューに列を追加するには、列見出しを右クリックし、追加する列を選択します (列を削除するには選択を解除します)。また、列を左右にドラッグして列の順序を変更することもできます。 列のショートカット メニューを次の図に示します。  
  
 ![並列タスク ウィンドウのショートカット ビュー メニュー](../debugger/media/parallel-tasks-contextmenu.png "Parallel_Tasks_ContextMenu")  
  
## <a name="sorting-tasks"></a>タスクの並べ替え  
 列を基準にタスクを並べ替えるには、列ヘッダーをクリックします。 たとえば、 **[ID]** 列ヘッダーをクリックすると、タスクをタスク ID 順に並べ替えることができます (例: 1、2、3、4、5)。 並べ替え順序を逆にするには、もう一度列ヘッダーをクリックします。 現在の並べ替え列と並べ替え順序は、列に矢印で示されます。  
  
## <a name="grouping-tasks"></a>タスクのグループ化  
 リスト ビューの任意の列に基づいてタスクをグループ化することができます。 たとえば、 **status** 列のヘッダーを右クリックし、[ **状態でグループ化**] をクリックすると、同じ状態のすべてのタスクをグループ化できます。 このようにすると、たとえば待機中のタスクをすばやく表示して、ブロックされている理由を集中的に確認することができます。 また、デバッグ セッションでは関係のないグループを折りたたむこともできます。 他の列を基準にしても、同じようにしてグループ化できます。 グループに対しては、グループ ヘッダーの横にあるボタンをクリックするだけで、まとめてフラグを設定したり解除したりすることができます。 次の図は、グループ化されたモードの **[タスク]** ウィンドウを示しています。  
  
 ![並列タスク ウィンドウのグループ化されたモード](../debugger/media/parallel-tasks-groupedmode.png "Parallel_Tasks_GroupedMode")  
  
## <a name="parent-child-view"></a>親子ビュー  
 (このビューはマネージコードでのみ使用できます)。列見出しを右クリックし、[親の **子ビュー**] をクリックすると、タスクの一覧を階層ビューに変更できます。このビューでは、すべての子タスクが、親の下に表示または非表示にできるサブノードになります。 次の図は、親子ビューでのタスクの表示を示しています。  
  
 ![[並列タスク] ウィンドウの親&#45;子ビュー](../debugger/media/parallel-tasks-parentchildview.png "Parallel_Tasks_ParentChildView")  
  
## <a name="flagging-tasks"></a>タスクに対するフラグの設定  
 タスクが実行されているタスクをスレッドにフラグを付けるには、タスク一覧の項目を選択し、コンテキストメニューから [ **フラグ** ] を選択するか、最初の列のフラグアイコンをクリックします。 複数のタスクにフラグを設定してそれらだけを集中して確認する場合、フラグ列で並べ替えを行うことで、フラグを設定したすべてのタスクが上に表示されるようにすることができます。 **[並列スタック]** ウィンドウを使用して、フラグを設定したタスクだけを表示することもできます。 これにより、デバッグには関係のないタスクを除外することができます。 フラグはデバッグ セッション間で保持されません。  
  
## <a name="freezing-and-thawing-tasks"></a>タスクの凍結と凍結解除  
 タスク一覧の項目を右クリックして **[割り当てられたスレッドを凍結]** をクリックすると、タスクを実行しているスレッドを凍結することができます (タスクが既に凍結されている場合は、コマンドは **[割り当てられたスレッドの凍結を解除]** になります)。スレッドを凍結すると、現在のブレークポイントの後のコードのステップ実行でそのスレッドが実行されなくなります。 **すべてのスレッドを凍結**しますが、このコマンドは、タスクリスト項目を実行しているスレッドを除くすべてのスレッドをフリーズします。  
  
 各タスクのその他のメニュー項目を次の図に示します。  
  
 ![並列タスク ウィンドウのショートカット スレッド メニュー](../debugger/media/parallel-tasks-contextmenu2.png "Parallel_Tasks_ContextMenu2")  
  
## <a name="see-also"></a>参照  
 [デバッガーの基本](../debugger/debugger-basics.md)   
 [マネージコードのデバッグ](../debugger/debugging-managed-code.md)   
 [並列プログラミング](https://msdn.microsoft.com/library/4d83c690-ad2d-489e-a2e0-b85b898a672d)   
 [同時実行ランタイム](https://msdn.microsoft.com/library/874bc58f-8dce-483e-a3a1-4dcc9e52ed2c)   
 [[並列スタック] ウィンドウの使用](../debugger/using-the-parallel-stacks-window.md)   
 [チュートリアル: 並列アプリケーションのデバッグ](../debugger/walkthrough-debugging-a-parallel-application.md)
