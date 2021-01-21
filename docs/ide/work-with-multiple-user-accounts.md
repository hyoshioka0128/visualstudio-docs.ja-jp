---
title: 複数のユーザー アカウントを使って作業する
description: すべての Microsoft アカウントを Visual Studio に追加して、個別にサインインしなくても任意のアカウントからリソースにアクセスできるようにする方法を説明します。
ms.custom: SEO-VS-2020
ms.date: 11/16/2020
ms.topic: conceptual
author: ornellaalt
ms.author: ornella
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 071c6061417e26b45e5f9e67bc6ac1001bf08530
ms.sourcegitcommit: df6ba39a62eae387e29f89388be9e3ee5ceff69c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/02/2020
ms.locfileid: "96480344"
---
# <a name="work-with-multiple-user-accounts"></a>複数のユーザー アカウントを使って作業する

複数の Microsoft アカウントや職場または学校のアカウントを所有している場合、そのすべてを Visual Studio に追加すると、個別にサインインしなくても、すべてのアカウントのリソースにアクセスできます。 Azure、Application Insights、Azure DevOps、Microsoft 365 サービスでは、合理化されたサインイン エクスペリエンスがサポートされています。

1 台のコンピューターで複数のアカウントを追加した後、別のコンピューターで Visual Studio にサインインすると、そのアカウント セットがユーザーと共に移動されます。

> [!NOTE]
> アカウント名はローミングしますが、資格情報はローミングしません。 新しいコンピューターでそのリソースを初めて使用しようとすると、他のアカウントの資格情報の入力を求められます。

この記事では、Visual Studio に複数のアカウントを追加する方法を示します。 また、 **[接続済みサービスの追加]** ダイアログ、**サーバー エクスプローラー**、**チーム エクスプローラー** などの場所でそれらのアカウントからアクセス可能なリソースを表示する方法についても示します。

## <a name="sign-in-to-visual-studio"></a>Visual Studio にサインイン

Microsoft アカウントまたは組織アカウントで、Visual Studio にサインインします。 ウィンドウの右上隅に、次のようにユーザー名が表示されます。

![現在ログインしているユーザー](../ide/media/vs2015_username.png)

### <a name="access-your-azure-account-in-server-explorer"></a>サーバー エクスプローラーで Azure アカウントにアクセス

サーバー エクスプローラーを開くには、 **[表示]**  >  **[サーバー エクスプローラー]** を選択します (または、"全般" [環境設定](../ide/environment-settings.md)を使用している場合は、**Ctrl**+**Alt**+**S** キーを押します)。 **Azure** ノードを展開し、Visual Studio にサインインするときに使用したアカウントに関連付けられた Azure アカウントで使用可能なリソースが含まれることを確認します。 次の図のように表示されます。

![Azure ノードが展開されたサーバー エクスプローラー](../ide/media/work-with-multiple-user-accounts/server-explorer.png)

特定のデバイスで初めて Visual Studio を使用するときは、サインインに使用したアカウントで登録されているサブスクリプションだけがダイアログに表示されます。 **サーバー エクスプローラー** で **Azure** ノードを右クリックして **[サブスクリプションの管理とフィルター]** を選択し、アカウントの選択コントロールからアカウントを追加することにより、他のアカウントのリソースに直接アクセスできます。 その後は、必要に応じて、下矢印をクリックしてアカウントの一覧から選択することにより、別のアカウントを選択できます。 アカウントを選択した後は、**サーバー エクスプローラー** に表示されるそのアカウントのサブスクリプションをカスタマイズできます。

![[Azure サブスクリプションの管理] ダイアログ](../ide/media/vs2015_manage_subs.png)

次に **サーバー エクスプローラー** を開いたときは、そのサブスクリプションのリソースが表示されます。

### <a name="access-your-azure-account-via-add-connected-service-dialog"></a>[接続済みサービスの追加] ダイアログを通して Azure アカウントにアクセスします。

