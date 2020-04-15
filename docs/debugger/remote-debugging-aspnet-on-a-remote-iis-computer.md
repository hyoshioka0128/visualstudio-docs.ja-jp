---
title: リモート IIS コンピュータ上のリモート デバッグ ASP.NET コア |マイクロソフトドキュメント
ms.custom: remotedebugging
ms.date: 05/21/2018
ms.topic: conceptual
ms.assetid: 573a3fc5-6901-41f1-bc87-557aa45d8858
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- aspnet
- dotnetcore
ms.openlocfilehash: b33ead969456935dab54c042ba4fbaf1f5ff44f4
ms.sourcegitcommit: cc58ca7ceae783b972ca25af69f17c9f92a29fc2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/15/2020
ms.locfileid: "81385478"
---
# <a name="remote-debug-aspnet-core-on-a-remote-iis-computer-in-visual-studio"></a>Visual Studio でリモート IIS コンピューター上のリモート デバッグ ASP.NET コア

IIS に展開されている ASP.NET Core アプリケーションをデバッグするには、アプリを展開したコンピューターにリモート ツールをインストールして実行し、Visual Studio から実行中のアプリにアタッチします。

![リモート デバッガー コンポーネント](../debugger/media/remote-debugger-aspnet.png "Remote_debugger_components")

このガイドでは、セットアップして、Visual Studio ASP.NET コアを構成し、IIS に配置し、Visual Studio からリモート デバッガーをアタッチする方法について説明します。 リモート デバッグ ASP.NET 4.5.2 については[、「IIS コンピュータのリモート デバッグ ASP.NET」](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md)を参照してください。 Azure を使用して IIS でデプロイおよびデバッグすることもできます。 Azure App Service の場合は、スナップショット デバッガーを使用するか、[サーバー エクスプローラーからデバッガーをアタッチ](../debugger/remote-debugging-azure.md)することで、IIS の構成済みインスタンスとリモート[デバッガー](../debugger/debug-live-azure-applications.md)で簡単にデプロイおよびデバッグできます。

## <a name="prerequisites"></a>前提条件

::: moniker range=">=vs-2019"
この記事に示す手順を実行するには、Visual Studio 2019 が必要です。
::: moniker-end
::: moniker range="vs-2017"
この記事に示す手順を実行するには、Visual Studio 2017 が必要です。
::: moniker-end

これらの手順は、次のサーバー構成でテストされています。
* 2012 年の R2 および IIS 8
* 2016 年と IIS 10

## <a name="network-requirements"></a>ネットワークの要件

