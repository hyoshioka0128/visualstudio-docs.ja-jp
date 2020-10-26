---
title: Windows ストアアプリの中断イベント、再開イベント、およびバックグラウンドイベントをトリガーする方法
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.error.background_task_activate_failure
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: 824ff3ca-fedf-4cf5-b3e2-ac8dc82d40ac
caps.latest.revision: 20
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: d341f0550cfa3c978e94152fb792c5b73c68cc74
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65685939"
---
# <a name="how-to-trigger-suspend-resume-and-background-events-for-windows-store-apps-in-visual-studio"></a>Visual Studio で Windows ストア アプリの中断イベント、再開イベント、およびバックグラウンド イベントをトリガーする方法
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

デバッグが行われていないときは、Windows の **プロセス継続時間管理** (PLM) によってアプリの実行状態 (ユーザー アクションに応じたアプリの開始、中断、再開、および終了) とデバイスの状態が管理されます。 デバッグが行われているとき、これらのアクティブ化イベントは Windows によって無効にされます。 このトピックでは、デバッガーでこれらのイベントを発生させる方法について説明します。

 このトピックでは、 **バックグラウンド タスク**をデバッグする方法についても説明します。 バックグラウンド タスクは、アプリが実行されていない場合でもバックグラウンド プロセスで特定の操作を行うことを可能にします。 デバッガーを使用してアプリをデバッグ モードに変更した後、UI の起動なしでバックグラウンド タスクを開始してデバッグできます。

 プロセス継続時間管理とバックグラウンドタスクの詳細については、「 [起動、再開、およびマルチタスキング](https://msdn.microsoft.com/04307b1b-05af-46a6-b639-3f35e297f71b)」を参照してください。

## <a name="in-this-topic"></a><a name="BKMK_In_this_topic"></a> このトピックの内容
 [プロセス継続時間管理イベントのトリガー](#BKMK_Trigger_Process_Lifecycle_Management_events)

 [バックグラウンドタスクをトリガーする](#BKMK_Trigger_background_tasks)

- [標準デバッグセッションからバックグラウンドタスクイベントをトリガーする](#BKMK_Trigger_a_background_task_event_from_a_standard_debug_session)

- [アプリが実行されていないときにバックグラウンドタスクをトリガーする](#BKMK_Trigger_a_background_task_when_the_app_is_not_running)

  [インストールされているアプリからプロセス継続時間管理イベントとバックグラウンドタスクをトリガーする](#BKMK_Trigger_Process_Lifetime_Management_events_and_background_tasks_from_an_installed_app)

  [バックグラウンドタスクのアクティブ化エラーの診断](#BKMK_Diagnosing_background_task_activation_errors)

## <a name="trigger-process-lifetime-management-events"></a><a name="BKMK_Trigger_Process_Lifecycle_Management_events"></a> プロセス継続時間管理イベントを発生させる
 Windows では、ユーザーが他のアプリに切り替えた場合、または Windows が低電力状態に入った場合にアプリを中断できます。 `Suspending` イベントに応答して、関連するアプリとユーザー データを永続ストレージに保存し、リソースを解放できます。 **中断** 状態から再開されたアプリは **実行** 状態に入り、中断状態に入った時点の状態から実行を続行します。 `Resuming` イベントに応答してアプリの状態を復元するか更新し、リソースを再要求できます。

 Windows はできる限り多くの中断されたアプリをメモリに保持しようとしますが、十分なリソースが存在しない場合はアプリを終了できます。 ユーザーもアプリを明示的に閉じることができます。 ユーザーがアプリを閉じたことを示す特別なイベントはありません。

 Visual Studio デバッガーでは、アプリを手動で中断、再開、および終了して、プロセスのライフサイクル イベントをデバッグできます。 プロセスのライフサイクル イベントをデバッグするには:

1. デバッグするイベントのハンドラーの中にブレークポイントを設定します。

2. **F5** キーを押してデバッグを開始します。

3. **[デバッグの場所]** ツール バーで、トリガーするイベントを選択します。

     ![中断タスク、再開タスク、終了タスク、およびバックグラウンド タスク](../debugger/media/dbg-suspendresumebackground.png "DBG_SuspendResumeBackground")

     **[Suspend and terminate]** (中断して終了) は、アプリを閉じ、デバッグ セッションを終了します。

## <a name="trigger-background-tasks"></a><a name="BKMK_Trigger_background_tasks"></a> バックグラウンド タスクをトリガーする
 すべてのアプリは、アプリが実行されていない場合でも特定のシステム イベントに応答するためのバックグラウンド タスクを登録できます。 バックグラウンド タスクは、UI を直接更新するコードは実行できません。代わりに、タイルの更新、バッジの更新、およびトースト通知を使用して、ユーザーに情報を表示します。 詳細については、「[バックグラウンドタスクを使用したアプリのサポート](https://msdn.microsoft.com/4c7bb148-eb1f-4640-865e-41f627a46e8e)」を参照してください。

 アプリのバックグラウンド タスクを開始するイベントをデバッガーからトリガーできます。

> [!NOTE]
> デバッガーは、データを含まないイベント (デバイスの状態の変更を示すイベントなど) だけをトリガーできます。 ユーザー入力やその他のデータを必要とするバックグラウンド タスクは手動でトリガーする必要があります。

 バックグラウンド タスク イベントをトリガーするための最も現実的な方法は、アプリが実行されていない時点です。 ただし、標準デバッグ セッション中のイベントのトリガーもサポートされています。

### <a name="trigger-a-background-task-event-from-a-standard-debug-session"></a><a name="BKMK_Trigger_a_background_task_event_from_a_standard_debug_session"></a> 標準デバッグ セッションからバックグラウンド タスク イベントをトリガーする

1. デバッグするバックグラウンド タスク コードの中にブレークポイントを設定します。

2. **F5** キーを押してデバッグを開始します。

3. **[デバッグの場所]** ツール バーのイベントの一覧から、開始するバックグラウンド タスクを選択します。

     ![中断タスク、再開タスク、終了タスク、およびバックグラウンド タスク](../debugger/media/dbg-suspendresumebackground.png "DBG_SuspendResumeBackground")

### <a name="trigger-a-background-task-when-the-app-is-not-running"></a><a name="BKMK_Trigger_a_background_task_when_the_app_is_not_running"></a> アプリが実行されていないときにバックグラウンド タスクをトリガーする

1. デバッグするバックグラウンド タスク コードの中にブレークポイントを設定します。

2. スタートアップ プロジェクトのデバッグ プロパティ ページを開きます。 ソリューション エクスプローラーでプロジェクトを選択します。 **[デバッグ]** メニューの **[プロパティ]** をクリックします。

     C++ プロジェクトの場合は、 **[構成プロパティ]** を展開し、 **[デバッグ]** をクリックする必要があります。

3. 次のいずれかの操作を行います。

    - Visual C# プロジェクトと Visual Basic プロジェクトの場合は、 **[起動しないが、開始時にコードをデバッグ]** をクリックします。

         ![C&#35; と VB のデバッグ起動アプリケーション プロパティ](../debugger/media/dbg-csvb-dontlaunchapp.png "DBG_CsVb_DontLaunchApp")

    - JavaScript プロジェクトと Visual C++ プロジェクトの場合は、 **[アプリケーションの起動]** の一覧の **[No]** をクリックします。

         ![C&#43;&#43; と VB の起動アプリケーションのデバッグ プロパティ](../debugger/media/dbg-cppjs-dontlaunchapp.png "DBG_CppJs_DontLaunchApp")

4. **F5** キーを押して、アプリをデバッグ モードにします。 デバッグ モードであることを示すために、 **[デバッグの場所]** ツール バーの **[プロセス]** の一覧にアプリのパッケージ名が表示されます。

     ![バックグラウンド タスクのプロセス リスト](../debugger/media/dbg-backgroundtask-processlist.png "DBG_BackgroundTask_ProcessList")

5. **[デバッグの場所]** ツール バーのイベントの一覧から、開始するバックグラウンド タスクを選択します。

     ![中断タスク、再開タスク、終了タスク、およびバックグラウンド タスク](../debugger/media/dbg-suspendresumebackground.png "DBG_SuspendResumeBackground")

## <a name="trigger-process-lifetime-management-events-and-background-tasks-from-an-installed-app"></a><a name="BKMK_Trigger_Process_Lifetime_Management_events_and_background_tasks_from_an_installed_app"></a> インストール済みのアプリからプロセス継続時間管理イベントとバックグラウンド タスクをトリガーする
 [インストールされているアプリケーション パッケージのデバッグ] ダイアログ ボックスを使用して、既にインストールされているアプリをデバッガーに読み込みます。 たとえば、Windows ストアからインストールされたアプリや、ソース ファイルはあっても Visual Studio プロジェクトがないアプリをデバッグできます。 [インストールされているアプリケーション パッケージのデバッグ] ダイアログ ボックスを使用すると、Visual Studio のコンピューターまたはリモート デバイスで、アプリをデバッグ モードで起動できます。また、アプリを起動せずにデバッグ モードで実行するように設定することもできます。 詳細については、 **JavaScript** バージョンまたは、 [Visual C++、Visual C#、Visual Basic](../debugger/start-a-debugging-session-for-store-apps-in-visual-studio-javascript.md#BKMK_Start_an_installed_app_in_the_debugger) バージョンの「 [デバッグ セッションを開始する方法](../debugger/start-a-debugging-session-for-a-store-app-in-visual-studio-vb-csharp-cpp-and-xaml.md#BKMK_Start_an_installed_app_in_the_debugger) 」の「 **デバッガーでインストール済みのアプリを起動する** 」を参照してください。

 アプリをデバッガーに読み込んだら、前の各手順を使用できます。

## <a name="diagnosing-background-task-activation-errors"></a><a name="BKMK_Diagnosing_background_task_activation_errors"></a> バックグラウンド タスクのアクティブ化エラーの診断
 バックグラウンド インフラストラクチャ用の Windows イベント ビューアーの診断ログには、バックグラウンド タスク エラーの診断とトラブルシューティングを行うために使用できる詳細情報が含まれています。 このログを表示するには:

1. イベント ビューアー アプリケーションを開きます。

2. **操作** ウィンドウで、 **[表示]** をクリックし、 **[分析およびデバッグ ログの表示]** がオンになっていることを確認します。

3. **[イベント ビューアー (ローカル)]** ツリーで、ノード **Applications and Services Logs** / **Microsoft** / **Windows** / **BackgroundTasksInfrastructure** を展開します。

4. **診断** ログを選択します。

## <a name="see-also"></a>参照
 Visual [studio でのストアアプリのテスト](../test/testing-store-apps-with-visual-studio.md) [visual studio でのアプリのデバッグ](../debugger/debug-store-apps-in-visual-studio.md)[アプリケーションライフサイクル](https://msdn.microsoft.com/53cdc987-c547-49d1-a5a4-fd3f96b2259d)の[起動、再開、およびマルチタスキング](https://msdn.microsoft.com/04307b1b-05af-46a6-b639-3f35e297f71b)
