---
title: Azure App Service での Python の構成 (Windows)
description: Azure App Service に Python インタープリターとライブラリをインストールし、そのインタープリターを正しく参照するように Web アプリケーションを構成する方法について説明します。
ms.date: 01/07/2019
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.custom: seodec18
ms.workload:
- python
- data-science
- azure
ms.openlocfilehash: f7c874a5cd2742f795c6d8b04db88b98b19a556d
ms.sourcegitcommit: 8590cf6b3351e82827fd21159beefef0c02bf162
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/08/2021
ms.locfileid: "102470015"
---
# <a name="how-to-set-up-a-python-environment-on-azure-app-service-windows"></a>Azure App Service で Python 環境を設定する方法 (Windows)

> [!Important]
> この記事で説明するとおり Microsoft では、App Service 用の Python の拡張機能を非推奨にし、[Linux の App Service](publishing-python-web-applications-to-azure-from-visual-studio.md) の直接デプロイを選択しまました。

[Azure App Service](https://azure.microsoft.com/services/app-service/) は、Web アプリに提供するサービスとしてのプラットフォームです。Web アプリがブラウザーでアクセスされるサイト、自身のクライアントで使用される REST API、またはイベント トリガーされる処理かどうかは関係ありません。 App Service は、Python を使用してアプリの実装を完全にサポートします。

Azure App Service でのカスタマイズ可能な Python のサポートは、App Service *サイトの拡張機能* のセットとして提供されます。拡張機能にはそれぞれ Python ランタイムの特定のバージョンが含まれています。 その後、この記事の説明に従って、希望のパッケージを直接環境にインストールすることができます。 App Service 自体で環境をカスタマイズすることにより、Web アプリ プロジェクトでパッケージを管理したり、アプリ コードと一緒にアップロードする必要はありません。

> [!Tip]
> 既定で App Service には、サーバーのルート フォルダーに Python 2.7 と Python 3.4 がインストールされていますが、これらの環境は、カスタマイズしたり、パッケージをインストールすることはできません。また、その存在に依存することもできません。 代わりに、この記事の説明どおりに、制御しているサイトの拡張機能に依存する必要があります。

## <a name="choose-a-python-version-through-the-azure-portal"></a>Azure Portal から Python のバージョンを選択する

1. Azure ポータルで Web アプリの App Service を作成します。
1. App Service のページで、**[開発ツール]** セクションまでスクロールし、**[拡張機能]** を選択してから、**[+ 追加]** を選択します。
1. 必要な Python のバージョンを含む拡張機能まで、一覧を下にスクロールします。

    ![Python の拡張機能を示す Azure Portal](media/python-on-azure-extensions.png)

    > [!Tip]
    > Python の古いバージョンが必要で、サイト拡張機能の一覧にそれが表示されない場合、次のセクションの説明に従って、Azure Resource Manager を介してインストールすることが可能です。

1. 拡張機能を選択し、法的条項に同意して、**[OK]** を選択します。
1. インストールが完了すると、ポータルに通知が表示されます。

## <a name="choose-a-python-version-through-the-azure-resource-manager"></a>Azure Resource Manager から Python のバージョンを選択する

Azure Resource Manager テンプレートを使用して App Service をデプロイしている場合は、サイト拡張機能をリソースとして追加します。 具体的には、拡張機能は、入れ子になったリソース (`resources` の下の `resources` オブジェクト) として、型 `siteextensions` で表示されます。

たとえば、`python361x64` (Python 3.6.1 x 64) への参照を追加すると、テンプレートは、次のようになります (いくつかのプロパティは省略しています)。

```json
"resources": [
  {
    "apiVersion": "2015-08-01",
    "name": "[parameters('siteName')]",
    "type": "Microsoft.Web/sites",

    // ...

    "resources": [
      {
        "apiVersion": "2015-08-01",
        "name": "python361x64",
        "type": "siteextensions",
        "properties": { },
        "dependsOn": [
          "[resourceId('Microsoft.Web/sites', parameters('siteName'))]"
        ]
      },
      // ...
    ]
  }
```

## <a name="set-webconfig-to-point-to-the-python-interpreter"></a>Python インタープリターをポイントする web.config の設定

(ポータルまたは Azure Resource Manager テンプレートのいずれかを使って) サイト拡張機能をインストールすると、次はアプリの *web.config* ファイルを Python インタープリターへポイントさせます。 *web.config* ファイルは、HttpPlatform (推奨) と FastCGI いずれかを使用して Python 要求を処理する方法を、App Service 上で実行される IIS (7 以降) の Web サーバーに指示します。

サイト拡張機能の *python.exe* への完全なパスを探し、適切な *web.config* ファイルを作成および変更します。

### <a name="find-the-path-to-pythonexe"></a>python.exe へのパスを探す

Python のサイト拡張機能は、Python のバージョンとアーキテクチャ (いくつかの古いバージョンは除きます) に応じた、*d:\home* の下のフォルダー内にインストールされます。 たとえば、Python 3.6.1 x64 は、*d:\home\python361x64* にインストールされます。 この場合、Python インタープリターの完全なパスは、*d:\home\python361x64\python.exe*. になります。

App Service でパスを具体的に確認するには、[App Service] ページで **[拡張機能]** を選択し、一覧から拡張機能を選択します。

![Azure App Service での拡張機能のリスト](media/python-on-azure-extension-list.png)

この操作では、次のパスを含む拡張機能の説明ページが開きます。

![Azure App Service での拡張機能の詳細](media/python-on-azure-extension-detail.png)

拡張機能のパスの表示で問題がある場合、コンソールを使用して手動で検索できます。

1. [App Service] ページで、 **[開発ツール]**  >  **[コンソール]** の順に選択します。
1. `ls ../home` または `dir ..\home` のコマンドを入力して、*Python361x64* などの最上位レベルの拡張機能フォルダーを表示します。
1. `ls ../home/python361x64` または `dir ..\home\python361x64` のようなコマンドを入力して、*python.exe* やその他のインタープリター ファイルが含まれていることを確認します。

### <a name="configure-the-httpplatform-handler"></a>Httpplatform のハンドラーの構成

HttpPlatform モジュールは、スタンドアロンの Python プロセスに直接ソケット接続を渡します。 このパススルーにより、任意の Web サーバーを実行することができますが、ローカル Web サーバーを実行するスタートアップ スクリプトが必要になります。 スクリプトは、*web.config* の `<httpPlatform>` 要素で指定します。ここで、`processPath` 属性はサイト拡張機能の Python インタープリターをポイントし、`arguments` 属性はスクリプトと指定する任意の引数をポイントします。

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.webServer>
    <handlers>
      <add name="PythonHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified"/>
    </handlers>
    <httpPlatform processPath="D:\home\Python361x64\python.exe"
                  arguments="D:\home\site\wwwroot\runserver.py --port %HTTP_PLATFORM_PORT%"
                  stdoutLogEnabled="true"
                  stdoutLogFile="D:\home\LogFiles\python.log"
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

FastCGI は、要求レベルで動作するインターフェイスです。 IIS は、受信接続を受信し、各要求を 1 つ以上の永続的な Python プロセスで実行されている WSGI アプリへ転送します。 [wfastcgi パッケージ](https://pypi.io/project/wfastcgi)は、Python の各サイト拡張機能と共にプレインストールされ構成されているため、以下の Bottle フレームワークを使用した Web アプリ用のコードのように、*web.config* に含めて簡単に有効にできます。 *python.exe* と *wfastcgi.py* への完全なパスが `PythonHandler` キーに配置されることに注意してください。

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <appSettings>
    <add key="PYTHONPATH" value="D:\home\site\wwwroot"/>
    <!-- The handler here is specific to Bottle; other frameworks vary. -->
    <add key="WSGI_HANDLER" value="app.wsgi_app()"/>
    <add key="WSGI_LOG" value="D:\home\LogFiles\wfastcgi.log"/>
  </appSettings>
  <system.webServer>
    <handlers>
      <add name="PythonHandler" path="*" verb="*" modules="FastCgiModule"
           scriptProcessor="D:\home\Python361x64\python.exe|D:\home\Python361x64\wfastcgi.py"
           resourceType="Unspecified" requireAccess="Script"/>
    </handlers>
  </system.webServer>
</configuration>
```

ここで定義した `<appSettings>` はアプリで環境変数として使用できます。

- `PYTHONPATH` の値は、自由に拡張できますが、アプリのルートを含める必要があります。
- `WSGI_HANDLER` はアプリからインポート可能な WSGI アプリをポイントする必要があります。
- `WSGI_LOG` は省略可能ですが、アプリのデバッグのために推奨します。

Bottle、Flask、および Django Web アプリ用の *web.config* コンテンツのその他の詳細については、[Azure への発行](publishing-python-web-applications-to-azure-from-visual-studio.md)に関するページをご覧ください。

## <a name="install-packages"></a>パッケージをインストールする

サイトの拡張機能を使用してインストールされた Python インタープリターは、Python 環境の一部にすぎません。 その環境に別のパッケージもインストールする必要があります。

サーバー環境にパッケージを直接インストールするには、次のいずれかの方法を使用します。

| メソッド | 使用 |
| --- | --- |
| [Azure App Service Kudu コンソール](#azure-app-service-kudu-console) | パッケージを対話形式でインストールします。 パッケージは、純粋な Python であるか、ホイールを発行する必要があります。 |
| [Kudu REST API](#kudu-rest-api) | パッケージのインストールを自動化するために使用できます。  パッケージは、純粋な Python であるか、ホイールを発行する必要があります。 |
| アプリとのバンドル | プロジェクトに直接パッケージをインストールし、それをアプリの一部として App Service にデプロイすることができます。 依存関係の数とそれらの更新頻度によっては、これは実用的なデプロイを開始するための最も簡単な方法になる場合があります。 ライブラリは、サーバー上の Python のバージョンと正確に一致している必要があります。一致していない場合、デプロイ後に原因不明のエラーが発生します。 しかし、App Service のサイト拡張機能での Python のバージョンは、python.org でリリースされたバージョンとまったく同じであるため、ローカル開発のために互換性のあるバージョンを簡単に取得できます。 |
| 仮想環境 | サポートされていません。 代わりに、バンドルを使用し、`PYTHONPATH` 環境変数をパッケージの場所をポイントするよう設定します。 |

### <a name="azure-app-service-kudu-console"></a>Azure App Service Kudu コンソール

[Kudu コンソール](https://github.com/projectkudu/kudu/wiki/Kudu-console)は、App Service サーバーとそのファイル システムに直接アクセスするための昇格されたコマンド ライン アクセスを提供します。 これは、重要なデバッグ ツールであると同時に、これでパッケージのインストールなどの CLI 操作を実行できます。

1. Azure Portal の [App Service] ページから、 **[開発ツール]**  >  **[高度なツール]** を選択し、 **[移動]** を選択して Kudu を開きます。 このアクションにより、`.scm` が挿入されることを除いて、ベースの App Service URL と同じ URL に移動します。 たとえば、ベースの URL が `https://vspython-test.azurewebsites.net/` の場合、Kudu は (ブックマークを設定できる) `https://vspython-test.scm.azurewebsites.net/` にあります。

    ![Azure App Service の Kudu コンソール](media/python-on-azure-console01.png)

1. **[デバッグ コンソール]**  >  **[CMD]** を選択してコンソールを開きます。このコンソールで Python のインストール環境に移動し、既存のライブラリを確認できます。

1. 1 つのパッケージをインストールするには、次の手順を実行します。

    a. パッケージのインストール先の Python のインストール フォルダーに移動します (*d:\home\python361x64* など)。

    b. `python.exe -m pip install <package_name>` を使用してパッケージをインストールします。

    ![Azure App Service の Kudu コンソールを使用して bottle をインストールする例](media/python-on-azure-console02.png)

1. サーバーに既にアプリ用の *requirements.txt* がデプロイ済みの場合、それらのすべての要件を次のようにインストールします。

    a. パッケージのインストール先の Python のインストール フォルダーに移動します (*d:\home\python361x64* など)。

    b. コマンド `python.exe -m pip install --upgrade -r d:\home\site\wwwroot\requirements.txt` を実行します。

    *requirements.txt* は、ローカルおよびサーバーで設定されたのと同じパッケージを簡単に再現できるため、これを使用することをお勧めします。 *requirements.txt* に何らかの変更を行った後に、コンソールにアクセスし、コマンドを再実行することを忘れないでください。

> [!Note]
> App Service には C コンパイラがないため、ネイティブ拡張モジュールを使用して任意のパッケージのホイールをインストールする必要があります。 多くの普及しているパッケージでは、独自のホイールを提供しています。 提供していないパッケージの場合は、ローカルの開発用コンピューターで `pip wheel <package_name>` を使用してホイールをサイトにアップロードします。 例については、「[requirements.txt での必須パッケージの管理](managing-required-packages-with-requirements-txt.md)」をご覧ください。

### <a name="kudu-rest-api"></a>Kudu REST API

Azure Portal から Kudu コンソールを使用する代わりに、`https://yoursite.scm.azurewebsites.net/api/command` にコマンドをポストすることで、Kudu REST API からコマンドをリモートで実行することができます。 たとえば、`bottle` パッケージをインストールするには、次の JSON を `/api/command` にポストします。

```json
{
    "command": 'python.exe -m pip install bottle',
    "dir": '\home\python361x64'
}
```

コマンドと認証の詳細については、[Kudu のドキュメント](https://github.com/projectkudu/kudu/wiki/REST-API)を参照してください。

Azure CLI の `az webapp deployment list-publishing-profiles` コマンドを使用して、資格情報を参照することもできます (「[az webapp deployment](/cli/azure/webapp/deployment?view=azure-cli-latest&preserve-view=true#az-webapp-deployment-list-publishing-profiles)」 (az webapp のデプロイ) を参照してください)。 Kudu コマンドをポストするためのヘルパー ライブラリは [GitHub で入手](https://github.com/lmazuel/azure-webapp-publish/blob/master/azure_webapp_publish/kudu.py#L42)することができます。
