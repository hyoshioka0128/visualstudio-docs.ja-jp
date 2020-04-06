---
title: Visual Studio Tools for Docker と ASP.NET
author: ghogen
description: Visual Studio 2019 ツールと Docker for Windows を使用する方法について説明します
ms.author: ghogen
ms.date: 02/01/2019
ms.prod: visual-studio-dev16
ms.technology: vs-azure
ms.topic: include
ms.openlocfilehash: bd9ac1bda9cb5f5d9cc5d84248200434426307c8
ms.sourcegitcommit: ce3d0728ec1063ab548dac71c8eaf26d20450acc
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/01/2020
ms.locfileid: "80501683"
---
Visual Studio を使用すると、コンテナー化された .NET、ASP.NET、および ASP.NET Core アプリを簡単にビルド、デバッグ、および実行して、Azure Container Registry (ACR)、Docker Hub、Azure App Service、または独自のコンテナー レジストリに発行することができます。 この記事では、ASP.NET Core アプリを ACR に発行します。

## <a name="prerequisites"></a>必須コンポーネント

* [Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-windows)
* **Web 開発**、**Azure Tools** ワークロード、および/または **.NET Core クロスプラットフォーム開発**ワークロードがインストールされた [Visual Studio 2019](https://visualstudio.microsoft.com/downloads)
* .NET Core を使って開発するための [.NET Core 開発ツール](https://dotnet.microsoft.com/download/dotnet-core/)
* Azure Container Registry に発行する場合、Azure サブスクリプション。 [無料試用版にサインアップします](https://azure.microsoft.com/offers/ms-azr-0044p/)。

## <a name="installation-and-setup"></a>インストールとセットアップ

Docker をインストールするには、まず、「[Docker Desktop for Windows: What to know before you install](https://docs.docker.com/docker-for-windows/install/#what-to-know-before-you-install)」 (Docker Desktop for Windows: インストール前に知っておくべきこと) の情報を確認します。 次に、[Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-windows) をインストールします。

## <a name="add-a-project-to-a-docker-container"></a>Docker コンテナーにプロジェクトを追加する

1. **[ASP.NET Core Web アプリケーション]** テンプレートを使用して新しいプロジェクトを作成します。または、.NET Core ではなく .NET Framework を使用する場合は、 **[ASP.NET Web アプリケーション (.NET Framework)]** を選択します。
1. **[Web アプリケーション]** を選択し、 **[Enable Docker Support]\(Docker サポートを有効にする\)** チェックボックスがオンになっていることを確認します。

   ![[Enable Docker Support]\(Docker サポートを有効にする\) チェック ボックス](../../media/container-tools/vs-2019/create-new-web-application.PNG)

   このスクリーンショットには .NET Core が表示されています。 .NET Framework を使用している場合は、少し異なります。

1. コンテナーの種類 (Windows または Linux) を選択し、 **[作成]** をクリックします。

## <a name="dockerfile-overview"></a>Dockerfile の概要

*Dockerfile* (Docker の最終イメージを作成するためのレシピ) は、プロジェクトで作成されます。 その中に含まれるコマンドの詳細については、「[Dockerfile reference](https://docs.docker.com/engine/reference/builder/)」 (Dockerfile リファレンス) を参照してください。

```
FROM microsoft/dotnet:2.2-aspnetcore-runtime-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk-stretch AS build
WORKDIR /src
COPY ["HelloDockerTools/HelloDockerTools.csproj", "HelloDockerTools/"]
RUN dotnet restore "HelloDockerTools/HelloDockerTools.csproj"
COPY . .
WORKDIR "/src/HelloDockerTools"
RUN dotnet build "HelloDockerTools.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "HelloDockerTools.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "HelloDockerTools.dll"]
```

前の *Dockerfile* は、[microsoft/aspnetcore](https://hub.docker.com/r/microsoft/aspnetcore/) イメージに基づいており、プロジェクトをビルドしてコンテナーに追加することで基本イメージを変更するための手順が含まれています。 .NET Framework を使用している場合、基本イメージは異なります。

新しいプロジェクト ダイアログの **[Configure for HTTPS]\(HTTPS 用に構成する\)** チェック ボックスがオンになっている場合、*Dockerfile* は 2 つのポートを公開します。 1 つのポートは HTTP トラフィック用、もう 1 つのポートは HTTPS 用に使用されます。 チェック ボックスがオンになっていない場合は、HTTP トラフィック用に単一のポート (80) が公開されます。

## <a name="debug"></a>デバッグ

ツールバーのデバッグ ドロップダウンから **[Docker]** を選択し、アプリのデバッグを開始します。 証明書の信頼を求めるメッセージが表示される場合があります。続行するには、証明書を信頼することを選びます。

**[出力]** ウィンドウの **[コンテナー ツール]** オプションに、実行されているアクションの内容が表示されます。 初めての場合、基本イメージのダウンロードにしばらく時間がかかる場合がありますが、以降の実行でははるかに高速になります。

>[!NOTE]
> デバッグ用にポートを変更する必要がある場合は、*launchSettings.json* ファイルで行うことができます。 [コンテナーの起動設定](../../container-launch-settings.md)に関する記事を参照してください。

## <a name="containers-window"></a>コンテナー ウィンドウ

Visual Studio 2019 バージョン 16.4 以降をお持ちの場合は、 **[コンテナー]** ウィンドウを使用して、ご利用のコンピューター上で実行中のコンテナー、および使用可能なイメージを確認できます。

IDE の [検索] ボックスを使用して (**Ctrl**+**Q** を押して使用)、 **[コンテナー]** ウィンドウを開き、`container` を入力し、一覧から **[コンテナー]** ウィンドウを選択します。

**[コンテナー]** ウィンドウをエディターの下などの便利な場所に配置するには、ウィンドウを移動してウィンドウ配置ガイドに従います。

ウィンドウで、ご利用のコンテナーを見つけ、各タブをステップ実行して、環境変数、ポート マッピング、ログ、およびファイル システムを表示します。

![コンテナー ウィンドウのスクリーンショット](../../media/overview/vs-2019/container-tools-window.png)

詳細については、[Visual Studio でのコンテナーおよびイメージの表示および診断](../../view-and-diagnose-containers.md)に関するページを参照してください。

## <a name="publish-docker-images"></a>Docker イメージの発行

アプリの開発とデバッグのサイクルが完了すると、アプリの実稼働イメージを作成できます。

1. 構成ドロップダウンを **[リリース]** に変更し、アプリを構築します。
1. **ソリューション エクスプローラー**で対象のプロジェクトを右クリックし、 **[発行]** を選択します。
1. 発行先ダイアログで **[コンテナー レジストリ]** タブを選択します。
1. **[新しい Azure コンテナー レジストリを作成する]** を選択し、 **[発行]** をクリックします。
1. **[新しい Azure コンテナー レジストリを作成する]** で、目的の値を入力します。

    | 設定      | 推奨値  | 説明                                |
    | ------------ |  ------- | -------------------------------------------------- |
    | **DNS プレフィックス** | グローバルに一意の名前 | コンテナー レジストリを一意に識別する名前。 |
    | **サブスクリプション** | サブスクリプションの選択 | 使用する Azure サブスクリプション。 |
    | **[リソース グループ](/azure/azure-resource-manager/resource-group-overview)** | myResourceGroup |  コンテナー レジストリを作成するリソース グループの名前。 新しいリソース グループを作成する場合は、 **[新規]** を選択します。|
    | **[SKU](/azure/container-registry/container-registry-skus)** | 標準 | コンテナー レジストリのサービス層  |
    | **レジストリの場所** | 近くの場所 | [[地域]](https://azure.microsoft.com/regions/) で、自分に近いか、またはコンテナー レジストリを使用する他のサービスに近い場所を選択します。 |

    ![Visual Studio の Azure コンテナー レジストリを作成するダイアログ][0]

1. **[作成]**

   ![発行の成功を示すスクリーンショット](../../media/container-tools/publish-succeeded.png)

## <a name="next-steps"></a>次の手順

これでレジストリからコンテナーを、[Azure Container Instances](/azure/container-instances/container-instances-tutorial-deploy-app) などの Docker イメージを実行できるホストにプルできるようになりました。

[0]:../../media/hosting-web-apps-in-docker/vs-acr-provisioning-dialog-2019.png
