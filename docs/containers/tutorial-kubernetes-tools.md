---
title: Kubernetes ツールのチュートリアル | Microsoft Docs
ms.date: 06/08/2018
ms.topic: conceptual
author: ghogen
ms.author: ghogen
manager: jillfra
ms.technology: vs-azure
ms.workload:
- azure
ms.openlocfilehash: f5868f97301eba62d16ea68cdaa0c97c8e20edd1
ms.sourcegitcommit: 939407118f978162a590379997cb33076c57a707
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/13/2020
ms.locfileid: "75916958"
---
# <a name="get-started-with-visual-studio-kubernetes-tools"></a>Visual Studio Kubernetes ツールの概要

Visual Studio Kubernetes ツールを使用すると、Kubernetes を対象とするコンテナー化されたアプリケーションの開発を効率化できます。 Visual Studio では、Dockerfiles や Helm グラフなどの Kubernetes 展開をサポートするために必要な configuration-as-code ファイルを自動的に作成できます。 Azure Dev Spaces を使用してライブ Azure Kubernetes Service (AKS) クラスターでコードをデバッグしたり、Visual Studio 内から AKS クラスターに直接発行したりすることができます。

このチュートリアルでは、Visual Studio を使用して Kubernetes サポートをプロジェクトに追加し、AKS に発行する方法について説明します。 [Azure Dev Spaces](/azure/dev-spaces/) を使用して AKS で実行されているプロジェクトのデバッグとテストを行うことに関心がある場合は、代わりに [Azure Dev Spaces のチュートリアル](/azure/dev-spaces/get-started-netcore-visualstudio)に進んでください。

## <a name="prerequisites"></a>必須コンポーネント

この新機能を利用するには、以下が必要です。

