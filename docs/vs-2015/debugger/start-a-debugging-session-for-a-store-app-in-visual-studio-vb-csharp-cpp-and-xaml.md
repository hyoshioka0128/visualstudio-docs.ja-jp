---
title: ストアアプリのデバッグセッションを開始する (VB、 C#、 C++および XAML) |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- VC.Project.IVCAppHostRemoteDebugPageObject.MachineName
- VC.Project.IVCAppHostRemoteDebugPageObject.BreakpointBehavior
- VC.Project.IVCAppHostLocalDebugPageObject.GPUDebuggerTargetType
- VC.Project.IVCAppHostTetheredDebugPageObject.DebuggerType
- VC.Project.IVCAppHostLocalDebugPageObject.BreakpointBehavior
- VC.Project.IVCAppHostRemoteDebugPageObject.LaunchApplication
- VC.Project.IVCAppHostRemoteDebugPageObject.GPUDebuggerTargetType
- VC.Project.IVCAppHostLocalDebugPageObject.DebuggerType
- VC.Project.IVCAppHostSimulatorDebugPageObject.DebuggerType
- ImmersiveProjects.Properties.Debug
- VC.Project.IVCAppHostTetheredDebugPageObject.LaunchApplication
- VC.Project.IVCAppHostSimulatorDebugPageObject.LaunchApplication
- VC.Project.IVCAppHostSimulatorDebugPageObject.GPUDebuggerTargetType
- VC.Project.IVCAppHostLocalDebugPageObject.LaunchApplication
- VC.Project.IVCAppHostLocalDebugPageObject.AllowLocalNetworkLoopback
- AppPackage.Properties.Debug
- VC.Project.IVCAppHostRemoteDebugPageObject.Authentication
- VC.Project.IVCAppHostRemoteDebugPageObject.DebuggerType
- VC.Project.IVCAppHostSimulatorDebugPageObject.BreakpointBehavior
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: 66ec0e79-8261-4c19-a618-3fd1b3f71bbd
caps.latest.revision: 23
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: f12d6cde30dec9062dd67a18558bd0571e6fe6b1
ms.sourcegitcommit: 3154387056160bf4c36ac8717a7fdc0cd9faf3f9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78409697"
---
# <a name="start-a-debugging-session-for-a-store-app-in-visual-studio-vb-c-c-and-xaml"></a>Visual Studio でのストア アプリのデバッグ セッションの開始 (VB、C#、C++、および XAML)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Windows および Windows Phone] (../Image/windows_and_phone_content "windows_and_phone_content")

 このトピックでは、XAML および Visual C++、Visual C#、または Visual Basic で記述されたストア アプリのデバッグ セッションを開始する方法について説明します。 アプリのデバッグには、デバッグ セッションの構成と、アプリの起動方法の選択の両方が関係します。

> [!NOTE]
> JavaScript および HTML で記述されたアプリについて[は、「デバッグセッションを開始する (javascript)](../debugger/start-a-debugging-session-for-store-apps-in-visual-studio-javascript.md)」を参照してください。

## <a name="BKMK_In_this_topic"></a> このトピックの内容
 [デバッグを開始する簡単な方法](#BKMK_The_easy_way_to_start_debugging)

 [デバッグ セッションを構成する](#BKMK_Configure_the_debugging_session)

- [プロジェクトのデバッグ プロパティ ページを開く](#BKMK_Open_the_debugging_property_page_for_the_project)

- [ビルド構成オプションを選択する](#BKMK_Choose_the_build_configuration_options)

- [配置ターゲットを選択する](#BKMK_Choose_the_deployment_target)

- [使用するデバッガーを選択する](#BKMK_Choose_the_debugger_to_use)

- [(省略可能) デバッグ セッションの開始を遅らせる](#BKMK__Optional__Delay_starting_the_debug_session)

- [(省略可能) ネットワーク ループバックを無効にする](#BKMK__Optional__Disable_network_loopbacks)

- [(省略可能) デバッグの開始時にアプリケーションを再インストールする](#BKMK__Optional__Reinstall_the_app_when_you_start_debugging)

- [(省略可能) リモート デバッガーを起動するための認証要件を無効にする](#BKMK__Optional__Disable_authentication_requirement_to_start_the_remote_debugger)

  [デバッグ セッションを開始する](#BKMK_Start_the_debugging_session)

- [デバッグを開始する (F5)](#BKMK_Start_debugging__F5_)

- [デバッグは開始する (F5 キー) がアプリの起動は遅らせる](#BKMK_Start_debugging__F5__but_delay_the_app_start)

- [デバッガーでインストール済みのアプリを起動する](#BKMK_Start_an_installed_app_in_the_debugger)

- [実行中のアプリにデバッガーをアタッチする](#BKMK_Attach_the_debugger_to_a_running_app_)

  - [デバッグ モードで実行するようにアプリを設定する](#BKMK_Set_the_app_to_run_in_debug_mode)

  - [デバッガーをアタッチします。](#BKMK_Attach_the_debugger)

## <a name="BKMK_The_easy_way_to_start_debugging"></a> デバッグを開始する簡単な方法

1. Visual Studio でアプリ ソリューションを開きます。

2. F5 キーを選択します。

   Visual Studio によってアプリがビルドされ、アタッチされたデバッガーが起動します。 実行は、ブレークポイントに達するか、実行が手動で中断されるか、ハンドルされていない例外が発生するか、アプリが終了するまで続行されます。 詳細については、「[デバッグセッションに移動するC#(Xaml および)](../debugger/navigate-a-debugging-session-in-visual-studio-xaml-and-csharp.md) 」を参照してください。

## <a name="BKMK_Configure_the_debugging_session"></a> デバッグ セッションを構成する

### <a name="BKMK_Open_the_debugging_property_page_for_the_project"></a> プロジェクトのデバッグ プロパティ ページを開く

1. ソリューション エクスプローラーでプロジェクトを選択します。 ショートカット メニューの **[プロパティ]** をクリックします。

2. 次の方法でプロジェクトのデバッグ プロパティ ページを開きます。

    - Visual C# アプリと Visual Basic アプリの場合は、 **[デバッグ]** をクリックします。

         ![C&#35; &#47; VB プロジェクトデバッグプロパティページ](../debugger/media/dbg-csvb-debugpropertypage.png "DBG_CsVb_DebugPropertyPage")

    - Visual C++ アプリの場合は、 **[構成プロパティ]**  ノードを展開し、 **[デバッグ]** をクリックします。

         ![C&#43; &#43; Windows ストアアプリのデバッグプロパティページ](../debugger/media/dbg-cpp-debugpropertypage.png "DBG_CPP_DebugPropertyPage")

### <a name="BKMK_Choose_the_build_configuration_options"></a> ビルド構成オプションを選択する

1. **[構成]** ボックスの一覧の **[デバッグ]** または **[(アクティブ) デバッグ]** をクリックします。

2. **[プラットフォーム]** ボックスの一覧で、ビルドするターゲット プラットフォームを選択します。 ほとんどの場合、 **[Any CPU]** (Visual C++ では **[すべてのプラットフォーム]** ) が最も適しています。

### <a name="BKMK_Choose_the_deployment_target"></a> 配置ターゲットを選択する
 ![Windows のみに適用されます](../debugger/media/windows-only-content.png "windows_only_content")

 Visual Studio コンピューター、ローカル コンピューター上の Visual Studio シミュレーター、またはリモート デバイス上に Windows ストア アプリを配置してデバッグできます。

- C# アプリと Visual Basic アプリの場合は、プロジェクトの **[デバッグ]** プロパティ ページの **[ターゲット デバイス]** ボックスの一覧からターゲットを選択します。

- C++ アプリの場合は、 **[デバッグ]** プロパティ ページの **[起動するデバッガー]** ボックスの一覧からターゲットを選択します。

  次のいずれかのオプションを選択します。

|||
|-|-|
|**ローカル コンピューター**|ローカル コンピューターの現在のセッションでアプリをデバッグします。 「[ローカルコンピューターでの Windows ストアアプリの実行」を](../debugger/run-windows-store-apps-on-the-local-machine.md)参照してください。|
|**シミュレーター**|[!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)] アプリ用の Visual Studio シミュレーターでアプリをデバッグします。 シミュレーターは、ローカル コンピューターでは使用できないデバイスの機能 (タッチ ジェスチャやデバイスの回転など) をデバッグできるようにするデスクトップ ウィンドウです。 「[シミュレーターでの Windows ストアアプリの実行」を](../debugger/run-windows-store-apps-in-the-simulator.md)参照してください。|
|**リモート コンピューター**|ローカル コンピューターにイントラネットを介して接続されているかイーサネット ケーブルを使用して直接接続されているデバイス上のアプリをデバッグします。 リモートでデバッグするには、リモート デバイス上に Visual Studio リモート ツールがインストールされ、実行されている必要があります。 「[リモートコンピューターでの Windows ストアアプリの実行](../debugger/run-windows-store-apps-on-a-remote-machine.md)」を参照してください。|

 **[リモート コンピューター]** をクリックした場合は、次のいずれかの方法でリモート コンピューターの IP アドレスを指定します。

- リモート コンピューターの IP アドレスを入力します。

  - C# アプリと Visual Basic アプリの場合は、 **[リモート コンピューター]** ボックスに名前または IP アドレスを入力します。

  - C++ アプリの場合は、 **[コンピューター名]** ボックスに名前または IP アドレスを入力します。

- **[リモート デバッガー接続の選択]** ダイアログ ボックスでリモート コンピューターを選択します。

   このダイアログ ボックスを開くには:

  - Visual C# アプリと Visual Basic アプリの場合は、 **[検索]** をクリックします。

  - アプリC++の場合は、 **[コンピューター名]** ボックスの下向き矢印をクリックし、[**検索\<] を選択します。>** 。

    ![[リモートデバッガー接続の選択] ダイアログボックス](../debugger/media/vsrun-selectremotedebuggerdlg.png "VSRUN_SelectRemoteDebuggerDlg")

  > [!NOTE]
  > **[リモート デバッガー接続の選択]** ダイアログ ボックスには、ローカル サブネット上にあるコンピューターとイーサネット ケーブルによって Visual Studio コンピューターに直接接続されているコンピューターが表示されます。 別のコンピューターを指定するには、 **[コンピューター名]** ボックスに名前を入力します。

  ![Windows Phone にのみ適用されます](../debugger/media/phone-only-content.png "phone_only_content")

  Windows Phone ストア アプリはデバイスまたは Visual Studio Phone エミュレーターの 1 つに配置できます。 **[ターゲット デバイス]** ボックスの一覧からデバイスまたはエミュレーターを選択します。

### <a name="BKMK_Choose_the_debugger_to_use"></a> 使用するデバッガーを選択する
 既定では、Visual Studio は C# アプリと Visual Basic アプリのマネージド コードをデバッグします。

 C# アプリと Visual Basic アプリでは、アプリのマネージド C/C++ コードとネイティブ C/C++ コードの両方をデバッグすることを選択できます。 デバッグ セッションにネイティブ コードを含めるには **[アンマネージ コード デバッグを有効にする]** チェック ボックスをオンにします。

 既定では、Visual Studio は C++ アプリのネイティブ コードをデバッグします。

 C++ アプリでは、ネイティブ コードの代わりに、またはネイティブ コードに加えて、アプリのコンポーネントで使用されている特定の種類のコードをデバッグすることを選択できます。 デバッグするコードは、アプリ プロジェクトの **[デバッグ]** プロパティ ページの **[デバッガーの種類]** の一覧で指定します。

 **[アプリケーション プロセス]** の一覧から次のデバッガーのいずれかを選択します。

|||
|-|-|
|**スクリプトのみ**|アプリの JAvaScript コードをデバッグします。 マネージド コードとネイティブ コードは無視されます。|
|**ネイティブのみ**|アプリのネイティブ コードと C/C++ コードをデバッグします。 マネージド コードと JAvaScript コードは無視されます。|
|**マネージドのみ**|アプリのマネージド コードをデバッグします。 JavaScript コードとネイティブ C/C++ コードは無視されます。|
|**混合 (マネージドとネイティブ)**|アプリのネイティブ C/C++ コードとマネージド コードをデバッグします。 JavaScript コードは無視されます。|
|**GPU のみ**|GPU (Graphics Processing Unit) で実行されるネイティブ C++ コードをデバッグします。|

 ![Windows Phone にのみ適用されます](../debugger/media/phone-only-content.png "phone_only_content")

 Windows ストア Phone アプリについては、 **[バックグラウンド タスク プロセス]** の一覧でバックグラウンド プロセスに使用するデバッガーを選択することもできます。

### <a name="BKMK__Optional__Delay_starting_the_debug_session"></a> (省略可能) デバッグ セッションの開始を遅らせる
 既定では、Visual Studio はデバッグの開始と同時にアプリを起動します。 デバッグ セッションは開始するが、アプリの起動は遅らせることもできます。 このオプションを選択すると、アプリは、スタート画面から起動されたとき、アクティブ化コントラクトによって起動されたとき、または別のプロセスやメソッドによって起動されたときに、デバッガー内で起動します。 アプリケーション自体が実行されていないときにバックグラウンド タスクをデバッグすると、アプリケーションの起動が遅くなります。

 アプリの起動を遅らせるには:

- Visual C# アプリと Visual Basic アプリの場合は、 **[デバッグ]** プロパティ ページの **[起動しないが、開始時にコードをデバッグ]** をクリックします。

- Visual C++ アプリの場合は、 **[デバッグ]** プロパティ ページの **[アプリケーションの起動]** ボックスの一覧の **[はい]** をクリックします。

### <a name="BKMK__Optional__Disable_network_loopbacks"></a> (省略可能) ネットワーク ループバックを無効にする
 ![Windows のみに適用されます](../debugger/media/windows-only-content.png "windows_only_content")

 セキュリティ上の理由から、標準的な方法でインストールされた Windows ストア アプリは、インストール先のデバイスに対してネットワーク呼び出しを行うことはできません。 既定では、Visual Studio による配置では、配置されたアプリに対するこの規則の適用は免除されます。 この免除によって、1 台のコンピューター上で通信プロシージャをテストできます。 Windows ストアにアプリを送信する前に、この免除なしでアプリをテストする必要があります。

 ネットワーク ループバックの免除を削除するには:

- Visual C# アプリおよび Visual Basic アプリの場合、 **[デバッグ]** プロパティ ページの **[ネットワーク ループバックの許可]** チェック ボックスをオフにします。

- Visual C++ アプリの場合は、 **[デバッグ]** プロパティ ページの **[ネットワーク ループバックの許可]** ボックスの一覧の **[いいえ]** をクリックします。

### <a name="BKMK__Optional__Reinstall_the_app_when_you_start_debugging"></a> (省略可能) デバッグの開始時にアプリケーションを再インストールする
 Visual C# または Visual Basic アプリケーションのインストールと初期化に関する問題を診断するには、デバッグの開始時に元のインストールを再作成するように **[デバッグ]** プロパティ ページの **[Uninstall and then reinstall my package]**  (パッケージをアンインストールしてから再インストールする) をクリックします。 このオプションは、Visual C++ プロジェクトでは使用できません。

### <a name="BKMK__Optional__Disable_authentication_requirement_to_start_the_remote_debugger"></a> (省略可能) リモート デバッガーを起動するための認証要件を無効にする
 ![Windows のみに適用されます](../debugger/media/windows-only-content.png "windows_only_content")

 既定では、リモート デバッガーを実行するために資格情報を指定する必要があります。

> [!IMPORTANT]
> リモート デバッガーを認証なしモードで実行することも選択できますが、このモードの使用は避けることを強く推奨します。 このモードで実行した場合、ネットワーク セキュリティはまったく提供されません。 認証なしモードは、ネットワークに悪意のあるコードや悪意のあるトラフィックのリスクがないことが確実である場合のみ選択してください。

 認証要件を削除するには:

1. Visual C# アプリおよび Visual Basic アプリの場合、 **[デバッグ]** プロパティ ページの **[認証を使用]** チェック ボックスをオフにします。

2. Visual C++ アプリの場合は、 **[デバッグ]** プロパティ ページの **[認証が必要]** ボックスの一覧の **[いいえ]** をクリックします。

   [このトピックの内容](#BKMK_In_this_topic)

## <a name="BKMK_Start_the_debugging_session"></a> デバッグ セッションを開始する

### <a name="BKMK_Start_debugging__F5_"></a> デバッグを開始する (F5)
 **[デバッグ]** メニューの **[デバッグの開始]** (キーボード: F5) を選択すると、デバッガーがアタッチされた状態でアプリが起動します。 実行は、ブレークポイントに達するか、実行が手動で中断されるか、例外が発生するか、アプリが終了するまで続行されます。

### <a name="BKMK_Start_debugging__F5__but_delay_the_app_start"></a> デバッグは開始する (F5 キー) がアプリの起動は遅らせる
 デバッグ モードで実行されるようにアプリを設定し、デバッガー以外の方法でアプリを起動できます。 たとえば、[スタート] メニューからのアプリの起動をデバッグしたり、アプリを起動せずにアプリのバックグラウンド プロセスをデバッグしたりできます。アプリの起動を遅らせるには、次の手順を実行します。

- アプリの **[デバッグ]** プロパティ ページで (Visual C++ の**デバッグ** )

  - Visual C# アプリと Visual Basic アプリの場合は、 **[起動しないが、開始時にコードをデバッグ]** をクリックします。

  - Visual C++ アプリの場合は、 **[アプリケーションの起動]** の一覧の **[Yes]** をクリックします。

- **[デバッグ]** メニューの **[デバッグの開始]** をクリックします (キーボードの場合: F5 キーを押します)。

- [スタート] メニュー、実行コントラクト、または別のプロシージャからアプリを起動します。

  アプリがデバッグ モードで起動します。 実行は、ブレークポイントに達するか、実行が手動で中断されるか、ハンドルされない例外が発生するか、アプリが終了するまで続行されます。

  。 バックグラウンドタスクのデバッグの詳細については、「 [Windows ストアの中断、再開、およびバックグラウンドイベントのトリガー](../debugger/how-to-trigger-suspend-resume-and-background-events-for-windows-store-apps-in-visual-studio.md)」を参照してください。

### <a name="BKMK_Start_an_installed_app_in_the_debugger"></a> デバッガーでインストール済みのアプリを起動する
 F5 キーを使用してデバッグを開始すると、Visual Studio はアプリをビルドして配置し、デバッグ モードで実行されるようにアプリを設定してから起動します。 デバイスに既にインストールされているアプリを起動するには、[インストールされているアプリケーション パッケージのデバッグ] ダイアログ ボックスを使用します。 この方法は、Windows ストアからインストールされたアプリをデバッグする必要がある場合や、アプリのソース ファイルはあってもアプリの Visual Studio プロジェクトがない場合に役立ちます。 Visual Studio プロジェクトやソリューションを使用しないカスタム ビルド システムがこれに該当します。

 アプリはローカル デバイスにインストールすることも、リモート デバイスにインストールすることもできます。  アプリをすぐに起動できます。また、アプリを別のプロセスや方法で起動したときに ([スタート] メニューからの起動や、アクティブ化コントラクトによる起動など)、デバッガーで実行するようにアプリを設定することもできます。アプリを起動せずにバックグラウンド プロセスをデバッグする場合は、デバッグ モードで実行されるようにアプリを設定できます。 詳細については、「 [Windows ストアの中断、再開、およびバックグラウンドイベントのトリガー](../debugger/how-to-trigger-suspend-resume-and-background-events-for-windows-store-apps-in-visual-studio.md)」を参照してください。

 インストール済みのアプリがデバッグ モードで実行されるように設定するには、次の手順を実行します。

> [!NOTE]
> この手順は、アプリが実行されていないときに開始してください。

1. **[デバッグ]** メニューの **[デバッグ] Installed App Package**をクリックします。

2. 一覧から次のいずれかのオプションを選択します。

   |                    |                                                                                                                                                                                                                                                                                                                                                                                                           |
   |--------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   | **ローカル コンピューター**  |                                                                                                                ローカル コンピューターの現在のセッションでアプリをデバッグします。 「[ローカルコンピューターでの Windows ストアアプリの実行」を](../debugger/run-windows-store-apps-on-the-local-machine.md)参照してください。                                                                                                                 |
   |   **シミュレーター**    | [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)] アプリ用の Visual Studio シミュレーターでアプリをデバッグします。 シミュレーターは、ローカル コンピューターでは使用できないデバイスの機能 (タッチ ジェスチャやデバイスの回転など) をデバッグできるようにするデスクトップ ウィンドウです。 「[シミュレーターでの Windows ストアアプリの実行」を](../debugger/run-windows-store-apps-in-the-simulator.md)参照してください。 |
   | **リモート コンピューター** |                          ローカル コンピューターにイントラネットを介して接続されているかイーサネット ケーブルを使用して直接接続されているデバイス上のアプリをデバッグします。 リモートでデバッグするには、リモート デバイス上に Visual Studio リモート ツールがインストールされ、実行されている必要があります。 「[リモートコンピューターでの Windows ストアアプリの実行](../debugger/run-windows-store-apps-on-a-remote-machine.md)」を参照してください。                           |

3. **[インストールされているアプリケーション パッケージ]** ボックスの一覧からアプリを選択します。

4. **[このコードの種類をデバッグ]** ボックスの一覧から、使用するデバッグ エンジンを選択します。

5. (省略可能)。 他の方法で起動したアプリをデバッグするときや、バックグラウンド プロセスをデバッグするときは、 **[起動しないが、開始時にコードをデバッグ]** を選択します。

   **[開始]** をクリックすると、アプリが起動するか、デバッグ モードで実行するように設定されます。

### <a name="BKMK_Attach_the_debugger_to_a_running_app_"></a> 実行中のアプリにデバッガーをアタッチする
 [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)] アプリにデバッガーをアタッチするには、デバッグ可能パッケージ マネージャーを使用して、デバッグ モードで実行するようにアプリを設定する必要があります。 デバッグ可能パッケージ マネージャーは、Visual Studio リモート ツールと共にインストールされます。

 アプリへのデバッガーのアタッチは、インストール済みのアプリ ( [!INCLUDE[win8_appstore_long](../includes/win8-appstore-long-md.md)]からインストールされたアプリなど) をデバッグする場合に役に立ちます。 アタッチは、アプリのソース ファイルはあるが、アプリの Visual Studio プロジェクトがない場合に必要です。 Visual Studio プロジェクトやソリューションを使用しないカスタム ビルド システムがこれに該当します。

 アプリにデバッガーをアタッチするには、次の手順に従う必要があります。

1. デバッグ モードで実行するようにアプリを設定します。 これは、アプリが実行されていないときに行う必要があります。

2. アプリを起動します。 アプリの起動は、スタート画面、実行コントラクト、または他の方法で実行できます。

3. 実行中のアプリにデバッガーをアタッチします。

#### <a name="BKMK_Set_the_app_to_run_in_debug_mode"></a> デバッグ モードで実行するようにアプリを設定する

1. アプリをインストールするデバイスに Visual Studio リモート ツールをインストールします。 「 [リモート ツールのインストール](https://msdn.microsoft.com/library/windows/apps/hh441469.aspx#BKMK_Installing_the_Remote_Tools)」を参照してください。

2. スタート画面で `Debuggable Package Manager` を検索して起動します。

     AppxDebug コマンドレット用に適切に構成された PowerShell ウィンドウが表示されます。

3. アプリのデバッグを有効にするには、アプリの PackageFullName 識別子を指定する必要があります。 PackageFullName を含むすべてのアプリの一覧を表示するには、PowerShell プロンプトに「 `Get-AppxPackage` 」と入力します。

4. PowerShell プロンプトで、「`Enable-AppxDebug` *PackageFullName* 」と入力します。ここで*PackageFullName*はアプリの PackageFullName 識別子です。

#### <a name="BKMK_Attach_the_debugger"></a> デバッガーをアタッチします。
 デバッガーをアタッチするには:

1. **[デバッグ]** メニューの **[プロセスにアタッチ]** をクリックします

    **[プロセスにアタッチ]** ダイアログ ボックスが表示されます。

2. リモート デバイス上のアプリにアタッチするには、 **[修飾子]** ボックスにリモート デバイスを指定します。 次のようにすることができます。

   - **[修飾子]** ボックスに名前を入力します。

   - **[修飾子]** ボックスの下向き矢印をクリックし、デバイスの一覧から前にアタッチしたデバイスを選択します。

   - **[検索]** をクリックし、ローカル サブネットのデバイスの一覧からデバイスを選択します。

3. デバッグするコードの種類を **[アタッチ先]** ボックスに指定します。

    **[選択]** をクリックし、次のいずれかを実行します。

   - **[デバッグするコードの種類を自動的に判断する]** をクリックします。

   - **[次のコードの種類をデバッグする]** をクリックし、一覧から 1 つ以上の型を選択します。

4. **[選択可能なプロセス]**  の一覧から、アプリのプロセスを選択します。

5. **[アタッチ]** をクリックします。

   Visual Studio によって、デバッガーがプロセスにアタッチされます。 実行は、ブレークポイントに達するか、実行が手動で中断されるか、ハンドルされない例外が発生するか、アプリが終了するまで続行されます。

   [このトピックの内容](#BKMK_In_this_topic)

## <a name="see-also"></a>参照
 [Visual Studio でのデバッグアプリ](../debugger/debug-store-apps-in-visual-studio.md)[のデバッグセッションのナビゲートC#(Xaml および)](../debugger/navigate-a-debugging-session-in-visual-studio-xaml-and-csharp.md)
