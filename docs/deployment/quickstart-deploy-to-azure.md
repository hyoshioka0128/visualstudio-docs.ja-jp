---
title: Azure App Service に発行する
ms.date: 01/29/2019
ms.topic: quickstart
helpviewer_keywords:
- deployment, website
ms.assetid: fc82b1f1-d342-4b82-9a44-590479f0a895
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- azure
ms.openlocfilehash: 4bbff0c2d149afddc355afe5f6c93e9d0aea54c0
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/20/2020
ms.locfileid: "72806913"
---
# <a name="publish-a-web-app-to-azure-app-service-using-visual-studio"></a>Visual Studio を使用して Azure App Service に Web アプリを発行する

ASP.NET、ASP.NET Core、Node.js、および .NET Core アプリの場合、次のいずれかの方法を使用して、Azure App Service または Azure App Service Linux (コンテナーを使用) に発行します。

* アプリの継続的 (または自動的) なデプロイの場合は、[Azure Pipelines](/azure/devops/pipelines/get-started-yaml?view=azdevops) で Azure DevOps を使用します。

* アプリの 1 回限り (または手動) のデプロイの場合は、Visual Studio の**発行**ツールを使用して、Azure App Service または App Service for Linux (コンテナーを使用) に ASP.NET、ASP.NET Core、Node.js、および .NET Core アプリをデプロイします。 Python アプリの場合は、[Python - Azure App Service への発行](../python/publishing-python-web-applications-to-azure-from-visual-studio.md)に関するページの手順に従います。

この記事では、1 回限りのデプロイに**発行**ツールを使用する方法について説明します。

[!INCLUDE [quickstart-prereqs-azure](includes/quickstart-prereqs-azure.md)]

## <a name="publish-to-azure-app-service"></a>Azure App Service に発行する

1. ソリューション エクスプローラーで、プロジェクトを右クリックして、**[発行]** を選択します (または **[ビルド]** > **[発行]** メニュー項目を使用します)。

    ![ソリューション エクスプローラーのプロジェクト コンテキスト メニューにある [発行] コマンド](../deployment/media/quickstart-publish.png "[発行] を選択する")

1. 以前に発行プロファイルを構成した場合、**[発行]** ウィンドウが表示されます。その場合は、**[新しいプロファイルの作成]** を選択します。

1. **[発行先を選択]** ダイアログ ボックスで、**[App Service]** を選びます。

    ![Azure App Service を選ぶ](../deployment/media/quickstart-publish-azure.png "Azure App Service を選ぶ")

1. **[発行]** を選択します。 **[App Service の作成]** ダイアログ ボックスが表示されます。 必要に応じて、Azure アカウントでサインインすると、既定のアプリ サービス設定がフィールドに取り込まれます。

    ![App Service の作成](../deployment/media/quickstart-publish-settings-app-service.png "Azure App Service を作成する")

1. **作成** を選択します。 Visual Studio によってアプリが Azure App Service にデプロイされ、ブラウザに Web アプリが読み込まれます。 プロジェクト プロパティの **[発行]** ウィンドウに、サイト URL とその他の詳細が示されます。

    ![プロファイルの概要を示す [発行] プロパティ ウィンドウ](../deployment/media/quickstart-publish-app-service-summary.png)

## <a name="clean-up-resources"></a>リソースをクリーンアップする

前の手順では、リソース グループ内に Azure リソースを作成しました。 これらのリソースが将来必要になると思わない場合は、リソース グループを削除してリソースを削除できます。
Azure Portal の左側のメニューで、**[リソース グループ]**、**[myResourceGroup]** の順に選択します。
リソース グループのページで、一覧表示されたリソースが、削除しようとするリソースであることを確認します。
**[削除]** を選択し、テキスト ボックスに「**myResourceGroup**」と入力してから、**[削除]** を選択します。

## <a name="next-steps"></a>次のステップ

このクイック スタートでは、Visual Studio を使用して、Azure にデプロイするための発行プロファイルを作成する方法を学習しました。 Azure App Service から発行設定をインポートして、発行プロファイルを構成することもできます。

> [!div class="nextstepaction"]
> [発行設定のインポートと Azure へのデプロイ](tutorial-import-publish-settings-azure.md)
