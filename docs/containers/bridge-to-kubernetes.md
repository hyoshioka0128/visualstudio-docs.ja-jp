---
title: Visual Studio で Bridge to Kubernetes を使用する
titleSuffix: ''
ms.technology: vs-azure
ms.date: 06/02/2020
ms.topic: how-to
description: Visual Studio で Bridge to Kubernetes を使用して開発用コンピューターを Kubernetes クラスターに接続する方法について説明します
keywords: Bridge to Kubernetes, Azure Dev Spaces, Dev Spaces, Docker, Kubernetes, Azure, コンテナー
monikerRange: '>=vs-2019'
ms.author: ghogen
author: ghogen
manager: jillfra
ms.openlocfilehash: 7bbeec2baab018ea770dbee60db507399ebeb745
ms.sourcegitcommit: e38419bb842d587fd9e37c24b6cf3fc5c2e74817
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91860447"
---
# <a name="use-bridge-to-kubernetes"></a>Bridge to Kubernetes を使用する

Bridge to Kubernetes を使用すると、Kubernetes クラスターと、開発用コンピューターで実行されているコードの間で、トラフィックをリダイレクトすることができます。 また、このガイドでは、Kubernetes クラスター上の複数のマイクロサービスを含む大規模なサンプル アプリケーションをデプロイするためのスクリプトも提供します。

## <a name="before-you-begin"></a>開始する前に

このガイドでは、[自転車共有サンプル アプリケーション][bike-sharing-github]を使用して、開発用コンピューターを Kubernetes クラスターに接続する方法を示します。 Kubernetes クラスター上で実行されている独自のアプリケーションが既にある場合でも、以下の手順に従い、独自のサービスの名前を使用できます。

### <a name="prerequisites"></a>前提条件

