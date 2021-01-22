---
title: リモートの IIS コンピューター上で ASP.NET Core をリモート デバッグする | Microsoft Docs
description: Visual Studio リモート デバッガーを使用してリモート インターネット インフォメーション サービス (IIS) コンピューターに配置されている ASP.NET Core アプリケーションをデバッグします。
ms.custom: remotedebugging, SEO-VS-2020
ms.date: 05/06/2020
ms.topic: conceptual
ms.assetid: 573a3fc5-6901-41f1-bc87-557aa45d8858
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- aspnet
- dotnetcore
ms.openlocfilehash: bc746d5139b897d51d4d038f077906f56aa5d552
ms.sourcegitcommit: a436ba564717b992eb1984b28ea0aec801eacaec
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2021
ms.locfileid: "98205815"
---
# <a name="remote-debug-aspnet-core-on-a-remote-iis-computer-in-visual-studio"></a>リモートの IIS コンピューター上の Visual Studio 2017 で ASP.NET Core をリモート デバッグする

IIS に配置されている ASP.NET Core アプリケーションをデバッグするには、アプリを配置したコンピューターにリモート ツールをインストールして実行し、Visual Studio から実行中のアプリにアタッチします。

![リモート デバッガーのコンポーネント](../debugger/media/remote-debugger-aspnet.png "Remote_debugger_components")

このガイドでは、Visual Studio ASP.NET Core を設定して構成し、それを IIS に配置し、Visual Studio からリモート デバッガーをアタッチする方法について説明します。 ASP.NET 4.5.2 をリモート デバッグするには、「[IIS コンピューター上の ASP.NET のリモート デバッグ](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md)」を参照してください。 Azure を使用して、IIS に配置し、デバッグすることもできます。 Azure App Service の場合、[スナップショット デバッガー](../debugger/debug-live-azure-applications.md)を使用するか、[サーバー エクスプローラーからデバッガーをアタッチする](../debugger/remote-debugging-azure.md)ことで、IIS の事前構成済みインスタンスとリモート デバッガーで配置とデバッグを簡単に行うことができます。

## <a name="prerequisites"></a>必須コンポーネント

::: moniker range=">=vs-2019"
この記事に記載されている手順を実行するには、Visual Studio 2019 が必要です。
::: moniker-end
::: moniker range="vs-2017"
この記事に記載されている手順を実行するには、Visual Studio 2017 が必要です。
::: moniker-end

これらの手順は、次のサーバー構成でテストされています。
* Windows Server 2012 R2 および IIS 8
* Windows Server 2016 および IIS 10
* Windows Server 2019 および IIS 10

## <a name="network-requirements"></a>ネットワーク要件

