---
title: '手順 5: Azure に ASP.NET Core アプリをデプロイする'
description: このビデオ チュートリアルとステップ バイ ステップの手順に従って、Azure に ASP.NET Core Web アプリをデプロイします。
ms.custom: get-started
ms.date: 08/14/2020
ms.technology: vs-ide-general
ms.prod: visual-studio-windows
monikerRange: vs-2019
ms.topic: tutorial
ms.devlang: CSharp
author: ardalis
ms.author: ornella
manager: jmartens
dev_langs:
- CSharp
ms.workload:
- aspnet
- dotnetcore
ms.openlocfilehash: d2fdd255e35d23b337ce5eaa9f8de6b856e23b25
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99878787"
---
# <a name="step-5-deploy-your-aspnet-core-app-to-azure"></a>手順 5: Azure に ASP.NET Core アプリをデプロイする

Azure に ASP.NET Core アプリとそのデータベースをデプロイするには、以下の手順に従います。

_Azure に ASP.NET Core アプリを初めてデプロイする際は、このビデオを見て、手順を理解してください。_

> [!VIDEO https://www.youtube.com/embed/n8wz_f5_4wI]

## <a name="open-your-project"></a>プロジェクトを開く

Visual Studio 2019 で ASP.NET Core アプリを開きます。 アプリでは、[このチュートリアル シリーズの手順 4](tutorial-aspnet-core-ef-step-04.md) で構成された EF Core および作業 Web API の設定が既に使用されているはずです。

## <a name="publish-to-azure-app-service"></a>Azure App Service に発行する

1. ソリューション エクスプローラー内でプロジェクトを右クリックし、 **[発行]** を選択します。 **[発行]** ウィザードでターゲットとして **[Azure]** を選択します。

   ![Azure App Service のスクリーンショット 1](media/vs-2019/app-service-screen-1.png)

1. 特定のターゲットであれば、 **[Azure App Service (Windows)]** を選択します。

   ![Azure App Service のスクリーンショット 2](media/vs-2019/app-service-screen-2.png)

1. **[新しい Azure App Service の作成]** を選択します。 Azure アカウントをまだお持ちでない場合は、**[無料 Azure アカウントを作成する]** をクリックして、簡単な登録プロセスを完了してください。

   ![Azure App Service のスクリーンショット 3](media/vs-2019/app-service-screen-3.png)

1. 名前とリソース グループを指定するか、既定値をそのまま採用し、 **[作成]** を選択します。 リソース グループは、Azure で関連性のあるリソースを整理する方法です。たとえば、ストレージ アカウント、キー コンテナー、データベースと一緒に機能するサービスを整理します。

   ![Azure App Service のスクリーンショット 4](media/vs-2019/app-service-screen-4.png)

1. **[完了]** を選択します。 Azure でリソースが作成され、アプリがデプロイされ、作成したものに関する情報が **[発行]** タブに入力されます。 **[発行]** タブには、同じ構成でワン クリックで発行するためのボタンがあります。このタブではまた、構成の詳細を確認したり、データベースなど、サービスを追加したりできます。

ここで、Azure SQL Server データベースを追加します。

1. **[発行]** タブの **[サービスの依存関係]** の下で、 **[SQL Server データベース]** の横にある **[構成]** を選択します。

1. 次の画面で、 **[Azure SQL Database]** を選択します。

   ![Azure SQL Database 画面のスクリーンショット](media/vs-2019/app-service-azure-sql-db.png)

1. **[SQL Database の構成]** 画面で **[SQL データベースを作成する]** を選択します。

   ![[SQL Database の構成] 画面のスクリーンショット](media/vs-2019/app-service-azure-sql-db-2.png)

1. **[Azure SQL Database] の [新規作成]** 画面で、新しいデータベース サーバーを作成します。

   ![Azure SQL Database のスクリーンショット新規作成](media/vs-2019/app-service-azure-sql-db-3.png)

1. **[SQL Server] の [新規作成]** 画面で、名前と場所を選択し、管理者のユーザー名とパスワードを指定します。

   ![Visual Studio 2019 での Azure SQL Server の作成](media/vs-2019/app-service-azure-sql-db-overlayed.png)

## <a name="exploring-the-azure-portal-and-your-hosted-app"></a>Azure portal およびホスト対象アプリを探索する

App Service が作成されると、ブラウザー内でサイトが起動します。 読み込み中に Azure portal 内で App Service を探すこともできます。 App Service の使用可能なオプションを探索すると、**[概要]** セクションが見つかります。このセクションでは、アプリの起動や停止が可能です。

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

*/Games* パスに移動すると、新しいゲームを追加して、一覧表示できます。 次に、*/swagger* パスに移動すると、ここから Web API エンドポイントを使用して、アプリの API が機能しているかも確認できます。

おめでとうございます! このビデオ チュートリアル シリーズが完了しました。

## <a name="next-steps"></a>次のステップ

これらの無料リソースを使用して ASP.NET Core アプリケーションを設計する方法を詳しく学びます。

[ASP.NET Core アプリケーションのアーキテクチャ](https://dotnet.microsoft.com/learn/web/aspnet-architecture)

## <a name="see-also"></a>関連項目

- [Visual Studio を使用して Azure に ASP.NET Core アプリを発行する](/aspnet/core/tutorials/publish-to-azure-webapp-using-vs?view=aspnetcore-2.2&preserve-view=true)