---
title: IIS と Azure でのリモートデバッグ ASP.NET Core |Microsoft Docs
ms.custom: remotedebugging
ms.date: 05/21/2018
ms.topic: conceptual
ms.assetid: a6c04b53-d1b9-4552-a8fd-3ed6f4902ce6
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- aspnet
- dotnetcore
- azure
ms.openlocfilehash: c6a41a332e16f79673b475404af27e540689938d
ms.sourcegitcommit: 3d64bfb9bf85395357effe054db9a9afaa0be5ea
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/29/2020
ms.locfileid: "78181131"
---
# <a name="remote-debug-aspnet-core-on-iis-in-azure-in-visual-studio"></a>Visual Studio での Azure での IIS のリモートデバッグ ASP.NET Core

このガイドでは、Visual Studio ASP.NET Core アプリをセットアップして構成し、Azure を使用して IIS にデプロイし、Visual Studio からリモートデバッガーをアタッチする方法について説明します。

Azure でのリモートデバッグに推奨される方法は、シナリオによって異なります。

* Azure App Service で ASP.NET Core をデバッグするには、「[スナップショットデバッガーを使用した Azure アプリのデバッグ](../debugger/debug-live-azure-applications.md)」を参照してください。 このセキュリティ メソッドをお勧めします。
* より従来のデバッグ機能を使用して Azure App Service の ASP.NET Core をデバッグするには、このトピックの手順に従います ( [Azure App Service のリモートデバッグに関する](#remote_debug_azure_app_service)セクションを参照してください)。

    このシナリオでは、アプリを Visual Studio から Azure にデプロイする必要がありますが、次の図に示すように、IIS またはリモートデバッガーを手動でインストールまたは構成する必要はありません (これらのコンポーネントは点線で表されます)。

    ![リモートデバッガーコンポーネント](../debugger/media/remote-debugger-azure-app-service.png "Remote_debugger_components")

* Azure VM で IIS をデバッグするには、このトピックの手順を実行します (「 [AZURE vm のリモートデバッグ](#remote_debug_azure_vm)」セクションを参照してください)。 これにより、カスタマイズされた IIS の構成を使用できますが、セットアップと展開の手順はより複雑になります。

    Azure VM の場合は、次の図に示すように、Visual Studio から Azure にアプリをデプロイする必要があります。また、IIS ロールとリモートデバッガーを手動でインストールする必要もあります。

    ![リモートデバッガーコンポーネント](../debugger/media/remote-debugger-azure-vm.png "Remote_debugger_components")

* Azure Service Fabric で ASP.NET Core をデバッグするには、「[リモート Service Fabric アプリケーションのデバッグ](/azure/service-fabric/service-fabric-debugging-your-application#debug-a-remote-service-fabric-application)」を参照してください。

> [!WARNING]
> このチュートリアルの手順を完了したら、作成した Azure リソースを必ず削除してください。 そうすれば、不要な料金の発生を回避できます。

## <a name="prerequisites"></a>前提条件

::: moniker range=">=vs-2019"
この記事に記載されている手順を実行するには、Visual Studio 2019 が必要です。
::: moniker-end
::: moniker range="vs-2017"
この記事に記載されている手順を実行するには、Visual Studio 2017 が必要です。
::: moniker-end

### <a name="network-requirements"></a>ネットワーク要件

プロキシ経由で接続されている2台のコンピューター間のデバッグはサポートされていません。 高待機時間接続または低帯域幅接続 (ダイヤルアップインターネットなど) またはインターネット経由でのデバッグは推奨されません。また、障害が発生する可能性があります。 要件の完全な一覧については、「[要件](../debugger/remote-debugging.md#requirements_msvsmon)」を参照してください。

## <a name="create-the-aspnet-core-application-on-the-visual-studio-computer"></a>Visual Studio コンピューターで ASP.NET Core アプリケーションを作成する

1. 新しい ASP.NET Core アプリケーションを作成します。

    ::: moniker range=">=vs-2019"
    Visual Studio 2019 で、 **Ctrl キーを押しながら Q キーを押し**て検索ボックスを開き、「 **asp.net**」と入力します。次に、 **[テンプレート]** を選択し、 **[新しい ASP.NET Core Web アプリケーションの作成]** を選択します。 表示されるダイアログボックスで、プロジェクトに**MyASPApp**という名前を指定し、 **[作成]** を選択します。 次に、 **[Web アプリケーション (モデルビューコントローラー)]** を選択し、 **[作成]** を選択します。
    ::: moniker-end
    ::: moniker range="vs-2017"
    Visual Studio 2017 で、 **[ファイル > 新しい > プロジェクト]** を選択し、 **[visual C# > web > ASP.NET Core web アプリケーション]** を選択します。 ASP.NET Core テンプレート セクションで、 **Web アプリケーション (モデルビューコントローラー)** を選択します。 ASP.NET Core 2.1 が選択され、 **[Docker サポートを有効に]** する が選択されておらず、**認証**が **[認証なし]** に設定されていることを確認します。 プロジェクトに**MyASPApp**という名前を指定します。
    ::: moniker-end

1. About.cshtml.cs ファイルを開き、`OnGet` メソッドにブレークポイントを設定します (以前のテンプレートでは、代わりに HomeController.cs を開いて、`About()` メソッドにブレークポイントを設定します)。

## <a name="remote_debug_azure_app_service"></a>Azure App Service 上のリモートデバッグ ASP.NET Core

Visual Studio から、完全にプロビジョニングされた IIS インスタンスにアプリをすばやく発行し、デバッグすることができます。 ただし、IIS の構成は事前設定されており、カスタマイズすることはできません。 詳細な手順については、「 [Visual Studio を使用した Azure への ASP.NET Core web アプリのデプロイ](/aspnet/core/tutorials/publish-to-azure-webapp-using-vs)」を参照してください。 (IIS をカスタマイズする必要がある場合は、 [AZURE VM](#remote_debug_azure_vm)でデバッグを試してください。)

#### <a name="to-deploy-the-app-and-remote-debug-using-server-explorer"></a>サーバーエクスプローラーを使用してアプリとリモートデバッグをデプロイするには

1. Visual Studio で、プロジェクトノードを右クリックし、 **[発行]** を選択します。

    以前に発行プロファイルを構成してある場合、 **[発行]** ウィンドウが表示されます。 **[新しいプロファイル]** をクリックします。

1. **[発行]** ダイアログボックスで **[Azure App Service]** を選択し、 **[新規作成]** を選択して、表示される指示に従って発行します。

    詳細な手順については、「[Visual Studio を使用して Azure に ASP.NET Core アプリを発行する](/aspnet/core/tutorials/publish-to-azure-webapp-using-vs)」を参照してください。

    ![Azure App Service に発行する](../debugger/media/remotedbg_azure_app_service_profile.png)

1. **サーバーエクスプローラー** (**ビュー** > **サーバーエクスプローラー**) を開き、App Service インスタンスを右クリックし、 **[デバッガーのアタッチ]** を選択します。

1. 実行中の ASP.NET アプリケーションで、 **[バージョン情報]** ページへのリンクをクリックします。

    Visual Studio で、ブレークポイントにヒットするはずです。

    以上で終わりです。 このトピックの残りの手順は、Azure VM でのリモートデバッグに適用されます。

## <a name="remote_debug_azure_vm"></a>Azure VM 上のリモートデバッグ ASP.NET Core

Windows Server 用の Azure VM を作成し、IIS とその他の必要なソフトウェアコンポーネントをインストールして構成することができます。 これには Azure App Service へのデプロイよりも時間がかかり、このチュートリアルの残りの手順に従う必要があります。

これらの手順は、次のサーバー構成でテストされています。
* Windows Server 2012 R2 および IIS 8
* Windows Server 2016 および IIS 10

### <a name="app-already-running-in-iis-on-the-azure-vm"></a>アプリは Azure VM の IIS で既に実行されていますか?

この記事では、Windows server で IIS の基本的な構成を設定し、Visual Studio からアプリをデプロイする手順について説明します。 これらの手順は、サーバーに必要なコンポーネントがインストールされていること、アプリが正常に実行できること、およびリモートデバッグの準備ができていることを確認するために含まれています。

* アプリが IIS で実行されていて、リモートデバッガーをダウンロードしてデバッグを開始するだけの場合は、「 [Windows Server でのリモートツールのダウンロードとインストール](#BKMK_msvsmon)」を参照してください。

* アプリケーションをデバッグできるように IIS で正しくセットアップ、展開、および実行するためのヘルプが必要な場合は、このトピックのすべての手順に従ってください。

  * 開始する前に、「 [IIS のインストールと実行](/azure/virtual-machines/windows/quick-create-portal)」に記載されているすべての手順を実行します。

  * ネットワークセキュリティグループでポート80を開いた場合は、リモートデバッガーの[正しいポート](#bkmk_openports)(4024 または 4022) も開きます。 このようにして、後で開く必要はありません。

### <a name="update-browser-security-settings-on-windows-server"></a>Windows Server でブラウザーのセキュリティ設定を更新する

Internet Explorer で [セキュリティ強化の構成] が有効になっている場合 (既定では有効になっています)、一部のドメインを信頼済みサイトとして追加して、一部の web サーバーコンポーネントをダウンロードできるようにする必要があります。 信頼済みサイトを追加するには、[**インターネットオプション] > [セキュリティ > 信頼済みサイト > サイト**] の順に移動します。 次のドメインを追加します。

- microsoft.com
- go.microsoft.com
- download.microsoft.com
- iis.net

ソフトウェアをダウンロードするときに、さまざまな web サイトのスクリプトとリソースを読み込むためのアクセス許可を付与するように求められる場合があります。 これらのリソースの一部は必須ではありませんが、プロセスを簡略化するために、メッセージが表示されたら **[追加]** をクリックします。

### <a name="install-aspnet-core-on-windows-server"></a>Windows Server に ASP.NET Core をインストールする

1. ホスティング システムに [.NET Core Windows Server ホスティング](https://aka.ms/dotnetcore-2-windowshosting) バンドルをインストールします。 このバンドルをインストールすることで、.NET Core ランタイム、.NET Core ライブラリ、ASP.NET Core モジュールがインストールされます。 詳細な手順については、「 [IIS への発行](/aspnet/core/publishing/iis?tabs=aspnetcore2x#iis-configuration)」を参照してください。

    > [!NOTE]
    > システムにインターネット接続が設定されていない場合は、.NET Core Windows Server ホスティング バンドルをインストールする前に、 *[Microsoft Visual C++ 2015 再頒布可能パッケージ](https://www.microsoft.com/download/details.aspx?id=53840)* を入手してインストールしてください。

3. システムを再起動します (または、コマンド プロンプトから **net stop was /y** の後に続けて **net start w3svc** を実行して、システム PATH への変更を適用します)。

## <a name="choose-a-deployment-option"></a>デプロイオプションの選択

IIS へのアプリの展開に関するヘルプが必要な場合は、次のオプションを検討してください。

* IIS で発行設定ファイルを作成し、Visual Studio で設定をインポートしてデプロイします。 シナリオによっては、これはアプリをデプロイするための迅速な方法です。 発行設定ファイルを作成すると、IIS でアクセス許可が自動的に設定されます。

* ローカルフォルダーに発行し、推奨される方法で出力を IIS 上の準備済みアプリフォルダーにコピーして配置します。

## <a name="optional-deploy-using-a-publish-settings-file"></a>Optional発行設定ファイルを使用したデプロイ

このオプションを使用して、発行設定ファイルを作成し、Visual Studio にインポートすることができます。

> [!NOTE]
> この展開方法では、Web 配置を使用します。 設定をインポートするのではなく、Visual Studio で Web 配置手動で構成する場合は、ホスティングサーバー用に 3.6 Web 配置ではなく Web 配置3.6 をインストールできます。 ただし、Web 配置を手動で構成する場合は、サーバー上のアプリフォルダーに正しい値とアクセス許可が構成されていることを確認する必要があります ( [ASP.NET Web サイトの構成](#BKMK_deploy_asp_net)に関するページを参照してください)。

### <a name="install-and-configure-web-deploy-for-hosting-servers-on-windows-server"></a>Windows Server でサーバーをホストするための Web 配置のインストールと構成

[!INCLUDE [install-web-deploy-with-hosting-server](../deployment/includes/install-web-deploy-with-hosting-server.md)]

### <a name="create-the-publish-settings-file-in-iis-on-windows-server"></a>Windows Server 上の IIS に発行設定ファイルを作成する

[!INCLUDE [install-web-deploy-with-hosting-server](../deployment/includes/create-publish-settings-iis.md)]

### <a name="import-the-publish-settings-in-visual-studio-and-deploy"></a>Visual Studio で発行設定をインポートして配置する

[!INCLUDE [install-web-deploy-with-hosting-server](../deployment/includes/import-publish-settings-vs.md)]

アプリが正常に配置されたら、自動的に起動されます。 アプリが Visual Studio から起動しない場合は、IIS でアプリを起動します。 ASP.NET Core の場合、**DefaultAppPool** の [アプリケーション プール] フィールドが **[マネージド コードなし]** に設定されていることを確認する必要があります。

1. **[設定]** ダイアログボックスで、 **[次へ]** をクリックしてデバッグを有効にし、**デバッグ**構成を選択します。次に、 **[ファイルの発行]** オプションで、 **[変換先の追加ファイルを削除]** する を選択します。

    > [!NOTE]
    > リリース構成を選択した場合は、発行時に*web.config ファイルで*デバッグを無効にします。

1. **[保存]** をクリックし、アプリを再発行します。

## <a name="optional-deploy-by-publishing-to-a-local-folder"></a>Optionalローカルフォルダーへの発行による配置

PowerShell または RoboCopy を使用してアプリを IIS にコピーする場合、または手動でファイルをコピーする場合は、このオプションを使用してアプリをデプロイできます。

### <a name="BKMK_deploy_asp_net"></a>Windows Server コンピューターで ASP.NET Core Web サイトを構成する

発行設定をインポートする場合は、このセクションを省略できます。

1. **インターネット インフォメーション サービス (IIS) マネージャー** を開き、 **[サイト]** に移動します。

2. **[既定の Web サイト]** ノードを右クリックして、 **[アプリケーションの追加]** を選択します。

3. **エイリアス** フィールドを **MyASPApp** に設定し、アプリケーションプール フィールドを **マネージコードなし** に設定します。 **物理パス**を**c:\ Publish** (後で ASP.NET Core プロジェクトをデプロイする場所) に設定します。

4. IIS マネージャーでサイトを選択した状態で、 **[アクセス許可の編集]** を選択し、IUSR、IIS_IUSRS、またはアプリケーションプール用に構成されたユーザーが、読み取り & 実行権限を持つ承認されたユーザーであることを確認します。

    これらのユーザーのいずれかがアクセスできない場合は、「Read & Execute 権限を持つユーザーとして IUSR を追加する手順」を参照してください。

### <a name="optional-publish-and-deploy-the-app-by-publishing-to-a-local-folder-from-visual-studio"></a>OptionalVisual Studio からローカルフォルダーに発行してアプリを発行してデプロイする

Web 配置を使用していない場合は、ファイルシステムまたはその他のツールを使用して、アプリを発行して展開する必要があります。 まず、ファイルシステムを使用してパッケージを作成してから、パッケージを手動で展開するか、PowerShell、RoboCopy、XCopy などの他のツールを使用します。 このセクションでは、Web 配置を使用していない場合に、パッケージを手動でコピーすることを前提としています。

[!INCLUDE [remote-debugger-deploy-app-local](../debugger/includes/remote-debugger-deploy-app-local.md)]

### <a name="BKMK_msvsmon"></a>Windows Server でのリモートツールのダウンロードとインストール

使用している Visual Studio のバージョンに対応するバージョンのリモートツールをダウンロードします。

[!INCLUDE [remote-debugger-download](../debugger/includes/remote-debugger-download.md)]

### <a name="BKMK_setup"></a>Windows Server でリモートデバッガーを設定する

[!INCLUDE [remote-debugger-configuration](../debugger/includes/remote-debugger-configuration.md)]

> [!NOTE]
> 追加のユーザーにアクセス許可を追加する必要がある場合、リモートデバッガーの認証モードまたはポート番号を変更するには、「[リモートデバッガーの構成](../debugger/remote-debugging.md#configure_msvsmon)」を参照してください。

### <a name="BKMK_attach"></a> Visual Studio コンピューターから ASP.NET アプリケーションにアタッチする

1. Visual Studio コンピューターで、デバッグしようとしているソリューションを開きます (この記事の手順に従っている場合は**MyASPApp** )。
2. Visual Studio で、**デバッグ > プロセスにアタッチ** をクリックします (Ctrl + Alt + P)。

    > [!TIP]
    > Visual Studio 2017 以降のバージョンでは、**デバッグ > プロセスに**再アタッチ (Shift + Alt + P) を使用して、以前にアタッチした同じプロセスに再アタッチできます。

3. [修飾子] フィールドを **\<リモートコンピューター名 >** に設定し **、enter キーを押します。**

    Visual Studio によって、必要なポートがコンピューター名に追加されることを確認します。これは、 **\<リモートコンピューター名 >:p ort**という形式で表示されます。

    ::: moniker range=">=vs-2019"
    Visual Studio 2019 で **\<リモートコンピューター名 >: 4024**が表示されるはずです。
    ::: moniker-end
    ::: moniker range="vs-2017"
    Visual Studio 2017 で **\<リモートコンピューター名 >: 4022**が表示されるはずです。
    ::: moniker-end
    ポートが必要です。 ポート番号が表示されない場合は、手動で追加します。

4. **[最新の情報に更新]** をクリックします。
    **[選択可能なプロセス]** ウィンドウにプロセスがいくつか表示されます。

    すべてのプロセスが表示されない場合は、(ポートが必要です)、リモート コンピューター名ではなく IP アドレスを使用してください。 コマンドラインで `ipconfig` を使用すると、IPv4 アドレスを取得できます。

    **[検索]** ボタンを使用する場合は、サーバーで[UDP ポート3702を開く](#bkmk_openports)必要がある場合があります。

5. **[すべてのユーザーからのプロセスを表示する]** をオンにします。

6. アプリケーションをすばやく検索するには、プロセス名の最初の文字を入力します。

    * Dotnet (.NET Core の場合) を選択し**ます。**

      **Dotnet**を表示しているプロセスが複数ある場合は、 **[ユーザー名]** 列を確認します。 場合によっては、 **[ユーザー名]** 列に、 **IIS APPPOOL\DefaultAppPool**などのアプリケーションプール名が表示されます。 アプリケーションプールが表示されている場合、適切なプロセスを簡単に識別するには、デバッグするアプリインスタンスの新しい名前付きアプリプールを作成します。その後、 **[ユーザー名]** 列で簡単に見つけることができます。

    * 一部の IIS シナリオでは、 **MyASPApp**などのアプリケーション名がプロセス一覧に表示される場合があります。 代わりに、このプロセスにアタッチできます。

    ::: moniker range=">=vs-2019"
    ![RemoteDBG_AttachToProcess](../debugger/media/vs-2019/remotedbg-attachtoprocess-aspnetcore.png "RemoteDBG_AttachToProcess")
    ::: moniker-end
    ::: moniker range="vs-2017"
    ![RemoteDBG_AttachToProcess](../debugger/media/remotedbg-attachtoprocess-aspnetcore.png "RemoteDBG_AttachToProcess")
    ::: moniker-end

7. **[アタッチ]** をクリックします。

8. リモート コンピューターの Web サイトを開きます。 ブラウザーで、**http://\<リモート コンピューター名>** に移動します。

    ASP.NET の Web ページが表示されるはずです。
9. 実行中の ASP.NET アプリケーションで、 **[バージョン情報]** ページへのリンクをクリックします。

    Visual Studio で、ブレークポイントにヒットするはずです。

### <a name="bkmk_openports"></a> トラブルシューティングWindows Server で必要なポートを開く

ほとんどのセットアップでは、ASP.NET とリモートデバッガーのインストールによって必要なポートが開かれます。 ただし、展開の問題のトラブルシューティングを行い、アプリがファイアウォールの内側でホストされている場合は、正しいポートが開いていることを確認する必要があります。

Azure VM では、[ネットワークセキュリティグループ](/azure/virtual-machines/windows/nsg-quickstart-portal)を介してポートを開く必要があります。

必要なポート:

* 80-IIS で必要
::: moniker range=">=vs-2019"
* 4024-Visual Studio 2019 からのリモートデバッグに必要です (詳細については、「[リモートデバッガーのポートの割り当て](../debugger/remote-debugger-port-assignments.md)」を参照してください)。
::: moniker-end
::: moniker range="vs-2017"
* 4022-Visual Studio 2017 からのリモートデバッグに必要です (詳細については、「[リモートデバッガーのポートの割り当て](../debugger/remote-debugger-port-assignments.md)」を参照してください)。
::: moniker-end
* UDP 3702-(省略可能) 探索ポートを使用すると、Visual Studio でリモートデバッガーにアタッチするときに **[検索]** ボタンを使用できます。

また、これらのポートは、ASP.NET インストールによって既に開かれている必要があります。
- 8172-(省略可能) Visual Studio からアプリを配置する Web 配置に必要
