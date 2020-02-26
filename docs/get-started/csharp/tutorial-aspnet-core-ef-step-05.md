---
title: '手順 5: Azure に ASP.NET Core アプリをデプロイする'
description: このビデオ チュートリアルとステップ バイ ステップの手順に従って、Azure に ASP.NET Core Web アプリをデプロイします。
ms.custom: get-started
ms.date: 03/31/2019
ms.technology: vs-ide-general
ms.prod: visual-studio-windows
monikerRange: vs-2019
ms.topic: tutorial
ms.devlang: CSharp
author: ardalis
ms.author: ornella
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- aspnet
- dotnetcore
ms.openlocfilehash: dc13dbdadb0c9bca25a816b15c5a99039bff454c
ms.sourcegitcommit: 2ae2436dc3484b9dfa10e0483afba1e5a02a52eb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/25/2020
ms.locfileid: "77580034"
---
# <a name="step-5-deploy-your-aspnet-core-app-to-azure"></a>手順 5: Azure に ASP.NET Core アプリをデプロイする

Azure に ASP.NET Core アプリとそのデータベースをデプロイするには、以下の手順に従います。

_Azure に ASP.NET Core アプリを初めてデプロイする際は、このビデオを見て、手順を理解してください。_

> [!VIDEO https://www.youtube.com/embed/n8wz_f5_4wI]

## <a name="open-your-project"></a>プロジェクトを開く

Visual Studio 2019 で ASP.NET Core アプリを開きます。 アプリでは、[このチュートリアル シリーズの手順 4](tutorial-aspnet-core-ef-step-04.md) で構成された EF Core および作業 Web API の設定が既に使用されているはずです。

## <a name="publish-to-azure-app-service"></a>Azure App Service に発行する

ソリューション エクスプローラー内でプロジェクトを右クリックし、 **[発行]** を選択します。 **[App Service]** と **[新規作成]** の設定は既定のままにして、 **[発行]** ボタンをクリックします。 Azure アカウントをまだお持ちでない場合は、 **[無料 Azure アカウントを作成する]** をクリックして、簡単な登録プロセスを完了してください。

SQL Server を追加します。 管理者のユーザー名とパスワードを指定します。

![Visual Studio 2019 での Azure SQL Server の作成](media/vs-2019/vs2019-azure-sql-server.png)

Application Insights を追加します。

**[作成]** ボタンをクリックして続行します。

![Visual Studio 2019 での Azure App Service の新規作成](media/vs-2019/vs2019-azure-create-new-app-service.png)

## <a name="exploring-the-azure-portal-and-your-hosted-app"></a>Azure portal およびホスト対象アプリを探索する

App Service が作成されると、ブラウザー内でサイトが起動します。 読み込み中に Azure portal 内で App Service を探すこともできます。 App Service の使用可能なオプションを探索すると、 **[概要]** セクションが見つかります。このセクションでは、アプリの起動や停止が可能です。

![Azure App Service のオプション](media/vs-2019/vs2019-azure-app-service-menu-options.png)

### <a name="scalability"></a>スケーラビリティ

アプリをスケールアップするオプションとスケールアウトするオプションを確認できます。スケールアップとは、アプリをホストする各インスタンスで利用可能なリソースを増やすことです。 スケールアウトとは、アプリをホストするインスタンスの数を増やすことです。 アプリに対して自動スケールを構成することもできます。この場合は、アプリのホストに使用されるインスタンスの数が負荷に応じて自動的に増減されます。

### <a name="security-and-compliance"></a>セキュリティとコンプライアンス

Azure を使用してアプリをホストするもう 1 つの利点は、セキュリティとコンプライアンスです。 Azure App Service では、ISO、SOC、および PCI の各コンプライアンスに対応できます。 ユーザー認証の手段として、Azure Active Directory を選択することも、Twitter、Facebook、Google、Microsoft などのソーシャル ログインを選択することもできます。 また、IP 制限の作成、サービス ID の管理、カスタム ドメインの追加、アプリの SSL サポートのほか、復元可能なアーカイブ コピー (アプリのコンテンツ、構成、およびデータベース) を使用したバックアップの構成も可能です。 これらの機能は、認証/承認、ID、バックアップ、および SSL 設定の各メニュー オプションで利用できます。

### <a name="deployment-slots"></a>デプロイ スロット

アプリをデプロイした場合、アプリの再起動中に短時間のダウンタイムが発生することがよくあります。 デプロイ スロットは、この問題を回避するために、別個のステージング インスタンス、または一連のインスタンスに対してデプロイを行い、それらのインスタンスをウォームアップしてから、スワップして実稼働できるようにするものです。 スワップは一瞬で実行され、トラフィックのリダイレクトもシームレスに行われます。 スワップ後に実稼働で問題が発生した場合は、いつでも直前の正常な実稼働状態に戻すことができます。

## <a name="update-connection-string"></a>接続文字列を更新する

Azure の場合、既定では、アプリから新しい SQL Server データベースへの新規接続で `DefaultConnection` という接続文字列が使用されることが想定されています。 現在、このチュートリアル シリーズで前に作成したアプリでは、`AppDbContext` という接続文字列が使用されています。 そのため、*appsettings.json* および *Startup.cs* 内でこの文字列を変更して、アプリを再デプロイする必要があります。

## <a name="test-the-app-running-in-azure"></a>Azure 内で実行されているアプリをテストする

*/Games* パスに移動すると、新しいゲームを追加して、一覧表示できます。 次に、 */swagger* パスに移動すると、ここから Web API エンドポイントを使用して、アプリの API が機能しているかも確認できます。

おめでとうございます! このビデオ チュートリアル シリーズが完了しました。

## <a name="next-steps"></a>次の手順

これらの無料リソースを使用して ASP.NET Core アプリケーションを設計する方法を詳しく学びます。

[ASP.NET Core アプリケーションのアーキテクチャ](https://dotnet.microsoft.com/learn/web/aspnet-architecture)

## <a name="see-also"></a>関連項目

- [Visual Studio を使用して Azure に ASP.NET Core アプリを発行する](/aspnet/core/tutorials/publish-to-azure-webapp-using-vs?view=aspnetcore-2.2)