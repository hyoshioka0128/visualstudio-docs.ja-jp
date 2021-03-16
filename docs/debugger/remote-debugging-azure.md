---
title: IIS と Azure 上で ASP.NET Core をリモート デバッグする | Microsoft Docs
description: Visual Studio ASP.NET Core アプリをセットアップして構成し、Azure を使用して IIS に配置して、Visual Studio からリモート デバッガーをアタッチする方法について説明します。
ms.custom: remotedebugging
ms.date: 05/06/2020
ms.topic: conceptual
ms.assetid: a6c04b53-d1b9-4552-a8fd-3ed6f4902ce6
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- aspnet
- dotnetcore
- azure
ms.openlocfilehash: 619f1f1cc99cbab425bc1bcb2bac181e09db8fc4
ms.sourcegitcommit: 79a6be815244f1cfc7b4123afff29983fce0555c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2021
ms.locfileid: "102250066"
---
# <a name="remote-debug-aspnet-core-on-iis-in-azure-in-visual-studio"></a>Azure の Visual Studio で IIS 上の ASP.NET Core をリモート デバッグする

このガイドでは、Visual Studio ASP.NET Core アプリを設定して構成し、Azure を使用してアプリを IIS に配置して、Visual Studio からリモート デバッガーをアタッチする方法について説明します。

Azure 上でリモート デバッグする際の推奨される方法は、シナリオによって異なります。