プロキシ経由で接続された 2 台のコンピューター間のデバッグはサポートされていません。 待機時間の長い接続や低帯域幅の接続 (ダイヤルアップ インターネットなど)、または国をまたぐインターネット経由のデバッグは推奨されません。これらは、障害が発生するか、または過度に低速になる可能性があります。 詳細な要件の一覧については、「[要件](../debugger/remote-debugging.md#requirements_msvsmon)」を参照してください。

## <a name="app-already-running-in-iis"></a>アプリは既に IIS で実行されていますか?

この記事には、Windows サーバー上で IIS の基本構成を設定し、Visual Studio からアプリを配置する手順が含まれています。 これらの手順は、サーバーに必要なコンポーネントがインストールされていること、アプリを正しく実行できること、およびリモート デバッグの準備ができていることを確認するために含まれています。

* アプリが IIS で実行されていて、リモート デバッガーをダウンロードしてデバッグを開始するだけの場合は、「[Windows Server 上でリモート ツールをダウンロードしてインストールする](#BKMK_msvsmon)」を参照してください。

* アプリが IIS で正しく設定、配置、および実行されていることを確認してデバッグできるようにするためにヘルプが必要な場合は、このトピックのすべての手順に従ってください。

## <a name="create-the-aspnet-core-application-on-the-visual-studio-computer"></a>Visual Studio コンピューター上で ASP.NET Core アプリケーションを作成する

1. 新しい ASP.NET Core Web アプリケーションを作成します。

    ::: moniker range=">=vs-2019"
    Visual Studio 2019 で **Ctrl + Q** キーを押して検索ボックスを開き、「**asp.net**」と入力し、 **[テンプレート]** を選択してから、 **[新しい ASP.NET Core Web アプリケーションの作成]** を選択します。 表示されるダイアログ ボックスで、プロジェクトに「**MyASPApp**」という名前を付け、 **[作成]** を選択します。 次に、 **[Web アプリケーション (Model-View-Controller)]** を選択し、 **[作成]** を選択します。
    ::: moniker-end
    ::: moniker range="vs-2017"
    Visual Studio 2017 で、 **[ファイル] > [新規] > [プロジェクト]** を選択し、次に **[Visual C#] > [Web] > [ASP.NET Core Web アプリケーション]** を選択します。 ASP.NET Core テンプレート セクションで、 **[Web アプリケーション (モデル ビュー コントローラー)]** を選択します。 ASP.NET Core 2.1 が選択されていること、 **[Docker サポートを有効にする]** がオフであること、 **[認証]** が **[認証なし]** に設定されていることを確認します。 プロジェクトに「**MyASPApp**」と名前を付けます。
    ::: moniker-end

4. About.cshtml.cs ファイルを開き、`OnGet` メソッドにブレークポイントを設定します (以前のテンプレートでは、代わりに HomeController.cs を開き、`About()` メソッドにブレークポイントを設定します)。

## <a name="install-and-configure-iis-on-windows-server"></a><a name="bkmk_configureIIS"></a> Windows Server に IIS をインストールして構成する

[!INCLUDE [remote-debugger-install-iis-role](../debugger/includes/remote-debugger-install-iis-role.md)]

## <a name="update-browser-security-settings-on-windows-server"></a>Windows Server 上でブラウザーのセキュリティ設定を更新する

Internet Explorer で [セキュリティ強化の構成] が有効な場合は (既定値は有効です)、一部のドメインを信頼済みサイトとして追加し、一部の Web サーバー コンポーネントをダウンロードできるようにする必要があります。 信頼済みサイトを追加するには、 **[インターネット オプション] > [セキュリティ] > [信頼済みサイト] > [サイト]** に移動します。 次のドメインを追加します。

- microsoft.com
- go.microsoft.com
- download.microsoft.com
- iis.net

ソフトウェアをダウンロードすると、さまざまな Web サイトのスクリプトとリソースを読み込むためのアクセス許可を付与する要求を受け取る場合があります。 これらのリソースの一部は不要ですが、プロセスを簡略化するために、プロンプトが表示されたら **[追加]** をクリックします。

## <a name="install-aspnet-core-on-windows-server"></a>Windows Server に ASP.NET Core をインストールする

1. ホスト システムに .NET Core ホスティング バンドルをインストールします。 このバンドルをインストールすることで、.NET Core ランタイム、.NET Core ライブラリ、ASP.NET Core モジュールがインストールされます。 詳細な手順については、[IIS への発行](/aspnet/core/publishing/iis?tabs=aspnetcore2x#iis-configuration)に関するページを参照してください。

    .NET Core 3 の場合は、[.NET Core ホスティング バンドル](https://dotnet.microsoft.com/permalink/dotnetcore-current-windows-runtime-bundle-installer)をインストールします。
    .NET Core 2 の場合は、[.NET Core Windows Server ホスティング](https://aka.ms/dotnetcore-2-windowshosting)をインストールします。

    > [!NOTE]
    > システムにインターネット接続が設定されていない場合は、.NET Core Windows Server ホスティング バンドルをインストールする前に、 *[Microsoft Visual C++ 2015 再頒布可能パッケージ](https://www.microsoft.com/download/details.aspx?id=53840)* を入手してインストールしてください。

3. システムを再起動します (または、コマンド プロンプトから **net stop was /y** の後に続けて **net start w3svc** を実行して、システム PATH への変更を適用します)。

## <a name="choose-a-deployment-option"></a>配置オプションを選択する

IIS へのアプリの配置についてヘルプが必要な場合は、次のオプションを検討してください。

* IIS で発行設定ファイルを作成し、Visual Studio に設定をインポートして配置します。 シナリオによっては、この方法でアプリを迅速に配置できます。 発行設定ファイルを作成すると、IIS でアクセス許可が自動的に設定されます。

* ローカル フォルダーに発行し、適切な方法で出力を IIS 上の準備されたアプリ フォルダーにコピーすることで配置します。

## <a name="optional-deploy-using-a-publish-settings-file"></a>(省略可能) 発行設定ファイルを使用してデプロイする

このオプションを使用すると、発行設定ファイルを作成し、それを Visual Studio にインポートすることができます。

> [!NOTE]
> この配置方法では Web 配置を使用するため、サーバーに Web 配置がインストールされている必要があります。 設定をインポートするのではなく、Web 配置を手動で構成する場合は、ホスティング サーバー用 Web 配置 3.6 ではなく、Web 配置 3.6 をインストールすることができます。 ただし、Web 配置を手動で構成する場合は、サーバー上のアプリ フォルダーが正しい値とアクセス許可で構成されていることを確認する必要があります ([ASP.NET Web サイトの構成](#BKMK_deploy_asp_net)に関するセクションを参照してください)。

### <a name="configure-the-aspnet-core-web-site"></a>ASP.NET Core Web サイトを構成する

1. IIS マネージャーの左側のウィンドウで、 **[接続]** の **[アプリケーション プール]** を選択します。 **DefaultAppPool** を開き、 **[.NET CLR バージョン]** を **[マネージド コードなし]** に設定します。 これは ASP.NET Core に必要です。 既定の Web サイトで DefaultAppPool が使用されます。

2. DefaultAppPool を停止して再起動します。

### <a name="install-and-configure-web-deploy-for-hosting-servers-on-windows-server"></a>Windows Server にホスティング サーバー用 Web 配置をインストールして構成する

[!INCLUDE [install-web-deploy-with-hosting-server](../deployment/includes/install-web-deploy-with-hosting-server.md)]

### <a name="create-the-publish-settings-file-in-iis-on-windows-server"></a>Windows Server 上の IIS に発行設定ファイルを作成する

[!INCLUDE [install-web-deploy-with-hosting-server](../deployment/includes/create-publish-settings-iis.md)]

### <a name="import-the-publish-settings-in-visual-studio-and-deploy"></a>Visual Studio で発行設定をインポートして配置する

[!INCLUDE [install-web-deploy-with-hosting-server](../deployment/includes/import-publish-settings-vs.md)]

アプリが正常に配置されたら、自動的に起動されます。 Visual Studio からアプリが起動しない場合は、IIS でアプリを起動し、正常に動作することを確認します。 ASP.NET Core の場合は、**DefaultAppPool** の [アプリケーション プール] フィールドが **[マネージド コードなし]** に設定されていることも確認する必要があります。

1. **[設定]** ダイアログ ボックスで、 **[次へ]** をクリックしてデバッグを有効にし、 **[デバッグ]** 構成を選択し、 **[ファイル発行オプション]** の **[発行先の追加ファイルを削除する]** を選択します。

    > [!IMPORTANT]
    > リリース構成を選択した場合、発行時に *web.config* ファイルのデバッグを無効にします。

1. **[保存]** をクリックしてアプリを再発行します。

## <a name="optional-deploy-by-publishing-to-a-local-folder"></a>(省略可能) ローカル フォルダーに発行して配置する

PowerShell、RoboCopy を使用してアプリを IIS にコピーする場合、またはファイルを手動でコピーする場合は、このオプションを使用してアプリを配置できます。

### <a name="configure-the-aspnet-core-web-site-on-the-windows-server-computer"></a><a name="BKMK_deploy_asp_net"></a> Windows Server コンピューター上で ASP.NET Core Web サイトを構成する

1. エクスプローラーを開き、新しいフォルダー **C:\Publish** を作成します。後でここに ASP.NET Core プロジェクトを配置します。

2. **インターネット インフォメーション サービス (IIS) マネージャー** をまだ開いていない場合は開きます (サーバー マネージャーの左側のペインで、 **[IIS]** を選択します。 サーバーを右クリックして **[インターネット インフォメーション サービス (IIS) マネージャー]** を選択します。)

3. 左側のペインの **[接続]** で、 **[サイト]** に移動します。

4. **[既定の Web サイト]** を選択し、 **[基本設定]** を選択して、 **[物理パス]** を **C:\Publish** に設定します。

4. **[既定の Web サイト]** ノードを右クリックして、 **[アプリケーションの追加]** を選択します。

5. **[エイリアス]** フィールドを「**MyASPApp**」に設定し、既定のアプリケーション プール (**DefaultAppPool**) のままにして **[物理パス]** を **C:\ Publish** に設定します。

6. **[接続]** の **[アプリケーション プール]** を選択します。 **DefaultAppPool** を開き、[アプリケーション プール] フィールドを **[マネージ コードなし]** に設定します。

7. IIS マネージャーで新しいサイトを右クリックし、 **[アクセス許可の編集]** を選択して、IUSR、IIS_IUSRS、または Web アプリへのアクセス用に構成されたユーザーが、読み取りと実行のアクセス権を持つ承認済みユーザーであることを確認します。

    これらのアクセス権を持つユーザーが 1 人も表示されない場合は、読み取りおよび実行アクセス権を持つユーザーとして IUSR を追加する手順を実行します。

### <a name="publish-and-deploy-the-app-by-publishing-to-a-local-folder-from-visual-studio"></a>Visual Studio からローカル フォルダーに発行してアプリを発行および配置する

ファイル システムやその他のツールを使用して、アプリを発行および配置することもできます。

[!INCLUDE [remote-debugger-deploy-app-local](../debugger/includes/remote-debugger-deploy-app-local.md)]

## <a name="download-and-install-the-remote-tools-on-windows-server"></a><a name="BKMK_msvsmon"></a> Windows Server 上でリモート ツールをダウンロードしてインストールする

Visual Studio のバージョンと一致するバージョンのリモート ツールをダウンロードします。

[!INCLUDE [remote-debugger-download](../debugger/includes/remote-debugger-download.md)]

## <a name="set-up-the-remote-debugger-on-windows-server"></a><a name="BKMK_setup"></a> Windows Server 上でリモート デバッガーを設定する

[!INCLUDE [remote-debugger-configuration](../debugger/includes/remote-debugger-configuration.md)]

> [!NOTE]
> 追加のユーザーのアクセス許可を追加し、認証モード、またはリモート デバッガーのポート番号を変更する必要がある場合は、「[リモート デバッガーを構成する](../debugger/remote-debugging.md#configure_msvsmon)」を参照してください。

リモート デバッガーをサービスとして実行する方法の詳細については、[サービスとしてのリモート デバッガーの実行](../debugger/remote-debugging.md#bkmk_configureService)に関するページを参照してください。

## <a name="attach-to-the-aspnet-application-from-the-visual-studio-computer"></a><a name="BKMK_attach"></a> Visual Studio コンピューターから ASP.NET アプリケーションにアタッチする

1. Visual Studio コンピューター上で、デバッグ対象のソリューション (この記事のすべての手順を実行している場合は、**MyASPApp**) を開きます。
2. Visual Studio で **[デバッグ] > [プロセスにアタッチ]** (Ctrl + Alt + P キー) をクリックします。

    > [!TIP]
    > Visual Studio 2017 以降のバージョンで以前にアタッチしたものと同じプロセスに再アタッチするには、 **[デバッグ] > [プロセスに再アタッチする]** (Shift + Alt + P キー) を使用します。

3. [修飾子] フィールドを **\<remote computer name>** に設定し、**Enter** キーを押します。

    Visual Studio で必要なポートがコンピューター名に追加されていることを確認します ( **\<remote computer name>:port** という形式で表示されます)

    ::: moniker range=">=vs-2019"
    Visual Studio 2019 では、 **\<remote computer name>:4024** が表示されます
    ::: moniker-end
    ::: moniker range="vs-2017"
    Visual Studio 2017 では、 **\<remote computer name>:4022** が表示されます
    ::: moniker-end
    ポートは必須です。 ポート番号が表示されない場合は、手動で追加します。

4. **[最新の情報に更新]** をクリックします。
    **[選択可能なプロセス]** ウィンドウにプロセスがいくつか表示されます。

    プロセスが表示されない場合は、リモート コンピューター名ではなく IP アドレスを使用してみてください (ポートは必須です)。 コマンド ラインで `ipconfig` を使用すると、IPv4 アドレスを取得できます。

    **[検索]** ボタンを使用する場合は、サーバー上で必要に応じて [UDP ポート 3702](#bkmk_openports) を開きます。

5. **[すべてのユーザーからのプロセスを表示する]** をオンにします。

6. プロセス名の最初の文字を入力すると、アプリをすばやく見つけることができます。

    * IIS で [インプロセス ホスティング モデル](/aspnet/core/host-and-deploy/aspnet-core-module?view=aspnetcore-3.1&preserve-view=true#hosting-models)を使用している場合は、正しい **w3wp.exe** プロセスを選択します。 .NET Core 3 以降では、これが既定値です。

    * それ以外の場合は、**dotnet.exe** プロセスを選択します (これはアウト プロセス ホスティング モデルです)。

    *w3wp.exe* または *dotnet.exe* を示す複数のプロセスがある場合は、 **[ユーザー名]** 列を確認します。 一部のシナリオでは、 **[ユーザー名]** 列に **IIS APPPOOL\DefaultAppPool** などのアプリ プール名が表示されます。 アプリ プールが表示され、一意ではない場合は、デバッグするアプリ インスタンスの新しい名前付きアプリ プールを作成すると、 **[ユーザー名]** 列で簡単に見つけることができます。

    ::: moniker range=">=vs-2019"
    ![RemoteDBG_AttachToProcess](../debugger/media/vs-2019/remotedbg-attachtoprocess-aspnetcore.png "RemoteDBG_AttachToProcess")
    ::: moniker-end
    ::: moniker range="vs-2017"
    ![RemoteDBG_AttachToProcess](../debugger/media/remotedbg-attachtoprocess-aspnetcore.png "RemoteDBG_AttachToProcess")
    ::: moniker-end

7. **[アタッチ]** をクリックします。

8. リモート コンピューターの Web サイトを開きます。 ブラウザーで、**http://\<remote computer name>** に移動します。

    ASP.NET の Web ページが表示されるはずです。

9. 実行中の ASP.NET アプリケーションで、 **[バージョン情報]** ページのリンクをクリックします。

    Visual Studio で、ブレークポイントにヒットするはずです。

## <a name="troubleshooting-open-required-ports-on-windows-server"></a><a name="bkmk_openports"></a> トラブルシューティング: Windows Server で必要なポートを開く

ほとんどの設定では、ASP.NET とリモート デバッガーのインストールによって必要なポートが開かれます。 ただし、場合によってはポートが開いていることを確認する必要があります。

> [!NOTE]
> Azure VM では、[ネットワーク セキュリティ グループ](/azure/virtual-machines/windows/nsg-quickstart-portal)を使用してポートを開く必要があります。

必要なポート:

* 80 - IIS に必要です
::: moniker range=">=vs-2019"
* 4024 - Visual Studio 2019 からのリモート デバッグに必要です (詳細については、「[リモート デバッガーのポートの割り当て](../debugger/remote-debugger-port-assignments.md)」を参照してください)。
::: moniker-end
::: moniker range="vs-2017"
* 4022 - Visual Studio 2017 からのリモート デバッグに必要です (詳細については、「[リモート デバッガーのポートの割り当て](../debugger/remote-debugger-port-assignments.md)」を参照してください)。
::: moniker-end
* UDP 3702 - (省略可能) 検出ポートを使用すると、Visual Studio でリモート デバッガーにアタッチするときに **[検索]** ボタンを使用できます。

1. Windows サーバーでポートを開くには、 **[スタート]** メニューを開き、 **[セキュリティが強化された Windows ファイアウォール]** を検索します。

2. 次に、 **[受信の規則] > [新しい規則] > [ポート]** を選択し、 **[次へ]** をクリックします (UDP 3702 の場合は、代わりに **[送信規則]** を選択します)。

3. **[特定のローカル ポート]** にポート番号を入力し、 **[次へ]** をクリックします。

4. **[接続を許可する]** をクリックし、 **[次へ]** をクリックします。

5. ポートに対して有効にする 1 つ以上のネットワークの種類を選択し、 **[次へ]** をクリックします。

    選ぶ種類には、リモート コンピューターが接続しているネットワークが含まれている必要があります。
6. [受信規則] の名前 (たとえば、**IIS**、**Web 配置**、**msvsmon**) を追加し、 **[完了]** をクリックします。

    [受信の規則] または [送信の規則] の一覧に新しい規則が表示されます。

    Windows ファイアウォールの構成の詳細については、「[Windows ファイアウォールをリモート デバッグ用に構成する](../debugger/configure-the-windows-firewall-for-remote-debugging.md)」を参照してください。

3. その他の必要なポートに追加の規則を作成します。
