---
title: デプロイの概要 | Microsoft Docs
ms.custom: seodec18
ms.date: 06/22/2018
ms.topic: overview
dev_langs:
- FSharp
- VB
- CSharp
- C++
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ff5091a7ca7136cd8b62f75ee7f317b1e5b1f3be
ms.sourcegitcommit: d20ce855461c240ac5eee0fcfe373f166b4a04a9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2020
ms.locfileid: "84173729"
---
# <a name="overview-of-deployment-in-visual-studio"></a>Visual Studio での配置の概要

アプリケーション、サービス、またはコンポーネントを配置すると、他のコンピューターのデバイス、サーバー、またはクラウドに対してインストールするために、それらを配布することになります。 必要な配置の種類に合わせて、Visual Studio で適切な手法を選択します。

多くの一般的なアプリの種類では、Visual Studio でソリューション エクスプローラーから直接アプリケーションを配置することができます。 この機能のクイック ツアーについては、[配置の概要](../deployment/deploying-applications-services-and-components.md)に関するページを参照してください。

![発行オプションを選択する](../deployment/media/quickstart-publish-dialog.png)

## <a name="what-publishing-options-are-right-for-me"></a>状況に適した発行オプション

Visual Studio 内から、次のターゲットにアプリケーションを直接発行できます。

