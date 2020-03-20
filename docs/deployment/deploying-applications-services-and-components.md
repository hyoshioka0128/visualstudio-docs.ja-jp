---
title: 配置でのはじめに
description: Visual Studio からアプリを配置する際の選択肢について説明します。
ms.custom: mvc
ms.date: 01/29/2019
ms.topic: quickstart
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- .NET applications, deploying
- components [Visual Studio], deploying
- installers
- publishing
- deploying applications [Visual Studio]
- deploying applications [Visual Studio], about deploying applications
- components [.NET Framework], deploying
ms.assetid: 63fcdd5b-2e54-4210-9038-65bc23167725
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 006ecdffd7b109c32f7063fee5f454e43c6c4597
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/20/2020
ms.locfileid: "72806916"
---
# <a name="first-look-at-deployment-in-visual-studio"></a>Visual Studio での配置の概要

他のコンピューター、デバイス、サーバー、クラウドにインストールする目的でアプリケーション、サービス、またはコンポーネントを配布する手法として配置が行われます。 必要な配置の種類に合わせて、Visual Studio で適切な手法を選択します。 (コマンド ラインによる配置など、その他の配置ツールに対応しているアプリの種類はたくさんありますが、それらのツールについてはここでは触れていません。)

詳細な配置手順については、クイックスタートとチュートリアルをご覧ください。 配置オプションの概要については、「[状況に適した発行オプション](deploying-applications-services-and-components-resources.md#what-publishing-options-are-right-for-me)」を参照してください。

## <a name="deploy-to-local-folder"></a>ローカル フォルダーに配置する

ローカル フォルダーへの配置は通常、テスト目的で使用されます。あるいは、最終的な配置に別のツールを使用する段階式配置を開始する目的で使用されます。

- **ASP.NET**、**ASP.NET Core**、**Node.js**、**Python**、.**NET Core**:発行ツールを使用して、ローカル フォルダーに配置します。 利用できるオプションは厳密にはアプリの種類によって異なります。 ソリューション エクスプローラーで、プロジェクトを右クリックし、 **[発行]** を選択します。 (発行プロファイルを以前に構成していない場合、 **[新しいプロファイルの作成]** をクリックする必要があります。)次に **[フォルダー]** を選択します。 詳細については、「[ローカル フォルダーに配置する](quickstart-deploy-to-local-folder.md)」を参照してください

    ![[発行] を選択する](../deployment/media/quickstart-publish.png)

- **Windows デスクトップ**: ClickOnce 配置を使用し、フォルダーに Windows デスクトップ アプリケーションを発行できます。 その後、ユーザーはシングル クリックでアプリケーションをインストールできます。 詳細については、[ClickOnce を使用したデスクトップ アプリの配置](how-to-publish-a-clickonce-application-using-the-publish-wizard.md)に関するページ (C# と Visual Basic) を参照してください。 C++/CLI については、[ClickOnce を使用したネイティブ アプリの配置](/cpp/windows/clickonce-deployment-for-visual-cpp-applications)に関するページを、C/C++ については、[セットアップ プロジェクトを使用したネイティブ アプリの配置](/cpp/windows/walkthrough-deploying-a-visual-cpp-application-by-using-a-setup-project)に関するページを参照してください。

## <a name="publish-to-azure"></a>Azure に発行する

- **ASP.NET**、**ASP.NET Core**、**Python**、**Node.js**:次のいずれかの方法を使用して、Azure App Service または Azure App Service Linux (コンテナーを使用) に発行します。

  - アプリの継続的 (または自動的) なデプロイの場合は、[Azure Pipelines](/azure/devops/pipelines/get-started-yaml?view=azdevops) で Azure DevOps を使用します。

  - アプリを一回だけ (手動で) 配置する場合、Visual Studio の **[発行]** ツールを使用します。

  サーバー構成のカスタマイズ機能が多い配置の場合、 **[発行]** ツールを使用し、Azure Virtual Machine にアプリを配置することもできます。

  **[発行]** ツールを使用するには、ソリューション エクスプローラーでプロジェクトを右クリックし、 **[発行]** を選択します。 (発行プロファイルを以前に構成している場合、 **[新しいプロファイルの作成]** をクリックする必要があります。)[発行] ダイアログ ボックスで、 **[App Service]** または **[Azure Virtual Machines]** を選択し、構成手順に従います。

  ![Azure App Service を選ぶ](../deployment/media/quickstart-publish-azure.png "Azure App Service を選ぶ")

  Visual Studio 2017 バージョン 15.7 以降では、ASP.NET Core アプリを **Linux 用 App Service** に配置できます。

  Python アプリについては、[Python で Azure App Service に発行する](../python/publishing-python-web-applications-to-azure-from-visual-studio.md?toc=/visualstudio/deployment/toc.json&bc=/visualstudio/deployment/_breadcrumb/toc.json)方法に関するページも参照してください。

  概要については、[Azure に発行する方法](quickstart-deploy-to-azure.md)に関するページと [Linux に発行する方法](quickstart-deploy-to-linux.md)に関するページを参照してください。 [Azure に ASP.NET Core アプリを発行する](/aspnet/core/tutorials/publish-to-azure-webapp-using-vs)方法に関するページも参照してください。 Git を使用した配置については、[Git を使用して Azure に ASP.NET Core を継続的に配置する](/aspnet/core/publishing/azure-continuous-deployment)方法に関するページを参照してください。

  Azure App Service から Visual Studio に発行プロファイルをインポートする方法については、[発行設定のインポートと Azure へのデプロイ](../deployment/tutorial-import-publish-settings-azure.md)に関するページを参照してください。

  > [!NOTE]
  > Azure アカウントをお持ちでない場合、[こちらから新規登録](https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=doc&utm_campaign=visualstudio)できます。

## <a name="publish-to-web-or-deploy-to-network-share"></a>Web に発行するか、ネットワーク共有に配置する

- **ASP.NET**、**ASP.NET Core**、**Node.js**、**Python**:発行ツールを使用することで、FTP または Web 配置を使って Web サイトに配置できます。 詳細については、[Web サイトに配置する](quickstart-deploy-to-a-web-site.md)方法に関するページを参照してください。

    ソリューション エクスプローラーで、プロジェクトを右クリックして、 **[発行]** を選択します。 (発行プロファイルを以前に構成している場合、 **[新しいプロファイルの作成]** をクリックする必要があります。)発行ツールで、必要なオプションを選択し、構成手順に従います。

    ![IIS や FTP などを選択します。](../deployment/media/quickstart-publish-iis-ftp.png)

    Visual Studio に発行プロファイルをインポートする方法については、[発行設定のインポートと IIS への配置](../deployment/tutorial-import-publish-settings-iis.md)に関するページを参照してください。

    ASP.NET のアプリケーションとサービスは他にもさまざまな方法で配置できます。 詳細については、[ASP.NET の Web アプリケーション/サービスを配置する](/aspnet/mvc/overview/deployment/)方法に関するページをご覧ください。

- **Windows デスクトップ**: ClickOnce 配置を使用し、Web サーバーまたはネットワーク ファイル共有に Windows デスクトップ アプリケーションを発行できます。 その後、ユーザーはシングル クリックでアプリケーションをインストールできます。 詳細については、[ClickOnce を使用したデスクトップ アプリの配置](how-to-publish-a-clickonce-application-using-the-publish-wizard.md)に関するページ (C# と Visual Basic) を参照してください。 C++/CLI については、[ClickOnce を使用したネイティブ アプリの配置](/cpp/windows/clickonce-deployment-for-visual-cpp-applications)に関するページを、C/C++ については、[セットアップ プロジェクトを使用したネイティブ アプリの配置](/cpp/windows/walkthrough-deploying-a-visual-cpp-application-by-using-a-setup-project)に関するページを参照してください。

## <a name="publish-to-microsoft-store"></a>Microsoft Store に発行する

Visual Studio から、Microsoft Store に配置するためのアプリ パッケージを作成できます。

- **UWP**:アプリをパッケージ化し、メニュー項目を使用してそれを配置できます。 詳細については、[Visual Studio を使用して UWP アプリをパッケージ化する](/windows/uwp/packaging/packaging-uwp-apps)方法に関するページをご覧ください。

    ![アプリケーション パッケージの作成](../deployment/media/feature-tour-create-app-package.jpg)

- **Windows デスクトップ**:Visual Studio 2017 バージョン 15.4 以降では、Microsoft Store に配置できます。 これを行うには、まず Windows アプリケーション パッケージ プロジェクトを作成します。 詳細については、「[Microsoft ストアのデスクトップ アプリをパッケージ化する](/windows/msix/desktop/desktop-to-uwp-packaging-dot-net)」を参照してください。

    ![デスクトップ アプリをパッケージ化する](../deployment/media/feature-tour-desktop-bridge.png)

## <a name="deploy-net-packages-to-nugetorg"></a>.NET パッケージを NuGet.org に配置する

これらのパッケージを使用するプロジェクトで必要とされる他のコンテンツと共にコンパイル済みのコードを (DLL として) 含む "パッケージ" にバンドルされたコードを配置するには、Visual Studio を使用して NuGet パッケージと CLI ツールを作成し、最終デプロイ コマンドを発行します。

- [.NET Standard パッケージの作成と公開](/nuget/quickstart/create-and-publish-a-package-using-visual-studio)
- [.NET Framework パッケージの作成と公開](/nuget/quickstart/create-and-publish-a-package-using-visual-studio-net-framework)

## <a name="deploy-to-a-device-uwp"></a>デバイスに配置する (UWP)

デバイスでテストする目的で UWP アプリを配置する場合、[Visual Studio からリモート コンピューター上で UWP アプリを実行する](../debugger/run-windows-store-apps-on-a-remote-machine.md)方法に関するページを参照してください。

## <a name="create-an-installer-package-windows-desktop"></a>インストーラー パッケージを作成する (Windows デスクトップ)

デスクトップ アプリケーションを [ClickOnce](how-to-publish-a-clickonce-application-using-the-publish-wizard.md) でできることよりも複雑な方法でインストールする必要がある場合、Windows インストーラー パッケージ (MSI または EXE インストール ファイル) またはカスタム ブートストラップを作成できます。

- MSI ベースのインストーラー パッケージを [WiX Toolset Extension](https://marketplace.visualstudio.com/items?itemName=WixToolset.WiXToolset) を使用して作成できます。 これはコマンドライン ツールセットです。

   ::: moniker range=">=vs-2019"
   Visual Studio 2019 については、[WiX Toolset Visual Studio 2019 Extension](https://marketplace.visualstudio.com/items?itemName=WixToolset.WixToolsetVisualStudio2019Extension) を取得します。
   ::: moniker-end

- MSI または EXE インストーラー パッケージは Flexera Software の [InstallShield](https://www.flexerasoftware.com/producer/products/software-installation/installshield-software-installer/tab/requirements) を使用して作成できます。 InstallShield は Visual Studio 2017 以降のバージョンで使用できます (Community Edition はサポートされていません)。 InstallShield Limited Edition は Visual Studio に含まれなくなっており、Visual Studio 2017 以降のバージョンではサポートされていないことに注意してください。今後の使用可能性については、[Flexera Software](https://info.flexerasoftware.com/IS-EVAL-InstallShield-Limited-Edition-Visual-Studio) にお問い合わせください。

- MSI または EXE インストーラー パッケージはセットアップ プロジェクト (vdproj) を使用して作成できます。 このオプションを使用するには、[Visual Studio Installer Projects 拡張機能](https://marketplace.visualstudio.com/items?itemName=VisualStudioProductTeam.MicrosoftVisualStudio2017InstallerProjects#overview)をインストールします。

- ブートストラップと呼ばれる汎用インストーラーを構成する方法でデスクトップ アプリケーションの必須コンポーネントをインストールすることもできます。 詳細については、「[Application Deployment Prerequisites](../deployment/application-deployment-prerequisites.md)」 (アプリケーション配置の必要条件) を参照してください。

## <a name="deploy-to-test-lab"></a>テスト ラボに配置する

アプリケーションを仮想環境に配置することで、より高度な開発と試験が可能になります。 詳細については、[ラボ環境のテスト](../test/lab-management/using-a-lab-environment-for-your-application-lifecycle.md)に関するページを参照してください。

## <a name="continuous-deployment"></a>継続的配置

Azure Pipelines を使用し、アプリの継続的配置を有効にできます。 詳細については、[Azure Pipelines](/azure/devops/pipelines/index?view=vsts) に関するページと [Azure に配置する](/azure/devops/deploy-azure/index?view=vsts)方法に関するページを参照してください。

## <a name="deploy-a-sql-database"></a>SQL データベースを配置する

- [ターゲット プラットフォームを変更し、データベース プロジェクトを発行する (SQL Server Data Tools (SSDT))](/sql/ssdt/how-to-change-target-platform-and-publish-a-database-project)

- [Analysis Services (SSAS) プロジェクトを配置する](/sql/analysis-services/multidimensional-tutorial/lesson-2-5-deploying-an-analysis-services-project)

- [Integration Services (SSIS) プロジェクトとパッケージを配置する](/sql/integration-services/packages/deploy-integration-services-ssis-projects-and-packages)

- [ローカル データベースでビルドおよび配置を行う](/sql/ssdt/how-to-build-and-deploy-to-a-local-database)

## <a name="deployment-for-other-app-types"></a>他の種類のアプリを配置する

| アプリの種類 | 配置シナリオ | Link |
| --- | --- | --- |
| **Office アプリ** | Visual Studio から Office 用のアドインを発行できます。 | [Office アドインを配置し、発行する](https://dev.office.com/docs/add-ins/publish/publish) |
| **WCF または OData サービス** | Web サーバーに配置した WCF RIA サービスを他のアプリケーションで使用できます。 | [WCF Data Services の開発と配置](/dotnet/framework/data/wcf/developing-and-deploying-wcf-data-services) |
| **LightSwitch** | LightSwitch は、Visual Studio 2017 以降ではサポートされていませんが、Visual Studio 2015 以前からは引き続き配置できます。 | [LightSwitch アプリケーションの配置](https://msdn.microsoft.com/Library/4818d933-295c-4ecc-9148-7ad9ca28dcdb) |

## <a name="next-steps"></a>次の手順

このチュートリアルでは、さまざまなアプリケーションの配置オプションを簡単に見てきました。

> [!div class="nextstepaction"]
> [状況に適した発行オプション](deploying-applications-services-and-components-resources.md#what-publishing-options-are-right-for-me)
