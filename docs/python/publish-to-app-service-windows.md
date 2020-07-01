---
title: Windows 上の Azure App Service への Python アプリの発行
description: web.config ファイルに必要な内容など、Visual Studio から Windows 上の Azure App Service に直接 Python Web アプリケーションを発行する方法を説明します。
ms.date: 01/07/2019
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
- azure
ms.openlocfilehash: 649d40a3b95f9e3d4df51cc4ab22a3fb79ac1498
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85531847"
---
# <a name="publishing-to-azure-app-service-on-windows"></a>Windows 上の Azure App Service への発行

> [!Note]
> このコンテンツと記載されている機能は非推奨ですが、引き続き機能します。 Python 開発者は、可能な場合には、[Linux 上の App Service](publishing-python-web-applications-to-azure-from-visual-studio.md) に移行することをお勧めします。

Visual Studio には、Windows 上の Azure App Service に Python Web アプリを発行する機能が用意されています。 Windows 上の Azure App Service に発行することは、サーバーに必要なファイルをコピーし、アプリの起動方法を Web サーバーに指示する適切な `web.config` ファイルを設定することを意味します。

発行プロセスは、Visual Studio 2017 以降と Visual Studio 2015 では異なります。 具体的には、Visual Studio 2015 は `web.config` の作成などの一部の操作を自動化しますが、この自動化により、長期的な柔軟性と制御が制限されます。 Visual Studio 2017 以降では、より多くの手動操作を必要としますが、ご利用の Python 環境をより厳密に制御することができます。 ここでは、両方のオプションについて説明します。