1. 既存のプロジェクトを開くか、新しいプロジェクトを作成します。

1. **ソリューション エクスプローラー** でプロジェクト ノードを選択し、右クリックして **[追加]**  >  **[接続済みサービス]** の順に選択します。

   **[接続済みサービスの追加]** ウィザードが表示され、Visual Studio のパーソナル化アカウントに関連付けられた Azure アカウントのサービスの一覧が表示されます。 Azure に個別にサインインする必要はありません。 ただし、異なるコンピューターから他のアカウントのリソースへのアクセスを初めて試みるときは、そのアカウントにサインインする必要があります。

### <a name="access-azure-active-directory-in-a-web-project"></a>Web プロジェクトで Azure Active Directory にアクセス

Azure Active Directory (AAD) では、ASP.NET MVC の Web アプリでのエンド ユーザー シングル サインオンや、Web API サービスでの AD 認証がサポートされています。 ドメインの認証は、個々のユーザー アカウントの認証とは異なります。 Active Directory ドメインにアクセスできるユーザーは、各自の既存の Azure AD アカウントを使用して、Web アプリケーションに接続できます。 Microsoft 365 アプリでは、ドメイン認証も使用できます。

::: moniker range="vs-2017"

アクション内でこれを表示するには、新しい **ASP.NET Core Web アプリケーション** プロジェクトを作成します。 **[新しい ASP.NET Core Web アプリケーション]** ダイアログ ボックスで、 **[Web アプリケーション]** テンプレートを選択してから、 **[認証の変更]** を選択します。

::: moniker-end

::: moniker range=">=vs-2019"

アクション内でこれを表示するには、新しい **ASP.NET Core Web アプリケーション** プロジェクトを作成します。 **[新しい ASP.NET Core Web アプリケーションの作成]** ダイアログ ボックスで、**[Web アプリケーション]** テンプレートを選択してから、**[認証]** の下にある **[変更]** を選択します。

::: moniker-end

**[認証の変更]** ダイアログ ボックスが表示されます。ここでは、ご利用のアプリケーションで使用する認証の種類を選択できます。

![ASP.NET の認証の変更ダイアログ](../ide/media/vs2015_change_authentication.png)