::: moniker range="vs-2017"
- *ASP.NET および Web 開発*ワークロードと共に、最新バージョンの [Visual Studio 2017](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)。
- 個別のダウンロードとして入手できる [Visual Studio 用 Kubernetes ツール](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vs-tools-for-kubernetes)。
::: moniker-end
::: moniker range="vs-2019"
- [Visual Studio 2019](https://visualstudio.microsoft.com/downloads) と *ASP.NET と Web 開発*ワークロード。
::: moniker-end
- Docker イメージのビルド、ローカルで実行されている Docker コンテナーのデバッグ、または AKS への発行を行う場合は、開発ワークステーション (つまり、Visual Studio を実行する場所) にインストールされている [Docker Desktop](https://store.docker.com/editions/community/docker-ce-desktop-windows) (Azure Dev Spaces を使用して AKS で Docker コンテナーをビルドおよびデバッグするためには Docker は必要*ありません*)。
::: moniker range="vs-2017"
- Visual Studio から AKS に発行する場合 (Azure Dev Spaces を使用した AKS でのデバッグには必要*ありません*):

    1. 個別のダウンロードとして入手できる [AKS 発行ツール](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vs-tools-for-kubernetes)。

    1. Azure Kubernetes Service クラスター。 詳細については、[AKS クラスターの作成](/azure/aks/kubernetes-walkthrough-portal#create-an-aks-cluster)に関する記事を参照してください。 必ず開発ワークステーションから[クラスターに接続](/azure/aks/kubernetes-walkthrough#connect-to-the-cluster)してください。

    1. 開発ワークステーションにインストールされた Helm CLI。 詳細については、「[Installing Helm](https://github.com/kubernetes/helm/blob/master/docs/install.md)」(Helm のインストール) を参照してください。

    1. `helm init` コマンドを使用して、AKS クラスターに対して構成された Helm。 これを行う方法の詳細については、[Helm の構成方法](/azure/aks/kubernetes-helm#configure-helm)に関する記事を参照してください。
::: moniker-end

## <a name="create-a-new-kubernetes-project"></a>新しい Kubernetes プロジェクトを作成する

::: moniker range="vs-2017"

適切なツールをインストールしたら、Visual Studio を起動して新しいプロジェクトを作成します。 **[クラウド]** で、 **[Kubernetes 用のコンテナー アプリケーション]** のプロジェクトの種類を選択します。 このプロジェクトの種類を選択し、 **[OK]** を選択します。

![新しい Kubernetes アプリ プロジェクトの作成のスクリーンショット](media/tutorial-kubernetes-tools/k8s-tools-new-k8s-app.png)

::: moniker-end
::: moniker range=">= vs-2019"

Visual Studio の開始ウィンドウで、*Kubernetes* を検索し、 **[Kubernetes 用のコンテナー アプリケーション]** を選択します。

![新しい Kubernetes アプリ プロジェクトの作成のスクリーンショット](media/tutorial-kubernetes-tools/vs-2019/k8s-tools-new-k8s-app1.png)

プロジェクト名を指定します。

![新しい Kubernetes アプリ プロジェクトの作成のスクリーンショット](media/tutorial-kubernetes-tools/vs-2019/k8s-tools-new-k8s-app2.png)

::: moniker-end

次に、作成する ASP.NET Core Web アプリケーションの種類を選択できます。 **[Web アプリケーション]** を選択します。 このダイアログには、通常の **[Docker サポートを有効にする]** オプションは表示されません。  Kubernetes 用のコンテナー アプリケーションでは、既定で Docker のサポートが有効です。

::: moniker range="vs-2017"

![Web アプリの選択のスクリーンショット](media/tutorial-kubernetes-tools/k8s-tools-web-app-selection-screen.png)

::: moniker-end
::: moniker range=">=vs-2019"

![Web アプリの選択のスクリーンショット](media/tutorial-kubernetes-tools/vs-2019/k8s-tools-web-app-selection-screen-2019.png)

::: moniker-end

## <a name="add-kubernetes-support-to-an-existing-project"></a>既存のプロジェクトに Kubernetes のサポートを追加する

または、既存の ASP.NET Core Web アプリケーション プロジェクトに Kubernetes のサポートを追加することもできます。 これを行うには、プロジェクトを右クリックし、 **[追加]**  >  **[コンテナー オーケストレーター サポート]** を選択します。

::: moniker range="vs-2017"

![[追加] の [コンテナー オーケストレーター サポート] メニュー項目のスクリーンショット](media/tutorial-kubernetes-tools/k8s-tools-add-container-orchestrator.png)

::: moniker-end
::: moniker range=">=vs-2019"

![[追加] の [コンテナー オーケストレーター サポート] メニュー項目のスクリーンショット](media/tutorial-kubernetes-tools/vs-2019/k8s-tools-add-container-orchestrator-2019.png)

::: moniker-end

ダイアログ ボックスで **[Kubernetes/Helm]** を選択し、 **[OK]** を選択します。

![[コンテナー オーケストレーターの追加] ダイアログ ボックスのスクリーンショット](media/tutorial-kubernetes-tools/k8s-tools-add-container-orchestrator-dialog-box.PNG)

## <a name="what-visual-studio-creates-for-you"></a>Visual Studio で自動的に作成される内容

新しい **Kubernetes 用のコンテナー アプリケーション** プロジェクトを作成するか、既存のプロジェクトに Kubernetes コンテナー オーケストレーター サポートを追加すると、Kubernetes への展開が容易になるいくつかの追加ファイルがプロジェクトに表示されます。

::: moniker range="vs-2017"

![コンテナー オーケストレーター サポートを追加した後のソリューション エクスプローラーのスクリーンショット](media/tutorial-kubernetes-tools/k8s-tools-solution-explorer.png)

::: moniker-end
::: moniker range="vs-2019"

![コンテナー オーケストレーター サポートを追加した後のソリューション エクスプローラーのスクリーンショット](media/tutorial-kubernetes-tools/vs-2019/k8s-tools-solution-explorer-2019.png)

::: moniker-end

追加されるファイルは次のとおりです。

- Dockerfile。この Web アプリケーションをホストしている Docker コンテナー イメージを生成することができます。 ご覧のように、Visual Studio ツールではデバッグ時と Kubernetes への展開時にこの Dockerfile が利用されます。 Docker イメージを直接操作する場合は、Dockerfile を右クリックし、 **[Docker イメージのビルド]** を選択します。

   ![[Docker イメージのビルド] オプションのスクリーンショット](media/tutorial-kubernetes-tools/k8s-tools-build-docker-image.png)

- Helm グラフと *charts* フォルダー。 これらの yaml ファイルで、アプリケーションの Helm グラフが構成されます。これを使用して、Kubernetes に展開できます。 Helm の詳細については、[https://www.helm.sh](https://www.helm.sh) を参照してください。

- *azds.yaml*。 これには Azure Dev Spaces の設定が含まれており、Azure Kubernetes Service での反復的なデバッグ エクスペリエンスが高速になります。 詳細については、[Azure Dev Spaces のドキュメント](/azure/dev-spaces/azure-dev-spaces)を参照してください。

::: moniker range="vs-2017"

## <a name="publish-to-azure-kubernetes-service-aks"></a>Azure Kubernetes Service (AKS) に発行する

これらのファイルがすべて配置されたら、Visual Studio IDE を使用して、通常どおりにアプリケーション コードを記述およびデバッグできます。 また、[Azure Dev Spaces](/azure/dev-spaces/) を使用して、AKS クラスターでコードをすばやく実行し、ライブ実行されているコードをデバッグすることもできます。 詳細については、[Azure Dev Spaces のチュートリアル](/azure/dev-spaces/get-started-netcore-visualstudio)を参照してください。

目的の方法でコードを実行したら、Visual Studio から AKS クラスターに直接発行できます。

これを行うには、まず、AKS への発行の項目以下にある「[必須コンポーネント](#prerequisites)」セクションの説明に従って、すべてがインストールされていることを再確認し、リンクに記載されているすべてのコマンド ライン手順を行う必要があります。 次に、コンテナー イメージを Azure Container Registry (ACR) に発行する発行プロファイルを設定します。 AKS では、ACR からコンテナー イメージをプルし、それをクラスターに展開できます。

1. **ソリューション エクスプローラー**で、*プロジェクト*を右クリックし、 **[発行]** を選択します。

   ![[発行] メニュー項目のスクリーンショット](media/tutorial-kubernetes-tools/k8s-tools-publish-project.png)

2. **[発行]** 画面で、発行先として **[コンテナー レジストリ]** を選択し、画面の指示に従ってコンテナー レジストリを選択します。 コンテナー レジストリをまだ持っていない場合は、Visual Studio から **[新しい Azure コンテナー レジストリを作成する]** を選択して作成します。 詳細については、[Azure Container Registry へのコンテナーの発行](hosting-web-apps-in-docker.md)に関する記事を参照してください。

   ![[発行先を選択] 画面のスクリーンショット](media/tutorial-kubernetes-tools/k8s-tools-publish-to-acr.png)

3. ソリューション エクスプローラーに戻り、*ソリューション*を右クリックし、 **[Azure AKS に発行する]** をクリックします。

   ![[Azure AKS に発行する] メニュー項目のスクリーンショット](media/tutorial-kubernetes-tools/k8s-tools-publish-solution.png)

4. 先ほど作成した ACR 発行プロファイルと共に、サブスクリプションと AKS クラスターを選択します。 次に、 **[OK]** をクリックします。

   ![AKS への発行画面のスクリーンショット](media/tutorial-kubernetes-tools/k8s-tools-publish-to-aks.png)

   これにより、 **[Azure AKS に発行する]** 画面が表示されます。

5. **[Helm の構成]** リンクを選択し、サーバー上での Helm グラフのインストールに使用するコマンド ラインを更新します。

   ![[Helm の構成] リンクのスクリーンショット](media/tutorial-kubernetes-tools/k8s-tools-configure-helm.png)

   コマンド ラインの更新は、別の Kubernetes コンテキストやグラフ名など、指定するカスタム コマンド ライン引数がある場合に便利です。

   ![[Helm の構成] 画面のスクリーンショット](media/tutorial-kubernetes-tools/k8s-tools-helm-configure-screen.png)

6. 展開する準備ができたら、 **[発行]** ボタンをクリックしてアプリケーションを AKS に発行します。

   ![Azure AKS への発行画面のスクリーンショット](media/tutorial-kubernetes-tools/k8s-tools-publish-screen.png)

::: moniker-end

おめでとうございます! すべての Kubernetes アプリの開発に Visual Studio のすべての機能を使用できるようになりました。

## <a name="next-steps"></a>次の手順

Azure での Kubernetes 開発の詳細については、[AKS のドキュメント](/azure/aks)を参照してください。

Azure Dev Spaces の詳細については、[Azure Dev Spaces のドキュメント](/azure/dev-spaces/)を参照してください。
