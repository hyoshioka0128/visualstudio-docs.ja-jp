---
title: Node.js アプリを Linux App Service に発行する
description: Visual Studio で作成した Node.js アプリケーションを、Azure 上の Linux App Service に発行できます
ms.date: 11/22/2019
ms.topic: tutorial
ms.devlang: javascript
author: mikejo5000
ms.author: mikejo
manager: jmartens
dev_langs:
- JavaScript
ms.workload:
- nodejs
ms.openlocfilehash: c83516891a33a026399a6e5fcfc2458b5e03a0bd
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99945436"
---
# <a name="publish-a-nodejs-application-to-azure-linux-app-service"></a>Node.js アプリケーションを Azure (Linux App Service) に発行する

このチュートリアルでは、簡単な Node.js アプリケーションを作成して Azure に発行するタスクの手順を説明します。

Azure に Node.js アプリケーションを発行するときは、いくつかのオプションがあります。 たとえば、Azure App Service、ユーザーが選択した OS を実行している VM、Kubernetes での管理のための Azure Container Service (AKS)、Docker を使用するコンテナー インスタンスなどで、それ以外にもあります。 これらの各オプションの詳細については、「[コンピューティング](https://azure.microsoft.com/product-categories/compute/)」をご覧ください。

このチュートリアルでは、アプリを [Linux App Service](/azure/app-service/containers/app-service-linux-intro) にデプロイします。
Linux App Service は、Node.js アプリケーションを実行するために Linux Docker コンテナーをデプロイします (Windows 上の IIS の背後で Node.js アプリを実行する Windows アプリ サービスとはその点が異なります)。

このチュートリアルでは、Node.js Tools for Visual Studio と共にインストールされるテンプレートから Node.js アプリケーションを作成し、GitHub 上のリポジトリにコードをプッシュした後、GitHub リポジトリからデプロイできるように Azure Web ポータルを使って Azure App Service をプロビジョニングする方法を示します。 コマンド ラインを使って Azure App Service をプロビジョニングし、ローカルの Git リポジトリからコードをプッシュする方法については、[Node.js アプリの作成](/azure/app-service/containers/quickstart-nodejs)に関するページをご覧ください。

このチュートリアルでは、次の作業を行う方法について説明します。
> [!div class="checklist"]
> * Node.js プロジェクトを作成する
> * コード用の GitHub リポジトリを作成する
> * Azure に Linux App Service を作成する
> * Linux にデプロイする

## <a name="prerequisites"></a>必須コンポーネント

* Visual Studio および Node.js 開発ワークロードをインストールしている必要があります。

    ::: moniker range=">=vs-2019"
    Visual Studio 2019 をまだインストールしていない場合は、[Visual Studio のダウンロード](https://visualstudio.microsoft.com/downloads/) ページに移動し、無料試用版をインストールしてください。
    ::: moniker-end
    ::: moniker range="vs-2017"
    Visual Studio 2017 をまだインストールしていない場合は、[Visual Studio のダウンロード](https://visualstudio.microsoft.com/downloads/) ページに移動し、無料試用版をインストールしてください。
    ::: moniker-end

    Visual Studio は既にあり、ワークロードだけをインストールする必要がある場合は、 **[ツール]**  >  **[ツールと機能を取得]** に移動すると、Visual Studio インストーラーが開きます。 **[Node.js 開発]** ワークロードを選択し、 **[変更]** を選択します。

    ![VS インストーラーの Node.js ワークロード](../ide/media/quickstart-nodejs-workload.png)

* Node.js ランタイムをインストールしている必要があります。

    インストールされていない場合は、LTS バージョンを [Node.js](https://nodejs.org/en/download/) Web サイトからインストールしてください。 一般に、Visual Studio はインストール済みの Node.js ランタイムを自動的に検出します。 インストールされているランタイムが検出されない場合は、プロパティ ページで、インストールされているランタイムを参照するプロジェクトを構成することができます (プロジェクトを作成した後、プロジェクト ノードを右クリックして、 **[プロパティ]** を選択します)。

## <a name="create-a-nodejs-project-to-run-in-azure"></a>Azure 内で実行するための Node.js プロジェクトを作成する

1. Visual Studio を開きます。

1. 新しい TypeScript Express アプリを作成します。

    ::: moniker range=">=vs-2019"
    **Esc** キーを押してスタート ウィンドウを閉じます。 **Ctrl + Q** キーを押して検索ボックスを開き、「**Node.js**」と入力してから、 **[新しい基本の Azure Node.js Express 4 アプリケーション プロジェクトの作成]** (TypeScript) を選択します。 表示されたダイアログ ボックスで、 **[作成]** を選択します。
    ::: moniker-end
    ::: moniker range="vs-2017"
    上部のメニュー バーから、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** の順に選択します。 **[新しいプロジェクト]** ダイアログ ボックスの左側のウィンドウで、 **[TypeScript]** を展開して、 **[Node.js]** を選択します。 真ん中のウィンドウで **[基本の Azure Node.js Express 4 アプリケーション]** を選択し、 **[OK]** を選択します。

    ![新しい TypeScript Express アプリを作成する](../javascript/media/azure-ts-express-app.png)
    ::: moniker-end
    **[基本の Azure Node.js Express 4 アプリケーション]** プロジェクト テンプレートが表示されない場合は、**Node.js 開発** ワークロードを追加する必要があります。 手順について詳しくは、「[必須コンポーネント](#prerequisites)」をご覧ください。

    Visual Studio によってプロジェクトが作成され、それがソリューション エクスプローラー (右側のウィンドウ) で開かれます。

1. **F5** キーを押してアプリをビルドして実行し、すべてが想定どおり実行していることを確認します。

1. **[ファイル]**  >  **[ソース管理に追加]** を選択して、プロジェクト用にローカル Git リポジトリを作成します。

    この時点で、Express フレームワークを使用する、TypeScript で記述された Node.js アプリが動作するようになり、ローカル ソース管理にチェックインされます。

1. 次の手順に進む前に、必要に応じてプロジェクトを編集します。

## <a name="push-code-from-visual-studio-to-github"></a>Visual Studio から GitHub にコードをプッシュする

Visual Studio 用に GitHub を設定するには:

1. **[ツール]**  >  **[拡張機能と更新プログラム]** メニュー項目を使って、[Visual Studio 向け GitHub 拡張](https://visualstudio.github.com/)がインストールされて有効になっていることを確認します。

2. メニューから **[表示]**  >  **[その他のウィンドウ]**  >  **[GitHub]** の順に選択します。

    [GitHub] ウィンドウが開きます。

3. [GitHub] ウィンドウに **[作業の開始]** ボタンが表示されない場合は、 **[ファイル]**  >  **[ソース管理に追加]** をクリックして、UI が更新されるまで待ちます。

    ![[GitHub] ウィンドウを開く](../javascript/media/azure-github-get-started.png)

4. **[作業の開始]** をクリックする。

    GitHub に既に接続している場合、次の図のようなツールボックスが表示されます。

    ![GitHub リポジトリの設定](../javascript/media/azure-github-publish.png)

5. 発行する新しいリポジトリのフィールドを入力して、 **[発行]** をクリックします。

    しばらくすると、"リポジトリが正常に作成されました" と表示されます。

    次のセクションでは、このリポジトリから Linux 上の Azure App Service に発行する方法について説明します。

## <a name="create-a-linux-app-service-in-azure"></a>Azure に Linux App Service を作成する

1. [Azure Portal](https://portal.azure.com) にサインインします。

2. 左側のサービスの一覧から **[App Services]** を選び、 **[追加]** をクリックします。

3. 必要な場合は、新しいアプリをホストするための新しいリソース グループと App Service プランを作成します。

4. 次の図に示すように、 **[OS]** を **[Linux]** に設定し、 **[ランタイム スタック]** を必要な Node.js のバージョンに設定します。

    ![Linux App Service を作成する](../javascript/media/azure-create-appservice-annotated.png)

5. **[作成]** をクリックして、App Service を作成します。

    デプロイに数分かかる場合があります。

6. デプロイが済んだ後、 **[アプリケーション設定]** セクションに移動し、`SCM_SCRIPT_GENERATOR_ARGS` という名前と `--node` という値で設定を追加します。

    ![アプリケーションの設定](../javascript/media/azure-script-generator-args.png)

    > [!WARNING]
    > App Service のデプロイ プロセスは、ヒューリスティックのセットを使って、試して実行するアプリケーションの種類を決定します。 デプロイされるコンテンツで *sln* ファイルが検出された場合、プロセスは MSBuild ベースのプロジェクトがデプロイされているものと想定します。 上で追加した設定はこのロジックをオーバーライドし、これが Node.js アプリケーションであることを明示的に指定します。 この設定がない場合、App Service にデプロイされるリポジトリに *sln* ファイルが含まれる場合、Node.js アプリケーションの展開は失敗します。

7. **[アプリケーションの設定]** で、名前が `WEBSITE_NODE_DEFAULT_VERSION` で値が `8.9.0` の別の設定を追加します。

8. 展開後、App Service を開き、 **[デプロイ オプション]** を選択します。

    ![配置オプション](../javascript/media/azure-deployment-options.png)

9. **[ソースの選択]** をクリックし、 **[GitHub]** を選んで、必要なアクセス許可を構成します。

    ![GitHub のアクセス許可](../javascript/media/azure-choose-source.png)

10. 発行するリポジトリとブランチを選択して、 **[OK]** を選択します。

    ![Linux App Service に発行する](../javascript/media/azure-repo-and-branch.png)

    同期中に **デプロイ オプション** ページが表示されます。

    ![GitHub でのデプロイと同期](../javascript/media/azure-deployment-options-sync.png)

    同期が完了すると、チェック マークが表示されます。

    サイトが GitHub リポジトリからの Node.js アプリケーションを実行するようになり、Azure App Service に対して作成された URL (既定では、Azure App Service に指定した名前の後に ". azurewebsites.net" が付いたもの) でアクセスできます。

## <a name="modify-your-app-and-push-changes"></a>アプリを変更して変更をプッシュする

1. 次に示すコードを、*app.ts* の行 `app.use('/users', users);` の後に追加します。 これにより、URL */api* の REST API が追加されます。

    ```typescript
    app.use('/api', (req, res, next) => {
        res.json({"result": "success"});
    });
    ```

2. コードをビルドしてローカルにテストした後、チェックインして GitHub にプッシュします。

    しばらくすると Azure portal で GitHub リポジトリの変更が検出され、デプロイの新しい同期が開始されます。 次の図のように表示されます。

    ![変更と同期](../javascript/media/azure-changes-detected.png)

3. デプロイが完了した後、パブリック サイトに移動し、URL に */api* を追加します。 JSON 応答が返されます。

## <a name="troubleshooting"></a>トラブルシューティング

* node.exe が強制終了 (つまり、ハンドルされない例外の発生) を処理する場合、コンテナーは再起動します。
* コンテナーは開始時に、さまざまなヒューリスティックを実行して、Node.js プロセスを開始する方法を明らかにします。 実装の詳細は、[generateStartupCommand.js](https://github.com/Azure/app-service-builtin-images/blob/master/node/8.9.4/startup/generateStartupCommand.js) で見ることができます。
* SSH を使って実行中のコンテナーに接続して調査できます。 これは、Azure portal を使って簡単に行うことができます。 App Service を選択し、ツールの一覧で **[開発ツール]** セクションの **[SSH]** まで下にスクロールします。
* トラブルシューティングに役立てるには、App Service の **[診断ログ]** 設定に移動し、 **[Docker コンテナー ログ]** の設定を **[オフ]** から **[ファイル システム]** に変更します。 ログは、 */home/LogFiles/* _docker.log* の下のコンテナーに作成され、SSH または FTP(S) を使ってボックスでアクセスできます。
* 既定で割り当てられる *.azurewebsites.net という URL の代わりに、カスタム ドメイン名をサイトに割り当てることができます。 詳細については、[カスタム ドメインのマップ](/azure/app-service/app-service-web-tutorial-custom-domain)に関するページをご覧ください。
* 運用環境に移行する前にステージング サイトにデプロイしてさらにテストを行うのがベスト プラクティスです。 その構成方法の詳細については、[ステージング環境の作成](/azure/app-service/web-sites-staged-publishing)に関するページをご覧ください。
* よくあるご質問については、[Linux での App Service の FAQ](/azure/app-service/containers/app-service-linux-faq) に関するページをご覧ください。

## <a name="next-steps"></a>次の手順

このチュートリアルでは、Linux App Service を作成し、Node.js アプリケーションをサービスにデプロイする方法を説明しました。 Linux App Service についてさらに学習してください。

> [!div class="nextstepaction"]
> [Linux App Service](/azure/app-service/containers/app-service-linux-intro)
