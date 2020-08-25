---
title: 接続済みサービスを使用して Azure Storage を追加する | Microsoft Docs
description: Visual Studio を使用して、アプリに Azure Storage サービスの依存関係を追加接続済みサービス
author: ghogen
manager: jillfra
assetId: 521ec044-ad4b-4828-8864-01decde2e758
ms.custom: vs-azure
ms.workload: azure-vs
ms.topic: how-to
ms.date: 08/13/2020
ms.author: ghogen
ms.openlocfilehash: f2f55a149420205435d9f64ea1f66c8c6854ec38
ms.sourcegitcommit: a801ca3269274ce1de4f6b2c3f40b58bbaa3f460
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/25/2020
ms.locfileid: "88800516"
---
# <a name="adding-azure-storage-by-using-visual-studio-connected-services"></a>Visual Studio 接続済みサービスを使用した Azure ストレージの追加

Visual Studio では、次のいずれかを、 **接続済みサービス** 機能を使用して Azure Storage に接続できます。

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

## <a name="connect-to-azure-storage-using-connected-services"></a>接続済みサービスを使用して Azure Storage に接続する

::: moniker range="vs-2017"

1. Visual Studio でプロジェクトを開きます。

1. **ソリューションエクスプローラー**で、[**接続済みサービス**] ノードを右クリックし、コンテキストメニューの [**接続済みサービスの追加**] を選択します。

    ![Azure の接続済みサービスを追加する](./media/vs-azure-tools-connected-services-storage/add-connected-service.png)

1. **[接続済みサービス]** ページで、**[Azure Storage を使用したクラウド ストレージ]** を選択します。

    ![Azure Storage を追加する](./media/vs-azure-tools-connected-services-storage/add-azure-storage.png)

1. **[Azure Storage]** ダイアログで、既存のストレージ アカウントを選択し、**[追加]** をクリックします。

    ストレージ アカウントを作成する必要がある場合は、次の手順に進みます。 それ以外の場合、手順 6. に進みます。

    ![既存のストレージ アカウントをプロジェクトに追加する](./media/vs-azure-tools-connected-services-storage/select-azure-storage-account.png)

1. ストレージ アカウントを作成するには、以下の手順を実行します。

   1. ダイアログの下部にある **[新しいストレージ アカウントを作成します]** を選択します。

   1. **[ストレージ アカウントの作成]** ダイアログに入力し、**[作成]** をクリックします。

       ![新しい Azure ストレージ アカウント](./media/vs-azure-tools-connected-services-storage/create-storage-account.png)

   1. **[Azure Storage]** ダイアログが表示されると、新しいストレージ アカウントが一覧に表示されます。 一覧で新しいストレージ アカウントを選択し、**[追加]** をクリックします。

1. プロジェクトの **[サービス参照]** ノードに、ストレージの接続済みサービスが表示されます。
:::moniker-end

:::moniker range=">=vs-2019"

1. Visual Studio でプロジェクトを開きます。

1. **ソリューションエクスプローラー**で、[**接続済みサービス**] ノードを右クリックし、コンテキストメニューの [**接続済みサービスの追加**] を選択します。

    ![Azure の接続済みサービスを追加する](./media/vs-azure-tools-connected-services-storage/vs-2019/add-connected-service.png)

1. [ **接続済みサービス** ] タブで、 **サービスの依存関係**の [+] アイコンを選択します。

    ![サービスの依存関係の追加](./media/vs-azure-tools-connected-services-storage/vs-2019/connected-services-tab.png)

1. [ **依存関係の追加** ] ページで、[ **Azure Storage**] を選択します。

    ![Azure Storage を追加する](./media/vs-azure-tools-connected-services-storage/vs-2019/add-azure-storage.png)

    まだサインインしていない場合は、Azure アカウントにサインインします。 Azure アカウントを持っていない場合、[無料試用版](https://azure.microsoft.com/account/free)でサインアップできます。

1. [ **Azure Storage の構成** ] 画面で、既存のストレージアカウントを選択し、[ **次へ**] を選択します。

    ストレージ アカウントを作成する必要がある場合は、次の手順に進みます。 それ以外の場合、手順 6. に進みます。

    ![既存のストレージ アカウントをプロジェクトに追加する](./media/vs-azure-tools-connected-services-storage/vs-2019/select-azure-storage-account.png)

1. ストレージ アカウントを作成するには、以下の手順を実行します。

   1. ダイアログの下部にある [ **ストレージアカウントの作成** ] を選択します。

   1. [Azure Storage の **作成** ] ダイアログボックスに入力し、[ **作成**] を選択します。

       ![新しい Azure ストレージ アカウント](./media/vs-azure-tools-connected-services-storage/vs-2019/create-storage-account.png)

   1. **[Azure Storage]** ダイアログが表示されると、新しいストレージ アカウントが一覧に表示されます。 一覧で新しいストレージアカウントを選択し、[ **次へ**] を選択します。

1. 接続文字列名を入力し、接続文字列をローカルシークレットファイルに保存するか、 [Azure Key Vault](/azure/key-vault)に格納するかを選択します。

   ![接続文字列の指定](./media/vs-azure-tools-connected-services-storage/vs-2019/connection-string.png)

1. [ **変更の概要** ] 画面には、プロセスが完了した場合にプロジェクトに対して行われるすべての変更が表示されます。 変更が OK の場合は、[ **完了**] を選択します。

   ![変更の概要](./media/vs-azure-tools-connected-services-storage/vs-2019/summary-of-changes.png)

1. プロジェクトの **[サービス参照]** ノードに、ストレージの接続済みサービスが表示されます。
:::moniker-end

## <a name="see-also"></a>関連項目

- [Azure Storage フォーラム](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata)
- [Azure Storage のドキュメント](/azure/storage/)
- [接続済みサービス (Visual Studio for Mac)](/visualstudio/mac/connected-services)
