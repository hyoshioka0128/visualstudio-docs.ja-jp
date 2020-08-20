---
title: 接続を Azure SQL Database | に追加します。Microsoft Docs
description: Visual Studio を使用してアプリへの Azure SQL Database 接続を追加接続済みサービス
author: AngelosP
manager: jillfra
ms.custom: vs-azure
ms.workload: azure-vs
ms.topic: conceptual
ms.date: 08/17/2020
ms.author: angelpe
monikerRange: '>= vs-2019'
ms.openlocfilehash: e1594ea4239b4200bf72ec4a2ef2c558839ef95c
ms.sourcegitcommit: 3ef987e99616c3eecf4731bf5ac89e16238e68aa
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88643170"
---
# <a name="add-a-connection-to-azure-sql-database"></a>接続を Azure SQL Database に追加します

Visual Studio では、 **接続済みサービス** 機能を使用して、次のいずれかを Azure SQL database に接続できます。

- .NET Framework コンソールアプリ
- ASP.NET MVC (.NET Framework) 
- ASP.NET Core
- .NET Core (コンソールアプリ、WPF、Windows フォーム、クラスライブラリを含む)
- .NET Core Worker ロール
- Azure Functions
- ユニバーサル Windows プラットフォームアプリ
- Xamarin
- Cordova

接続済みサービス機能により、必要なすべての参照と接続コードがプロジェクトに追加され、構成ファイルが適切に変更されます。

> [!NOTE]
> このトピックは、Windows 上の Visual Studio に適用されます。 Visual Studio for Mac については、[Visual Studio for Mac での接続済みサービス](/visualstudio/mac/connected-services)に関するページを参照してください。
## <a name="prerequisites"></a>前提条件

- Azure ワークロードがインストールされている Visual Studio。
- サポートされている種類の1つのプロジェクト

## <a name="connect-to-azure-sql-database-using-connected-services"></a>接続済みサービスを使用して Azure SQL Database に接続する

1. Visual Studio でプロジェクトを開きます。

1. **ソリューションエクスプローラー**で、[**接続済みサービス**] ノードを右クリックし、コンテキストメニューの [**接続済みサービスの追加**] を選択します。

1. [ **接続済みサービス** ] タブで、 **サービスの依存関係**の [+] アイコンを選択します。

    ![サービスの依存関係の追加](./media/vs-azure-tools-connected-services-storage/vs-2019/connected-services-tab.png)

1. [ **依存関係の追加** ] ページで、[ **Azure SQL Database**] を選択します。

    ![Azure SQL Database サービスの追加](./media/azure-sql-database-add-connected-service/azure-sql-database.png)

    まだサインインしていない場合は、Azure アカウントにサインインします。 Azure アカウントを持っていない場合、[無料試用版](https://azure.microsoft.com/account/free)でサインアップできます。

1. [ **Azure SQL Database の構成** ] 画面で、既存の Azure SQL Database を選択し、[ **次へ**] を選択します。

    新しいコンポーネントを作成する必要がある場合は、次の手順に進んでください。 それ以外の場合は、手順 7 に進みます。

    ![既存の Azure SQL Database コンポーネントに接続する](./media/azure-sql-database-add-connected-service/created-azure-sql-database.png)

1. Azure SQL Database を作成するには:

   1. 画面の下部にある [ **SQL Database の作成** ] を選択します。

   1. [Azure SQL Database の **作成** ] 画面に入力し、[ **作成**] を選択します。

       ![新しい Azure SQL Database](./media/azure-sql-database-add-connected-service/create-new-azure-sql-database.png)

   1. [ **Azure SQL Database の構成** ] 画面が表示されたら、新しいデータベースが一覧に表示されます。 一覧から新しいデータベースを選択し、[ **次へ**] を選択します。

1. 接続文字列名を入力するか、既定値を選択して、接続文字列をローカルシークレットファイルに保存するか、 [Azure Key Vault](/azure/key-vault)に格納するかを選択します。

   ![接続文字列の指定](./media/azure-sql-database-add-connected-service/connection-string.png)

1. [ **変更の概要** ] 画面には、プロセスが完了した場合にプロジェクトに対して行われるすべての変更が表示されます。 変更が OK の場合は、[ **完了**] を選択します。

   ![変更の概要](./media/azure-sql-database-add-connected-service/summary-of-changes.png)

   ファイアウォール規則の設定を求めるメッセージが表示されたら、[ **はい]** を選択します。

   ![ファイアウォール規則](./media/azure-sql-database-add-connected-service/firewall-rules.png)

1. 接続は、[**接続済みサービス**] タブの [**サービスの依存関係**] セクションに表示されます。

   ![サービスの依存関係](./media/azure-sql-database-add-connected-service/service-dependencies-after.png)

## <a name="see-also"></a>関連項目

- [Azure SQL Database の製品ページ](https://azure.microsoft.com/services/sql-database/)
- [Azure SQL Database のドキュメント](/azure/azure-sql/database/)
- [接続済みサービス (Visual Studio for Mac)](/visualstudio/mac/connected-services)
