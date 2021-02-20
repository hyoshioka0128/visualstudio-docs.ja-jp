---
title: IIS コンピューター上の ASP.NET のリモート デバッグ
description: Visual Studio ASP.NET MVC 4.5.2 アプリケーションを設定して構成し、それを IIS に配置し、Visual Studio からリモート デバッガーをアタッチする方法を学習します。
ms.custom:
- remotedebugging
- seodec18
ms.date: 05/06/2020
ms.topic: conceptual
ms.assetid: 9cb339b5-3caf-4755-aad1-4a5da54b2a23
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- aspnet
ms.openlocfilehash: 854d3e23252e63d6330abd9f1704890d3b90ae36
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99908307"
---
# <a name="remote-debug-aspnet-on-a-remote-iis-computer"></a>リモートの IIS コンピューター上の ASP.NET のリモート デバッグ
IIS に配置されている ASP.NET アプリケーションをデバッグするには、アプリを配置したコンピューターにリモート ツールをインストールして実行し、Visual Studio から実行中のアプリにアタッチします。

![リモート デバッガーのコンポーネント](../debugger/media/remote-debugger-aspnet.png "Remote_debugger_components")

このガイドでは、ASP.NET MVC 4.5.2 アプリケーションを設定して構成し、それを IIS に配置し、Visual Studio からリモート デバッガーをアタッチする方法について説明します。

> [!NOTE]
> 代わりに ASP.NET Core をリモート デバッグするには、「[IIS コンピューター上の ASP.NET Core のリモート デバッグ](../debugger/remote-debugging-aspnet-on-a-remote-iis-computer.md)」を参照してください。 Azure App Service の場合、[スナップショット デバッガー](../debugger/debug-live-azure-applications.md) (.NET 4.6.1 が必要です) を使用するか、[サーバー エクスプローラーからデバッガーをアタッチする](../debugger/remote-debugging-azure.md)ことで、IIS の事前構成済みインスタンスで配置とデバッグを簡単に行うことができます。

## <a name="prerequisites"></a>必須コンポーネント

::: moniker range=">=vs-2019"
この記事に記載されている手順を実行するには、Visual Studio 2019 が必要です。
::: moniker-end
::: moniker range="vs-2017"
この記事に記載されている手順を実行するには、Visual Studio 2017 が必要です。
::: moniker-end

これらの手順は、次のサーバー構成でテストされています。
* Windows Server 2012 R2 および IIS 8 (Windows Server 2008 R2 では、サーバーの手順が異なります)

## <a name="network-requirements"></a>ネットワーク要件

