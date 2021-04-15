---
title: Visual Studio コンテナー ツールのビルドとデバッグの概要
author: ghogen
description: コンテナー ツールのビルドとデバッグのプロセスの概要
ms.author: ghogen
ms.date: 03/15/2021
ms.technology: vs-azure
ms.topic: conceptual
ms.openlocfilehash: 6b860abeab0745ebae580e3020c94e446f2441c8
ms.sourcegitcommit: c875360278312457f4d2212f0811466b4def108d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/13/2021
ms.locfileid: "107315954"
---
# <a name="how-visual-studio-builds-containerized-apps"></a>Visual Studio でコンテナー化されたアプリをビルドする方法

Visual Studio IDE からビルドする場合でも、コマンド ライン ビルドを設定する場合でも、プロジェクトのビルドのために Visual Studio によって Dockerfile が使用されるしくみを知っておく必要があります。  パフォーマンス上の理由から、Visual Studio ではコンテナー化されたアプリの特別なプロセスに従います。 Visual Studio がプロジェクトをビルドする方法を理解することは、Dockerfile を変更してビルド プロセスをカスタマイズする場合に特に重要です。

Visual Studio では、Docker コンテナーを使用しないプロジェクトをビルドするときに、ローカル コンピューター上で MSBuild が呼び出され、ローカル ソリューション フォルダーの下のフォルダー (通常は `bin`) 内に出力ファイルが生成されます。 ただし、コンテナー化されたプロジェクトの場合、コンテナー化されたアプリをビルドするため、ビルド プロセスで Dockerfile の命令が考慮されます。 Visual Studio で使用される Dockerfile は、複数のステージに分割されます。 このプロセスは、Docker の *マルチステージ ビルド* 機能に依存しています。

## <a name="multistage-build"></a>マルチステージ ビルド

マルチステージ ビルド機能を使用すると、コンテナーのビルド プロセスが効率化され、実行時にアプリに必要なビットしか含めないようにすることで、コンテナーのサイズを小さくすることができます。 マルチステージ ビルドは、.NET Framework プロジェクトではなく、.NET Core プロジェクトに使用されます。

マルチステージ ビルドを使用すると、中間イメージを生成するステージでコンテナー イメージを作成できます。 例として、Visual Studio によって生成される一般的な Dockerfile を考えてみます。最初のステージは `base` です。

```
FROM mcr.microsoft.com/dotnet/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443
```

Dockerfile 内の行は、Microsoft Container Registry (mcr.microsoft.com) の Debian イメージから始まり、ポート 80 および 443 を公開する中間イメージ `base` を作成し、作業ディレクトリを `/app` に設定します。

次のステージは `build` で、次のように表示されます。

```
FROM mcr.microsoft.com/dotnet/sdk:3.1-buster-slim AS build
WORKDIR /src
COPY ["WebApplication43/WebApplication43.csproj", "WebApplication43/"]
RUN dotnet restore "WebApplication43/WebApplication43.csproj"
COPY . .
WORKDIR "/src/WebApplication43"
RUN dotnet build "WebApplication43.csproj" -c Release -o /app/build
```

`build` のステージは、base からの続きではなく、レジストリ (`aspnet` ではなく `sdk`) からの別の、元のイメージから開始されることがわかります。  `sdk` のイメージにはすべてのビルド ツールがあるため、実行時コンポーネントのみを含む aspnet イメージよりもかなり大きくなります。 別のイメージを使用する理由は、Dockerfile の残りの部分を確認すると明確になります。

```
FROM build AS publish
RUN dotnet publish "WebApplication43.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WebApplication43.dll"]
```

最後のステージは、もう一度 `base` から始まります。発行された出力を最終イメージにコピーするための `COPY --from=publish` が含まれます。 このプロセスを使用すると、`sdk` イメージに含まれていたすべてのビルド ツールを含める必要がないため、最終的なイメージがかなり小さくなる可能性があります。

## <a name="building-from-the-command-line"></a>コマンド ラインからのビルド

Visual Studio 以外でビルドする場合は、`docker build` または `MSBuild` を使用してコマンド ラインからビルドできます。

### <a name="docker-build"></a>docker build