プロキシ経由で接続された 2 台のコンピュータ間のデバッグはサポートされていません。 ダイヤルアップ インターネットやインターネット経由など、遅延が長い接続や帯域幅の低い接続を介したデバッグは推奨されず、失敗したり、許容できないほど遅くなる可能性があります。 要件の完全なリストについては、[要件](../debugger/remote-debugging.md#requirements_msvsmon)を参照してください。

## <a name="app-already-running-in-iis"></a>IIS で既に実行されているアプリですか?

この記事では、Windows サーバー上で IIS の基本構成を設定し、Visual Studio からアプリを展開する手順について説明します。 これらの手順は、サーバーに必要なコンポーネントがインストールされていること、アプリが正しく実行できること、リモート デバッグの準備ができていることを確認するために含まれています。

* アプリが IIS で実行されており、リモート デバッガーをダウンロードしてデバッグを開始するだけの場合は[、「Windows Server でリモート ツールをダウンロードしてインストール](#BKMK_msvsmon)する」を参照してください。

* アプリが IIS で正しく設定、展開、および実行されていることを確認してデバッグできるようにする場合は、このトピックのすべての手順に従います。

## <a name="create-the-aspnet-core-application-on-the-visual-studio-computer"></a>visual Studio コンピューター上にASP.NET コア アプリケーションを作成します。

1. 新しい ASP.NET Core Web アプリケーションを作成します。 

    ::: moniker range=">=vs-2019"
    Visual Studio 2019 で **、Ctrl + Q と**入力して検索ボックスを開き **、asp.net**と入力し、[**テンプレート**] を選択し、[コア**Web アプリケーションの新規作成 ASP.NET]** を選択します。 表示されるダイアログ ボックスで **、MyASPApp**という名前を付け、[**作成**] をクリックします。 次に **、[Web アプリケーション (モデル ビュー コントローラー)]** を選択し、[**作成**] を選択します。
    ::: moniker-end
    ::: moniker range="vs-2017"
    Visual Studio 2017 で、[**ファイル>新しい> プロジェクト**] を選択し **、[Visual C# > Web >ASP.NETコア Web アプリケーション**] を選択します。 [ASP.NET コア テンプレート] セクションで **、[Web アプリケーション (モデル ビュー コントローラー)]** を選択します。 Core 2.1 ASP.NET選択されていること **、Docker サポートを有効に**する] が**Authentication**選択されておらず、[**認証] が [認証なし**] に設定されていることを確認します。 プロジェクトに**MyASPApp という名前を付けます**。
    ::: moniker-end

4. About.cshtml.csファイルを開き、メソッドにブレークポイントを`OnGet`設定します (古いテンプレートでは、代わりにHomeController.cs開き、`About()`メソッドにブレークポイントを設定します)。

## <a name="install-and-configure-iis-on-windows-server"></a><a name="bkmk_configureIIS"></a>Windows サーバーに IIS をインストールして構成する

[!INCLUDE [remote-debugger-install-iis-role](../debugger/includes/remote-debugger-install-iis-role.md)]

## <a name="update-browser-security-settings-on-windows-server"></a>Windows サーバーでブラウザーのセキュリティ設定を更新する

Internet Explorer でセキュリティ強化の構成が有効になっている場合 (既定で有効)、いくつかのドメインを信頼済みサイトとして追加して、Web サーバー コンポーネントの一部をダウンロードできるようにする必要があります。 [インターネット オプション] > [**信頼済みサイト> サイト>セキュリティ] に進み、信頼済みサイトを**追加する。 次のドメインを追加します。

- microsoft.com
- go.microsoft.com
- download.microsoft.com
- iis.net

ソフトウェアをダウンロードすると、さまざまな Web サイトのスクリプトやリソースを読み込む許可を与える要求が表示されることがあります。 これらのリソースの一部は必須ではありませんが、プロセスを簡略化するには、プロンプトが表示されたら [**追加**] をクリックします。

## <a name="install-aspnet-core-on-windows-server"></a>Windows サーバーにASP.NET コアをインストールする

1. ホスティング システムに [.NET Core Windows Server ホスティング](https://aka.ms/dotnetcore-2-windowshosting) バンドルをインストールします。 このバンドルをインストールすることで、.NET Core ランタイム、.NET Core ライブラリ、ASP.NET Core モジュールがインストールされます。 詳細な手順については、「 [IIS への公開](/aspnet/core/publishing/iis?tabs=aspnetcore2x#iis-configuration)」を参照してください。

    > [!NOTE]
    > システムにインターネット接続が設定されていない場合は、.NET Core Windows Server ホスティング バンドルをインストールする前に、*[Microsoft Visual C++ 2015 再頒布可能パッケージ](https://www.microsoft.com/download/details.aspx?id=53840)* を入手してインストールしてください。

3. システムを再起動します (または **、net stop を**実行すると、コマンド プロンプトから net start **w3svc**が続き、システム PATH への変更が取り出されます)。

## <a name="choose-a-deployment-option"></a>展開オプションの選択

アプリを IIS に展開する際にヘルプが必要な場合は、次のオプションを検討してください。

* IIS で発行設定ファイルを作成し、Visual Studio で設定をインポートして配置します。 一部のシナリオでは、これはアプリを迅速に展開する方法です。 発行設定ファイルを作成すると、アクセス許可は IIS で自動的に設定されます。

* ローカル フォルダーに発行し、優先する方法で出力を IIS 上の準備済みアプリ フォルダーにコピーして展開します。

## <a name="optional-deploy-using-a-publish-settings-file"></a>(オプション)発行設定ファイルを使用した展開

このオプションを使用すると、発行設定ファイルを作成し、Visual Studio にインポートできます。

> [!NOTE]
> この配置方法では、Web 配置を使用します。 設定をインポートする代わりに Visual Studio で Web 配置を手動で構成する場合は、ホスティング サーバーの Web 配置 3.6 ではなく Web 配置 3.6 をインストールできます。 ただし、Web 配置を手動で構成する場合は、サーバー上のアプリ フォルダーが正しい値とアクセス許可で構成されていることを確認する必要があります[(「ASP.NET Web サイトを構成](#BKMK_deploy_asp_net)する 」を参照)。

### <a name="install-and-configure-web-deploy-for-hosting-servers-on-windows-server"></a>Windows サーバー上のホスティング サーバーの Web 配置をインストールおよび構成する

[!INCLUDE [install-web-deploy-with-hosting-server](../deployment/includes/install-web-deploy-with-hosting-server.md)]

### <a name="create-the-publish-settings-file-in-iis-on-windows-server"></a>Windows Server 上の IIS に発行設定ファイルを作成する

[!INCLUDE [install-web-deploy-with-hosting-server](../deployment/includes/create-publish-settings-iis.md)]

### <a name="import-the-publish-settings-in-visual-studio-and-deploy"></a>Visual Studio で発行設定をインポートして配置する

[!INCLUDE [install-web-deploy-with-hosting-server](../deployment/includes/import-publish-settings-vs.md)]

アプリが正常に配置されたら、自動的に起動されます。 アプリが Visual Studio から起動しない場合は、IIS でアプリを起動します。 ASP.NET Core の場合、**DefaultAppPool** の [アプリケーション プール] フィールドが **[マネージド コードなし]** に設定されていることを確認する必要があります。

1. [**設定]** ダイアログ ボックスで、[**次へ**] をクリックしてデバッグを有効にし、[**デバッグ**] 構成を選択して、[**ファイルの発行**] オプションの [**出力先で追加ファイルを削除**する] を選択します。

    > [!NOTE]
    > リリース構成を選択した場合は、発行時に*web.config*ファイルのデバッグを無効にします。

1. [**保存**] をクリックし、アプリを再公開します。

## <a name="optional-deploy-by-publishing-to-a-local-folder"></a>(オプション)ローカル フォルダーに発行して展開する

PowerShell、RoboCopy を使用して IIS にアプリをコピーする場合、または手動でファイルをコピーする場合は、このオプションを使用してアプリを展開できます。

### <a name="configure-the-aspnet-core-web-site-on-the-windows-server-computer"></a><a name="BKMK_deploy_asp_net"></a>Windows サーバー コンピューター上のASP.NETコア Web サイトを構成します。

1. Windows エクスプローラを開き、新しいフォルダ**C:\Publish**を作成 ASP.NETします。

2. まだ開いていない場合は、インターネット インフォメーション**サービス (IIS) マネージャ**を開きます。 (サーバー マネージャーの左側のウィンドウで **、[IIS]** を選択します。 サーバーを右クリックして **[インターネット インフォメーション サービス (IIS) マネージャー]** を選択します。)

3. 左側のウィンドウの [**接続**] で、[**サイト]** に移動します。

4. **[既定**の Web サイト] を選択し **、[基本設定]** をクリックして、[**物理パス**] を **[C:\Publish]** に設定します。

4. **[既定の Web サイト]** ノードを右クリックして、 **[アプリケーションの追加]** を選択します。

5. [**エイリアス**] フィールドを**MyASPApp**に設定し、既定のアプリケーション プール (**DefaultAppPool**) をそのまま使用し、**物理パス**を**C:\Publish**に設定します。

6. [**接続]** で、[**アプリケーション プール]** を選択します。 **DefaultAppPool**を開き、[アプリケーション プール] フィールドを **[マネージ コードなし**] に設定します。

7. IIS マネージャで新しいサイトを右クリックし、[**権限の編集**] を選択し、Web アプリへのアクセスを許可するように構成された IUSR、IIS_IUSRS、またはユーザーが、読み取り&実行権限を持つ権限のあるユーザーであることを確認します。

    アクセス権を持つユーザーが表示されない場合は、手順を実行して、読み取り&実行権限を持つユーザーとして IUSR を追加します。

### <a name="publish-and-deploy-the-app-by-publishing-to-a-local-folder-from-visual-studio"></a>Visual Studio からローカル フォルダーに発行してアプリを発行および展開する

また、ファイル システムやその他のツールを使用してアプリを発行および展開することもできます。

[!INCLUDE [remote-debugger-deploy-app-local](../debugger/includes/remote-debugger-deploy-app-local.md)]

## <a name="download-and-install-the-remote-tools-on-windows-server"></a><a name="BKMK_msvsmon"></a>リモート ツールをダウンロードしてインストールする

使用しているバージョンの Visual Studio に一致するリモート ツールのバージョンをダウンロードします。

[!INCLUDE [remote-debugger-download](../debugger/includes/remote-debugger-download.md)]

## <a name="set-up-the-remote-debugger-on-windows-server"></a><a name="BKMK_setup"></a>Windows サーバーでリモート デバッガーを設定する

[!INCLUDE [remote-debugger-configuration](../debugger/includes/remote-debugger-configuration.md)]

> [!NOTE]
> リモート デバッガーの認証モードまたはポート番号を変更する、追加のユーザーのアクセス許可を追加する必要がある場合は、[リモート デバッガーの構成を](../debugger/remote-debugging.md#configure_msvsmon)参照してください。

リモート デバッガーをサービスとして実行する方法については、「[サービスとしてリモート デバッガーを実行する](../debugger/remote-debugging.md#bkmk_configureService)」を参照してください。

## <a name="attach-to-the-aspnet-application-from-the-visual-studio-computer"></a><a name="BKMK_attach"></a>Visual Studio コンピューターからASP.NET アプリケーションにアタッチします。

1. Visual Studio コンピューターで、デバッグしようとしているソリューションを開きます **(MyASPApp**この資料のすべての手順を実行している場合)。
2. Visual Studio で、[デバッグ] をクリック **>プロセスにアタッチ**(Ctrl + Alt + P) します。

    > [!TIP]
    > Visual Studio 2017 以降のバージョンでは、デバッグ > プロセスに再アタッチする..(Shift + Alt + P)を使用して、以前にアタッチしたのと同じ**プロセスに再アタッチ**できます。

3. [修飾子] フィールドを**\<リモート コンピュータ名>** に設定し **、Enter**キーを押します。

    Visual Studio がコンピューター名に必要なポートを追加することを確認します**\<>。**

    ::: moniker range=">=vs-2019"
    Visual Studio 2019 では、**\<リモート コンピューター名>:4024 が表示されます。**
    ::: moniker-end
    ::: moniker range="vs-2017"
    Visual Studio 2017 では、**\<リモート コンピューター名>:4022 が表示されます。**
    ::: moniker-end
    ポートが必要です。 ポート番号が表示されない場合は、手動で追加します。

4. **[最新の情報に更新]** をクリックします。
    **[選択可能なプロセス]** ウィンドウにプロセスがいくつか表示されます。

    プロセスが表示されない場合は、リモート コンピュータ名の代わりに IP アドレスを使用してみてください (ポートが必要です)。 コマンド ライン`ipconfig`で IPv4 アドレスを取得できます。

    [**検索**] ボタンを使用する場合は、サーバーで[UDP ポート 3702 を開く](#bkmk_openports)必要があります。

5. **[すべてのユーザーからのプロセスを表示する]** をオンにします。

6. アプリをすばやく見つけるには、プロセス名の最初の文字を入力します。

    * IIS で[アプリ内ホスティング モデル](/aspnet/core/host-and-deploy/aspnet-core-module?view=aspnetcore-3.1#hosting-models)を使用している場合は、正しい**w3wp.exe**プロセスを選択します。 NET Core 3 以降は、これがデフォルトです。

    * それ以外の場合は **、dotnet.exe**プロセスを選択します。 (これはアウトプロセスのホスティング モデルです。

    *w3wp.exe*または*dotnet.exe*を示す複数のプロセスがある場合は、[**ユーザー名]** 列を確認してください。 一部のシナリオでは、**ユーザー名**列には **、IIS APPPOOL\DefaultAppPool**などのアプリ プール名が表示されます。 アプリ プールが表示されるが一意ではない場合は、デバッグするアプリ インスタンスの名前を新しく作成し、[**ユーザー名]** 列で簡単に見つけることができます。

    ::: moniker range=">=vs-2019"
    ![RemoteDBG_AttachToProcess](../debugger/media/vs-2019/remotedbg-attachtoprocess-aspnetcore.png "RemoteDBG_AttachToProcess")
    ::: moniker-end
    ::: moniker range="vs-2017"
    ![RemoteDBG_AttachToProcess](../debugger/media/remotedbg-attachtoprocess-aspnetcore.png "RemoteDBG_AttachToProcess")
    ::: moniker-end

7. **[アタッチ]** をクリックします。

8. リモート コンピューターの Web サイトを開きます。 ブラウザーで、**http://\<リモート コンピューター名>** に移動します。

    ASP.NET の Web ページが表示されるはずです。

9. 実行中のASP.NETアプリケーションで、[**関連**情報] ページへのリンクをクリックします。

    Visual Studio で、ブレークポイントにヒットするはずです。

## <a name="troubleshooting-open-required-ports-on-windows-server"></a><a name="bkmk_openports"></a> トラブルシューティングWindows Server で必要なポートを開く

ほとんどのセットアップでは、ASP.NETとリモート デバッガーのインストールによって必要なポートが開かれます。 ただし、ポートが開いているかどうかを確認する必要があります。

> [!NOTE]
> Azure VM では、[ネットワーク セキュリティ グループ](/azure/virtual-machines/windows/nsg-quickstart-portal)を使用してポートを開く必要があります。

必要なポート:

* 80 - IIS に必要
::: moniker range=">=vs-2019"
* 4024 - Visual Studio 2019 からのリモート デバッグに必要です (詳細については、「[リモート デバッガーポートの割り当て](../debugger/remote-debugger-port-assignments.md)」を参照)。
::: moniker-end
::: moniker range="vs-2017"
* 4022 - Visual Studio 2017 からのリモート デバッグに必要です (詳細については、「[リモート デバッガーポートの割り当て](../debugger/remote-debugger-port-assignments.md)」を参照)。
::: moniker-end
* UDP 3702 - (オプション) 探索ポートを使用すると、Visual Studio でリモート デバッガーにアタッチするときに **[検索**] ボタンを使用できます。

1. Windows Server でポートを開くには、[**スタート]** メニューを開き、[**セキュリティが強化された Windows ファイアウォール**] を検索します。

2. 次に、[**受信規則>新しい規則> ポート**] を選択し、[**次へ**] をクリックします。 (UDP 3702 の場合は、代わりに **[送信規則**] を選択します)。

3. [**特定のローカル ポート**] ボックスにポート番号を入力し、[**次へ**] をクリックします。

4. [**接続を許可する**] をクリックし、[**次へ**] をクリックします。

5. ポートに対して有効にするネットワークの種類を 1 つ以上選択し、[**次へ**] をクリックします。

    選ぶ種類には、リモート コンピューターが接続しているネットワークが含まれている必要があります。
6. 受信規則の名前 (**たとえば、 IIS**、 **Web 配置**、または**msvsmon**) を追加し、[**完了**] をクリックします。

    [受信の規則] または [送信の規則] の一覧に新しい規則が表示されます。

    Windows ファイアウォールの構成の詳細については、「 リモート[デバッグ用の Windows ファイアウォールの構成](../debugger/configure-the-windows-firewall-for-remote-debugging.md)」を参照してください。

3. 他の必要なポートに対して追加のルールを作成します。