リモート デバッガーは、Windows Server の Windows Server 2008 Service Pack 2 以降でサポートされます。 詳細な要件の一覧については、「[要件](../debugger/remote-debugging.md#requirements_msvsmon)」を参照してください。

> [!NOTE]
> プロキシ経由で接続された 2 台のコンピューター間のデバッグはサポートされていません。 待機時間の長い接続や低帯域幅の接続 (ダイヤルアップ インターネットなど)、または国をまたぐインターネット経由のデバッグは推奨されません。これらは、障害が発生するか、または過度に低速になる可能性があります。

## <a name="app-already-running-in-iis"></a>アプリは既に IIS で実行されていますか?

この記事には、Windows サーバー上で IIS の基本構成を設定し、Visual Studio からアプリを配置する手順が含まれています。 これらの手順は、サーバーに必要なコンポーネントがインストールされていること、アプリを正しく実行できること、およびリモート デバッグの準備ができていることを確認するために含まれています。

* アプリが IIS で実行されていて、リモート デバッガーをダウンロードしてデバッグを開始するだけの場合は、「[Windows Server 上でリモート ツールをダウンロードしてインストールする](#BKMK_msvsmon)」を参照してください。

* アプリが IIS で正しく設定、配置、および実行されていることを確認してデバッグできるようにするためにヘルプが必要な場合は、このトピックのすべての手順に従ってください。

## <a name="create-the-aspnet-452-application-on-the-visual-studio-computer"></a>Visual Studio コンピューター上で ASP.NET 4.5.2 アプリケーションを作成する

1. MVC の ASP.NET アプリケーションを新規作成します。

    ::: moniker range=">=vs-2019"
    Visual Studio 2019 で **Ctrl + Q** キーを押して検索ボックスを開き、「**asp.net**」と入力し、 **[テンプレート]** を選択してから、 **[新しい ASP.NET Web アプリケーションの作成 (.NET Framework)]** を選択します。 表示されるダイアログ ボックスで、プロジェクトに「**MyASPApp**」という名前を付け、 **[作成]** を選択します。 **[MVC]** を選択し、 **[作成]** を選択します。
    ::: moniker-end
    ::: moniker range="vs-2017"
    Visual Studio 2017 でこれを行うには、 **[ファイル] > [新規] > [プロジェクト]** を選択し、次に **[Visual C#] > [Web] > [ASP.NET Web アプリケーション]** を選択します。 **[ASP.NET 4.5.2** テンプレート] セクションで、 **[MVC]** を選択します。 **[Docker サポートを有効にする]** がオフであること、 **[認証]** が **[認証なし]** に設定されていることを確認します。 プロジェクトに「**MyASPApp**」という名前を付けます。
    ::: moniker-end

2. *HomeController.cs* ファイルを開き、`About()` メソッド内にブレークポイントを設定します。

## <a name="install-and-configure-iis-on-windows-server"></a><a name="bkmk_configureIIS"></a> Windows Server に IIS をインストールして構成する

[!INCLUDE [remote-debugger-install-iis-role](../debugger/includes/remote-debugger-install-iis-role.md)]

## <a name="update-browser-security-settings-on-windows-server"></a>Windows Server 上でブラウザーのセキュリティ設定を更新する

Internet Explorer で [セキュリティ強化の構成] が有効な場合は (既定値は有効です)、一部のドメインを信頼済みサイトとして追加し、一部の Web サーバー コンポーネントをダウンロードできるようにする必要があります。 信頼済みサイトを追加するには、 **[インターネット オプション] > [セキュリティ] > [信頼済みサイト] > [サイト]** に移動します。 次のドメインを追加します。

- microsoft.com
- go.microsoft.com
- download.microsoft.com
- iis.net

ソフトウェアをダウンロードすると、さまざまな Web サイトのスクリプトとリソースを読み込むためのアクセス許可を付与する要求を受け取る場合があります。 これらのリソースの一部は不要ですが、プロセスを簡略化するために、プロンプトが表示されたら **[追加]** をクリックします。

## <a name="install-aspnet-45-on-windows-server"></a><a name="BKMK_deploy_asp_net"></a>Windows Server に ASP.NET 4.5 をインストールする

ASP.NET を IIS にインストールするための詳細な情報が必要な場合は、「[ASP.NET 3.5 と ASP.NET 4.5を使用する IIS 8.0](/iis/get-started/whats-new-in-iis-8/iis-80-using-aspnet-35-and-aspnet-45)」を参照してください。

1. サーバー マネージャーの左側のペインで、 **[IIS]** を選択します。 サーバーを右クリックして **[インターネット インフォメーション サービス (IIS) マネージャー]** を選択します。

1. Web Platform Installer (WebPI) を使用して、ASP.NET 4.5 をインストールします (Windows Server 2012 R2 のサーバー ノードから **[Get New Web Platform Components]\(新しい Web プラットフォーム コンポーネントを取得する\)** を選択し、[ASP.NET] を検索します)。

    ![Web Platform Installer 5.0 のスクリーンショット。asp.net の検索結果が表示され、Web プラットフォーム コンポーネント IIS: ASP.NET 4.5 が赤い円で囲まれています。](../debugger/media/remotedbg_iis_aspnet_45.png)

    > [!NOTE]
    > Windows Server 2008 R2 を使用している場合は、次のコマンドを使用して、代わりに ASP.NET 4 をインストールしてください。

     **C:\Windows\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe -ir**

2. システムを再起動します (または、コマンド プロンプトから **net stop was /y** の後に続けて **net start w3svc** を実行して、システム PATH への変更を適用します)。

## <a name="choose-a-deployment-option"></a>配置オプションを選択する

IIS へのアプリの配置についてヘルプが必要な場合は、次のオプションを検討してください。

* IIS で発行設定ファイルを作成し、Visual Studio に設定をインポートして配置します。 シナリオによっては、この方法でアプリを迅速に配置できます。 発行設定ファイルを作成すると、IIS でアクセス許可が自動的に設定されます。

* ローカル フォルダーに発行し、適切な方法で出力を IIS 上の準備されたアプリ フォルダーにコピーすることで配置します。

## <a name="optional-deploy-using-a-publish-settings-file"></a>(省略可能) 発行設定ファイルを使用してデプロイする

このオプションを使用すると、発行設定ファイルを作成し、それを Visual Studio にインポートすることができます。

> [!NOTE]
> この配置方法では Web 配置を使用するため、サーバーに Web 配置がインストールされている必要があります。 設定をインポートするのではなく、Web 配置を手動で構成する場合は、ホスティング サーバー用 Web 配置 3.6 ではなく、Web 配置 3.6 をインストールすることができます。 ただし、Web 配置を手動で構成する場合は、サーバー上のアプリ フォルダーが正しい値とアクセス許可で構成されていることを確認する必要があります ([ASP.NET Web サイトの構成](#BKMK_deploy_asp_net)に関するセクションを参照してください)。

### <a name="install-and-configure-web-deploy-for-hosting-servers-on-windows-server"></a>Windows Server にホスティング サーバー用 Web 配置をインストールして構成する

[!INCLUDE [install-web-deploy-with-hosting-server](../deployment/includes/install-web-deploy-with-hosting-server.md)]

### <a name="create-the-publish-settings-file-in-iis-on-windows-server"></a>Windows Server 上の IIS に発行設定ファイルを作成する

[!INCLUDE [install-web-deploy-with-hosting-server](../deployment/includes/create-publish-settings-iis.md)]

### <a name="import-the-publish-settings-in-visual-studio-and-deploy"></a>Visual Studio で発行設定をインポートして配置する

[!INCLUDE [install-web-deploy-with-hosting-server](../deployment/includes/import-publish-settings-vs.md)]

アプリが正常に配置されたら、自動的に起動されます。 Visual Studio からアプリが起動しない場合は、IIS でアプリを起動します。

1. **[設定]** ダイアログ ボックスで、 **[次へ]** をクリックしてデバッグを有効にし、 **[デバッグ]** 構成を選択し、 **[ファイル発行オプション]** の **[発行先の追加ファイルを削除する]** を選択します。

    > [!IMPORTANT]
    > リリース構成を選択した場合、発行時に *web.config* ファイルのデバッグを無効にします。

1. **[保存]** をクリックしてアプリを再発行します。

## <a name="optional-deploy-by-publishing-to-a-local-folder"></a>(省略可能) ローカル フォルダーに発行して配置する

PowerShell、RoboCopy を使用してアプリを IIS にコピーする場合、またはファイルを手動でコピーする場合は、このオプションを使用してアプリを配置できます。

### <a name="configure-the-aspnet-web-site-on-the-windows-server-computer"></a><a name="BKMK_deploy_asp_net"></a> Windows Server コンピューター上で ASP.NET Web サイトを構成する

1. Windows エクスプローラーを開き、新しいフォルダー **C:\Publish** を作成します。後でここに ASP.NET プロジェクトを配置します。

2. **インターネット インフォメーション サービス (IIS) マネージャー** をまだ開いていない場合は開きます (サーバー マネージャーの左側のペインで、 **[IIS]** を選択します。 サーバーを右クリックして **[インターネット インフォメーション サービス (IIS) マネージャー]** を選択します。)

3. 左側のペインの **[接続]** で、 **[サイト]** に移動します。

4. **[既定の Web サイト]** を選択し、 **[基本設定]** を選択して、 **[物理パス]** を **C:\Publish** に設定します。

5. **[既定の Web サイト]** ノードを右クリックして、 **[アプリケーションの追加]** を選択します。

6. **[エイリアス]** フィールドを「**MyASPApp**」に設定し、既定のアプリケーション プール (**DefaultAppPool**) のままにして **[物理パス]** を **C:\ Publish** に設定します。

7. **[接続]** の **[アプリケーション プール]** を選択します。 **DefaultAppPool** を開き、[アプリケーション プール] フィールドを **[ASP.NET v4.0]** に設定します (ASP.NET 4.5 はアプリケーション プールのオプションではありません)。

8. IIS マネージャーでサイトを選択した状態で、 **[アクセス許可の編集]** を選択し、IUSR、IIS_IUSRS、またはアプリケーション プール用に構成されたユーザーが、読み取りと実行の権限を持つ承認済みユーザーであることを確認します。 これらのユーザーのいずれも存在しない場合は、読み取り権限と実行権限を持つユーザーとして IUSR を追加します。

### <a name="publish-and-deploy-the-app-by-publishing-to-a-local-folder-from-visual-studio"></a>Visual Studio からローカル フォルダーに発行してアプリを発行および配置する

ファイル システムやその他のツールを使用して、アプリを発行および配置することもできます。

1. (ASP.NET 4.5.2) web.config ファイルに .NET の正しいバージョンが示されていることを確認します。  たとえば、ASP.NET 4.5.2 をターゲットとしている場合は、このバージョンが web.config に示されていることを確認します。

    ```xml
    <system.web>
      <compilation debug="true" targetFramework="4.5.2" />
      <httpRuntime targetFramework="4.5.2" />
      <httpModules>
        <add name="ApplicationInsightsWebTracking" type="Microsoft.ApplicationInsights.Web.ApplicationInsightsHttpModule, Microsoft.AI.Web" />
      </httpModules>
    </system.web>

    ```

    たとえば 4.5.2 の代わりに ASP.NET 4 をインストールした場合、バージョンは 4.0 になります。

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

5. **[すべてのユーザーからのプロセスを表示する]** をオンにします。

6. プロセス名の最初の文字を入力すると、ASP.NET 4.5 用の **w3wp.exe** をすばやく見つけることができます。

    **w3wp.exe** と表示されているプロセスが複数ある場合は、 **[ユーザー名]** 列を確認します。 一部のシナリオでは、 **[ユーザー名]** 列に **IIS APPPOOL\DefaultAppPool** などのアプリ プール名が表示されます。 アプリ プールが表示される場合、正しいプロセスを特定する簡単な方法は、デバッグするアプリ インスタンスの新しい名前付きアプリ プールを作成することです。 **[ユーザー名]** 列で簡単に見つけられるようになります。

    ::: moniker range=">=vs-2019"
    ![RemoteDBG_AttachToProcess](../debugger/media/vs-2019/remotedbg-attachtoprocess.png "RemoteDBG_AttachToProcess")
    ::: moniker-end
    ::: moniker range="vs-2017"
    ![RemoteDBG_AttachToProcess](../debugger/media/remotedbg-attachtoprocess.png "RemoteDBG_AttachToProcess")
    ::: moniker-end

7. **[アタッチ]** をクリックします

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

2. 次に、 **[受信規則] > [新しい規則] > [ポート]** を選択します。 **[次へ]** を選択します。 **[特定のローカル ポート]** にポート番号を入力し、 **[次へ]** をクリックします。その後、 **[接続を許可する]** 、[次へ] をクリックし、受信規則の名前 (**IIS**、**Web Deploy**、または **msvsmon**) を追加します。

    Windows ファイアウォールの構成の詳細については、「[Windows ファイアウォールをリモート デバッグ用に構成する](../debugger/configure-the-windows-firewall-for-remote-debugging.md)」を参照してください。

3. その他の必要なポートに追加の規則を作成します。