- [Azure](#azure)
- [Docker コンテナー レジストリ](#docker-container-registry)
- [フォルダー](#folder)
- [カスタム ターゲット (IIS、FTP)](#Custom targets (IIS、FTP))

**[発行]** タブでは、既存の発行プロファイルを選んだり、既存の発行プロファイルをインポートしたり、ここで説明するオプションを使って新しい発行プロファイルを作成したりできます。 IDE でのアプリの種類別の発行オプションについては、[デプロイの概要](../deployment/deploying-applications-services-and-components.md)に関する記事を参照してください。

## <a name="azure"></a>Azure 

### <a name="azure-app-service"></a>Azure App Service

[Azure App Service](/azure/app-service/app-service-web-overview) では、拡張性のある Web アプリケーションとサービスをすばやく作成でき、インフラストラクチャを保守する必要はありません。 App Service は Azure のクラウドでホストされる仮想マシン上で実行されますが、これらの仮想マシンはユーザーが管理します。 App Service の各アプリには、\*.azurewebsites.net という一意の URL が割り当てられます。Free 以外のすべての価格レベルでは、カスタム ドメイン名をサイトに割り当てることもできます。

App Service の[価格レベルまたはプラン](/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview)を選ぶことで、App Service に備わるコンピューティング能力を決定します。 また、価格レベルを変更することなく、複数の Web アプリ (および他の種類のアプリ) で同じ App Service を共有することもできます。 たとえば、開発、ステージング、運用の Web アプリを同じ App Service でホストすることができます。

### <a name="when-to-choose-azure-app-service"></a>Azure App Service を選ぶ状況

- インターネット経由でアクセスできる Web アプリケーションをデプロイしたい。
- 再デプロイする必要なしに、需要に応じて Web アプリケーションを自動的に拡張したい。
- サーバーのインフラストラクチャを管理したくない (すべてのソフトウェアの更新を含む)。
- Web アプリケーションをホストするサーバーで、コンピューター レベルのカスタマイズを行う必要がない。

> 自社のデータセンターまたは他のオンプレミス コンピューターで Azure App Service を使いたい場合は、[Azure Stack](https://azure.microsoft.com/overview/azure-stack/) を使って行うことができます。

App Service への発行の詳細については、[クイック スタート - Azure App Service への発行](quickstart-deploy-to-azure.md)と[クイック スタート - Linux への ASP.NET Core の発行](quickstart-deploy-to-linux.md)に関するページを参照してください。

### <a name="azure-virtual-machines"></a>Azure Virtual Machines

[Azure Virtual Machines (VM)](https://azure.microsoft.com/documentation/services/virtual-machines/) を使うと、任意の数のコンピューティング リソースをクラウドに作成して管理できます。 VM 上のすべてのソフトウェアと更新プログラムについての責任を負うことにより、ユーザーはお使いのアプリケーションで必要なだけいくらでもカスタマイズできます。 また、ユーザーはリモート デスクトップを介して仮想マシンに直接アクセスでき、各マシンは必要な限り割り当てられた IP アドレスを保持します。

仮想マシンでホストされているアプリケーションのスケーリングには、需要に応じた追加 VM のスピンアップと、必要なソフトウェアのデプロイが含まれます。 このような制御レベルの追加により、グローバル リージョンごとに拡張方法を変えることができます。 たとえば、異なるリージョンの従業員がアプリケーションを利用している場合、リージョンの従業員の数に従って VM を拡張でき、コストを削減できる可能性があります。

詳しくは、Visual Studio の [カスタム] オプションを使ってデプロイ ターゲットとして使うことができる Azure App Service、Azure Virtual Machines、他の Azure サービスの間の[詳細な違い](https://azure.microsoft.com/documentation/articles/choose-web-site-cloud-service-vm/)をご覧ください。

### <a name="when-to-choose-azure-app-virtual-machines"></a>Azure Virtual Machines を選ぶ状況

- インターネット経由でアクセス可能な Web アプリケーションをデプロイし、割り当てられた IP アドレスの有効期間全体を通して完全に制御したい。
- 専用データベース システムなどの追加ソフトウェア、特定のネットワーク構成、ディスク パーティションなど、サーバーでコンピューター レベルのカスタマイズが必要である。
- Web アプリケーションのスケーリングをきめ細かく制御したい。
- その他の理由で、アプリケーションをホストするサーバーに直接アクセスする必要がある。

> 自社のデータセンターまたは他のオンプレミス コンピューターで Azure Virtual Machines を使いたい場合は、[Azure Stack](https://azure.microsoft.com/overview/azure-stack/) を使って行うことができます。

## <a name="docker-container-registry"></a>Docker コンテナー レジストリ

アプリケーションで Docker を使用している場合は、コンテナー化されたアプリケーションを Docker コンテナー レジストリに発行できます。

### <a name="when-to-choose-docker-container-registry"></a>Docker コンテナー レジストリを選択するタイミング

- コンテナー化されたアプリケーションを配置する場合

## <a name="folder"></a>フォルダー

ファイル システムへのデプロイとは、ユーザーが所有するコンピューターの特定のフォルダーにアプリケーションのファイルを単にコピーすることです。 この方法は、テスト目的で、またはコンピューターでサーバーも実行している場合に限られた数のユーザーが使うアプリケーションをデプロイする場合に、最もよく使われます。 ターゲット フォルダーがネットワークで共有されている場合、ファイル システムにデプロイすると、他のユーザーも Web アプリケーション ファイルを使用して特定のサーバーにデプロイできます。

アプリケーションの構成方法およびアプリケーションが接続されているネットワークに応じて、サーバーを実行しているすべてのローカル コンピューターで、インターネットまたはイントラネットを通してアプリケーションを利用できます (コンピューターがインターネットに直接接続されている場合、外部のセキュリティ脅威からの保護に特に注意が必要です)。ユーザーは、これらのコンピューターを管理するので、ソフトウェアとハードウェアの構成を完全に制御できます。

何らかの理由で (コンピューターのアクセスなど) ユーザーが Azure App Service や Azure Virtual Machines などのクラウド サービスを使用できない場合、ユーザーは自社のデータセンターで [Azure Stack](https://azure.microsoft.com/overview/azure-stack/) を使用できます。 Azure Stack を使うと、ユーザーは Azure App Service および Azure Virtual Machines によってコンピューティング リソースを管理および使用しながら、すべてのものをオンプレミスに保持できます。

### <a name="when-to-choose-file-system-deployment"></a>ファイル システムのデプロイを選ぶ状況

- ファイル共有にアプリケーションをデプロイし、他のユーザーがそれを別のサーバーにデプロイすることだけが必要である。
- ローカル テスト デプロイのみが必要である。
- 別のデプロイ ターゲットに送る前にアプリケーション ファイルを調べて場合によっては個別に変更したい。

詳細については、[ローカル フォルダーへの配置のクイック スタート](quickstart-deploy-to-local-folder.md)に関するページを参照してください

## <a name="custom-targets-iis-ftp"></a>カスタム ターゲット (IIS、FTP)

カスタム ターゲットを使うと、Azure App Service、Azure Virtual Machines、ローカル ファイル システム以外のターゲットにアプリケーションをデプロイできます。 アクセスできるファイル システムや他のサーバー (インターネットまたはイントラネット) にデプロイできます。他のクラウド サービスも含まれます。 Web デプロイ (ファイルまたは .ZIP) および FTP で使用できます。

カスタム ターゲットを選ぶと、Visual Studio はユーザーにプロファイル名の指定を求めた後、ターゲット サーバーまたは場所、サイト名、資格情報などの追加の**接続**情報を収集します。 **[設定]** タブで次のビヘイビアーをコントロールできます。

- デプロイする構成。
- 宛先から既存のファイルを削除するかどうか。
- 発行中にプリコンパイルするかどうか。
- App_Data フォルダーのファイルをデプロイから除外するかどうか。

Visual Studio では任意の数のカスタム デプロイ プロファイルを作成し、異なる設定でプロファイルを管理できます。

### <a name="when-to-choose-custom-deployment"></a>カスタム デプロイを選ぶ状況

- URL でアクセスできる Azure 以外のプロバイダーでクラウド サービスを使っている。
- Visual Studio で使っている資格情報または Azure アカウントに直接結び付けられている資格情報とは異なる資格情報を使ってデプロイしたい。
- デプロイするたびに、ターゲットからファイルを削除したい。

詳細については、[Web サイトへの配置のクイック スタート](quickstart-deploy-to-a-web-site.md)に関するページを参照してください

## <a name="next-steps"></a>次の手順

チュートリアル:

- [発行ツールを使用して .NET Core アプリケーションを展開する](/dotnet/core/deploying/deploy-with-vs?toc=/visualstudio/deployment/toc.json&bc=/visualstudio/deployment/_breadcrumb/toc.json)
- [Azure に ASP.NET Core アプリを発行する](/aspnet/core/tutorials/publish-to-azure-webapp-using-vs?toc=/visualstudio/deployment/toc.json&bc=/visualstudio/deployment/_breadcrumb/toc.json)
- [Visual C++ での配置](/cpp/windows/deployment-in-visual-cpp)
- [UWP アプリを配置する](/windows/uwp/packaging/packaging-uwp-apps?toc=/visualstudio/deployment/toc.json&bc=/visualstudio/deployment/_breadcrumb/toc.json)
- [Web 配置を使用して Azure に Node.js アプリを発行する](https://github.com/Microsoft/nodejstools/wiki/Publish-to-Azure-Website-using-Web-Deploy?toc=/visualstudio/deployment/toc.json&bc=/visualstudio/deployment/_breadcrumb/toc.json)
- [Azure App Service に Python アプリを発行する](../python/publishing-python-web-applications-to-azure-from-visual-studio.md?toc=/visualstudio/deployment/toc.json&bc=/visualstudio/deployment/_breadcrumb/toc.json)