* Azure サブスクリプション。 Azure サブスクリプションをお持ちでない場合は、[無料のアカウント](https://azure.microsoft.com/free)を作成できます。
* [Azure CLI がインストールされていること][azure-cli]。
* *Azure の開発*ワークロードがインストールされている Windows 10 で、[Visual Studio 2019][visual-studio] バージョン 16.7 Preview 4 以降が実行されていること。
* [Bridge to Kubernetes 拡張機能がインストールされていること][btk-extension]。

また、.NET コンソール アプリケーションの場合は、*Microsoft.VisualStudio.Azure.Kubernetes.Tools.Targets* NuGet パッケージをインストールします。

## <a name="create-a-kubernetes-cluster"></a>Kubernetes クラスターを作成する

[サポートされているリージョン][supported-regions]に AKS クラスターを作成します。 下記のコマンドを使用すると、*MyResourceGroup* というリソース グループと *MyAKS* という AKS クラスターが作成されます。

```azurecli-interactive
az group create \
    --name MyResourceGroup \
    --location eastus

az aks create \
    --resource-group MyResourceGroup \
    --name MyAKS \
    --location eastus \
    --node-count 3 \
    --generate-ssh-keys
```

## <a name="install-the-sample-application"></a>サンプル アプリケーションをインストールする

提供されているスクリプトを使用して、サンプル アプリケーションをクラスターにインストールします。 [Azure Cloud Shell][azure-cloud-shell] を使用してこのスクリプトを実行できます。

```azurecli-interactive
git clone https://github.com/Microsoft/mindaro
cd mindaro
chmod +x ./bridge-quickstart.sh
./bridge-quickstart.sh -g MyResourceGroup -n MyAKS
```

パブリック URL を開いて、クラスターで実行されているサンプル アプリケーションに移動します。この URL は、インストール スクリプトの出力に表示されます。

```console
$ ./bridge-quickstart.sh -g MyResourceGroup -n MyAKS
Defaulting Dev spaces repository root to current directory : ~/mindaro
Setting the Kube context
...
To try out the app, open the url:
bikeapp.bikesharingweb.EXTERNAL_IP.nip.io
```

上の例では、パブリック URL は `bikeapp.bikesharingweb.EXTERNAL_IP.nip.io` です。

## <a name="connect-to-your-cluster-and-debug-a-service"></a>クラスターに接続してサービスをデバッグする

開発用コンピューターで、[az aks get-credentials][az-aks-get-credentials] を使用して、Kubernetes CLI をダウンロードし、Kubernetes クラスターに接続するように構成します。

```azurecli
az aks get-credentials --resource-group MyResourceGroup --name MyAKS
```

GitHub の [Bike Sharing (自転車共有) サンプル アプリケーション][bike-sharing-github] リポジトリから、緑色の **[Code]\(コード\)** ボタンのドロップダウンを使用し、 **[Open in Visual Studio]\(Visual Studio で開く\)** を選択し、リポジトリをローカルに複製して、Visual Studio でそのフォルダーを開きます。 次に、 **[ファイル]**  >  **[プロジェクトを開く]** を使用して、*samples/BikeSharingApp/ReservationEngine* フォルダー内の **app.csproj** プロジェクトを開きます。

次の図のように、プロジェクトで起動設定のドロップダウンから **[Bridge to Kubernetes]** を選択します。

![Bridge to Kubernetes を選択する](media/bridge-to-kubernetes/choose-bridge-to-kubernetes.png)

*[Bridge to Kubernetes]* の横にある開始ボタンをクリックします。 **[Create profile for Bridge to Kubernetes]\(Bridge to Kubernetes のプロファイルの作成\)** ダイアログで、次の手順を実行します。

* サブスクリプションを選択します。
* クラスターとして *MyAKS* を選択します。
* 名前空間として *bikeapp* を選択します。
* リダイレクトするサービスとして *reservationengine* を選択します。
* 起動プロファイルとして *app* を選択します。
* ブラウザーを起動する URL として `http://bikeapp.bikesharingweb.EXTERNAL_IP.nip.io` を選択します。

![Bridge to Kubernetes クラスターを選択する](media/bridge-to-kubernetes/choose-bridge-cluster2.png)

> [!IMPORTANT]
> リダイレクトできるのは、ポッドが 1 つのサービスだけです。

分離して実行するかどうかを選択します。つまり、変更しても、クラスターを使用している他のユーザーは影響を受けません。 影響を受ける各サービスのコピーに要求をルーティングし、他のすべてのトラフィックは通常どおりルーティングすることで、この分離モードは達成されます。 この実行方法の詳細については、「[Bridge to Kubernetes のしくみ][btk-overview-routing]」を参照してください。

**[Save and start debugging]\(保存してデバッグを開始する\)** をクリックします。

*reservationengine* サービスに対する Kubernetes クラスター内のすべてのトラフィックが、開発用コンピューターで実行されているアプリケーションのバージョンにリダイレクトされます。 Bridge to Kubernetes ではまた、アプリケーションからのすべての送信トラフィックが、Kubernetes クラスターにルーティングされます。

> [!NOTE]
> *EndpointManager* が管理者特権で実行して hosts ファイルを変更することを許可するように求められます。

`reservationengine` サービスに接続していることがステータス バーに表示されたら、開発用コンピューターに接続されています。

![接続された開発用コンピューター](media/bridge-to-kubernetes/development-computer-connected.png)

> [!NOTE]
> 以降の起動時には、 **[Create profile for Bridge to Kubernetes]\(Bridge to Kubernetes のプロファイルの作成\)** ダイアログは表示されません。 これらの設定は、プロジェクトのプロパティの **[デバッグ]** で更新します。

開発用コンピューターが接続されると、置き換えているサービスのトラフィックの、開発用コンピューターに対するリダイレクトが開始されます。

## <a name="set-a-break-point"></a>ブレーク ポイントを設定する

[BikesHelper.cs][bikeshelper-cs-breakpoint] を開き、26 行目のどこかをクリックして、カーソルをそこに置きます。 *F9* キーを押すか、 **[デバッグ]**  >  **[ブレークポイントの設定/解除]** の順に選択してブレークポイントを設定します。

パブリック URL を開いて、サンプル アプリケーションに移動します。 ユーザーとして **Aurelia Briggs (顧客)** を選択してから、借りる自転車を選択します。 **[Rent Bike]\(自転車をレンタルする\)** を選択します。 Visual Studio に戻って、26 行目が強調表示されていることを確認します。 設定したブレークポイントによって、26 行目でサービスが一時停止されました。 サービスを再開するには、**F5** キーを押すか、 **[デバッグ]**  >  **[続行]** の順にクリックします。 ブラウザーに戻り、自転車をレンタルしたことがページに表示されることを確認します。

`BikesHelper.cs` の 26 行目にカーソルを置いて **F9** キーを押すことで、ブレークポイントを削除します。

> [!NOTE]
> 既定では、デバッグ タスクを停止すると、開発用コンピューターも Kubernetes クラスターから切断されます。 デバッグ オプションの **[Kubernetes Debugging Tools]\(Kubernetes デバッグ ツール\)** セクションで **[Disconnect after debugging]\(デバッグ後に切断する\)** を `false` に変更することで、この動作を変更できます。 この設定を更新した後は、デバッグを停止して開始するとき、開発用コンピューターは接続されたままになります。 開発用コンピューターをクラスターから切断するには、ツール バーの **[切断]** ボタンをクリックします。

## <a name="additional-configuration"></a>追加構成

Bridge to Kubernetes では、ルーティング トラフィックを処理し、追加の構成なしで環境変数をレプリケートできます。 ConfigMap ファイルなど、Kubernetes クラスターのコンテナーにマウントされているファイルをダウンロードする必要がある場合、`KubernetesLocalProcessConfig.yaml` を作成し、開発用コンピューターにそれらのファイルをダウンロードできます。 詳細については、[Bridge to Kubernetes 向けの追加の構成に KubernetesLocalProcessConfig.yaml を使用する][kubernetesLocalProcessConfig-yaml]方法に関するページを参照してください。

## <a name="using-logging-and-diagnostics"></a>ログ記録と診断の使用

診断ログは、開発用コンピューターの *TEMP* ディレクトリの `Bridge to Kubernetes` ディレクトリにあります。 

## <a name="remove-the-sample-application-from-your-cluster"></a>クラスターからサンプル アプリケーションを削除する

クラスターからサンプル アプリケーションを削除するには、提供されているスクリプトを使用します。

```azurecli-interactive
./bridge-quickstart.sh -c -g MyResourceGroup -n MyAKS
```

## <a name="next-steps"></a>次のステップ

Bridge to Kubernetes のしくみについて説明します。

> [!div class="nextstepaction"]
> [Bridge to Kubernetes のしくみ](overview-bridge-to-kubernetes.md)

[azds-cli]: /azure/dev-spaces/how-to/install-dev-spaces#install-the-client-side-tools
[azds-vs-code]: https://marketplace.visualstudio.com/items?itemName=azuredevspaces.azds
[azure-cli]: /cli/azure/install-azure-cli?view=azure-cli-lates&preserve-view=true
[azure-cloud-shell]: /azure/cloud-shell/overview.md
[az-aks-get-credentials]: /cli/azure/aks?view=azure-cli-latest&preserve-view=true#az-aks-get-credentials
[az-aks-vs-code]: https://marketplace.visualstudio.com/items?itemName=ms-kubernetes-tools.vscode-aks-tools
[bike-sharing-github]: https://github.com/Microsoft/mindaro
[preview-terms]: https://azure.microsoft.com/support/legal/preview-supplemental-terms/
[bikeshelper-cs-breakpoint]: https://github.com/Microsoft/mindaro/blob/master/samples/BikeSharingApp/ReservationEngine/BikesHelper.cs#L26
[supported-regions]: https://azure.microsoft.com/global-infrastructure/services/?products=kubernetes-service
[troubleshooting]: /azure/dev-spaces/troubleshooting#fail-to-restore-original-configuration-of-deployment-on-cluster
[visual-studio]: https://www.visualstudio.com/vs/
[btk-extension]: https://marketplace.visualstudio.com/items?itemName=ms-azuretools.mindaro
[kubernetesLocalProcessConfig-yaml]: configure-bridge-to-kubernetes.md
[btk-overview-routing]: overview-bridge-to-kubernetes.md#using-routing-capabilities-for-developing-in-isolation