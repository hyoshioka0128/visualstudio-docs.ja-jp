---
title: Azure Functions の概要
description: Visual Studio for Mac での Azure Functions の使用。
author: sayedihashimi
ms.author: sayedha
ms.date: 04/02/2019
ms.technology: vs-ide-install
ms.assetid: 25CD47A4-5B32-4734-8EF3-E24A02AABF29
ms.openlocfilehash: dac6a1c53cea8982a75c7b12661c98f2feb37f83
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/20/2020
ms.locfileid: "73189665"
---
# <a name="introduction-to-azure-functions"></a>Azure Functions の概要

Azure Functions を利用すると、クラウドでイベント ドリブンのコード スニペットつまり関数を作成できます。インフラストラクチャを明示的にプロビジョニングまたは管理する必要はありません。 Azure Functions について詳しくは、[Azure Functions のドキュメント](/azure/azure-functions/)をご覧ください。

## <a name="requirements"></a>必要条件

Azure Function ツールは **Visual Studio for Mac 7.5** 以降に付属しています。

関数を作成して展開するには、Azure サブスクリプションも必要です。 Azure アカウントをお持ちでない場合は、今すぐ無料でサインアップすることができます。サインアップすると、人気のあるサービスへの 12 か月間無料のアクセス、200 ドル分の無料クレジット、25 以上のサービスへの常時無料のアクセスの特典を受けることができます -> [https://azure.com/free](https://azure.com/free/dotnet)。

## <a name="creating-your-first-azure-functions-project"></a>初めての Azure Functions プロジェクトの作成

1. Visual Studio for Mac で **[ファイル]、[新しいソリューション]** の順に選びます。
2. [新しいプロジェクト] ダイアログで、 **[クラウド] > [全般]** から Azure Functions テンプレートを選び、 **[次へ]** をクリックします。

    ![Azure Functions のオプションが表示されている [新しいプロジェクト] ダイアログ](media/azure-functions-image1.png)

3. 使用する最初の Azure Functions テンプレートを選択し、関数名を入力し、 **[次へ]** をクリックします。

    ![Azure Functions のテンプレートが表示されている [新しいプロジェクト] ダイアログ](media/azure-functions-image2.png)

    > [!TIP]
    > バンドルされている Azure Functions のランタイムとテンプレート (CLI) は可能な限り最新であるようにしていますが、必ず古くなります。 新しい Functions プロジェクトを作成する場合、Visual Studio for Mac は CLI の更新プログラムを確認して、次の画像のとおり通知を行います。 更新されたテンプレートをダウンロードするには、単純にボタンをクリックします。
    > ![Azure Functions の更新プログラムが入手可能であることを示す [新しいプロジェクト] ダイアログ](media/azure-functions-update.png)

    次のページでは、選択した関数の種類に応じて、次の図のようにアクセス権などの入力が求められます。

    ![追加のオプションが表示されている [新しいプロジェクト] ダイアログ](media/azure-functions-image3.png)

    さまざまな種類の Azure Functions テンプレート、および各テンプレートの構成に必要なバインド用のプロパティについては、「[使用可能な関数テンプレート](#available-function-templates)」のセクションを参照してください。 この例では、アクセス権が匿名に設定された Http トリガーを使用しています。

4. パラメーターを設定したら、プロジェクトの場所を選択し、 **[作成]** をクリックします。

Visual Studio for Mac によって、既定の関数が含まれる .NET Standard プロジェクトが作成されます。 また、さまざまな **AzureWebJobs** パッケージと、**Newtonsoft.Json** パッケージへの NuGet 参照も含まれます。

![テンプレートからの新しい Azure Function が表示されている Visual Studio for Mac エディター](media/azure-functions-newproj.png)

新しいプロジェクトには次のファイルが含まれます。

* **お使いの関数名.cs**: このクラスには、選択した関数の定型コードが含まれます。 関数名を保持する **FunctionName** 属性と、何が関数をトリガーするかを指定するトリガー属性 (例: HTTP 要求) が含まれます。 関数のメソッドについて詳しくは、「[Azure Functions C# 開発者向けリファレンス](/azure/azure-functions/functions-dotnet-class-library)」をご覧ください。
* **host.json** – このファイルでは、Functions ホストのグローバル構成オプションが記述されています。 ファイルの例と、このファイルで使用可能な設定については、「[Azure Functions の host.json のリファレンス](/azure/azure-functions/functions-host-json)」をご覧ください。
* **local.settings.json** – このファイルには、関数をローカルで実行するためのすべての設定が含まれます。 これらの設定は、Azure Functions Core Tools によって使用されます。 詳細については、Azure Functions Core Tools の記事の[ローカル設定ファイル](/azure/azure-functions/functions-run-local#local-settings-file)に関する記事を参照してください。

Visual Studio for Mac で新しい Azure Functions プロジェクトが作成されたので、ローカル コンピューターから既定の HTTP によってトリガーされる関数をテストできます。

## <a name="testing-the-function-locally"></a>関数のローカルなテスト

Visual Studio for Mac での Azure Functions のサポートを使うと、開発用のローカル コンピューター上で関数をテストおよびデバッグすることができます。

1. 関数をローカルにテストするには、Visual Studio for Mac で **[実行]** ボタンをクリックします。

    ![Visual Studio for Mac のデバッグ開始ボタン](media/azure-functions-run.png)

1. プロジェクトを実行すると、Azure Functions でのローカルなデバッグが開始し、次の図に示すように、新しいターミナル ウィンドウを開きます。

    ![関数の出力が表示されているターミナル ウィンドウ](media/azure-functions-terminal.png)

    出力から URL をコピーします。

3. HTTP 要求の URL をブラウザーのアドレス バーに貼り付けます。 URL の末尾にクエリ文字列 `?name=<yourname>` を追加し、要求を実行します。 次の図は、関数によって返されるローカル GET 要求に対するブラウザーでの応答です。

    ![ブラウザーでの HTTP 要求](media/azure-functions-httpreq.png)

## <a name="adding-another-function-to-your-project"></a>プロジェクトへの別の関数の追加

関数テンプレートを使用すると、最も一般的なトリガーとテンプレートを使って、新しい関数をすばやく作成できます。 別の種類の関数を作成するには、次のようにします。

1. 新しい関数を追加するには、プロジェクト名を右クリックして、 **[追加] > [関数の追加]** を選びます。

    ![新しい関数を追加するコンテキスト アクション](media/azure-functions-addnew.png)

2. **[新しい Azure Function ]** ダイアログで、必要な関数を選びます。

    ![[新しい Azure Function ] ダイアログ](media/azure-functions-image4.png)

    「[使用可能な関数テンプレート](#available-function-templates)」のセクションには、Azure Functions のテンプレート一覧があります。

上記の手順を使用して、複数の関数を関数アプリ プロジェクトに追加できます。 プロジェクト内の各関数で異なるトリガーを使用できますが、1 つの関数には 1 つのトリガーのみを使用する必要があります。 詳しくは、「[Azure Functions でのトリガーとバインドの概念](/azure/azure-functions/functions-triggers-bindings)」をご覧ください。

## <a name="publish-to-azure"></a>Azure に発行する

1. プロジェクト名を右クリックし、 **[発行]、[Azure に発行する]** の順に選択します。![[Azure に発行する] メニュー オプション](media/azure-functions-image5.png)
2. ご自分の Azure アカウントを既に Visual Studio for Mac に接続している場合、利用可能なアプリ サービスの一覧が表示されます。 ログインしていない場合、それを行うよう求められます。
3. **[Azure App Service に発行する]** ダイアログでは、既存のアプリ サービスを選択するか、 **[新規]** をクリックして新しいものを作成することができます。
4. **[新しい App Service を作成する]** ダイアログに設定を入力します。![[Azure に発行する] メニュー オプション](media/azure-functions-image7.png)

    |設定  |Description  |
    |---------|---------|
    |**App Service の名前**|新しい関数アプリを識別する、グローバルに一意な名前。|
    |**サブスクリプション**|使用する Azure サブスクリプション。|
    |**[リソース グループ](/azure/azure-resource-manager/resource-group-overview)**|関数アプリを作成するリソース グループの名前。 新しいリソース グループを作成するには、 **+** を選択します。|
    |**[サービス プラン](/azure/azure-functions/functions-scale)**|既存のプランを選択するか、カスタム プランを作成します。 ご自分の近くのリージョン、またはご使用の関数がアクセスする他のサービスに近い場所を選択します。|

5. **[次へ]** をクリックし、ストレージ アカウントを作成します。 Functions ランタイムには Azure Storage アカウントが必要です。 **[カスタム]** をクリックし、汎用のストレージ アカウントを作成するか、既存のものを使用します。

    ![[Azure に発行する] メニュー オプション](media/azure-functions-image8.png)

6. **[作成]** をクリックして、これらの設定で Azure に関数アプリと関連リソースを作成し、関数プロジェクト コードをデプロイします。

7. 発行時に "Azure で関数のバージョンを更新する" ことを求めるダイアログが表示される場合があります。 **[はい]** をクリックします。

    ![[Azure に発行する] メニュー オプション](media/azure-functions-image12.png)

## <a name="function-app-settings"></a>Function App の設定

Local.settings.json で追加したすべての設定は、Azure の関数アプリにも追加する必要があります。 プロジェクトを発行するとき、これらの設定は自動的にアップロードされません。

アプリの設定にアクセスするには、[https://ms.portal.azure.com/](https://ms.portal.azure.com/) の Azure portal にアクセスします。 **[Functions アプリ]** の **[Functions アプリ]** を選択し、関数名を強調表示します。

![Azure Functions のメニュー](media/azure-functions-image9.png)

**[概要]** タブで **[構成済みの機能]** の下から **[アプリケーションの設定]** を選択します。

![Azure 関数の [概要] タブ](media/azure-functions-image10.png)

ここから関数アプリのアプリケーション設定を行うことができます。ここでは、新しいアプリケーションの設定を追加したり、既存のものを変更することができます。

![Azure portal のアプリケーションの設定領域](media/azure-functions-image11.png)

設定する必要のある重要な設定の 1 つに、`FUNCTIONS_EXTENSION_VERSION` があります。 この値は、Visual Studio for Mac から発行する場合、**beta** に設定する必要があります。

## <a name="available-function-templates"></a>使用可能な関数テンプレート

- **GitHub トリガー** – GitHub リポジトリで発生するイベントに応答します。 詳しくは、[GitHub についての Azure Functions の記事](/azure/azure-functions/functions-create-github-webhook-triggered-function)をご覧ください。
  - GitHub コメンター – この関数は、問題または pull request の GitHub webhook を受信してコメントを追加すると実行されます。
  - GitHub WebHook – この関数は、GitHub webhook を受信すると実行されます。

- **HTTP** – HTTP 要求を使って、コードの実行をトリガーします。 次の HTTP トリガーに対する明示的なテンプレートがあります。
  - HTTP トリガー
  - Http GET CRUD
  - Http POST CRUD
  - パラメーター付き HTTP トリガー

- **タイマー**: 定義されているスケジュールに基づいて、クリーンアップまたは他のバッチ タスクを実行します。 このテンプレートは名前とスケジュールの 2 つのフィールドを受け取ります。6 フィールドの CRON 式です。 詳しくは、[タイマーについての Azure Functions の記事](/azure/azure-functions/functions-create-scheduled-function)をご覧ください。

- **キュー トリガー** – これは、Azure Storage キューに届いたメッセージに応答する関数です。 このテンプレートは、関数名だけでなく、**パス** (メッセージが読み取られるキューの名前) とストレージ アカウント**接続** (ストレージ アカウント接続文字列を含むアプリ設定の名前) を受け取ります。 詳しくは、[Queue Storage についての Azure Functions の記事](/azure/azure-functions/functions-create-storage-queue-triggered-function)をご覧ください。

- **BLOB トリガー** – Azure Storage Blob がコンテナーに追加されるとそれを処理します。 このテンプレートは、関数名だけでなく、パスと接続のプロパティも受け取ります。 パス プロパティは、トリガーが監視するストレージ アカウント内のパスです。 接続アカウントは、ストレージ アカウント接続文字列が含まれるアプリ設定の名前です。 詳しくは、[Blob Storage についての Azure Functions の記事](/azure/azure-functions/functions-create-storage-blob-triggered-function)をご覧ください。

- **汎用 webhook** – これは、webhook をサポートするサービスから要求を受信するたびに実行される単純な関数です。 詳細については、[汎用 webhook についての Azure Functions の記事](/azure/azure-functions/functions-create-generic-webhook-triggered-function)をご覧ください。

- **Durable Functions オーケストレーション** – Durable Functions を使うと、サーバーレス環境でステートフル関数を記述できます。 この拡張機能は状態、チェックポイント、再起動を管理します。 詳細については、[Durable Functions](/azure/azure-functions/durable-functions-overview)に関する Azure Functions ガイドをご覧ください。

- **イメージ リサイザー** – この関数は、コンテナーに BLOB が追加されるたびに異なるサイズのイメージを作成します。 このテンプレートは、トリガーに対するパスと接続文字列、小さいイメージ出力、および中くらいのイメージ出力を受け取ります。

- **SAS トークン** – この関数は、特定の Azure Storage コンテナーおよび BLOB 名に対して SAS トークンを生成します。 このテンプレートは、関数名だけでなく、パスと接続のプロパティも受け取ります。 パス プロパティは、トリガーが監視するストレージ アカウント内のパスです。 接続アカウントは、ストレージ アカウント接続文字列が含まれるアプリ設定の名前です。 **アクセス権**も設定する必要があります。 承認レベルは、関数に API キーが必要かどうか、および使用するキーを制御します。関数は関数キーを使います。管理者は、マスター キーを使います。 詳しくは、「[C# Azure Function for generating SAS tokens](https://github.com/Azure-Samples/functions-dotnet-sas-token/)」(SAS トークンを生成するための C# Azure Function) サンプルをご覧ください。