* Azure App Service 上で ASP.NET Core をデバッグするには、[スナップショット デバッガーを使用した Azure アプリのデバッグ](../debugger/debug-live-azure-applications.md)に関するページを参照してください。 これが推奨される方法です。
* 従来のデバッグ機能を使用して Azure App Service 上で ASP.NET Core をデバッグするには、このトピックの手順を実行してください ([Azure App Service 上のリモート デバッグ](#remote_debug_azure_app_service)に関するセクションを参照してください)。

    このシナリオでは、Visual Studio から Azure にアプリを配置する必要がありますが、次の図に示すように、IIS またはリモート デバッガー (これらのコンポーネントは点線で表されています) を手動でインストールまたは構成する必要はありません。

    ![Visual Studio、Azure App Service、ASP.NET アプリの関係を示す図。 IIS とリモート デバッガーは点線で表されています。](../debugger/media/remote-debugger-azure-app-service.png)

* Azure VM 上で IIS をデバッグするには、このトピックの手順を実行してください ([Azure VM 上のリモート デバッグ](#remote_debug_azure_vm)に関するセクションを参照してください)。 これにより、IIS のカスタマイズされた構成を使用できますが、設定と配置の手順はより複雑になります。

    Azure VM の場合は、次の図に示すように、アプリを Visual Studio から Azure に配置する必要があります。また、IIS ロールとリモート デバッガーを手動でインストールする必要もあります。

    ![Visual Studio、Azure VM、ASP.NET アプリの関係を示す図。 IIS とリモート デバッガーは実線で表されます。](../debugger/media/remote-debugger-azure-vm.png)

* Azure Service Fabric 上で ASP.NET Core をデバッグするには、「[リモートの Service Fabric アプリケーションをデバッグする](/azure/service-fabric/service-fabric-debugging-your-application#debug-a-remote-service-fabric-application)」を参照してください。

> [!WARNING]
> このチュートリアルの手順を完了したら、作成した Azure リソースを必ず削除してください。 これで、不要な料金の発生を回避できます。

## <a name="prerequisites"></a>必須コンポーネント

::: moniker range=">=vs-2019"
この記事に記載されている手順を実行するには、Visual Studio 2019 が必要です。
::: moniker-end
::: moniker range="vs-2017"
この記事に記載されている手順を実行するには、Visual Studio 2017 が必要です。
::: moniker-end

### <a name="network-requirements"></a>ネットワーク要件

プロキシ経由で接続された 2 台のコンピューター間のデバッグはサポートされていません。 待機時間の長い接続や低帯域幅の接続 (ダイヤルアップ インターネットなど)、または国をまたぐインターネット経由のデバッグは推奨されません。これらは、障害が発生するか、または過度に低速になる可能性があります。 詳細な要件の一覧については、「[要件](../debugger/remote-debugging.md#requirements_msvsmon)」を参照してください。

## <a name="create-the-aspnet-core-application-on-the-visual-studio-computer"></a>Visual Studio コンピューター上で ASP.NET Core アプリケーションを作成する

1. 新しい ASP.NET Core Web アプリケーションを作成します。

    ::: moniker range=">=vs-2019"
    Visual Studio 2019 で、スタート ウィンドウの **[新しいプロジェクトの作成]** を選択します。 スタート ウィンドウが開いていない場合は、 **[ファイル]**  >  **[スタート ウィンドウ]** を選択します。 「**Web アプリ**」と入力し、言語として **C#** を選択します。次に、 **[ASP.NET Core Web Application (Model-View-Controller)]\(ASP.NET Core Web アプリケーション (Model-View-Controller)\)** を選択し、 **[次へ]** を選択します。 次の画面で、プロジェクトに「**MyASPApp**」という名前を指定し、 **[次へ]** を選択します。

    推奨されるターゲット フレームワーク (.NET Core 3.1) または .NET 5 を選択し、 **[作成]** を選択します。
    ::: moniker-end
    ::: moniker range="vs-2017"
    Visual Studio 2017 で、 **[ファイル] > [新規] > [プロジェクト]** を選択し、次に **[Visual C#] > [Web] > [ASP.NET Core Web アプリケーション]** を選択します。 ASP.NET Core テンプレート セクションで、 **[Web アプリケーション (モデル ビュー コントローラー)]** を選択します。 ASP.NET Core 2.1 が選択されていること、 **[Docker サポートを有効にする]** がオフであること、 **[認証]** が **[認証なし]** に設定されていることを確認します。 プロジェクトに「**MyASPApp**」と名前を付けます。
    ::: moniker-end

1. About.cshtml.cs ファイルを開き、`OnGet` メソッドにブレークポイントを設定します (以前のテンプレートでは、代わりに HomeController.cs を開き、`About()` メソッドにブレークポイントを設定します)。

## <a name="remote-debug-aspnet-core-on-an-azure-app-service"></a><a name="remote_debug_azure_app_service"></a> Azure App Service 上で ASP.NET Core をリモート デバッグする

Visual Studio から、IIS の完全にプロビジョニングされたインスタンスにアプリをすばやく発行してデバッグできます。 ただし、IIS の構成は事前設定されており、カスタマイズすることはできません。 詳細な手順については、「[Visual Studio を使用して Azure に ASP.NET Core アプリを発行する](/aspnet/core/tutorials/publish-to-azure-webapp-using-vs)」を参照してください (IIS をカスタマイズする機能が必要な場合は、[Azure VM](#remote_debug_azure_vm) 上でデバッグしてみてください)。

#### <a name="to-deploy-the-app-and-remote-debug-using-cloud-explorer"></a>Cloud Explorer を使用してアプリを配置してリモート デバッグするには

1. Visual Studio で、プロジェクト ノードを右クリックし、 **[発行]** を選択します。

    以前に発行プロファイルを構成してある場合、 **[発行]** ウィンドウが表示されます。 **[新規]** または **[新しいプロファイル]** を選択します。

1. 新しい発行プロファイルを作成する

    ::: moniker range=">=vs-2019"
    **[発行]** ダイアログボックスから **[Azure]** を選択し、 **[次へ]** を選択します。 次に、 **[Azure App Service (Windows)]** を選択し、 **[次へ]** を選択し、画面の指示に従ってプロファイルを作成します。

    :::image type="content" source="../debugger/media/vs-2019/remotedbg-azure-app-service-profile.png" alt-text="Visual Studio を使用して Azure に ASP.NET Core Web アプリを配置する":::
    ::: moniker-end
    ::: moniker range="vs-2017"

    **[発行]** ダイアログボックスから **Azure App Service** を選択し、 **[新規作成]** を選択して、画面の指示に従ってプロファイルを作成します。

    ![Azure App Service に発行する](../debugger/media/remotedbg_azure_app_service_profile.png)
    ::: moniker-end

    詳細な手順については、「[Visual Studio を使用して Azure に ASP.NET Core アプリを発行する](/aspnet/core/tutorials/publish-to-azure-webapp-using-vs)」を参照してください

1. [発行] ウィンドウで、 **[構成の編集]** を選択し、[デバッグ構成] に切り替えて、 **[発行]** を選択します。

   [デバッグ構成] はアプリをデバッグするために必要です。

1. **Cloud Explorer** ( **[表示]**  >  **[Cloud Explorer]** ) を開き、App Service インスタンスを右クリックして、 **[デバッガーのアタッチ]** を選択します。

   Cloud Explorer を使用できない場合は、代わりにサーバー エクスプローラーを開きます。 次に、サーバー エクスプローラーで App Service インスタンスを右クリックし、 **[デバッガーのアタッチ]** を選択します。

1. 実行中の ASP.NET アプリケーションで、 **[バージョン情報]** ページのリンクをクリックします。

    Visual Studio で、ブレークポイントにヒットするはずです。

    これで完了です。 このトピックの残りの手順は、Azure VM 上のリモート デバッグに適用されます。

## <a name="remote-debug-aspnet-core-on-an-azure-vm"></a><a name="remote_debug_azure_vm"></a> Azure VM 上で ASP.NET Core をリモート デバッグする

Windows Server 用の Azure VM を作成し、IIS とその他の必要なソフトウェア コンポーネントをインストールして構成することができます。 これには Azure App Service への配置よりも時間がかかります。また、このチュートリアルの残りの手順に従う必要があります。

これらの手順は、次のサーバー構成でテストされています。

* Windows Server 2012 R2 および IIS 8
* Windows Server 2016 および IIS 10
* Windows Server 2019 および IIS 10

### <a name="app-already-running-in-iis-on-the-azure-vm"></a>アプリは Azure VM 上の IIS で既に実行されていますか?

この記事には、Windows サーバー上で IIS の基本構成を設定し、Visual Studio からアプリを配置する手順が含まれています。 これらの手順は、サーバーに必要なコンポーネントがインストールされていること、アプリを正しく実行できること、およびリモート デバッグの準備ができていることを確認するために含まれています。

* アプリが IIS で実行されていて、リモート デバッガーをダウンロードしてデバッグを開始するだけの場合は、「[Windows Server 上でリモート ツールをダウンロードしてインストールする](#BKMK_msvsmon)」を参照してください。

* アプリが IIS で正しく設定、配置、および実行されていることを確認してデバッグできるようにするためにヘルプが必要な場合は、このトピックのすべての手順に従ってください。

  * 開始する前に、[IIS のインストールと実行](/azure/virtual-machines/windows/quick-create-portal)に記載されているすべての手順を実行します。

  * ネットワーク セキュリティ グループでポート 80 を開くときは、リモート デバッガー用の[適切なポート](#bkmk_openports) (4024 または 4022) も開きます。 こうすることで後で開く必要がなくなります。 Web 配置を使用している場合は、ポート 8172 も開きます。

### <a name="update-browser-security-settings-on-windows-server"></a>Windows Server 上でブラウザーのセキュリティ設定を更新する

Internet Explorer で [セキュリティ強化の構成] が有効な場合は (既定値は有効です)、一部のドメインを信頼済みサイトとして追加し、一部の Web サーバー コンポーネントをダウンロードできるようにする必要があります。 信頼済みサイトを追加するには、 **[インターネット オプション] > [セキュリティ] > [信頼済みサイト] > [サイト]** に移動します。 次のドメインを追加します。

- microsoft.com
- go.microsoft.com
- download.microsoft.com
- iis.net

ソフトウェアをダウンロードすると、さまざまな Web サイトのスクリプトとリソースを読み込むためのアクセス許可を付与する要求を受け取る場合があります。 これらのリソースの一部は不要ですが、プロセスを簡略化するために、プロンプトが表示されたら **[追加]** をクリックします。

### <a name="install-aspnet-core-on-windows-server"></a>Windows Server に ASP.NET Core をインストールする

1. ホスト システムに .NET Core ホスティング バンドルをインストールします。 このバンドルをインストールすることで、.NET Core ランタイム、.NET Core ライブラリ、ASP.NET Core モジュールがインストールされます。 詳細な手順については、[IIS への発行](/aspnet/core/publishing/iis?tabs=aspnetcore2x#iis-configuration)に関するページを参照してください。

    .NET Core 3 の場合は、[.NET Core ホスティング バンドル](https://dotnet.microsoft.com/permalink/dotnetcore-current-windows-runtime-bundle-installer)をインストールします。
    .NET Core 2 の場合は、[.NET Core Windows Server ホスティング](https://aka.ms/dotnetcore-2-windowshosting)をインストールします。

    > [!NOTE]
    > システムにインターネット接続が設定されていない場合は、.NET Core Windows Server ホスティング バンドルをインストールする前に、 *[Microsoft Visual C++ 2015 再頒布可能パッケージ](https://www.microsoft.com/download/details.aspx?id=53840)* を入手してインストールしてください。

2. システムを再起動します (または、コマンド プロンプトから **net stop was /y** の後に続けて **net start w3svc** を実行して、システム PATH への変更を適用します)。

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

> [!NOTE]
> Azure VM を再起動すると、IP アドレスが変更される可能性があります。

アプリが正常に配置されたら、自動的に起動されます。 Visual Studio からアプリが起動しない場合は、IIS でアプリを起動し、正常に動作することを確認します。 ASP.NET Core の場合は、**DefaultAppPool** の [アプリケーション プール] フィールドが **[マネージド コードなし]** に設定されていることも確認する必要があります。

1. **[設定]** ダイアログ ボックスで、 **[次へ]** をクリックしてデバッグを有効にし、 **[デバッグ]** 構成を選択し、 **[ファイル発行オプション]** の **[発行先の追加ファイルを削除する]** を選択します。

    > [!IMPORTANT]
    > リリース構成を選択した場合、発行時に *web.config* ファイルのデバッグを無効にします。

1. **[保存]** をクリックしてアプリを再発行します。

## <a name="optional-deploy-by-publishing-to-a-local-folder"></a>(省略可能) ローカル フォルダーに発行して配置する

PowerShell、RoboCopy を使用してアプリを IIS にコピーする場合、またはファイルを手動でコピーする場合は、このオプションを使用してアプリを配置できます。

### <a name="configure-the-aspnet-core-web-site-on-the-windows-server-computer"></a><a name="BKMK_deploy_asp_net"></a> Windows Server コンピューター上で ASP.NET Core Web サイトを構成する

発行設定をインポートする場合は、このセクションをスキップできます。

1. **インターネット インフォメーション サービス (IIS) マネージャー** を開き、 **[サイト]** に移動します。

2. **[既定の Web サイト]** ノードを右クリックして、 **[アプリケーションの追加]** を選択します。

3. **[エイリアス]** フィールドを「**MyASPApp**」に、[アプリケーション プール] フィールドを **[マネージ コードなし]** に設定します。 **[物理パス]** を **C:\Publish** に設定します (後でここに ASP.NET Core プロジェクトを配置します)。

4. IIS マネージャーでサイトを選択した状態で、 **[アクセス許可の編集]** を選択し、IUSR、IIS_IUSRS、またはアプリケーション プール用に構成されたユーザーが、読み取りと実行の権限を持つ承認済みユーザーであることを確認します。

    これらのアクセス権を持つユーザーが 1 人も表示されない場合は、読み取りおよび実行アクセス権を持つユーザーとして IUSR を追加する手順を実行します。

### <a name="optional-publish-and-deploy-the-app-by-publishing-to-a-local-folder-from-visual-studio"></a>(省略可能) Visual Studio からローカル フォルダーに発行してアプリを発行および配置する

Web 配置を使用していない場合は、ファイル システムまたはその他のツールを使用して、アプリを発行して配置する必要があります。 まず、ファイル システムを使用してパッケージを作成し、パッケージを手動で展開するか、PowerShell、RoboCopy、XCopy などの他のツールを使用します。 このセクションでは、Web 配置を使用していない場合は、パッケージを手動でコピーすることを前提としています。

[!INCLUDE [remote-debugger-deploy-app-local](../debugger/includes/remote-debugger-deploy-app-local.md)]

### <a name="download-and-install-the-remote-tools-on-windows-server"></a><a name="BKMK_msvsmon"></a> Windows Server 上でリモート ツールをダウンロードしてインストールする

Visual Studio のバージョンと一致するバージョンのリモート ツールをダウンロードします。

[!INCLUDE [remote-debugger-download](../debugger/includes/remote-debugger-download.md)]

### <a name="set-up-the-remote-debugger-on-windows-server"></a><a name="BKMK_setup"></a> Windows Server 上でリモート デバッガーを設定する

[!INCLUDE [remote-debugger-configuration](../debugger/includes/remote-debugger-configuration.md)]

> [!NOTE]
> 追加のユーザーのアクセス許可を追加し、認証モード、またはリモート デバッガーのポート番号を変更する必要がある場合は、「[リモート デバッガーを構成する](../debugger/remote-debugging.md#configure_msvsmon)」を参照してください。

### <a name="attach-to-the-aspnet-application-from-the-visual-studio-computer"></a><a name="BKMK_attach"></a> Visual Studio コンピューターから ASP.NET アプリケーションにアタッチする

1. Visual Studio コンピューター上で、デバッグ対象のソリューション (この記事の手順を実行している場合は、**MyASPApp**) を開きます。
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

### <a name="troubleshooting-open-required-ports-on-windows-server"></a><a name="bkmk_openports"></a> トラブルシューティング: Windows Server で必要なポートを開く

ほとんどの設定では、ASP.NET とリモート デバッガーのインストールによって必要なポートが開かれます。 ただし、配置の問題をトラブルシューティングしていて、アプリがファイアウォールの背後でホストされている場合は、必要に応じて正しいポートが開いていることを確認します。

Azure VM では、[ネットワーク セキュリティ グループ](/azure/virtual-machines/windows/nsg-quickstart-portal)を使用してポートを開く必要があります。

必要なポート:

* 80 - IIS に必要です
::: moniker range=">=vs-2019"
* 4024 - Visual Studio 2019 からのリモート デバッグに必要です (詳細については、「[リモート デバッガーのポートの割り当て](../debugger/remote-debugger-port-assignments.md)」を参照してください)。
::: moniker-end
::: moniker range="vs-2017"
* 4022 - Visual Studio 2017 からのリモート デバッグに必要です (詳細については、「[リモート デバッガーのポートの割り当て](../debugger/remote-debugger-port-assignments.md)」を参照してください)。
::: moniker-end
* UDP 3702 - (省略可能) 検出ポートを使用すると、Visual Studio でリモート デバッガーにアタッチするときに **[検索]** ボタンを使用できます。

また、ASP.NET をインストールしている場合、これらのポートは既に開かれているはずです。
- 8172 - (省略可能) Web 配置で Visual Studio からアプリを配置する場合に必要です
