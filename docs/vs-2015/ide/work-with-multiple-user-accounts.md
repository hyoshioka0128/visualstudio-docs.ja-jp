---
title: 複数のユーザー アカウントを使って作業する | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
ms.assetid: b73c865c-74e0-420e-89cc-43524f4aafd0
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 2f68328fb243c00c43c8ef454f10ad94c7d004a4
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74296790"
---
# <a name="work-with-multiple-user-accounts"></a>複数のユーザー アカウントを使って作業する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

複数の Microsoft アカウントや職場または学校のアカウントを所有している場合、そのすべてを Visual Studio に追加すると、個別にサインインしなくても、すべてのアカウントのリソースにアクセスできます。 Visual Studio 2015 RTM の時点では、Azure、Application Insights、Team Foundation Server、Office 365 サービスが簡素化されたサインイン エクスペリエンスをサポートします。 今後、他のサービスが使用可能になる可能性があります。

 1 台のコンピューターで複数のアカウントを追加した後、別のコンピューターで Visual Studio にサインインすると、そのアカウント セットがユーザーと共に移動します。 アカウント名は移動しますが資格情報は移動しないことに注意することが重要です。 したがって、新しいコンピューターでそのリソースを初めて使用しようとすると、他のアカウントの資格情報の入力を求められます。

 このチュートリアルは複数のアカウントを Visual Studio に追加する方法について説明しており、それらのアカウントからアクセス可能なリソースを表示する方法については、 **[接続済みサービスの追加]** ダイアログ、 **サーバー エクスプローラー**、および **チーム エクスプローラー**などに反映されています。

#### <a name="sign-in-to-visual-studio"></a>Visual Studio にサインイン

1. Microsoft アカウントまたは組織アカウントで、Visual Studio 2015 にサインインします。 ウィンドウの右上に、次のようにユーザー名が反映されています。

     ![Currentlly logged in user](../ide/media/vs2015-username.png "VS2015_UserName")

### <a name="access-your-azure-account-in-server-explorer"></a>サーバー エクスプローラーで Azure アカウントにアクセス
 **Ctrl + Alt + S** を押して **サーバー エクスプローラー**を開きます。 Azure アイコンをクリックして展開すると、Visual Studio 2015 にログインするときに使用した ID に関連付けられた Azure アカウントで利用可能なリソースが表示されます。 次のようになりますが、表示されるのは自分のリソースであり、Mr. Guido のリソースではありません。

 ![Server Explorer showing Azure Tools node expanded](../ide/media/vs2015-serverexplorer.png "VS2015_ServerExplorer")

 特定のデバイスで初めて Visual Studio を使用するときは、IDE へのサインインに使用した ID で登録されているサブスクリプションだけがダイアログに表示されます。 **サーバー エクスプローラー** で Azure ノードを右クリックして **[サブスクリプションの管理とフィルター]** を選択し、アカウントの選択コントロールからアカウントを追加することにより、他のアカウントのリソースに直接アクセスできます。 その後は、必要に応じて、下矢印をクリックしてアカウントの一覧から選択することにより、別のアカウントを選択できます。 アカウントを選択した後は、そのアカウントからサーバー エクスプローラーに表示するサブスクリプションを選択できます。

 ![Manage Azure Subscriptions dialog](../ide/media/vs2015-manage-subs.png "vs2015_manage_subs")

 次にサーバー エクスプローラーを開いたときは、そのサブスクリプションのリソースが表示されます。

### <a name="access-your-azure-account-via-add-connected-service-dialog"></a>[接続済みサービスの追加] ダイアログを通して Azure アカウントにアクセスします。

1. C# でユニバーサル アプリ プロジェクトを作成します。

