---
title: リモートの IIS コンピューター上のリモートデバッグ ASP.NET Core |Microsoft Docs
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
ms.openlocfilehash: 3e11480949545781630dec0c533949dd200ecbc7
ms.sourcegitcommit: 7a9d5c10690c594dcdb414d88b20e070d43e7a4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "82218887"
---
# <a name="remote-debug-aspnet-core-on-a-remote-iis-computer-in-visual-studio"></a>Visual Studio のリモート IIS コンピューター上のリモートデバッグ ASP.NET Core

IIS に配置されている ASP.NET Core アプリケーションをデバッグするには、アプリを配置したコンピューターにリモートツールをインストールして実行し、Visual Studio から実行中のアプリにアタッチします。

![リモートデバッガーコンポーネント](../debugger/media/remote-debugger-aspnet.png "Remote_debugger_components")

このガイドでは、Visual Studio ASP.NET Core のセットアップと構成、IIS への配置、および Visual Studio からのリモートデバッガーのアタッチを行う方法について説明します。 ASP.NET 4.5.2 のリモートデバッグについては、「 [IIS コンピューター上のリモートデバッグ ASP.NET](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md)」を参照してください。 Azure を使用して、IIS でデプロイおよびデバッグすることもできます。 Azure App Service の場合、[スナップショットデバッガー](../debugger/debug-live-azure-applications.md)を使用するか、[サーバーエクスプローラーからデバッガーをアタッチ](../debugger/remote-debugging-azure.md)することによって、IIS とリモートデバッガーの事前構成済みインスタンスに配置およびデバッグを簡単に行うことができます。

## <a name="prerequisites"></a>前提条件

::: moniker range=">=vs-2019"
この記事に記載されている手順を実行するには、Visual Studio 2019 が必要です。
::: moniker-end
::: moniker range="vs-2017"
この記事に記載されている手順を実行するには、Visual Studio 2017 が必要です。
::: moniker-end

これらの手順は、次のサーバー構成でテストされています。
* Windows Server 2012 R2 および IIS 8
* Windows Server 2016 および IIS 10

## <a name="network-requirements"></a>ネットワークの要件