コマンド ラインからコンテナー化されたソリューションをビルドするには、通常、ソリューション内の各プロジェクトに対してコマンド `docker build <context>` を使用します。 *build context* 引数を指定します。 Dockerfile の *build context* は、イメージを生成する作業フォルダーとして使用されるローカル コンピューター上のフォルダーです。 たとえば、コンテナーにコピーするときにファイルをコピーするフォルダーです。  .NET Core プロジェクトでは、ソリューション ファイル (.sln) が格納されているフォルダーを使用します。  相対パスとして表されます。この引数は、通常、プロジェクト フォルダー内の Dockerfile とその親フォルダー内のソリューション ファイルに対しては ".." です。  .NET Framework プロジェクトの場合、build context はソリューション フォルダーではなく、プロジェクト フォルダーです。

```cmd
docker build -f Dockerfile ..
```

### <a name="msbuild"></a>MSBuild

Visual Studio によって .NET Framework プロジェクト用 (および Visual Studio 2017 Update 4 より前のバージョンの Visual Studio で作成された .NET Core プロジェクト用) に作成された Dockerfile は、マルチステージの Dockerfile ではありません。  これらの Dockerfile のステップでは、コードはコンパイルされません。  代わりに、Visual Studio では .NET Framework Dockerfile をビルドする際に、まず MSBuild を使用してプロジェクトがコンパイルされます。  これが成功すると、Visual Studio によって Dockerfile がビルドされます。これは単純に、MSBuild からのビルド出力が、生成された Docker イメージにコピーされます。  コードをコンパイルするステップは Dockerfile に含まれていないため、コマンド ラインから `docker build` を使用して .NET Framework Dockerfile をビルドすることはできません。 これらのプロジェクトをビルドするには、MSBuild を使用する必要があります。

単一の Docker コンテナー プロジェクトのイメージをビルドするには、MSBuild を `/t:ContainerBuild` コマンド オプションと共に使用します。 次に例を示します。

```cmd
MSBuild MyProject.csproj /t:ContainerBuild /p:Configuration=Release
```