ASP.NET でのさまざまな種類の認証について詳しくは、「[Visual Studio 2013 で ASP.NET Web プロジェクトの作成](/aspnet/visual-studio/overview/2013/creating-web-projects-in-visual-studio#authentication-methods)」をご覧ください。

### <a name="access-your-azure-devops-organization"></a>Azure DevOps 組織にアクセスする

メイン メニューから **[チーム]**  >  **[接続の管理]** を選択して、 **[チーム エクスプローラー - 接続]** ウィンドウを開きます。 **[接続の管理]**  >  **[プロジェクトに接続]** の順に選択します。 **[プロジェクトに接続]** ダイアログで、一覧からプロジェクトを選択します (または、 **[TFS サーバーに追加する]** を選択してサーバーの URL を入力します)。 URL を選択すると、資格情報を再入力しなくてもログインできます。

詳しくは、「[チーム エクスプローラーのプロジェクトに接続する](connect-team-project.md)」をご覧ください。

## <a name="add-an-additional-account-to-visual-studio"></a>追加アカウントを Visual Studio に追加する

追加アカウントを Visual Studio に追加するには:

1. **[ファイル]**  >  **[アカウント設定]** を選択します。

1. **[すべてのアカウント]** で **[アカウントの追加]** を選択します。

1. **[アカウントにサインイン]** ページで、アカウントを選択するか、 **[別のアカウントを使用する]** を選択します。 プロンプトに応じて新しいアカウントの資格情報を入力します。

(省略可能) ここまで済むと、**サーバー エクスプローラー** に移動して、追加したアカウントに関連付けられている Azure サービスを確認できます。 **サーバー エクスプローラー** で、**Azure** ノードを右クリックして、 **[サブスクリプションの管理とフィルター]** を選択します。 現在のアカウントの横にあるドロップダウン矢印をクリックして新しいアカウントを選択し、**サーバー エクスプローラー** に表示するサブスクリプションを選択します。 指定したサブスクリプションに関連付けられているすべてのサービスが表示されます。 現在 2 番目のアカウントで Visual Studio にサインインしてはいませんが、そのアカウントのサービスとリソースにサインインします。 同じことが **[プロジェクト]**  >  **[接続済みサービスの追加]** および **[チーム]**  >  **[Team Foundation Server への接続]** にも当てはまります。

### <a name="add-an-account-using-device-code-flow"></a>デバイス コード フローを使用してアカウントを追加する

通常の方法ではサインインしたりアカウントを追加したりできない場合があります。 これは、Internet Explorer が何らかの理由でブロックされている場合、またはネットワークがファイアウォールの内側にある場合に発生することがあります。 これを回避するには、"*デバイス コード フロー*" を有効にして、アカウントを追加したり、アカウントを再認証したりすることができます。 デバイス コード フローを使用すると、別のブラウザーを使用して、または別のマシン (物理または仮想 (VM)) で、サインインすることができます。

デバイス コード フローを使用してサインインするには:

1. **[ツール]** > **[オプション]** > **[環境]** で **[[アカウント](reference/accounts-environment-options-dialog-box.md)]** ページを開き、**[アカウントの追加または再認証のときにデバイス コード フローを有効にする]** をオンにします。 **[OK]** を選択してオプション ページを閉じます。

1. **[ファイル]**  >  **[アカウント設定]** を選択してアカウント管理ページを開きます。

1. **[すべてのアカウント]** の **[アカウントの追加]** を選択します。

   ダイアログ ボックスに、Web ブラウザーに貼り付ける URL とコードが表示されます。

   ![デバイス コード フローの URL とコード](media/work-with-multiple-user-accounts/device-login-code.png)

1. **Ctrl**+**C** キーを押してダイアログのテキストをコピーし、 **[OK]** を選択してダイアログを閉じます。 コピーしたテキストをメモ帳などのテキスト エディターに貼り付けます。 これにより、次のステップでコードをコピーしやすくなります。

1. Visual Studio へのサインインに使用するマシンまたは Web ブラウザーでデバイス ログイン URL に移動し、 **[コード]** ボックスにコピーしたコードを貼り付けるか入力します。

   **Visual Studio** のアプリ名がページのさらに下に表示されます。

1. **[Visual Studio]** で **[続行]** を選択します。

   ![[続行] オプションを示す [デバイスのログイン] ページのスクリーンショット。](media/work-with-multiple-user-accounts/device-login-page.png)

1. プロンプトに従ってお使いのアカウントの資格情報を入力します。

   デバイスで Visual Studio にサインインしたこと、およびブラウザー ウィンドウを閉じてもかまわないことを示すページが表示されます。

   ![ブラウザーによる Visual Studio へのサインインの完了](media/work-with-multiple-user-accounts/sign-in-browser-complete.png)

1. Visual Studio でアカウント管理ページに戻ると、新しく追加したアカウントが **[すべてのアカウント]** の一覧に表示されます。 **[閉じる]** を選択します。

::: moniker range=">=vs-2019"

### <a name="add-a-github-account-to-visual-studio"></a>Visual Studio に GitHub アカウントを追加する

バージョン 16.8 以降では、GitHub と GitHub Enterprise 両方のアカウントをキーチェーンに追加できるようになります。 Microsoft アカウントの場合と同様にそれらを追加して活用できるようになります。つまり、Visual Studio 全体で GitHub リソースにより簡単にアクセスできるようになります。

詳細な手順については、「[Visual Studio の GitHub アカウントを使って作業する](work-with-github-accounts.md)」を参照してください。
::: moniker-end

## <a name="see-also"></a>関連項目

- [Visual Studio へのサインイン](signing-in-to-visual-studio.md)
- [Visual Studio for Mac にサインインする](/visualstudio/mac/signing-in)
