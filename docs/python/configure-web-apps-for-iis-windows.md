---
title: IIS 用に Python Web アプリを構築する
description: Windows 仮想マシンから IIS を使用して実行される Python Web アプリを構築する方法を説明します。
ms.date: 12/06/2018
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
- azure
ms.openlocfilehash: 3c756f3d9a89294ecce054650037be3f7b26c291
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85540934"
---
# <a name="configure-python-web-apps-for-iis"></a>IIS 用に Python Web アプリを構築する

IIS を ([Azure 上の Windows 仮想マシンを含む](/azure/architecture/reference-architectures/n-tier/windows-vm)) Windows コンピューター上の Web サーバーとして使用する場合、IIS が Python のコードを正常に処理できるよう、Python アプリの *web.config* ファイルに特定の設定が含まれている必要があります。 コンピューター自体にも、Web アプリが必要とするすべてのパッケージと共に、Python がインストールされている必要があります。

> [!Note]
> 以前、この記事には Windows 上の Azure App Service に Python を構成するガイダンスが含まれていました。 そのシナリオで使用された Python の拡張機能と Windows のホストは、非推奨となり、Linux 上の Azure App Service が選ばれました。 詳細については、[Azure App Service への Python アプリの発行 (Linux)](publishing-python-web-applications-to-azure-from-visual-studio.md) に関するページを参照してください。 ただし、前の記事は、[Python の拡張機能を使用した Windows での App Service の管理](managing-python-on-azure-app-service.md)に関するページで引き続きお読みいただくことができます。

## <a name="install-python-on-windows"></a>Windows に Python をインストールする

Web アプリを実行する場合、「[Python インタープリターのインストール](installing-python-interpreters.md)」の説明に従って、Python の必要なバージョンを直接 Windows ホスト マシンにインストールします。

後の手順用に `python.exe` インタープリターの場所を記録します。 便宜上、その場所は PATH 環境変数に追加できます。

## <a name="install-packages"></a>パッケージのインストール

専用のホストを使用している場合、アプリの実行場所として、仮想環境ではなく、グローバルな Python 環境を使用します。 そのようにすると、コマンド プロンプトから単純に `pip install -r requirements.txt` を実行することにより、アプリの要件をすべてグローバル環境にインストールできます。

## <a name="set-webconfig-to-point-to-the-python-interpreter"></a>Python インタープリターをポイントする web.config の設定

ご使用のアプリの *web.config* ファイルは、HttpPlatform (推奨) または FastCGI のいずれかを使用して Python 要求を処理する方法を、Windows 上で実行される IIS (7 以降) の Web サーバーに指示します。 Visual Studio 2015 以前のバージョンでは、これらの変更は自動的に行われます。 Visual Studio 2017 以降を使用する場合、*web.config* は手動で変更する必要があります。

### <a name="configure-the-httpplatform-handler"></a>Httpplatform のハンドラーの構成

HttpPlatform モジュールは、スタンドアロンの Python プロセスに直接ソケット接続を渡します。 このパススルーにより、任意の Web サーバーを実行することができますが、ローカル Web サーバーを実行するスタートアップ スクリプトが必要になります。 スクリプトは、*web.config* の `<httpPlatform>` 要素で指定します。ここで、`processPath` 属性はサイト拡張機能の Python インタープリターをポイントし、`arguments` 属性はスクリプトと指定する任意の引数をポイントします。

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.webServer>
    <handlers>
      <add name="PythonHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified"/>
    </handlers>
    <httpPlatform processPath="c:\python36-32\python.exe"
                  arguments="c:\home\site\wwwroot\runserver.py --port %HTTP_PLATFORM_PORT%"
                  stdoutLogEnabled="true"
                  stdoutLogFile="c:\home\LogFiles\python.log"
                  startupTimeLimit="60"
                  processesPerApplication="16">
      <environmentVariables>
        <environmentVariable name="SERVER_PORT" value="%HTTP_PLATFORM_PORT%" />
      </environmentVariables>
    </httpPlatform>
  </system.webServer>
