---
title: 複数のプロセスをデバッグする |マイクロソフトドキュメント
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.programs
- vs.debug.processes.attaching
- vs.debug.activeprogram
- vs.debug.attaching
- vs.debug.attachedprocesses
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: bde37134-66af-4273-b02e-05b3370c31ab
caps.latest.revision: 19
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 9a2679825d41a6360dde05e7511d607f8be69dfa
ms.sourcegitcommit: 95f26af1da51d4c83ae78adcb7372b32364d8a2b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79301441"
---
# <a name="debug-multiple-processes"></a>複数プロセスをデバッグする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ここでは、プロセスのデバッグ開始、プロセス間の切り替え、実行の中断と続行、ソースのステップ実行、デバッグの停止、プロセスの終了/プロセスからのデタッチの方法について説明します。  
  
## <a name="contents"></a><a name="BKMK_Contents"></a> Contents  
 [複数のプロセスの実行動作を構成する](#BKMK_Configure_the_execution_behavior_of_multiple_processes)  
  
 [ソースファイルとシンボル (.pdb) ファイルを検索する](#BKMK_Find_the_source_and_symbol___pdb__files)  
  
 [VS ソリューション内の複数のプロセスを開始する、プロセスにアタッチする、デバッガーでプロセスを自動的に開始する](#BKMK_Start_multiple_processes_in_a_VS_solution__attach_to_a_process__automatically_start_a_process_in_the_debugger)  
  
 [プロセスの切り替え、実行の中断と続行、ソースのステップ実行](#BKMK_Switch_processes__break_and_continue_execution__step_through_source)  
  
 [デバッグを停止する、プロセスを終了する/プロセスからデタッチする](#BKMK_Stop_debugging__terminate_or_detach_from_processes)  
  
## <a name="configure-the-execution-behavior-of-multiple-processes"></a><a name="BKMK_Configure_the_execution_behavior_of_multiple_processes"></a>複数のプロセスの実行動作を構成する  
 既定では、複数のプロセスがデバッガーで実行されているとき、デバッガーの中断、ステップ実行、停止のコマンドは通常、すべてのプロセスに影響を与えます。 たとえば、1 つのプロセスがブレークポイントで中断されると、他のすべてのプロセスの実行も一時停止されます。 コマンドの実行対象をより詳細に制御するために、この既定の動作を変更できます。  
  
1. **[デバッグ]** メニューの **[オプションと設定]** をクリックします。  
  
2. [**デバッグ**] ページの **[全般**] ページで **、[1 つのプロセスが中断したときにすべてのプロセスを中断**する] チェック ボックスをオフにします。  
  
   ![トップコンテンツに戻る](../debugger/media/pcs-backtotop.png "PCS_BackToTop")[Contents](#BKMK_Contents)  
  
## <a name="find-the-source-and-symbol-pdb-files"></a><a name="BKMK_Find_the_source_and_symbol___pdb__files"></a> ソースとシンボル (.pdb) ファイルを検索する  
 プロセスのソース コードを処理するために、デバッガーにはプロセスのソース ファイルとシンボル ファイルへのアクセスが必要になります。 [「シンボルの指定 (.pdb)」および「ソース ファイル](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)」を参照してください。  
  
 プロセスのこれらのファイルにアクセスできない場合は、[逆アセンブル] ウィンドウを使用してそれらのファイルを検索できます。 方法[: [逆アセンブリ] ウィンドウを使用する](../debugger/how-to-use-the-disassembly-window.md)  
  
 ![トップコンテンツに戻る](../debugger/media/pcs-backtotop.png "PCS_BackToTop")[Contents](#BKMK_Contents)  
  
## <a name="start-multiple-processes-in-a-vs-solution-attach-to-a-process-automatically-start-a-process-in-the-debugger"></a><a name="BKMK_Start_multiple_processes_in_a_VS_solution__attach_to_a_process__automatically_start_a_process_in_the_debugger"></a>VS ソリューションで複数のプロセスを開始し、プロセスにアタッチし、デバッガーでプロセスを自動的に開始する  
  
- [Visual Studio ソリューションで複数のプロセスのデバッグを開始](#BKMK_Start_debugging_multiple_processes_in_a_Visual_Studio_solution)する •[スタートアップ プロジェクトを変更](#BKMK_Change_the_startup_project)する •[ソリューション内の特定のプロジェクトを開始](#BKMK_Start_a_specific_project_in_a_solution)する •[ソリューション内の複数のプロジェクトを開始](#BKMK_Start_multiple_projects_in_a_solution)する •[プロセスにアタッチ](#BKMK_Attach_to_a_process)する •[デバッガーでプロセスを自動的に開始する](#BKMK_Automatically_start_an_process_in_the_debugger)  
  
> [!NOTE]
> デバッガーは、子プロジェクトが同じソリューション内にある場合でも、デバッグ対象のプロセスによって開始された子プロセスに自動的にアタッチされません。 子プロセスをデバッグするには:   
> 
> - 子プロセスが開始された後、そのプロセスにアタッチします。  
> 
>   または  
>   - デバッガーの新しいインスタンスで子プロセスが自動的に開始されるように Windows を構成します。  
  
### <a name="start-debugging-multiple-processes-in-a-visual-studio-solution"></a><a name="BKMK_Start_debugging_multiple_processes_in_a_Visual_Studio_solution"></a>Visual Studio ソリューションで複数のプロセスのデバッグを開始する  
 Visual Studio ソリューション内に独立して実行できる複数のプロジェクト (個別のプロセスで実行されるプロジェクト) があるときは、デバッガーによって起動されるプロジェクトを選択できます。  
  
 ![プロジェクトのスタートアップの種類の変更](../debugger/media/dbg-execution-startmultipleprojects.png "DBG_Execution_StartMultipleProjects")  
  
#### <a name="change-the-startup-project"></a><a name="BKMK_Change_the_startup_project"></a>スタートアップ プロジェクトを変更する  
 ソリューションのスタートアップ プロジェクトを変更するには、ソリューション エクスプローラーでプロジェクトを選択し、コンテキスト メニューから **[スタートアップ プロジェクトとして設定**] を選択します。  
  
#### <a name="start-a-specific-project-in-a-solution"></a><a name="BKMK_Start_a_specific_project_in_a_solution"></a>ソリューション内の特定のプロジェクトを開始する  
 既定のスタートアップ プロジェクトを変更せずにソリューションのプロジェクトを開始するには、ソリューション エクスプローラーでプロジェクトを選択し、コンテキスト メニューから **[デバッグ**] を選択します。 次に、[**新しいインスタンスの開始**] または **[新しいインスタンスにステップ イン**] を選択できます。  
  
 ![トップに戻る](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [VS ソリューションで複数のプロセスを開始し、プロセスにアタッチし、デバッガーでプロセスを自動的に開始します。](../debugger/debug-multiple-processes.md#BKMK_Start_multiple_processes_in_a_VS_solution__attach_to_a_process__automatically_start_a_process_in_the_debugger)  
  
 ![トップコンテンツに戻る](../debugger/media/pcs-backtotop.png "PCS_BackToTop")[Contents](#BKMK_Contents)  
  
#### <a name="start-multiple-projects-in-a-solution"></a><a name="BKMK_Start_multiple_projects_in_a_solution"></a>ソリューション内の複数のプロジェクトを開始する  
  
1. ソリューション エクスプローラーでソリューションを選択し、コンテキスト メニューの **[プロパティ]** をクリックします。  
  
2. [**プロパティ]** ダイアログ ボックスで、[共通プロパティ] の **[スタートアップ プロジェクト****] を**選択します。  
  
3. 変更するプロジェクトごとに、[**開始**]、[**デバッグなしで開始**]、[**なし**] のいずれかを選択します。  
  
   ![トップに戻る](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [VS ソリューションで複数のプロセスを開始し、プロセスにアタッチし、デバッガーでプロセスを自動的に開始します。](../debugger/debug-multiple-processes.md#BKMK_Start_multiple_processes_in_a_VS_solution__attach_to_a_process__automatically_start_a_process_in_the_debugger)  
  
   ![トップコンテンツに戻る](../debugger/media/pcs-backtotop.png "PCS_BackToTop")[Contents](#BKMK_Contents)  
  
### <a name="attach-to-a-process"></a><a name="BKMK_Attach_to_a_process"></a>プロセスにアタッチする  
 デバッガーは、リモート デバイスで実行されているプログラムを含む、Visual Studio の外部のプロセスで実行されているプログラムに*アタッチ*することもできます。 プログラムにアタッチした後、デバッガーの実行コマンドを使用したり、プログラムの状態をチェックしたりできます。 プログラムのチェック機能は、デバッグ情報付きでビルドされたプログラムかどうか、プログラムのソース コードにアクセスできるかどうか、および共通言語ランタイムの JIT コンパイラがデバッグ情報を追跡しているかどうかによって限定される場合があります。  
  
 詳細については、「[実行中のプロセスにアタッチ](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)する」を参照してください。  
  
 **ローカル コンピューター上で実行されているプロセスにアタッチする**  
  
 [**デバッグ**] の [**プロセスにアタッチ ] を**選択します。 [**プロセスにアタッチ]** ダイアログ ボックスで、[**使用可能なプロセス**] ボックスの一覧からプロセスを選択し、[**アタッチ**] をクリックします。  
  
 ![[プロセスにアタッチ] ダイアログ ボックス](../debugger/media/dbg-attachtoprocessdlg.png "DBG_AttachToProcessDlg")  
  
 ![トップコンテンツに戻る](../debugger/media/pcs-backtotop.png "PCS_BackToTop")[Contents](#BKMK_Contents)  
  
### <a name="automatically-start-a-process-in-the-debugger"></a><a name="BKMK_Automatically_start_an_process_in_the_debugger"></a>デバッガーでプロセスを自動的に開始する  
 場合によっては、別のプロセスで起動されたプログラムのスタートアップ コードをデバッグする必要があります。 たとえば、サービスやカスタムのセットアップ動作などです。 このような場合、アプリケーションの起動時にデバッガーを起動して自動的にアタッチできます。  
  
1. レジストリ エディタ **(regedit.exe)** を起動します。  
  
2. **HKEY_LOCAL_MACHINE\ソフトウェア\マイクロソフト\Windows NT\現在のバージョン\イメージ ファイル実行オプション**フォルダーに移動します。  
  
3. デバッガーで起動するアプリのフォルダーを選択します。  
  
    アプリの名前が子フォルダーとして表示されていない場合は、[**イメージ ファイルの実行オプション**] を選択し、コンテキスト メニューの **[新規**]、[**キー** ] の順に選択します。 新しいキーを選択し、ショートカット メニューの **[名前の変更**] をクリックして、アプリの名前を入力します。  
  
4. アプリ フォルダーのコンテキスト メニューで、[**新規作成**]、[**文字列値**] の順に選択します。  
  
5. 新しい値の名前を **[新しい値]** から に`debugger`変更します。  
  
6. デバッガー エントリのコンテキスト メニューで、[**変更**] を選択します。  
  
7. [文字列の編集] ダイアログ`vsjitdebugger.exe`ボックスで、[**値のデータ**] ボックスに入力します。  
  
    ![[文字列の編集] ダイアログ ボックス](../debugger/media/dbg-execution-automaticstart-editstringdlg.png "DBG_Execution_AutomaticStart_EditStringDlg")  
  
   ![regedit.exe の自動デバッガー開始エントリ](../debugger/media/dbg-execution-automaticstart-result.png "DBG_Execution_AutomaticStart_Result")  
  
   ![トップコンテンツに戻る](../debugger/media/pcs-backtotop.png "PCS_BackToTop")[Contents](#BKMK_Contents)  
  
## <a name="switch-processes-break-and-continue-execution-step-through-source"></a><a name="BKMK_Switch_processes__break_and_continue_execution__step_through_source"></a>プロセスの切り替え、実行の中断と続行、ソースのステップ実行  
  
- [プロセスの切り替え](#BKMK_Switch_between_processes)•[ブレーク、ステップ、続行コマンド](#BKMK_Break__step__and_continue_commands)  
  
### <a name="switch-between-processes"></a><a name="BKMK_Switch_between_processes"></a> プロセスの切り替え  
 デバッグ中には複数のプロセスにアタッチできますが、デバッガーでアクティブになっているプロセスは常に 1 つだけです。 アクティブまたは*現在*のプロセスは、[デバッグの場所] ツールバーまたは [**プロセス]** ウィンドウで設定できます。 プロセス間で切り替えるには、両方のプロセスが中断モードであることが必要です。  
  
 **現在のプロセスを設定するには**  
  
- [デバッグの場所] ツールバーの [**プロセス**] を選択して、[**プロセス**] リスト ボックスを表示します。 現在のプロセスとして指定するプロセスを選択します。  
  
   ![プロセスを切り替える](../debugger/media/dbg-execution-switchbetweenmodules.png "DBG_Execution_SwitchBetweenModules")  
  
   [**デバッグの場所]** ツールバーが表示されていない場合は、[**ツール]** の **[カスタマイズ**] を選択します。 [**ツール バー** ] タブで、[**デバッグの場所**] を選択します。  
  
- 「**プロセス」** ウィンドウ (ショートカット**の Ctrl+Alt+Z)** を開き、現在のプロセスとして設定するプロセスを探し、ダブルクリックします。  
  
   ![[プロセス] ウィンドウ](../debugger/media/dbg-processeswindow.png "DBG_ProcessesWindow")  
  
   現在のプロセスが黄色の矢印でマークされます。  
  
  プロジェクトを切り替えると、そのプロジェクトがデバッグ対象の現在のプロセスに設定されます。 表示するすべてのデバッガー ウィンドウに、現在のプロセスの状態が表示され、すべてのステップ実行コマンドは現在のプロセスにのみ影響を与えます。  
  
  ![トップスイッチプロセスに戻り](../debugger/media/pcs-backtotop.png "PCS_BackToTop")[、中断して実行を継続し、ソースをステップ実行](../debugger/debug-multiple-processes.md#BKMK_Switch_processes__break_and_continue_execution__step_through_source)  
  
  ![トップコンテンツに戻る](../debugger/media/pcs-backtotop.png "PCS_BackToTop")[Contents](#BKMK_Contents)  
  
### <a name="break-step-and-continue-commands"></a><a name="BKMK_Break__step__and_continue_commands"></a> 中断、ステップ実行、続行のコマンド  
  
> [!NOTE]
> 既定では、中断、続行、ステップ実行のコマンドはデバッグ中のすべてのプロセスに影響を与えます。 この動作を変更するには、[複数のプロセスの実行動作の構成を](#BKMK_Configure_the_execution_behavior_of_multiple_processes)参照してください。  
  
||||  
|-|-|-|  
|**コマンド**|**1 つのプロセスが中断したときにすべてのプロセスを中断する**<br /><br /> オンにした場合 (既定)|**1 つのプロセスが中断したときにすべてのプロセスを中断する**<br /><br /> クリア|  
|**デバッグ**メニュー:<br /><br /> -   **すべてを破る**|すべてのプロセスが中断されます。|すべてのプロセスが中断されます。|  
|**デバッグ**メニュー:<br /><br /> -   **続行**|すべてのプロセスが再開されます。|一時停止中のすべてプロセスが再開されます。|  
|**デバッグ**メニュー:<br /><br /> -   **ステップイン**<br />-   **ステップオーバー**<br />-   **ステップアウト**|現在のプロセスのステップ実行中にすべてのプロセスが実行されます。<br /><br /> その後、すべてのプロセスが中断されます。|現在のプロセスがステップ実行されます。<br /><br /> 一時停止中のプロセスが再開されます。<br /><br /> 実行中のプロセスが続行されます。|  
|**デバッグ**メニュー:<br /><br /> -   **現在のプロセスにステップ イン**<br />-   **現在のプロセスをステップ オーバーする**<br />-   **現在のプロセスをステップアウトする**|該当なし|現在のプロセスがステップ実行されます。<br /><br /> 他のプロセスの既存の状態 (一時停止中または実行中) が維持されます。|  
|ソース ウィンドウ<br /><br /> -   **ブレークポイント**|すべてのプロセスが中断されます。|ソース ウィンドウのプロセスのみ中断されます。|  
|ソース ウィンドウのコンテキスト メニュー: <br /><br /> -   **カーソルまで実行**<br /><br /> ソース ウィンドウのプロセスは現在のプロセスであることが必要です。|ソース ウィンドウのプロセスがカーソル位置まで実行されてから中断されている間に、すべてのプロセスが実行されます。<br /><br /> その後、他のすべてのプロセスが中断されます。|ソース ウィンドウのプロセスはカーソル位置まで実行されます。<br /><br /> 他のプロセスの既存の状態 (一時停止中または実行中) が維持されます。|  
|**プロセスウィンドウの**コンテキストメニュー:<br /><br /> -   **プロセスを中断する**|該当なし|選択したプロセスが中断されます。<br /><br /> 他のプロセスの既存の状態 (一時停止中または実行中) が維持されます。|  
|**プロセスウィンドウの**コンテキストメニュー:<br /><br /> -   **プロセスの続行**|該当なし|選択したプロセスが再開されます。<br /><br /> 他のプロセスの既存の状態 (一時停止中または実行中) が維持されます。|  
  
 ![トップスイッチプロセスに戻り](../debugger/media/pcs-backtotop.png "PCS_BackToTop")[、中断して実行を継続し、ソースをステップ実行](../debugger/debug-multiple-processes.md#BKMK_Switch_processes__break_and_continue_execution__step_through_source)  
  
 ![トップコンテンツに戻る](../debugger/media/pcs-backtotop.png "PCS_BackToTop")[Contents](#BKMK_Contents)  
  
## <a name="stop-debugging-terminate-or-detach-from-processes"></a><a name="BKMK_Stop_debugging__terminate_or_detach_from_processes"></a>デバッグの停止、終了、またはプロセスからのデタッチ  
  
- [停止、終了、デタッチのコマンド](#BKMK_Stop__terminate__and_detach_commands)  
  
  既定では、**デバッグ**、 デバッガーで複数のプロセスが開かれているときに**デバッグを停止**を選択すると、デバッガーは、デバッガーでプロセスが開かれた方法に応じて、すべてのプロセスを終了またはデタッチします。  
  
- 現在のプロセスがデバッガーで開始された場合、そのプロセスは終了します。  
  
- デバッガーを現在のプロセスにアタッチした場合、デバッガーはプロセスからデタッチされ、プロセスは実行中のままになります。  
  
  たとえば、Visual Studio ソリューションからプロセスのデバッグを開始し、既に実行中の別のプロセスにアタッチし、[**デバッグの停止**] を選択すると、デバッグ セッションが終了し、Visual Studio で開始されたプロセスは終了し、アタッチしたプロセスは実行されたままです。 次の手順を使用してデバッグの停止方法を制御できます。  
  
> [!NOTE]
> **[1 つのプロセスが中断したときにすべてのプロセスを中断する**] オプションは、デバッグの停止やプロセスからの終了とデタッチには影響しません。  
  
 **デバッグの停止による個々のプロセスへの影響を変更するには**  
  
- **[プロセス]** ウィンドウを開きます (**ショートカット Ctrl + Alt + Z**)。 プロセスを選択し、[**デバッグが停止したときにデタッチ**する] チェック ボックスをオンまたはオフにします。  
  
### <a name="stop-terminate-and-detach-commands"></a><a name="BKMK_Stop__terminate__and_detach_commands"></a>コマンドの停止、終了、およびデタッチ  
  
|||  
|-|-|  
|**コマンド**|**説明**|  
|**デバッグ**メニュー:<br /><br /> -   **デバッグの停止**|デバッグ停止時に **[プロセス]** ウィンドウ**の[デタッチ]** オプションで動作が変更されない限り、次の操作を行います。<br /><br /> 1. デバッガによって開始されたプロセスは終了します。<br />2. アタッチされたプロセスはデバッガからデタッチされます。|  
|**デバッグ**メニュー:<br /><br /> -   **すべて終了**|すべてのプロセスが終了します。|  
|**デバッグ**メニュー:<br /><br /> -   **すべてを取り外す**|すべてのプロセスからデバッガーがデタッチされます。|  
|**プロセスウィンドウの**コンテキストメニュー:<br /><br /> -   **プロセスのデタッチ**|選択したプロセスからデバッガーがデタッチされます。<br /><br /> 他のプロセスの既存の状態 (一時停止中または実行中) が維持されます。|  
|**プロセスウィンドウの**コンテキストメニュー:<br /><br /> -   **プロセスの終了**|選択したプロセスが終了します。<br /><br /> 他のプロセスの既存の状態 (一時停止中または実行中) が維持されます。|  
|**プロセスウィンドウの**コンテキストメニュー:<br /><br /> -   **デバッグが停止したときにデタッチする**|選択したプロセスの**デバッグ**、**デバッグの停止**の動作を切り替えます。<br /><br /> - オン: デバッガーがプロセスからデタッチします。<br />- クリア: プロセスが終了します。|  
  
 ![トップに戻る](../debugger/media/pcs-backtotop.png "PCS_BackToTop")[デバッグを停止、終了、またはプロセスからデタッチ](../debugger/debug-multiple-processes.md#BKMK_Stop_debugging__terminate_or_detach_from_processes)  
  
 ![トップコンテンツに戻る](../debugger/media/pcs-backtotop.png "PCS_BackToTop")[Contents](#BKMK_Contents)  
  
## <a name="see-also"></a>参照  
 [シンボル (.pdb) とソース ファイルの指定](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)   
 [実行中のプロセスにアタッチ](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)   
 [デバッガーを使用したコード間の移動](../debugger/navigating-through-code-with-the-debugger.md)   
 [ジャストインタイムデバッグ](../debugger/just-in-time-debugging-in-visual-studio.md)   
 [マルチスレッド アプリケーションのデバッグ](../debugger/debug-multithreaded-applications-in-visual-studio.md)