2. ソリューション エクスプローラーでプロジェクト ノードを右クリックし、 **[追加] > [接続済みサービス]** を選択します。 [接続済みサービスの追加] ウィザードが表示され、Visual Studio ログイン ID に関連付けられた Azure アカウントのサービスの一覧が表示されます。 なお、Azure には個別にサインインする必要はありません。 ただし、特定のコンピューターから他のアカウントのリソースへのアクセスを初めて試みるときは、そのアカウントにサインインする必要があります。

    > [!WARNING]
    > If this is the first time you are creating a Store app in Visual Studio 2015 on a specific computer, you will be prompted to enable your device for development mode by going to **Settings &#124; . Updates and Security &#124; For Developers** on your computer. 詳細については、「[デバイスを開発用に有効にする](https://msdn.microsoft.com/library/windows/apps/dn706236.aspx)」を参照してください。

### <a name="access_azure"></a>Web プロジェクトで Azure Active Directory にアクセス
 Azure AD では、ASP.NET MVC の Web アプリケーションでのエンド ユーザー シングル サインオンや、Web API サービスでの AD 認証をサポートしています。 ドメイン認証は個々のユーザー アカウント認証とは異なります。Active Directory ドメインにアクセスできるユーザーは、既存の Azure AD アカウントを使用して、Web アプリケーションに接続できます。 Office 365 アプリでは、ドメイン認証も使用できます。 これを実際に見るには、Web アプリケーションを作成します ( **[ファイル]、[新しいプロジェクト]、[C#]、[クラウド]、[ASP.NET Web アプリケーション]** )。 新しい ASP.NET プロジェクトのダイアログで、 **[認証の変更]** を選択します。 認証ウィザードが表示され、アプリケーションで使用する認証の種類を選択できます。

 ![Change authentication dialog for ASP.NET](../ide/media/vs2015-change-authentication.png "VS2015_change_authentication")

 ASP.NET での異なる種類の認証について詳しくは、「 [Visual Studio 2013 での ASP.NET Web プロジェクトの作成](https://docs.microsoft.com/aspnet/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauth) 」をご覧ください (認証に関する情報は Visual Studio 2015 にも引き続き該当します)。

### <a name="access-your-visual-studio-team-services-account"></a>Visual Studio Team Services のアカウントへのアクセス
 メイン メニューから、 **[チーム] > [Team Foundation Server への接続]** を選択して、**チーム エクスプローラー** ウィンドウを開きます。 **[チーム プロジェクトの選択]** をクリックすると、 **[Team Foundation Server の選択]** にあるリスト ボックスに Visual Studio Team Services アカウントの URL が表示されます。 URL を選択すると、資格情報を再入力しなくてもログインできます。

## <a name="add-a-second-user-account-to-visual-studio"></a>Visual Studio に 2 つ目にユーザー アカウントを追加
 Visual Studio の右上にあるユーザー名の横の矢印をクリックします。 その後、 **[アカウントの設定]** メニュー項目をクリックします。 **[アカウント マネージャー]** ダイアログが表示され、サインインしたアカウントが表示されます。 ダイアログの左下にある **[アカウントの追加]** リンクをクリックして、新しい Microsoft アカウントまたは新しい仕事や学校のアカウントを追加します。

 ![Visual Studio account picker](../ide/media/vs2015-acct-picker.png "VS2015_acct_picker")

 プロンプトに応じて新しいアカウントの資格情報を入力します。 次の図は、ユーザーが自分の Contoso.com の仕事用アカウントを追加した後のアカウント マネージャーを示しています。

 ![Account Manager](../ide/media/vs2015-accountmanager.gif "VS2015_AccountManager")

## <a name="revisit-the-add-connected-services-wizard-and-server-explorer"></a>[接続済みサービスの追加] ウィザードおよびサーバー エクスプローラーを再表示します。
 **サーバー エクスプローラー** に再び移動し、Azure ノードを右クリックして、 **[サブスクリプションの管理とフィルター]** を選択します。 現在のアカウントの横にあるドロップダウン矢印をクリックして新しいアカウントを選択し、サーバー エクスプローラーに表示するサブスクリプションを選択します。 指定したサブスクリプションに関連付けられているすべてのサービスが表示されます。現在 2 番目のアカウントで Visual Studio IDE にサインインしてはいませんが、そのアカウントのサービスとリソースにサインインします。 同じことが **[プロジェクト] > [接続済みサービスの追加]** および **[チーム] > [Team Foundation Server への接続]** にも当てはまります。
