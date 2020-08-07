---
title: チュートリアル - Docker Compose を使用して複数コンテナーのアプリを作成する
description: Visual Studio for Mac で複数のコンテナーを管理し、それらの間で通信を行う方法について学習します
author: heiligerdankgesang
ms.author: dominicn
ms.date: 07/03/2020
ms.topic: tutorial
ms.openlocfilehash: b15ba0200520d8a04abc30b606b5b10215e3c22e
ms.sourcegitcommit: dda98068c0f62ccd1a19fdfde4bdb822428d0125
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/30/2020
ms.locfileid: "87425428"
---
# <a name="create-a-multi-container-app-with-docker-compose"></a>Docker Compose を使用して複数コンテナーのアプリを作成する

このチュートリアルでは、Visual Studio for Mac で Docker Compose を使用しているときに、複数のコンテナーを管理し、それらの間で通信を行う方法について学習します。

## <a name="prerequisites"></a>必須コンポーネント

* [Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-mac)
* [Visual Studio for Mac 2019](https://visualstudio.microsoft.com/vs/mac)

## <a name="create-an-aspnet-core-web-application-and-add-docker-support"></a>ASP.NET Core Web アプリケーションを作成し、Docker のサポートを追加する

1. **[ファイル] > [新しいソリューション]** に移動して、新しいソリューションを作成します。
1. **[Web and Console]\(Web とコンソール\) > [アプリ]** で、 **[Web アプリケーション]** テンプレートを選択します。![新しい ASP.NET アプリケーションを作成する](media/docker-quickstart-1.png)
1. ターゲット フレームワークを選択します。 この例では、.NET Core 3.1 を使います。![ターゲット フレームワークを設定する](media/docker-quickstart-2.png)
1. プロジェクト名 (この例では _DockerDemoFrontEnd_) やソリューション名 (_DockerDemo_) など、プロジェクトの詳細を入力します。 作成されるプロジェクトには、ASP.NET Core の Web サイトをビルドして実行するために必要なすべての基本が含まれています。
1. Solution Pad で DockerDemoFrontEnd プロジェクトを右クリックし、 **[追加] > [Add Docker Support]\(Docker サポートの追加\)** を選択します。![Docker サポートの追加](media/docker-quickstart-3.png)

Visual Studio for Mac で、**docker-compose** という名前の新しいプロジェクトがソリューションに自動的に追加され、既存のプロジェクトに **Dockerfile** が追加されます。

## <a name="create-an-aspnet-core-web-api-and-add-docker-support"></a>ASP.NET Core Web API を作成し、Docker のサポートを追加する

次に、バックエンド API として機能する 2 番目のプロジェクトを作成します。 **.NET Core API** テンプレートには、RESTful 要求を処理できるコントローラーが含まれています。

1. ソリューションを右クリックして **[追加] > [新しいプロジェクトの追加]** を選択し、既存のソリューションに新しいプロジェクトを追加します。
1. **[Web and Console]\(Web とコンソール\) > [アプリ]** で、 **[API]** テンプレートを選択します。
1. ターゲット フレームワークを選択します。 この例では、.NET Core 3.1 を使います。
1. プロジェクト名 (この例では _MyWebAPI_) など、プロジェクトの詳細を入力します。
1. 作成されたら、Solution Pad に移動して MyWebAPI プロジェクトを右クリックし、 **[追加] > [Add Docker Support]\(Docker サポートの追加\)** を選択します。

**docker-compose** プロジェクトの **docker-compose.yml** ファイルが、既存の Web アプリ プロジェクトと共に API プロジェクトを含むように自動的に更新されます。 **docker-compose** プロジェクトをビルドして実行すると、これらの各プロジェクトが異なる Docker コンテナーに配置されます。

```yaml
version: '3.4'

services:
  dockerdemofrontend:
    image: ${DOCKER_REGISTRY-}dockerdemofrontend
    build:
      context: .
      dockerfile: DockerDemoFrontEnd/Dockerfile

  mywebapi:
    image: ${DOCKER_REGISTRY-}mywebapi
    build:
      context: .
      dockerfile: MyWebAPI/Dockerfile
```

## <a name="integrate-the-two-containers"></a>2 つのコンテナーを統合する

これで、ソリューションには 2 つの ASP.NET プロジェクトがあり、両方に Docker のサポートが構成されています。 次に、コードを追加する必要があります。

1. `DockerDemoFrontEnd` プロジェクトで、*Pages/Index.cshtml.cs* ファイルを開き、`OnGet` メソッドを次のコードに置き換えます。

   ```csharp
    public async Task OnGet()
    {
       ViewData["Message"] = "Hello from webfrontend";

       using (var client = new System.Net.Http.HttpClient())
       {
          // Call *mywebapi*, and display its response in the page
          var request = new System.Net.Http.HttpRequestMessage();
          request.RequestUri = new Uri("http://mywebapi/WeatherForecast");
          var response = await client.SendAsync(request);
          ViewData["Message"] += " and " + await response.Content.ReadAsStringAsync();
       }
    }
   ```
   
    > [!NOTE]
    > 運用環境のコードでは、各要求の後で `HttpClient` を破棄しないでください。 ベスト プラクティスについては、「[HttpClientFactory を使用して回復力の高い HTTP 要求を実装する](https://docs.microsoft.com/dotnet/architecture/microservices/implement-resilient-applications/use-httpclientfactory-to-implement-resilient-http-requests)」を参照してください。

1. *Index.cshtml* ファイルで、`ViewData["Message"]` を表示する行を追加し、ファイルを次のコードのようにします。

      ```cshtml
      @page
      @model IndexModel
      @{
          ViewData["Title"] = "Home page";
      }

      <div class="text-center">
          <h1 class="display-4">Welcome</h1>
          <p>Learn about <a href="https://docs.microsoft.com/aspnet/core">building Web apps with ASP.NET Core</a>.</p>
          <p>@ViewData["Message"]</p>
      </div>
      ```
  
1. フロントエンドと Web API の両方のプロジェクトで、*Startup.cs* 内の `Configure` メソッドでの [Microsoft.AspNetCore.Builder.HttpsPolicyBuilderExtensions.UseHttpsRedirection](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.builder.httpspolicybuilderextensions.usehttpsredirection) への呼び出しをコメントアウトしてください。このサンプル コードでは、Web API を呼び出すために HTTPS ではなく HTTP を使用するためです。

      ```csharp
                  //app.UseHttpsRedirection();
      ```

1. `docker-compose` プロジェクトをスタートアップ プロジェクトとして設定し、 **[実行] > [デバッグの開始]** に移動します。 すべてが正しく構成されている場合、"Hello from webfrontend and webapi (with value 1)" というメッセージが表示されます。

![Docker 複数コンテナー ソリューションの実行](media/docker-multicontainer-debug.png)
