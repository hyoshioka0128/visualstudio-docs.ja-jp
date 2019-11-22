---
title: Attach to Running Processes with the Debugger | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.processes.attach
- vs.debug.process
- vs.debug.programs
- vs.debug.detaching
- vs.debug.processes
- vs.debug.error.attach
- vs.debug.remotemachine
dev_langs:
- C++
- CSharp
- FSharp
- VB
- c++
helpviewer_keywords:
- remote debugging, attaching to programs
- processes, attaching to running processes
- Attach to Process dialog box
- debugging [Visual Studio], attaching to processes
- debugger, processes
ms.assetid: 27900e58-090c-4211-a309-b3e1496d5824
caps.latest.revision: 62
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 03cd890802e5563ce2daeb78438c56f4452d74f0
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74299518"
---
# <a name="attach-to-running-processes-with-the-visual-studio-debugger"></a>実行中のプロセスへのアタッチ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ローカルまたはリモート コンピューターで実行中のプロセスに、Visual Studio デバッガーをアタッチできます。 After the process is running, click **Debug / Attach to Process** (or press **CTRL+ALT+P**) to open the **Attach to Process** dialog box.

You can use this capability to debug apps that are running on a local or remote computer, debug multiple processes simultaneously, or debug an application that was not created in Visual Studio. It is often useful when you want to debug an app, but (for whatever reason) you did not start the app from Visual Studio with the debugger attached. For example, if you are running the app without the debugger and hit an exception, you might then attach to the process running the app to begin debugging.