</configuration>
```

ここの `HTTP_PLATFORM_PORT` 環境変数には、ローカル サーバーが localhost からの接続をリッスンするポートが含まれています。 この例では、必要に応じて、別の環境変数 (この場合は `SERVER_PORT`) を作成する方法も示しています。

### <a name="configure-the-fastcgi-handler"></a>FastCGI ハンドラーの構成

FastCGI は、要求レベルで動作するインターフェイスです。 IIS は、受信接続を受信し、各要求を 1 つ以上の永続的な Python プロセスで実行されている WSGI アプリへ転送します。

これを使用するには、[pypi.org/project/wfastcgi/](https://pypi.io/project/wfastcgi) で説明しているとおり、wfastcgi パッケージを最初にインストールして構成します。

次いでアプリの *web.config* ファイルを変更して、*python.exe* と *wfastcgi.py* への完全なパスが `PythonHandler` キーに含まれるようにします。 以下の手順では、Python は *c:\python36-32* にインストールされ、ご使用のアプリのコードは *c:\home\site\wwwroot* にあると想定されています (ご自分のパスに置き換えてください)。

1. *web.config* の `PythonHandler` エントリを変更して、パスが Python のインストール場所と一致するようにします (詳細については、[IIS 構成リファレンス](https://www.iis.net/configreference) (iis.net) に関するページを参照)。

    ```xml
    <system.webServer>
      <handlers>
        <add name="PythonHandler" path="*" verb="*" modules="FastCgiModule"
            scriptProcessor="c:\python36-32\python.exe|c:\python36-32\wfastcgi.py"
            resourceType="Unspecified" requireAccess="Script"/>
      </handlers>
    </system.webServer>
    ```

1. *web.config* の `<appSettings>` に、`WSGI_HANDLER`、`WSGI_LOG` (オプション)、および `PYTHONPATH` のキーを追加します。

    ```xml
    <appSettings>
      <add key="PYTHONPATH" value="c:\home\site\wwwroot"/>
      <!-- The handler here is specific to Bottle; see the next section. -->
      <add key="WSGI_HANDLER" value="app.wsgi_app()"/>
      <add key="WSGI_LOG" value="c:\home\LogFiles\wfastcgi.log"/>
    </appSettings>
    ```

    これらの `<appSettings>` 値はアプリで環境変数として使用できます。

    - `PYTHONPATH` の値は、自由に拡張できますが、アプリのルートを含める必要があります。
    - `WSGI_HANDLER` はアプリからインポート可能な WSGI アプリをポイントする必要があります。
    - `WSGI_LOG` は省略可能ですが、アプリのデバッグのために推奨します。

1. *web.config* の `WSGI_HANDLER` エントリを、使用しているフレームワークに合わせて適切に設定します。

    - **Bottle**: 以下のとおり、必ず `app.wsgi_app` の後にかっこがあるようにします。 これが必要なのは、そのオブジェクトが変数ではなく関数 (*app.py* を参照) であるためです。

        ```xml
        <!-- Bottle apps only -->
        <add key="WSGI_HANDLER" value="app.wsgi_app()"/>
        ```

    - **Flask**:`WSGI_HANDLER` 値を `<project_name>.app` に変更します。`<project_name>` はプロジェクトの名前に一致します。 *runserver.py* の `from <project_name> import app` ステートメントを見ると、正確な識別子が見つかります。 たとえば、プロジェクトの名前が "FlaskAzurePublishExample" の場合、エントリは次のように表示されます。

        ```xml
        <!-- Flask apps only: change the project name to match your app -->
        <add key="WSGI_HANDLER" value="flask_iis_example.app"/>
        ```

    - **Django**:Django プロジェクトの *web.config* には 2 つの変更が必要です。 最初に、`WSGI_HANDLER` 値を `django.core.wsgi.get_wsgi_application()` に変更します (オブジェクトは *wsgi.py* ファイル内にあります)。

        ```xml
        <!-- Django apps only -->
        <add key="WSGI_HANDLER" value="django.core.wsgi.get_wsgi_application()"/>
        ```

        次に、下のエントリを、`DjangoAzurePublishExample` を自分のプロジェクトの名前と置き換えて、`WSGI_HANDLER` に追加します。

        ```xml
        <add key="DJANGO_SETTINGS_MODULE" value="django_iis_example.settings" />
        ```

1. **Django アプリのみ**:Django プロジェクトの *settings.py* ファイルで、次に示すように、'vspython-test-02.azurewebsites.net' を自分の URL と置き換えて、サイト URL ドメインまたは IP アドレスを `ALLOWED_HOSTS` に追加します。このとき、もちろん '1.2.3.4' はご使用の URL または IP アドレスに置き換えます。

    ```python
    # Change the URL or IP address to your specific site
    ALLOWED_HOSTS = ['1.2.3.4']
    ```

    配列への URL の追加が失敗すると、次のエラーが発生します。**DisallowedHost at / Invalid HTTP_HOST header: '\<site URL\>'。'\<site URL\>' を ALLOWED_HOSTS に追加する必要がある場合があります。**

    配列が空の場合、Django は自動的に 'localhost' と '127.0.0.1' を許可しますが、実稼働環境の URL を追加するとその機能は削除されます。 このため、*settings.py* の開発用のコピーと実稼働環境用のコピーを別々に管理するか、環境変数を使用して実行時の値を制御することをお勧めします。

## <a name="deploy-to-iis-or-a-windows-vm"></a>IIS または Windows VM にデプロイする

プロジェクトに正しい *web.config* ファイルがある場合、**ソリューション エクスプローラー**のプロジェクトのコンテキスト メニューで **[発行]** コマンドを使用し、 **[IIS, FTP, etc.]** \(IIS、FTP など\) オプションを選択して、IIS を実行しているコンピューターに発行することができます。 この場合、Visual Studio は単純にプロジェクト ファイルをサーバーにコピーします。サーバー側の構成はご自分で行ってください。