> [!Note]
> Visual Studio 2015 と Visual Studio 2017 以降の間の変更の詳細については、ブログ記事「[Publish to Azure in Visual Studio 2017](https://devblogs.microsoft.com/python/publish-to-azure-in-vs-2017/)」 (Visual Studio 2017 での Azure への発行) を参照してください。

## <a name="prerequisites"></a>必須コンポーネント

このチュートリアルでは、Bottle、Flask、または Django のいずれかのフレームワークに基づく Web アプリ プロジェクトが必要になります。 プロジェクトがまだなく、発行プロセスを試してみたい場合は、次の手順に従って簡単なテスト プロジェクトを作成します。

1. Visual Studio で、 **[ファイル] > [新規] > [プロジェクト]** の順に選び、"Bottle" を検索して、 **[Bottle Web プロジェクト]** を選び、プロジェクトの名前とパスを指定し、 **[OK]** をクリックします (Bottle テンプレートは、Python 開発ワークロードに含まれています。[インストール](installing-python-support-in-visual-studio.md)のページを参照してください)。

1. 指示に従って外部パッケージをインストールします。 **[仮想環境にインストール]** と仮想環境の優先ベース インタープリターを選択します。 通常、これは App Service にインストールされている Python のバージョンと一致するものを選択します。

1. F5 キーを押すか、 **[デバッグ] > [デバッグの開始]** を選択して、プロジェクトをローカルでテストします。

## <a name="create-an-azure-app-service"></a>Azure App Service の作成

Azure への発行には、ターゲット App Service が必要です。 この目的のため、Azure サブスクリプションを使用して App Service を作成するか、一時的なサイトを使用することができます。

サブスクリプションがまだない場合は、[無料の完全な Azure アカウント](https://azure.microsoft.com/free/)から始めます。これには、Azure サービスのクレジットが含まれます。 [Visual Studio Dev Essentials](https://azure.microsoft.com/pricing/member-offers/vs-dev-essentials/) へのサインアップも検討してください。1 年間、毎月 25 ドルのクレジットが提供されます。

> [!Tip]
> アカウントの確認のため Azure からクレジット カードの入力を求められますが、カードに請求されることはありません。 無料クレジットと同じ[使用制限](/azure/billing/billing-spending-limit)を設定して、追加料金が発生しないようにすることもできます。 さらに、Azure では Free レベルの App Service プランを提供しており、次のセクションで説明されているような簡単なテスト アプリに最適です。

### <a name="using-a-subscription"></a>サブスクリプションの使用

アクティブな Azure サブスクリプションを使用して、次のように空の Web アプリがある App Service を作成します。

1. [portal.azure.com](https://portal.azure.com) でサインインします。
1. **[+新規]** を選択してから、 **[Web + モバイル]** 、 **[Web アプリ]** の順に選択します。
1. Web アプリの名前を指定し、 **[リソース グループ]** は "新規作成" のままにして、オペレーティング システムに **[Windows]** を選択します。
1. **[App Service プラン/場所]** を選択し、 **[新規作成]** を選択して名前と場所を指定します。 次に、 **[価格レベル]** を選択し、下にスクロールして **[F1 Free]** プランを選択し、 **[選択]** 、 **[OK]** 、 **[作成]** の順に押します。
1. (省略可能) App Service が作成されたら、それに移動し、 **[発行プロファイルの取得]** を選択し、ファイルをローカルに保存します。

### <a name="using-a-temporary-app-service"></a>一時的な App Service の使用

次の手順に従い、Azure サブスクリプションなしで一時的な App Service を作成します。

1. ブラウザーで [https://azure.microsoft.com/try/app-service/web/](https://azure.microsoft.com/try/app-service/web/) を開きます。
1. アプリの種類で **[Web App]** を選び、 **[次へ]** を選びます。
1. **[Empty Site]\(空のサイト\)** 、 **[作成]** の順に選択します。
1. 任意のソーシャル ログインを使ってサインインし、しばらくすると、表示される URL でサイトの準備ができます。
1. **[発行プロファイルのダウンロード]** を選び、`.publishsettings` ファイルを保存します。後でこのファイルを使います。

## <a name="configure-python-on-azure-app-service"></a>Azure App Service での Python の構成

空の Web アプリを持つ App Service を (サブスクリプションまたは無料サイトのいずれかで) 実行したら、「[Azure App Service での Python の管理](managing-python-on-azure-app-service.md)」の説明に従って、選択した Python のバージョンをインストールします。 Visual Studio 2017 以降から発行するには、その記事の説明に従って、サイトの拡張機能と共にインストールされた Python インタープリターへの正確なパスを記録します。

必要に応じて、これらの指示のプロセスを使用して、`bottle` パッケージもインストールできます。これはそのパッケージがこのチュートリアルの他のステップの一部としてインストールされるからです。

## <a name="publish-to-app-service---visual-studio-2017-and-later"></a>App Service への発行 - Visual Studio 2017 以降

Visual Studio 2017 以降から Azure App Service に発行すると、プロジェクト内のファイルのみがサーバーにコピーされます。 したがって、必要なファイルを作成して、サーバー環境を構成する必要があります。

1. Visual Studio の**ソリューション エクスプローラー**で、プロジェクトを右クリックし、 **[追加]、[新しい項目]** の順に選択します。表示されるダイアログ ボックスで、[Azure web.config (Fast CGI)] テンプレートを選択し、[OK] を選択します。 これによりプロジェクト ルートに `web.config` ファイルが作成されます。

1. `web.config` の `PythonHandler` エントリを変更して、パスがサーバー上の Python インストールと一致するようにします (詳細については、[IIS 構成リファレンス](https://www.iis.net/configreference) (iis.net) に関するページを参照してください)。 たとえば、Python 3.6.1 x64 の場合、エントリは次のように表示されます。

    ```xml
    <system.webServer>
      <handlers>
        <add name="PythonHandler" path="*" verb="*" modules="FastCgiModule"
            scriptProcessor="D:\home\Python361x64\python.exe|D:\home\Python361x64\wfastcgi.py"
            resourceType="Unspecified" requireAccess="Script"/>
      </handlers>
    </system.webServer>
    ```

1. `web.config` の `WSGI_HANDLER` エントリを、使用しているフレームワークに合わせて適切に設定します。

    - **Bottle**: 次のように、`app.wsgi_app` の後にかっこを追加します。 これが必要なのは、そのオブジェクトが変数ではなく関数 (`app.py` を参照) であるためです。

        ```xml
        <!-- Bottle apps only -->
        <add key="WSGI_HANDLER" value="app.wsgi_app()"/>
        ```

    - **Flask**:`WSGI_HANDLER` 値を `<project_name>.app` に変更します。`<project_name>` はプロジェクトの名前に一致します。 `runserver.py` の `from <project_name> import app` ステートメントを見ると、正確な識別子が見つかります。 たとえば、プロジェクトの名前が "FlaskAzurePublishExample" の場合、エントリは次のように表示されます。

        ```xml
        <!-- Flask apps only: change the project name to match your app -->
        <add key="WSGI_HANDLER" value="FlaskAzurePublishExample.app"/>
        ```

    - **Django**:Django プロジェクトの `web.config` には 2 つの変更が必要です。 最初に、`WSGI_HANDLER` 値を `django.core.wsgi.get_wsgi_application()` に変更します (オブジェクトは `wsgi.py` ファイル内にあります)。

        ```xml
        <!-- Django apps only -->
        <add key="WSGI_HANDLER" value="django.core.wsgi.get_wsgi_application()"/>
        ```

        次に、下のエントリを、`DjangoAzurePublishExample` を自分のプロジェクトの名前と置き換えて、`WSGI_HANDLER` に追加します。

        ```xml
        <add key="DJANGO_SETTINGS_MODULE" value="DjangoAzurePublishExample.settings" />
        ```

1. **Django アプリのみ**:Django プロジェクトの `settings.py` ファイルで、次に示すように、'vspython-test-02.azurewebsites.net' を自分の URL と置き換えて、サイト URL ドメインを `ALLOWED_HOSTS` に追加します。

    ```python
    # Change the URL to your specific site
    ALLOWED_HOSTS = ['vspython-test-02.azurewebsites.net']
    ```

    配列への URL の追加が失敗すると、次のエラーが発生します。"DisallowedHost at / Invalid HTTP_HOST header: '\<site URL\>'. You may need to add '\<site URL\>' to ALLOWED_HOSTS." (DisallowedHost / 無効な HTTP_HOST ヘッダー: <サイト URL>。必要に応じて ALLOWED_HOSTS に '<サイト URL>' を追加してください。)

    配列が空の場合、Django は自動的に 'localhost' を許可しますが、実稼働環境の URL を追加するとその機能は削除されます。 このため、`settings.py` の開発用のコピーと実稼働環境用のコピーを別々に管理するか、環境変数を使用して実行時の値を制御することをお勧めします。

1. **ソリューション エクスプローラー**で、プロジェクトと同じ名前が付いたフォルダーを展開し、`static` フォルダーを右クリックし、 **[追加] > [新しい項目]** を選択し、"Azure 静的ファイルの web.config" テンプレートを選択し、 **[OK]** を選択します。 この操作により `static` フォルダー内に別の `web.config` が作成され、そのフォルダーの Python 処理を無効にします。 この構成は、Python アプリケーションを使用せずに、静的ファイルの要求を既定の Web サーバーに送信します。

1. プロジェクトを保存し、Visual Studio の**ソリューション エクスプローラー**で、プロジェクトを右クリックし、 **[発行]** を選択します。

    ![プロジェクトのコンテキスト メニューの [発行] コマンド](media/template-web-publish-command.png)

1. 表示された **[発行]** タブで、発行先のターゲットを選択します。

    a. Azure サブスクリプション: **[Microsoft Azure App Service]** を選択し、 **[既存のものを選択]** 、 **[発行]** の順に選択します。 表示されたダイアログで、適切なサブスクリプションと App Service を選択できます。 App Service が表示されない場合は、次に説明されているように、一時的な App Service のダウンロードした発行プロファイルを使用します。

    ![Azure への発行手順 1、Visual Studio 2017 以降、既存のサブスクリプション](media/tutorials-common-publish-1a-2017.png)

    b. try.azurewebsites.net で一時的な App Service を使用している場合、または発行プロファイルを使用する必要がある場合は、 **>** コントロールを選択して **[プロファイルのインポート]** を見つけてそのオプションを選択し、 **[発行]** を選択します。 これにより、以前にダウンロードした `.publishsettings` ファイルの場所の入力が求められます。

    ![Azure への発行手順 1、Visual Studio 2017 以降、一時的なアプリ サービス](media/tutorials-common-publish-1b-2017.png)

1. Visual Studio で、[Web 発行アクティビティ] ウィンドウと [発行] ウィンドウに発行ステータスが表示されます。 発行が完了すると、サイト URL で既定のブラウザーが開きます。 URL は、[発行] ウィンドウにも表示されます。

1. ブラウザーが開いたときに、"内部サーバー エラーが発生したため、ページを表示できません。" というメッセージが表示される場合があります。 このメッセージは、サーバー上の Python 環境が完全に構成されていないことを示しています。その場合、次の手順を実行します。

    a. もう一度「[Azure App Service での Python の管理](managing-python-on-azure-app-service.md)」を参照して、適切な Python サイト拡張機能がインストールされていることを確認します。

    b. `web.config` ファイル内の Python インタープリターへのパスを再確認します。 パスは、選択したサイト拡張機能のインストール場所と完全に一致している必要があります。

    c. Kudu コンソールを使用してアプリの `requirements.txt` ファイルに一覧表示されている任意のパッケージをアップグレードする: `web.config` で使用されているのと同じ Python フォルダー (`/home/python361x64` など) に移動し、[Kudu コンソール](managing-python-on-azure-app-service.md#azure-app-service-kudu-console)のセクションの説明に従って、次のコマンドを実行します。

    ```command
    python -m pip install --upgrade -r /home/site/wwwroot/requirements.txt
    ```

    このコマンドの実行時にアクセス許可エラーが発生する場合は、コマンドを App Service の既定の Python インストールのいずれかのフォルダー*ではなく*、サイト拡張機能のフォルダーで実行していることを再確認します。 これらの既定の環境を変更することはできないため、パッケージをインストールしようとすると確実に失敗します。

    d. より詳細なエラー出力を得るため、次の行を `<system.webServer>` ノード内の `web.config` に追加します。

    ```xml
    <httpErrors errorMode="Detailed"></httpErrors>
    ```

    e. 新しいパッケージをインストールした後、App Service の再起動を試します。 `web.config` を変更するときには再起動は不要です。`web.config` が変更されるたびに、App Service により自動で再起動が行われます。

    > [!Tip]
    > アプリの `requirements.txt` ファイルに変更を加えた場合、必ずもう一度 Kudu コンソールを使用して、そのファイルに一覧表示されている任意のパッケージをインストールしてください。

1. サーバー環境を完全に構成したら、ブラウザーでページを更新すると、Web アプリが表示されます。

    ![App Service への Bottle、Flask、および Django アプリの発行結果](media/azure-publish-results.png)

## <a name="publishing-to-app-service---visual-studio-2015"></a>App Service への発行 - Visual Studio 2015

> [!Note]
> このプロセスの短いビデオについては、「[Visual Studio Python tutorial: Building a website](https://www.youtube.com/watch?v=FJx5mutt1uk&list=PLReL099Y5nRdLgGAdrb_YeTdEnd23s6Ff&index=6)」 (Visual Studio Python チュートリアル: Web サイトの構築) (youtube.com、3 分 10 秒) をご覧ください。

1. **ソリューション エクスプローラー**で、プロジェクトを右クリックして、 **[発行]** を選びます。

1. **[発行]** ダイアログで、 **[Microsoft Azure App Service]** を選びます。

  ![Azure 発行手順 1](media/tutorials-common-publish-1.png)

1. ターゲットを選びます。

    - Azure サブスクリプションがある場合は、発行先として **[Microsoft Azure App Service]** を選び、次のダイアログで、既存の App Service を選ぶか、 **[新規]** を選んで新しく作成します。
    - try.azurewebsites.net から一時的なサイトを使っている場合は、発行先として **[インポート]** を選び、サイトからダウンロードした `.publishsettings` ファイルを参照して、 **[OK]** を選びます。

1. App Service の詳細が、 **[発行]** ダイアログの **[接続]** タブに表示されます (下図参照)。

  ![Azure 発行手順 2](media/tutorials-common-publish-2.png)

1. 必要に応じて、 **[次へ >]** を選んで追加設定を確認します。

1. **[発行]** を選びます。 アプリケーションが Azure に配置されると、そのサイトで既定のブラウザーが開きます。

このプロセスの一環として、Visual Studio は次のステップも実行します。

- アプリの `wsgi_app` 関数と App Service の既定の Python 3.4 インタープリターへの適切なポインターを格納する `web.config` ファイルをサーバー上に作成します。
- プロジェクトの `static` フォルダー内のファイルの処理をオフにします (このルールは `web.config` にあります)。
- 仮想環境をサーバーに発行します。
- `web.debug.config` ファイルとデバッグ ツールを追加して、リモート デバッグを有効にします。 Visual Studio 2019 バージョン 16.4 以前の場合、デバッグ ツールは ptvsd です。 Visual Studio 2019 バージョン 16.5 以降の場合、デバッグ ツールは debugpy です。

前述したとおり、これらの自動ステップは発行プロセスを簡素化しますが、Python 環境の制御がより難しくなります。 たとえば、`web.config` ファイルはサーバーにのみ作成され、プロジェクトには追加されません。 発行プロセスは、サーバーの構成に依存するのではなく、開発用コンピューターから仮想環境全体をコピーするため、時間がかかります。

最終的に自分の `web.config` ファイルを保持して、`requirements.txt` を使用してパッケージをサーバー上で直接保持できます。 具体的には、`requirements.txt` を使用することで、開発環境とサーバー環境が常に一致することが保証されます。