> [!TIP]
> Not sure whether you need to use **Attach to Process** for your debugging scenario? See [Common debugging scenarios](#BKMK_Scenarios). If you want to debug ASP.NET applications that have been deployed to IIS, see [Remote Debugging ASP.NET on a remote IIS computer](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md).

## <a name="BKMK_Attach_to_a_running_process"></a> Attach to a running process on the local machine
 In order to attach to a process, you must know the name of the process (see [Common debugging scenarios](#BKMK_Scenarios) for a few common process names).

1. In Visual Studio, select **Debug / Attach to Process** (or press **CTRL+ALT+P**).

2. **[プロセスにアタッチ]** ダイアログ ボックスの **[選択可能なプロセス]** ボックスの一覧で、アタッチするプログラムを探します。

     To quickly select the process you want, type the first letter of the process name. If you don't know the process name, see [Common debugging scenarios](#BKMK_Scenarios).

     ![DBG_Basics_Attach_To_Process](../debugger/media/dbg-basics-attach-to-process.png "DBG_Basics_Attach_To_Process")

     プロセスが別のユーザー アカウントで実行されている場合は、 **[すべてのユーザーからのプロセスを表示する]** チェック ボックスをオンにします。

3. **[アタッチ先]** ボックスに、デバッグするコードの種類が表示されていることを確認します。 既定の **[自動]** 設定では、デバッグするコードの種類が自動的に判断されます。 コードの種類を手動で設定するには、次の操作を行います

    1. **[プロセスにアタッチ]** ボックスで、 **[選択]** をクリックします。

    2. **[コードの種類の選択]** ダイアログ ボックスで、 **[次のコードの種類をデバッグする]** をクリックし、デバッグする種類を選択します。

    3. **[OK]** をクリックします。

4. **[アタッチ]** をクリックします。

## <a name="BKMK_Attach_to_a_process_on_a_remote_computer"></a>リモート コンピューター上のプロセスにアタッチする
 In order to attach to a process, you must know the name of the process (see [Common debugging scenarios](#BKMK_Scenarios) for a few common process names). For more complete guidance for ASP.NET apps that have been deployed to IIS, see [Remote Debugging ASP.NET on a remote IIS computer](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md). 他のアプリについては、タスク マネージャーで、プロセスの名前を検索できる場合があります。

 **[プロセスにアタッチ]** ダイアログ ボックスでは、リモート デバッグ用にセットアップした他のコンピューターを選択できます。 For more information, see [Remote Debugging](https://msdn.microsoft.com/library/90f45630-0d26-4698-8c1f-63f85a12db9c). リモート コンピューターを選択すると、そのコンピューターで実行されている選択可能なプロセスの一覧を表示して、1 つ以上のプロセスにアタッチしてデバッグを実行できます。

 **To select a remote computer:**

1. In Visual Studio, select **Debug / Attach to Process** (or press **CTRL+ALT+P**).

2. **[プロセスにアタッチ]** ダイアログ ボックスの **[トランスポート]** ボックスの一覧で、該当する接続の種類を選択します。 **[既定値]** は、ほとんどの場合に適切な設定です。

   **[トランスポート]** の設定は、デバッグ セッション間で保持されます。

3. **[修飾子]** ボックスの一覧でリモート コンピューター名を選択します。以下のいずれかの方法を使用します。

   1. **[修飾子]** ボックスの一覧に名前を入力します。

      > [!NOTE]
      > If, in later steps, you can't connect using the remote computer name, use the IP address. (The port number may appear automatically after selecting the process. You can also enter it manually. In the illustration below, 4020 is the default port for the remote debugger.)

   2. **[修飾子]** ボックスの一覧の横のドロップダウン矢印をクリックし、一覧でコンピューター名を選択します。

   3. Click the **Find** button next to the **Qualifier** list to open the **Select Remote Debugger Connection** dialog box. **[リモート デバッガー接続の選択]** ダイアログ ボックスには、ローカル サブネット上にあるデバイスと、イーサネット ケーブルで自分のコンピューターに直接接続されているデバイスがすべて表示されます。 目的のコンピューターまたはデバイスをクリックし、 **[選択]** をクリックします。

      **[修飾子]** の設定は、その修飾子でデバッグ接続が成功した場合のみ、デバッグ セッション間で保持されます。

4. **[最新の情報に更新]** をクリックします。

     **[プロセス]** ダイアログ ボックスを開くと、 **[選択可能なプロセス]** ボックスが自動的に表示されます。 このダイアログ ボックスが開いている間に、プロセスをバックグラウンドで開始および停止できます。 このため、内容が常に最新であるとは限りません。 **[更新]** をクリックすると、いつでも一覧の内容を更新して、現在のプロセス一覧を確認できます。

5. **[プロセスにアタッチ]** ダイアログ ボックスの **[選択可能なプロセス]** ボックスの一覧で、アタッチするプログラムを探します。

    プロセスが別のユーザー アカウントで実行されている場合は、 **[すべてのユーザーからのプロセスを表示する]** チェック ボックスをオンにします。

6. **[アタッチ]** をクリックします。

## <a name="additional-info"></a>Additional info

デバッグ中には複数のプログラムにアタッチできますが、デバッガーでアクティブになっているプログラムは常に 1 つだけです。 アクティブなプログラムは、 **[デバッグの場所]** ツール バーまたは **[プロセス]** ウィンドウで設定できます。 詳細については、「 [方法 : 現在のプロセスを設定する](https://msdn.microsoft.com/7e1d7fa5-0e40-44cf-8c41-d3dba31c969e)」を参照してください。

信頼関係のないユーザー アカウントによって所有されているプロセスにアタッチしようとすると、セキュリティ警告の確認ダイアログ ボックスが表示されます。 詳細については、次を参照してください。[セキュリティ警告。信頼されていないユーザーによって所有されているプロセスにアタッチすると、危険なことができます。以下の情報に関して疑わしい点がある場合や、不明な場合は、このプロセスにアタッチしないでください](/visualstudio/debugger/security-warning-attaching-to-a-process-owned-by-an-untrusted-user?view=vs-2015)。

リモート デスクトップ (ターミナル サービス) セッションでのデバッグ時には、 **[選択可能なプロセス]** ボックスに、使用可能なプロセスのすべてが表示されない場合があります。 Visual Studio を、制限付きユーザー アカウントを持つユーザーとして実行している場合、 **[選択可能なプロセス]** ボックスの一覧には、セッション 0 で実行しているプロセスは表示されません。セッション 0 は、サービスおよび w3wp.exe を含むその他のサーバー プロセス用に使用されます。 この問題を解決するには、管理者アカウントで [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] を実行するか、ターミナル サービス セッションからではなくサーバー コンソールから [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] を実行します。 どちらの方法も実行できない場合、3 つ目の方法として、Windows コマンド ラインから `vsjitdebugger.exe -p` *ProcessId* を実行することによって、プロセスにアタッチできます。 プロセス ID は tlist.exe を使用して確認できます。 tlist.exe を入手するには、「  [WDK と WinDbg のダウンロード](https://go.microsoft.com/fwlink/?LinkId=168279)」で Windows 対応のデバッグ ツールをダウンロードし、インストールします。

## <a name="BKMK_Scenarios"></a> Common debugging scenarios

To help you identify whether you need to use **Attach to process** and what process to attach to, a few common debugging scenarios are shown here (the list is not exhaustive). Where more instructions are available, we provide links.

For some app types (like Windows Store apps), you don't attach directly to a process name, but use the **Debug Installed App Package** menu option instead (see table).

> [!NOTE]
> For information about basic debugging in Visual Studio, see [Getting started with the debugger](../debugger/getting-started-with-the-debugger.md).

|通信の種類|Debug Method|[プロセス名]|Notes and Links|
|-|-|-|-|
|Debug a managed or native app on the local machine|Use attach to process or [standard debugging](../debugger/getting-started-with-the-debugger.md)|*appname*.exe|To quickly access the dialog box, use **CTRL+ALT+P** and then type the first letter of the process name.|
|Debug ASP.NET apps on the local machine after starting the app without the debugger|Use attach to process|iiexpress.exe|This may be helpful to make your app load faster, such as (for example) when profiling. |
|Remote debug ASP.NET 4 or 4.5 on an IIS server|Use remote tools and attach to process|w3wp.exe|See [Remote Debugging ASP.NET on a remote IIS computer](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md)|
|Remote debug ASP.NET Core on an IIS server|Use remote tools and attach to process|dnx.exe|For app deployment, see [Publish to IIS](https://docs.asp.net/en/latest/publishing/iis.html). For debugging, see [Remote Debugging ASP.NET on a remote IIS computer](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md)|
|Debug other supported app types on a server process|Use remote tools (if server is remote) and attach to process|iexplore.exe or other processes|If necessary, use Task Manager to help identify the process. See [Remote Debugging](../debugger/remote-debugging.md) and later sections in this topic|
|Remote debug a Windows desktop app|Remote Tools and F5|N/A| See [Remote Debugging](../debugger/remote-debugging.md)|
|Remote debug a Windows Universal (UWP), OneCore, HoloLens, or IoT app|インストールされているアプリ パッケージのデバッグ|N/A|Use **Debug / Other Debug Targets / Debug Installed App Package** instead of **Attach to process**|
|Debug a Windows Universal (UWP), OneCore, HoloLens, or IoT app that you didn't start from Visual Studio|インストールされているアプリ パッケージのデバッグ|N/A|Use **Debug / Other Debug Targets / Debug Installed App Package** instead of **Attach to process**|

> [!WARNING]
> JavaScript で記述された Windows ユニバーサル アプリにアタッチするには、まずそのアプリに対してデバッグを有効にする必要があります。 Windows デベロッパー センター内の「 [Attach the debugger](../debugger/start-a-debugging-session-for-store-apps-in-visual-studio-javascript.md#BKMK_Attach_the_debugger) 」をご覧ください。

> [!NOTE]
> C++ で記述されたコードにデバッガーをアタッチするには、コードが `DebuggableAttribute`を生成する必要があります。 [/ASSEMBLYDEBUG](https://msdn.microsoft.com/library/94443af3-470c-41d7-83a0-7434563d7982) リンカー オプションを使ってリンクすると、これを自動的にコードに追加できます。

## <a name="what-debugger-features-can-i-use"></a>What debugger features can I use?

To use the full features of the Visual Studio debugger (like hitting breakpoints) when attaching to a process, the executable must exactly match your local source and symbols (that is, the debugger must be able to load the correct [symbol (.pbd) files](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)). By default, this requires a debug build.

For remote debugging scenarios, you must have the source code (or a copy of the source code) already open in Visual Studio. The compiled app binaries on the remote machine must come from the same build as on the local machine.

In some local debugging scenarios, you can debug in Visual Studio with no access to the source if the correct symbol files are present with the app (by default, this requires a debug build). For more info, see [Specify Symbol and Source Files](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md).

## <a name="BKMK_Troubleshoot_attach_errors"></a>アタッチ エラーをトラブルシューティングする
 実行中のプロセスにデバッガーがアタッチすると、このプロセスは、1 種類以上のコードを含むことができます。 デバッガーをアタッチできるコードの種類は **[コードの種類の選択]** ダイアログ ボックスで表示されて選択されています。

 デバッガーは、ある種類のコードに正常にアタッチできても、別の種類にはアタッチできないことがあります。 この問題は、リモート コンピューターで動作しているプロセスにアタッチしようとする場合に発生することがあります。 リモート コンピューターには、一部の種類のコードにしか対応しないリモート デバッグ コンポーネントがインストールされている場合があるためです。 また、ダイレクト データベース デバッグのために複数のプロセスにアタッチしようとした場合にも発生することがあります。 SQL デバッグ機能は、単一プロセスへのアタッチのみをサポートします。

 デバッガーが一部の種類のコードにしかアタッチできない場合は、アタッチできなかった種類を識別するメッセージが表示されます。

 デバッガーが少なくとも 1 種類のコードに正常にアタッチできる場合は、プロセスのデバッグを開始できます。 正常にアタッチされたコードの種類のみをデバッグできます。 上記のメッセージの例は、種類がスクリプトのコードにアタッチできなかったことを示しています。 この場合、プロセス内でスクリプト コードをデバッグできません。 プロセス内のスクリプト コードはそのまま実行されますが、スクリプトでのブレークポイントの設定、データの表示、またはその他のデバッグ操作は実行できません。

 デバッガーがコードの種類へのアタッチに失敗した理由についてより詳しい情報が必要な場合は、該当するコードの種類のみに再アタッチを試行できます。

 **To obtain specific information about why a code type failed to attach**

1. プロセスからデタッチします。 **[デバッグ]** メニューの **[すべてデタッチ]** をクリックします。

2. コードの種類を 1 つだけ選択して、プロセスに再度アタッチします。

   1. **[プロセスにアタッチ]** ダイアログ ボックスの **[選択可能なプロセス]** ボックスの一覧で、プロセスを選択します。

   2. **[選択]** をクリックします。

   3. **[コードの種類の選択]** ダイアログ ボックスの **[次のコードの種類をデバッグする]** をクリックし、アタッチに失敗したコードの種類を選択します。 他のコードをすべてオフにします。

   4. **[OK]** をクリックします。 **[コードの種類の選択]** ダイアログ ボックスが閉じます。

   5. **[プロセスにアタッチ]** ダイアログ ボックスで、 **[アタッチ]** をクリックします。

      このとき、アタッチは完全に失敗し、詳細なエラー メッセージが表示されます。

## <a name="see-also"></a>参照
 [Debug Multiple Processes](../debugger/debug-multiple-processes.md) [Just-In-Time Debugging](../debugger/just-in-time-debugging-in-visual-studio.md) [Remote Debugging](../debugger/remote-debugging.md)