プロキシ経由で接続されている2台のコンピューター間のデバッグはサポートされていません。 高待機時間または低帯域幅の接続 (ダイヤルアップインターネット、または複数の国にまたがるインターネットなど) でのデバッグは推奨されておらず、失敗したり、非常に時間がかかる場合があります。 要件の完全な一覧については、「[要件](../debugger/remote-debugging.md#requirements_msvsmon)」を参照してください。

## <a name="app-already-running-in-iis"></a>アプリは既に IIS で実行されていますか?

この記事では、Windows server で IIS の基本的な構成を設定し、Visual Studio からアプリをデプロイする手順について説明します。 これらの手順は、サーバーに必要なコンポーネントがインストールされていること、アプリが正常に実行できること、およびリモートデバッグの準備ができていることを確認するために含まれています。

* アプリが IIS で実行されていて、リモートデバッガーをダウンロードしてデバッグを開始するだけの場合は、「 [Windows Server でのリモートツールのダウンロードとインストール](#BKMK_msvsmon)」を参照してください。

* アプリケーションをデバッグできるように IIS で正しくセットアップ、展開、および実行するためのヘルプが必要な場合は、このトピックのすべての手順に従ってください。

## <a name="create-the-aspnet-core-application-on-the-visual-studio-computer"></a>Visual Studio コンピューターで ASP.NET Core アプリケーションを作成する

1. 新しい ASP.NET Core Web アプリケーションを作成します。 

    ::: moniker range=">=vs-2019"
    Visual Studio 2019 で、 **Ctrl キーを押しながら Q キーを押し**て検索ボックスを開き、「 **asp.net**」と入力します。次に、[**テンプレート**] を選択し、[**新しい ASP.NET Core Web アプリケーションの作成**] を選択します。 表示されるダイアログボックスで、プロジェクトに**MyASPApp**という名前を指定し、[**作成**] を選択します。 次に、[ **Web アプリケーション (モデルビューコントローラー)**] を選択し、[**作成**] を選択します。
    ::: moniker-end
    ::: moniker range="vs-2017"
    Visual Studio 2017 で、[**ファイル > 新しい > プロジェクト**] を選択し、[ **Visual C# > Web > ASP.NET Core web アプリケーション**] を選択します。 [ASP.NET Core テンプレート] セクションで、[ **Web アプリケーション (モデルビューコントローラー)**] を選択します。 ASP.NET Core 2.1 が選択され、[ **Docker サポートを有効に**する] が選択されておらず、**認証**が [**認証なし**] に設定されていることを確認します。 プロジェクトに**MyASPApp**という名前を指定します。
    ::: moniker-end

4. About.cshtml.cs ファイルを開き、 `OnGet`メソッドにブレークポイントを設定します (以前のテンプレートでは、代わりに HomeController.cs を開き、 `About()`メソッドにブレークポイントを設定します)。

## <a name="install-and-configure-iis-on-windows-server"></a><a name="bkmk_configureIIS"></a>Windows Server に IIS をインストールして構成する

[!INCLUDE [remote-debugger-install-iis-role](../debugger/includes/remote-debugger-install-iis-role.md)]

## <a name="update-browser-security-settings-on-windows-server"></a>Windows Server でブラウザーのセキュリティ設定を更新する

Internet Explorer で [セキュリティ強化の構成] が有効になっている場合 (既定では有効になっています)、一部のドメインを信頼済みサイトとして追加して、一部の web サーバーコンポーネントをダウンロードできるようにする必要があります。 信頼済みサイトを追加するには、[**インターネットオプション] > [セキュリティ > 信頼済みサイト > サイト**] の順に移動します。 次のドメインを追加します。

- microsoft.com
- go.microsoft.com
- download.microsoft.com
- iis.net

ソフトウェアをダウンロードするときに、さまざまな web サイトのスクリプトとリソースを読み込むためのアクセス許可を付与するように求められる場合があります。 これらのリソースの一部は必須ではありませんが、プロセスを簡略化するために、メッセージが表示されたら [**追加**] をクリックします。

## <a name="install-aspnet-core-on-windows-server"></a>Windows Server に ASP.NET Core をインストールする

1. ホスティング システムに [.NET Core Windows Server ホスティング](https://aka.ms/dotnetcore-2-windowshosting) バンドルをインストールします。 このバンドルをインストールすることで、.NET Core ランタイム、.NET Core ライブラリ、ASP.NET Core モジュールがインストールされます。 詳細な手順については、「 [IIS への発行](/aspnet/core/publishing/iis?tabs=aspnetcore2x#iis-configuration)」を参照してください。

    > [!NOTE]
    > システムにインターネット接続が設定されていない場合は、.NET Core Windows Server ホスティング バンドルをインストールする前に、*[Microsoft Visual C++ 2015 再頒布可能パッケージ](https://www.microsoft.com/download/details.aspx?id=53840)* を入手してインストールしてください。

3. システムを再起動します (または、コマンドプロンプトから net **stop was/y**の後に**net start w3svc**を実行して、システムパスへの変更を取得します)。

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

1. [**設定**] ダイアログボックスで、[**次へ**] をクリックしてデバッグを有効にし、**デバッグ**構成を選択します。次に、[**ファイルの発行**] オプションで、[**変換先の追加ファイルを削除**する] を選択します。

    > [!NOTE]
    > リリース構成を選択した場合は、発行時に*web.config ファイルで*デバッグを無効にします。

1. [**保存**] をクリックし、アプリを再発行します。

## <a name="optional-deploy-by-publishing-to-a-local-folder"></a>Optionalローカルフォルダーへの発行による配置

PowerShell または RoboCopy を使用してアプリを IIS にコピーする場合、または手動でファイルをコピーする場合は、このオプションを使用してアプリをデプロイできます。

### <a name="configure-the-aspnet-core-web-site-on-the-windows-server-computer"></a><a name="BKMK_deploy_asp_net"></a>Windows Server コンピューターで ASP.NET Core Web サイトを構成する

1. エクスプローラーを開き、新しいフォルダー **C:\ Publish**を作成します。このフォルダーには、後で ASP.NET Core プロジェクトを配置します。

2. まだ開いていない場合は、**インターネットインフォメーションサービス (IIS) マネージャー**を開きます。 (サーバーマネージャーの左側のウィンドウで、[ **IIS**] を選択します。 サーバーを右クリックして **[インターネット インフォメーション サービス (IIS) マネージャー]** を選択します。)

3. 左側のウィンドウの [**接続**] で、[**サイト**] に移動します。

4. [**既定の Web サイト**] を選択し、[**基本設定**] を選択して、**物理パス**を**c:\ Publish**に設定します。

4. **[既定の Web サイト]** ノードを右クリックして、 **[アプリケーションの追加]** を選択します。

5. [**エイリアス**] フィールドを**MyASPApp**に設定し、既定のアプリケーションプール (**DefaultAppPool**) をそのまま使用して、**物理パス**を**c:\ Publish**に設定します。

6. [**接続**] で [**アプリケーションプール**] を選択します。 **DefaultAppPool**を開き、[アプリケーションプール] フィールドを [**マネージコードなし**] に設定します。

7. IIS マネージャーで新しいサイトを右クリックし、[**アクセス許可の編集**] を選択し、IUSR、IIS_IUSRS、または web アプリへのアクセス用に構成されているユーザーが、Read & Execute 権限を持つ承認されたユーザーであることを確認します。

    これらのユーザーのいずれかがアクセスできない場合は、「Read & Execute 権限を持つユーザーとして IUSR を追加する手順」を参照してください。

### <a name="publish-and-deploy-the-app-by-publishing-to-a-local-folder-from-visual-studio"></a>Visual Studio からローカルフォルダーに発行してアプリを発行してデプロイする

また、ファイルシステムまたはその他のツールを使用して、アプリを発行してデプロイすることもできます。

[!INCLUDE [remote-debugger-deploy-app-local](../debugger/includes/remote-debugger-deploy-app-local.md)]

## <a name="download-and-install-the-remote-tools-on-windows-server"></a><a name="BKMK_msvsmon"></a>Windows Server でのリモートツールのダウンロードとインストール

使用している Visual Studio のバージョンに対応するバージョンのリモートツールをダウンロードします。

[!INCLUDE [remote-debugger-download](../debugger/includes/remote-debugger-download.md)]

## <a name="set-up-the-remote-debugger-on-windows-server"></a><a name="BKMK_setup"></a>Windows Server でリモートデバッガーを設定する

[!INCLUDE [remote-debugger-configuration](../debugger/includes/remote-debugger-configuration.md)]

> [!NOTE]
> 追加のユーザーにアクセス許可を追加する必要がある場合、リモートデバッガーの認証モードまたはポート番号を変更するには、「[リモートデバッガーの構成](../debugger/remote-debugging.md#configure_msvsmon)」を参照してください。

リモートデバッガーをサービスとして実行する方法の詳細については、「[サービスとしてのリモートデバッガーの実行](../debugger/remote-debugging.md#bkmk_configureService)」を参照してください。

## <a name="attach-to-the-aspnet-application-from-the-visual-studio-computer"></a><a name="BKMK_attach"></a>Visual Studio コンピューターから ASP.NET アプリケーションにアタッチする

1. Visual Studio コンピューターで、デバッグしようとしているソリューション (この記事のすべての手順を実行している場合は**MyASPApp** ) を開きます。
2. Visual Studio で、[**デバッグ > [プロセスにアタッチ**] をクリックします (Ctrl + Alt + P)。

    > [!TIP]
    > Visual Studio 2017 以降のバージョンでは、[**デバッグ > [プロセスに再アタッチ**] (Shift + Alt + P) を使用して、以前にアタッチしたのと同じプロセスに再アタッチできます。

3. [修飾子] フィールドを [ ** \<リモートコンピューター名>** に設定し、 **enter**キーを押します。

    Visual Studio によって、必要なポートがコンピューター名に追加されていることを確認します。これは、 ** \<リモートコンピューター名>:p ort の形式で表示されます。**

    ::: moniker range=">=vs-2019"
    Visual Studio 2019 では、 ** \<リモートコンピューター名>: 4024 が表示されるはずです。**
    ::: moniker-end
    ::: moniker range="vs-2017"
    Visual Studio 2017 では、 ** \<リモートコンピューター名>: 4022 が表示されるはずです。**
    ::: moniker-end
    ポートが必要です。 ポート番号が表示されない場合は、手動で追加します。

4. **[最新の情報に更新]** をクリックします。
    **[選択可能なプロセス]** ウィンドウにプロセスがいくつか表示されます。

    プロセスが表示されない場合は、リモートコンピューター名ではなく IP アドレスを使用してください (ポートが必要です)。 をコマンドライン`ipconfig`で使用して、IPv4 アドレスを取得することができます。

    [**検索**] ボタンを使用する場合は、サーバーで[UDP ポート3702を開く](#bkmk_openports)必要がある場合があります。

5. **[すべてのユーザーからのプロセスを表示する]** をオンにします。

6. アプリケーションをすばやく検索するには、プロセス名の最初の文字を入力します。

    * が IIS で[インプロセスホスティングモデル](/aspnet/core/host-and-deploy/aspnet-core-module?view=aspnetcore-3.1#hosting-models)を使用している場合は、適切な w3wp.exe プロセスを選択**します。** .NET Core 3 以降では、これが既定値です。

    * それ以外の場合は、 **dotnet**プロセスを選択します。 (これはアウトプロセスホスティングモデルです)。

    W3wp.exe または*dotnet*を表示しているプロセスが複数ある*場合は、* [**ユーザー名**] 列を確認します。 場合によっては、[**ユーザー名**] 列に、 **IIS APPPOOL\DefaultAppPool**などのアプリケーションプール名が表示されます。 アプリケーションプールが表示されていても一意ではない場合は、デバッグするアプリインスタンスの新しい名前付きアプリプールを作成し、[**ユーザー名**] 列で簡単に見つけることができます。

    ::: moniker range=">=vs-2019"
    ![RemoteDBG_AttachToProcess](../debugger/media/vs-2019/remotedbg-attachtoprocess-aspnetcore.png "RemoteDBG_AttachToProcess")
    ::: moniker-end
    ::: moniker range="vs-2017"
    ![RemoteDBG_AttachToProcess](../debugger/media/remotedbg-attachtoprocess-aspnetcore.png "RemoteDBG_AttachToProcess")
    ::: moniker-end

7. **[アタッチ]** をクリックします。

8. リモート コンピューターの Web サイトを開きます。 ブラウザーで、**http://\<リモート コンピューター名>** に移動します。

    ASP.NET の Web ページが表示されるはずです。

9. 実行中の ASP.NET アプリケーションで、[**バージョン情報**] ページへのリンクをクリックします。

    Visual Studio で、ブレークポイントにヒットするはずです。

## <a name="troubleshooting-open-required-ports-on-windows-server"></a><a name="bkmk_openports"></a> トラブルシューティングWindows Server で必要なポートを開く

ほとんどのセットアップでは、ASP.NET とリモートデバッガーのインストールによって必要なポートが開かれます。 ただし、ポートが開いていることを確認する必要がある場合もあります。

> [!NOTE]
> Azure VM では、[ネットワークセキュリティグループ](/azure/virtual-machines/windows/nsg-quickstart-portal)を介してポートを開く必要があります。

必要なポート:

* 80-IIS で必要
::: moniker range=">=vs-2019"
* 4024-Visual Studio 2019 からのリモートデバッグに必要です (詳細については、「[リモートデバッガーのポートの割り当て](../debugger/remote-debugger-port-assignments.md)」を参照してください)。
::: moniker-end
::: moniker range="vs-2017"
* 4022-Visual Studio 2017 からのリモートデバッグに必要です (詳細については、「[リモートデバッガーのポートの割り当て](../debugger/remote-debugger-port-assignments.md)」を参照してください)。
::: moniker-end
* UDP 3702-(省略可能) 探索ポートを使用すると、Visual Studio でリモートデバッガーにアタッチするときに [**検索**] ボタンを使用できます。

1. Windows Server でポートを開くには、[**スタート**] メニューを開き、 **[セキュリティが強化された windows ファイアウォール**] を検索します。

2. 次に、[**受信の規則] > 新しい規則 > ポート**] を選択し、[**次へ**] をクリックします。 (UDP 3702 の場合は、代わりに [**送信の規則**] を選択します)。

3. [**特定のローカルポート**] で、ポート番号を入力し、[**次へ**] をクリックします。

4. [**接続を許可する**] をクリックし、[**次へ**] をクリックします。

5. ポートに対して有効にする1つまたは複数のネットワークの種類を選択し、[**次へ**] をクリックします。

    選ぶ種類には、リモート コンピューターが接続しているネットワークが含まれている必要があります。
6. 受信規則に名前 ( **IIS**、 **Web 配置**、 **msvsmon**など) を追加し、[**完了**] をクリックします。

    [受信の規則] または [送信の規則] の一覧に新しい規則が表示されます。

    Windows ファイアウォールの構成の詳細については、「 [Windows ファイアウォールをリモートデバッグ用に構成](../debugger/configure-the-windows-firewall-for-remote-debugging.md)する」を参照してください。

3. その他の必要なポートに対して追加のルールを作成します。