Visual Studio IDE からソリューションをビルドすると、**出力** ウィンドウに表示されるような出力が表示されます。 Visual Studio でマルチステージ ビルドの最適化が使用されている場合は、**デバッグ** 構成をビルドするときに得られる結果が想定どおりでない場合があるため、常に `/p:Configuration=Release` を使用します。 「[デバッグ](#debugging)」を参照してください。

Docker Compose プロジェクトを使用している場合は、次のコマンドを使用してイメージをビルドします。

```cmd
msbuild /p:SolutionPath=<solution-name>.sln /p:Configuration=Release docker-compose.dcproj
```

## <a name="project-warmup"></a>プロジェクトのウォームアップ

*プロジェクトのウォームアップ* とは、後続の実行 (**F5** キーまたは **Ctrl**+**F5** キー) のパフォーマンスを向上させるために、プロジェクトの Docker プロファイルが選択されたとき (つまり、プロジェクトが読み込まれたとき、または Docker のサポートが追加されたとき) に実行される一連の手順を指します。 これは、 **[ツール]**  >  **[オプション]**  >  **[コンテナー ツール]** で構成できます。 バックグラウンドでは、次のタスクが実行されます。

- Docker Desktop がインストールされ、実行されていることを確認します。
- Docker Desktop がプロジェクトと同じオペレーティング システムに設定されていることを確認します。
- Dockerfile の最初のステージ (ほとんどの Dockerfile では `base` ステージ) でイメージをプルします。  
- Dockerfile をビルドし、コンテナーを開始します。

ウォームアップは **Fast** モードでのみ発生するため、実行中のコンテナーにはアプリ フォルダー ボリュームがマウントされます。 つまり、アプリを変更してもコンテナーが無効になることはありません。 そのため、デバッグのパフォーマンスが大幅に向上し、大きなイメージのプルなどの長時間実行されるタスクの待機時間が短縮されます。

## <a name="volume-mapping"></a>ボリューム マッピング

デバッグをコンテナーで機能させるために、Visual Studio では、ボリューム マッピングを使用してホスト マシンからデバッガーと NuGet フォルダーをマップします。 ボリューム マッピングの詳細については、Docker のドキュメント ([こちら](https://docs.docker.com/storage/volumes/)) を参照してください。 コンテナーにマウントされるボリュームは次のとおりです。

|ボリューム|説明|
|-|-|
| **リモート デバッガー** | プロジェクトの種類に応じて、コンテナーでデバッガーを実行するために必要なビットが含まれています。 これについては、「[デバッグ](#debugging)」のセクションで詳しく説明します。|
| **アプリ フォルダー** | Dockerfile が配置されているプロジェクト フォルダーが含まれています。|
| **ソース フォルダー** | Docker コマンドに渡されるビルド コンテキストが含まれています。|
| **NuGet パッケージのフォルダー** | プロジェクトの *obj\{project}.csproj.nuget.g.props* ファイルから読み取られる NuGet パッケージとフォールバック フォルダーが含まれています。 |

ASP.NET CoreWeb アプリの場合、SSL 証明書とユーザー シークレット用にさらに 2 つのフォルダーが存在する場合があります。詳細については、次のセクションを参照してください。

## <a name="ssl-enabled-aspnet-core-apps"></a>SSL 対応 ASP.NET Core アプリ

Visual Studio のコンテナー ツールは、コンテナーがない場合に想定される方法で、開発証明書を使用した SSL 対応 ASP.NET Core アプリのデバッグをサポートしています。 それを実現するために、Visual Studio では、証明書をエクスポートしてコンテナーで使用できるようにするために、さらにいくつかの手順を追加しています。 コンテナーでデバッグするときの Visual Studio の処理フローを次に示します。

1. ローカル開発証明書が存在し、`dev-certs` ツールを介してホスト マシン上で信頼されていることを確認します。
2. この特定のアプリのユーザー シークレット ストアに保存されているセキュリティで保護されたパスワードを使用して、証明書を %APPDATA%\ASP.NET\Https にエクスポートします。
3. 次のディレクトリのボリュームマウントを行います。

   - *%APPDATA%\Microsoft\UserSecrets*
   - *%APPDATA%\ASP.NET\Https*

ASP.NET Core により、*Https* フォルダー以下のアセンブリ名に一致する証明書が検索されます。これが、そのパスのコンテナーにマップされる理由です。 または、環境変数 (つまり、`ASPNETCORE_Kestrel__Certificates__Default__Path` および `ASPNETCORE_Kestrel__Certificates__Default__Password`) を使用して、またはユーザー シークレット json ファイルで証明書パスとパスワードを定義できます。次に例を示します。

```json
{
  "Kestrel": {
    "Certificates": {
      "Default": {
        "Path": "c:\\app\\mycert.pfx",
        "Password": "strongpassword"
      }
    }
  }
}
```

構成でコンテナー化されたビルドとコンテナー化されていないビルドの両方がサポートされている場合は、環境変数を使用する必要があります。これは、パスがコンテナー環境に固有であるためです。

コンテナー内の ASP.NET Core アプリで SSL を使用する方法の詳細については、「[HTTPS 経由で Docker を使用して ASP.NET Core イメージをホストする](/aspnet/core/security/docker-https)」を参照してください。

## <a name="debugging"></a>デバッグ

**[デバッグ]** 構成でビルドする場合、コンテナー化されたプロジェクトのビルド プロセスのパフォーマンス向上に役立つ Visual Studio の最適化がいくつかあります。 コンテナー化されたアプリのビルド プロセスは、Dockerfile に記載されている手順に単に従うほど簡単ではありません。 コンテナーでのビルドは、ローカル コンピューターでのビルドよりもはるかに低速です。  そのため、**デバッグ** 構成でビルドすると、Visual Studio によって実際にプロジェクトがローカル コンピューター上にビルドされてから、ボリューム マウントを使用して出力フォルダーがコンテナーに共有されます。 この最適化が有効になっているビルドは、*高速* モードのビルドと呼ばれます。

**高速** モードでは、Visual Studio により、`base` ステージのみをビルドするように Docker に指示する引数を指定して `docker build` が呼び出されます。  Visual Studio では、Dockerfile の内容に関係なく、プロセスの残りの部分が処理されます。 そのため、コンテナー環境をカスタマイズしたり、追加の依存関係をインストールしたりするために Dockerfile を変更する場合は、最初のステージで変更を加える必要があります。  Dockerfile の `build`、`publish`、`final` のいずれかのステージに配置されているカスタム ステップは実行されません。

このパフォーマンスの最適化は、**デバッグ** 構成でビルドする場合にのみ発生します。 **リリース** 構成では、Dockerfile で指定されているように、コンテナーでビルドが実行されます。

Dockerfile によって指定されているパフォーマンスの最適化とビルドを無効にする場合は、次のように、プロジェクト ファイルの **ContainerDevelopmentMode** プロパティを **Regular** に設定します。

```xml
<PropertyGroup>
   <ContainerDevelopmentMode>Regular</ContainerDevelopmentMode>
</PropertyGroup>
```

パフォーマンスの最適化を復元するには、プロジェクト ファイルからプロパティを削除します。

 デバッグを開始すると (**F5** キー)、可能であれば、以前に開始したコンテナーが再利用されます。 前のコンテナーを再利用しない場合は、Visual Studio で **Rebuild** または **Clean** コマンドを使用して、Visual Studio で新しいコンテナーを強制的に使用することができます。

デバッガーを実行するプロセスは、プロジェクトの種類とコンテナーのオペレーティング システムによって変わります。

|シナリオ|デバッガー プロセス|
|-|-|
| **.NET Core アプリ (Linux コンテナー)**| Visual Studio によって `vsdbg` がダウンロードされ、コンテナーにマップされ、プログラムと引数 (つまり `dotnet webapp.dll`) を使って呼び出され、デバッガーによってプロセスにアタッチされます。 |
| **.NET Core アプリ (Windows コンテナー)**| Visual Studio によって `onecoremsvsmon` を使用してコンテナーにマップされ、エントリ ポイントとして実行され、Visual Studio によってはそれが接続され、プログラムにアタッチされます。 これは、通常、別のコンピューターまたは仮想マシンでリモート デバッグを設定する方法に似ています。|
| **.NET Framework アプリ** | Visual Studio では `msvsmon` を使用してコンテナーがマップされ、Visual Studio から接続できるエントリ ポイントの一部として実行され、プログラムにアタッチされます。|

`vsdbg.exe` の詳細については、[Visual Studio からの Linux および OSX 上の .NET Core のオフロード デバッグ](https://github.com/Microsoft/MIEngine/wiki/Offroad-Debugging-of-.NET-Core-on-Linux---OSX-from-Visual-Studio)に関する記事を参照してください。

## <a name="container-entry-point"></a>コンテナーのエントリ ポイント

Visual Studio では、プロジェクトの種類とコンテナーのオペレーティング システムに応じて、カスタム コンテナーのエントリ ポイントを使用します。さまざまな組み合わせを次に示します。

|コンテナーの種類|エントリ ポイント|
|-|-|
| **Linux コンテナー** | エントリ ポイントは `tail -f /dev/null` です。コンテナーの実行を維持するために、無期限に待機します。 デバッガーを介してアプリを起動すると、アプリの実行を担当するのはデバッガーです (つまり、`dotnet webapp.dll`)。 デバッグなしで起動すると、ツールでは、アプリを実行するために `docker exec -i {containerId} dotnet webapp.dll` が実行されます。|
| **Windows コンテナー**| エントリ ポイントは、デバッガーを実行する `C:\remote_debugger\x64\msvsmon.exe /noauth /anyuser /silent /nostatus` のようなものであるため、接続をリッスンしています。 デバッガーによってアプリが実行され、`docker exec` コマンドがデバッグなしで起動される場合と同様の状況です。 .NET Framework Web アプリの場合、エントリ ポイントはわずかに異なり、`ServiceMonitor` がコマンドに追加されます。|

コンテナー エントリ ポイントは、単一コンテナー プロジェクトではなく、docker-compose プロジェクトでのみ変更できます。

## <a name="next-steps"></a>次の手順

プロジェクト ファイルで追加の MSBuild プロパティを設定して、ビルドをさらにカスタマイズする方法について学習します。 [コンテナーのプロジェクトの MSBuild プロパティ](container-msbuild-properties.md)に関するページを参照してください。

## <a name="see-also"></a>関連項目

[MSBuild](../msbuild/msbuild.md)
[Windows の Dockerfile](/virtualization/windowscontainers/manage-docker/manage-windows-dockerfile)
[Windows 上の Linux コンテナー](/virtualization/windowscontainers/deploy-containers/linux-containers)
