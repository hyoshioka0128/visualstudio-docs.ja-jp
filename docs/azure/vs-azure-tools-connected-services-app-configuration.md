---
title: 接続済みサービス | を使用して Azure アプリ構成を追加します。Microsoft Docs
description: Visual Studio を使用して、アプリに Azure 構成サービスの依存関係を追加接続済みサービス
author: ghogen
manager: ''
ms.custom: vs-azure
ms.workload: azure-vs
ms.topic: how-to
ms.date: 12/11/2020
ms.author: ghogen
monikerRange: '>=vs-2019'
ms.openlocfilehash: 250b89c983da039717982b31873a470172bde0f5
ms.sourcegitcommit: 5654b7a57a9af111a6f29239212d76086bc745c9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/03/2021
ms.locfileid: "101683283"
---
# <a name="adding-azure-app-configuration-by-using-visual-studio-connected-services"></a>Visual Studio を使用した Azure アプリ構成の追加接続済みサービス

このチュートリアルでは、Azure アプリ構成を使用して、Visual Studio で web プロジェクトの構成と機能フラグを管理するために必要なすべてのものを簡単に追加する方法について説明します。 Visual Studio の接続済みサービス機能を使用すると、Azure のアプリ構成リソースに接続するために必要なすべてのコード、NuGet パッケージ、および構成設定を Visual Studio で自動的に追加することができます。 この機能を使用するには、Visual Studio 2019 バージョン16.9 以降を使用している必要があります。

ASP.NET Core、.NET Core コンソール、.NET Framework プロジェクトのアプリ構成接続済みサービス機能を使用できます。

> [!NOTE]
> このトピックは、Windows 上の Visual Studio に適用されます。 Visual Studio for Mac については、[Visual Studio for Mac での接続済みサービス](/visualstudio/mac/connected-services)に関するページを参照してください。

## <a name="prerequisites"></a>前提条件

- Azure ワークロードがインストールされている Visual Studio。
- サポートされている種類の1つのプロジェクト

## <a name="connect-to-azure-app-configuration-using-connected-services"></a>接続済みサービスを使用して Azure アプリ構成に接続する

1. Visual Studio でプロジェクトを開きます。

1. **ソリューションエクスプローラー** で、[**接続済みサービス**] ノードを右クリックし、コンテキストメニューの [**接続済みサービスの追加**] を選択します。

    ![Azure の接続済みサービスを追加する](./media/vs-azure-tools-connected-services-storage/vs-2019/add-connected-service.png)

1. [ **接続済みサービス** ] タブで、 **サービスの依存関係** の [+] アイコンを選択します。

    ![サービスの依存関係の追加](./media/vs-azure-tools-connected-services-storage/vs-2019/connected-services-tab.png)

1. [ **依存関係の追加** ] ページで、[ **Azure アプリの構成**] を選択します。

    ![アプリ構成の追加](./media/vs-azure-tools-connected-services-app-configuration/add-azure-app-configuration.png)

    まだサインインしていない場合は、Azure アカウントにサインインします。 Azure アカウントを持っていない場合、[無料試用版](https://azure.microsoft.com/free/dotnet)でサインアップできます。

1. [ **Azure アプリ構成の構成** ] 画面で、サブスクリプションと既存の構成ストアを選択します。 **[次へ]** を選択します。

    アプリ構成ストアを作成する必要がある場合は、次の手順に進んでください。 それ以外の場合、手順 6. に進みます。

    ![既存の構成アカウントをプロジェクトに追加する](./media/vs-azure-tools-connected-services-app-configuration/select-config-store.png)

1. アプリ構成ストアを作成するには:

   1. **アプリ構成ストア** のヘッダーの右側にある [+] アイコンを選択します。 

   1. [Azure アプリの **構成: 新規作成** ] ダイアログボックスに入力し、[ **作成**] を選択します。 [リソース名] フィールドは一意である必要があることに注意してください。 

       ![新しい Azure アプリ構成ストア](./media/vs-azure-tools-connected-services-app-configuration/create-new-config-store.png)

   1. [ **Azure アプリの構成** ] ダイアログボックスが表示されたら、新しい構成ストアが一覧に表示されます。 この新しいストアを選択し、[ **次へ**] を選択します。

1. 接続文字列名を入力し、接続文字列をローカルシークレットファイルに保存するか、 [Azure Key Vault](/azure/key-vault)に格納するかを選択します。

   ![接続文字列の指定](./media/vs-azure-tools-connected-services-app-configuration/connection-string-app-config.png)

1. [ **変更の概要** ] 画面には、プロセスが完了した場合にプロジェクトに対して行われるすべての変更が表示されます。 変更が OK の場合は、[ **完了**] を選択します。

   ![変更の概要](./media/vs-azure-tools-connected-services-app-configuration/summary-of-changes-app-config.png)

1. **依存関係の構成プロセス** が完了すると、Azure アプリの構成がプロジェクトの [**サービスの依存関係**] ノードの下に表示されるようになります。

## <a name="next-steps"></a>次のステップ

[Azure アプリ構成のドキュメント](/azure/azure-app-configuration/overview)で Azure アプリの構成について説明します。

## <a name="see-also"></a>関連項目

- [アプリ構成で動的構成を使用して ASP.NET Core アプリに接続するためのチュートリアル](/azure/azure-app-configuration/enable-dynamic-configuration-aspnet-core)
- [接続済みサービス (Visual Studio for Mac)](/visualstudio/mac/connected-services)