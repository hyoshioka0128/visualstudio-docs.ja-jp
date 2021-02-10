---
title: Azure App Service に Python アプリを発行する
description: Python アプリを Azure App Service に発行する場合のオプション (Git デプロイ、Linux 用コンテナー、IIS へのデプロイなど)。
ms.date: 03/13/2019
ms.topic: conceptual
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.custom: seodec18
ms.workload:
- python
- data-science
- azure
ms.openlocfilehash: b2848a54ddbce41b538bf58f82db42ede76026d1
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99912417"
---
# <a name="publish-to-azure-app-service"></a>Azure App Service に発行する

現時点では、Python は Linux 用の Azure App Service でサポートされており、この記事で説明しているとおり、アプリの発行は、[Git デプロイ](#publish-to-app-service-on-linux-using-git-deploy)と[コンテナー](#publish-to-app-service-on-linux-using-containers)を使用して行います。

> [!Note]
> Windows 用の Azure App Service での Python のサポートは正式に非推奨になっています。 結果として、Visual Studio の **発行** コマンドは、[IIS ターゲット](#publish-to-iis)のみのために正式にサポートされ、Azure App Service のリモート デバッグでは正式にサポートされなくなりました。
>
> ただし、Windows 上の App Service 用の Python 拡張機能は、サービスの提供や更新はありませんが、まだ利用可能です。そのため、[Windows の App Service への発行](publish-to-app-service-windows.md) 機能はしばらくは機能します。

## <a name="publish-to-app-service-on-linux-using-git-deploy"></a>Git デプロイを使用した Linux の App Service への発行

Git デプロイは、Linux の App Service を Git リポジトリの特定のブランチに接続します。 そのブランチにコードをコミットすると App Service に自動的にデプロイされ、App Service によって *requirements.txt* に記述されている依存関係がすべてインストールされます。 この場合、Linux 上の App Service は Gunicorn Web サーバーを使用する事前構成されたコンテナー イメージにコードを実行します。 現時点では、このサービスはプレビューであり、運用環境での使用はサポートされていません。

詳細については、Azure のドキュメントの以下の記事を参照してください。

- 「[Quickstart: Create a Python web app in App Service](/azure/app-service/containers/quickstart-python?toc=%2Fpython%2Fazure%2FTOC.json)」 (クイック スタート: App Service で Python Web アプリを作成する) は、シンプルな Flask アプリとローカルの Git リポジトリからのデプロイを使用した Git デプロイの簡単なチュートリアルです。
- 「[How to configure Python](/azure/app-service/containers/how-to-configure-python)」 (Python の構成方法) では、Linux コンテナー上の App Service の特徴と、ご自分のアプリ用に Gunicorn 起動コマンドをカスタマイズする方法を説明します。

## <a name="publish-to-app-service-on-linux-using-containers"></a>コンテナーを使用した Linux の App Service への発行

Linux の App Service のあらかじめ構築されているコンテナーを使用する代わりに、自分でコンテナーを用意することができます。 このオプションでは、使用する Web サーバーを選択して、コンテナーの動作をカスタマイズすることができます。

コンテナーを構築、管理、プッシュする選択肢は 2 つあります。

- 「[Deploy Python using Docker Containers](https://code.visualstudio.com/docs/python/tutorial-deploy-containers)」 (Docker コンテナーを使用した Python のデプロイ) の説明に従って、Visual Studio Code と Docker 拡張機能を使用します。 Visual Studio Code を使用しない場合でも、この記事には、運用環境用に準備された uwsgi と nginx Web サーバーを使用した、Flask と Django アプリ用のコンテナー イメージの構築に役立つ詳細が含まれています。 これらの同じコンテナーは、Azure CLI を使用して展開できます。

- Azure ドキュメントの[カスタム Docker イメージを使用する](/azure/app-service/containers/tutorial-custom-docker-image)に関するページで説明されているとおり、コマンド ラインと Azure CLI を使用します。 ただし、このガイドは Python に限定されたものではなく汎用です。

## <a name="publish-to-iis"></a>IIS に公開する

Visual Studio で **発行** コマンドを使用して、Windows 仮想マシンまたはその他の IIS 対応のコンピューターに発行をすることができます。 IIS を使用する場合、Python インタープリターを探す場所を IIS に教える *web.config* ファイルを必ず作成または変更してください。 詳細については、「[Configure web apps for IIS](configure-web-apps-for-iis-windows.md)」 (IIS 用に Web アプリを構成する) を参照してください。
