---
title: Team Foundation バージョン管理 (TFVC)
description: Team Foundation バージョン管理 (TFVC) を利用して、Visual Studio for Mac から Team Foundation Server/Azure DevOps に接続します。
author: heiligerdankgesang
ms.author: dominicn
ms.date: 06/25/2019
ms.technology: vs-ide-general
ms.assetid: 52D3D26A-4D01-4FD1-AAA1-AE7D7BD39746
ms.topic: troubleshooting
ms.openlocfilehash: d2ba7f5d044b82c44d719b251a7d803212cf7b07
ms.sourcegitcommit: e38419bb842d587fd9e37c24b6cf3fc5c2e74817
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91860559"
---
# <a name="connecting-to-team-foundation-version-control"></a>Team Foundation バージョン管理に接続する

> [!NOTE]
> macOS 上での最善のバージョン管理エクスペリエンスのためには、Team Foundation バージョン管理ではなく Git を使用することをお勧めします。 Visual Studio for Mac では Git がサポートされており、Team Foundation Server (TFS)/Azure DevOps にホストされているリポジトリでの既定のオプションです。 TFS/Azure DevOps での Git の使用について詳しくは、「[Git リポジトリのセットアップ](./set-up-git-repository.md)」の記事をご覧ください。
>
> 以前に Visual Studio for Mac の TFVC 拡張機能のプレビュー リリースをご使用だった場合、これは Visual Studio 2019 for Mac にアップグレードするとサポートされなくなります。

Azure Repos では、バージョン管理の 2 つのモデルを提供しています。分散バージョン管理システムの [Git](/azure/devops/repos/git/?view=azure-devops) と、集中バージョン管理システムの [Team Foundation バージョン管理](/azure/devops/repos/tfvc/index?view=azure-devops) (TFVC) です。

Visual Studio for Mac では、Git リポジトリに対して完全なサポートを提供していますが、TFVC を利用するにはいくつかの回避策が必要になります。 現在、バージョン管理に TFVC を使用している場合は、TFVC にホストされているソース コードにアクセスするために、いくつかのソリューションを使用できます。

* [グラフィカル UI の場合、Visual Studio Code と Azure Repos 拡張機能を使用する](#use-visual-studio-code-and-the-azure-repos-extension)
* [Team Explorer Everywhere Command Line Client (TEE-CLC) を使用してお使いのリポジトリに接続する](#connecting-using-the-team-explorer-everywhere-command-line-client)
* [(非サポートの) Visual Studio for Mac 対応の Team Foundation バージョン管理を使用して TFVC に接続する](#connect-to-tfvc-using-the-team-foundation-version-control-extension)

以降、この記事では、上記の一覧に示したオプションについて説明していきます。

## <a name="requirements"></a>必要条件

* Visual Studio Community、Professional、Enterprise for Mac バージョン 7.8 以降。
* Azure DevOps Services、Team Foundation Server 2013 以降、または Azure DevOps Server 2018 以降。
* Team Foundation バージョン管理を使用して構成された、Azure DevOps Services または Team Foundation Server/Azure DevOps Server 内のプロジェクト。

## <a name="use-visual-studio-code-and-the-azure-repos-extension"></a>Visual Studio Code と Azure Repos 拡張機能を使用する

グラフィカル インターフェイスを操作してバージョン管理内のファイルを管理する場合、Visual Studio Code 対応の Azure Repos 拡張機能では、Microsoft からサポートされているソリューションを提供しています。 使用を開始するには、[Visual Studio Code](https://code.visualstudio.com) をダウンロードして、[Azure Repos 拡張機能を構成する](https://marketplace.visualstudio.com/items?itemName=ms-vsts.team)方法を確認します。

## <a name="connecting-using-the-team-explorer-everywhere-command-line-client"></a>Team Explorer Everywhere Command Line Client (TEE-CLC) を使用して接続する

macOS ターミナルを快適に使用している場合、Team Explorer Everywhere Command Line Client (TEE-CLC) では、TFVC 内のソースに接続するためのサポートされた方法を提供しています。

以下の手順に従って、TFVC への接続を設定し変更をコミットできます。

### <a name="setting-up-the-tee-clc"></a>TEE-CLC のセットアップ

TEE CLC のセットアップを行うには、2 つの方法があります。

* Homebrew を使用してクライアントをインストールする
* クライアントをダウンロードして手動でインストールする

最も簡単なソリューションは、macOS 用のパッケージ マネージャーである **HomeBrew を使用する**ことです。 この方法を使用してインストールするには、次の手順を実行します。

1. macOS ターミナルのアプリケーションを起動します。
1. ターミナルと [Homebrew ホーム ページ](https://brew.sh/)上の手順を使用して、Homebrew をインストールします。
1. Homebrew がインストールされたら、ご利用のターミナルから次のコマンドを実行します。`brew install tee-clc`

**TEE-CLC を手動でセットアップするには**:

1. Team Explorer Everywhere GitHub リポジトリのリリース ページから [ の最新バージョンをダウンロード](https://github.com/Microsoft/team-explorer-everywhere/releases)します (例えば、この記事の執筆時点では tee-clc-14.134.0.zip)。
1. .zip の内容をディスク上のフォルダーに抽出します。
1. macOS ターミナルのアプリを開き、`cd` コマンドを使用して前の手順で使用したフォルダーに切り替えます。
1. フォルダー内から、コマンド `./tf` を実行して、コマンド ライン クライアントが実行できることをテストします。Java またはその他の依存関係のインストールを求められる場合があります。

TEE-CLC がインストールされたら、コマンド `tf eula` を実行して、クライアント用のライセンス契約を表示して同意します。

最後に、お使いの TFS/Azure DevOps 環境による認証を行うために、サーバー上に個人用アクセス トークンを作成する必要があります。 詳しくは、「[Authenticating with personal access tokens (個人用アクセス トークンによる認証)](/azure/devops/integrate/get-started/authentication/pats?view=azure-devops)」をご覧ください。 TFVC によって使用される個人用アクセス トークンを作成する場合は、トークンの構成時に必ずフル アクセスを指定してください。

### <a name="using-the-tee-clc-to-connect-to-your-repo"></a>TEE CLC を使用してリポジトリに接続する

ソース コードに接続するには、最初に、`tf workspace` コマンドを使用してワークスペースを作成する必要があります。 たとえば、次のコマンドでは、Azure DevOps Services にある "MyOrganization" という組織に接続します。 

```bash
export TF_AUTO_SAVE_CREDENTIALS=1
tf workspace -new MyWorkspace -collection:https://dev.azure.com/MyOrganization
```

`TF_AUTO_SAVE_CREDENTIALS` 環境設定は、入力を複数回求められることがないように、資格情報を保存するために使用されます。 ユーザー名の入力を求められたら、前のセクションで作成した個人用アクセス トークンを使用し、空白のパスワードを使用します。

ローカル フォルダーへのソース ファイルのマッピングを作成するには、`tf workfold` コマンドを使用します。 次の例では、"MyRepository" TFVC プロジェクトから "WebApp.Services" というフォルダーをマップし、local ~/Projects/ フォルダー (つまり、現在のユーザーのホーム フォルダーにある "Projects" フォルダー) にコピーされるように設定します。

```bash
tf workfold -map $/MyRepository/WebApp.Services -workspace:MyWorkspace ~/Projects/
```

最後に、次のコマンドを使用してサーバーからソース ファイルを取得し、ローカルにコピーします。

```bash
tf get
```

### <a name="committing-changes-using-the-tee-clc"></a>TEE CLC を使用して変更をコミットする

Visual Studio for Mac 内のファイルに変更を加えた後は、ターミナルに戻って編集内容をチェックインできます。 `tf add` コマンドは、チェックインされる保留中の変更一覧にファイルを追加するために使用され、`tf checkin` コマンドはサーバーへの実際のチェックインを実行します。 `checkin` コマンドには、コメントを追加したり、関連する作業項目を結び付けたりするためのパラメーターが含まれます。 次のコード スニペットでは、`WebApp.Services` フォルダーにあるすべてのファイルが、再帰的にチェックインに追加されます。 次に、コードはコメントと共にチェックインされ、ID "42" の作業項目と結び付けられます。

```bash
cd WebApp.Services
tf add * /recursive
tf checkin -comment:"Replaced 'Northwand' typos with the correct word Northwind" -associate:42
```

ここで説明したコマンドなどについて詳細を確認するには、ターミナルから次のコマンドを使用できます。

`tf help`

## <a name="connect-to-tfvc-using-the-team-foundation-version-control-extension"></a>Team Foundation バージョン管理の拡張機能を使用して TFVC に接続する

> [!NOTE]
> macOS 上での最善のバージョン管理エクスペリエンスのためには、Team Foundation バージョン管理ではなく Git を使用することをお勧めします。 Visual Studio for Mac では Git がサポートされており、Team Foundation Server (TFS)/Azure DevOps にホストされているリポジトリでの既定のオプションです。 TFS/Azure DevOps での Git の使用について詳しくは、「[Git リポジトリのセットアップ](./set-up-git-repository.md)」の記事をご覧ください。
>
> 以前に Visual Studio for Mac の TFVC 拡張機能のプレビュー リリースをご使用だった場合、これは Visual Studio 2019 for Mac にアップグレードするとサポートされなくなります。

Visual Studio for Mac の拡張機能ギャラリーには、TFVC に接続するための制限付きサポートを提供している Team Foundation バージョン管理の拡張機能があります。 拡張機能は非サポートであり、いくつかの既知の問題があるため、使用時のエクスペリエンスは不安定になる可能性があります。

拡張機能をインストールするには、Visual Studio for Mac を起動して、**[Visual Studio] > [拡張機能]** メニューの順に選択します。 **[ギャラリー]** タブで **[バージョン管理] > [Team Foundation Version Control for TFS and Azure DevOps]\(TFS と Azure DevOps の Team Foundation バージョン管理\)** を順に選択し、**[インストール...]** をクリックします。

![拡張機能マネージャー](media/tfvc-install.png)

画面の指示に従って、拡張機能をインストールします。 インストールした後、IDE を再起動します。

### <a name="updating-the-extension"></a>拡張機能の更新

TFVC 拡張機能への更新プログラムは、定期的に作成されます。 更新プログラムにアクセスするには、メニューから **[Visual Studio]、[拡張機能]** の順に選び、 **[更新]** タブを選択します。リスト内の拡張機能を選択して、 **[更新]** ボタンを押します。

次のダイアログで **[インストール]** を押して古いパッケージをアンインストールし、新しいパッケージをインストールします。

### <a name="using-the-extension"></a>拡張機能を使用する

拡張機能をインストールしたら、**[バージョン管理] > [TFS/Azure DevOps] > [Open from Remote Repository...]\(リモート リポジトリから開く...\)** メニュー項目を順に選択します。

![拡張機能を開くメニュー項目](media/tfvc-source-control-explorer-devops.png)

最初に VSTS または Team Foundation Server のいずれかを選択して、**[続行]** を押します。

![サーバーで接続する](media/tfvc-choose-server-type-devops.png)

#### <a name="azure-repos-authentication"></a>Azure Repos の認証

Azure Repos でホストされているプロジェクトを選択すると、Microsoft アカウントの情報を入力する画面が表示されます。

![Azure Repos に接続する](media/tfvc-vsts-login.png)

#### <a name="tfs-authentication"></a>TFS 認証

TFS に接続するには、サーバーの詳細とアカウントの資格情報を入力します。 NTLM 認証するドメインを入力します。それ以外の場合は、空白のままにして基本認証を使用します。 **[サーバーの追加]** を選択します。

![TFS Server にサインインする](media/tfvc-login.png)

### <a name="selecting-a-project"></a>プロジェクトの選択

認証が正常に行われると、**[Open from Source Control]\(ソース管理から開く\)** ダイアログでアカウントに関連付けられているリポジトリのリストを確認できます。

![プロジェクトを表示しているソース管理から開くダイアログ](media/tfvc-vsts-projects.png)

このダイアログは、次のノードで構成されています。

- Azure DevOps の組織またはコレクション: ログインに使用した Microsoft アカウントに接続されているすべての組織を表示します。
- プロジェクト: 各組織またはコレクションには、多くのプロジェクトを持つことができます。 プロジェクトは、ソース コード、作業項目、自動化されたビルドがホストされている場所です。

この時点で、プロジェクトまたは組織の名前で検索およびフィルター処理を行うことができます。

#### <a name="adding-a-new-server"></a>新しいサーバーの追加

新しいサーバーをリストに追加するには、**[Open from Source Control]\(ソース管理から開く\)** ダイアログの **[ホストの追加]** ボタンを押します。

![新しいサーバーをリストに追加するための強調表示された追加ボタン](media/tfvc-add-new-server.png)

リストからプロバイダーを選択して、資格情報を入力します。

![ソース管理プロバイダー用のオプションを示すダイアログ](media/tfvc-add-new-creds-devops.png)

### <a name="creating-a-new-workspace"></a>新しいワークスペースの作成。

プロジェクトの操作を開始するには、_ワークスペース_が必要です。 まだワークスペースがない場合は、**[Open from Source Control]\(ソース管理から開く\)** ダイアログ内の **[ワークスペース]** コンボ ボックスからワークスペースを作成できます。

![新しいワークスペースの作成コンボ ボックスのオプション](media/tfvc-create-new-workspace.png)

新しいワークスペースの名前とローカル パスを設定して、**[ワークスペースの作成]** を選択します。

![新しいワークスペースの名前とローカル パスの入力](media/tfvc-local-workspace.png)

### <a name="using-the-source-code-explorer"></a>ソース コード エクスプローラーの使用

ワークスペースを作成してプロジェクトをマップしたら、_ソース コード エクスプローラー_の操作を開始できます。

ソース コード エクスプローラーを開くには、**[バージョン コントロール] > [TFS/Azure DevOps] > [ソース管理エクスプローラー]** の順にメニュー項目を選択します。

ソース コード エクスプローラーを使用すると、すべてのマップされているプロジェクト、そのファイルやフォルダー内を移動できます。 また、次のような基本のソース コントロール アクションをすべて実行することもできます。

- 最新バージョンの取得
- 特定バージョンの取得
- ファイルのチェックインとチェックアウト
- ファイルのロックとロック解除
- ファイルの追加、削除、名前の変更
- 履歴を表示する
- 変更の比較。

これらのアクションの多くは、プロジェクトのコンテキスト アクションで使用できます。

![プロジェクトに対するコンテキスト メニューのアクション](media/tfvc-sourcecode-actions.png)

### <a name="managing-workspaces"></a>ワークスペースの管理

「[新しいワークスペースの作成](#creating-a-new-workspace)」セクションで説明されたように、まだワークスペースを作成していない場合は、ソース コード エクスプローラーが空であることが表示されます。

![空のソース コード エクスプローラー](media/tfvc-setup-empty-sce.png)

ローカル ワークスペースを使ってリモート プロジェクトを設定するには、次の手順を使用します。

1. コンボ ボックスから**サーバー**を選択します。
1. "ワークスペースがありません" とローカル パスが "対応付けされていません" が示されていることに注意してください。 **[対応付けされていません]** リンクを選択して、**[新しいワークスペースの作成]** ダイアログを表示します。
1. ワークスペースの名前を入力し、**[Add Working Folder]\(作業フォルダーの追加\)** をクリックし、コンピューター上のローカル フォルダーにプロジェクトをマッピングします。

    ![既定のオプションを示している [新しいワークスペースの作成] ダイアログ](media/tfvc-workspace1.png)

1. "$" フォルダーを選択してサーバー上のすべてのプロジェクトを同じワークスペースにマッピングするか、個別のプロジェクトを選択して、**[OK]** をクリックします。

    ![すべてのプロジェクトを示している [フォルダーの参照] ダイアログ](media/tfvc-workspace2.png)

1. プロジェクトをマッピングするローカル コンピューター上の場所を選択して、**[フォルダーの選択]** をクリックします。
1. **[OK]** を押して、新しいワークスペースの詳細を確認します。

    ![追加された作業フォルダーを含む [新しいワークフローの追加] ダイアログ](media/tfvc-workspace3.png)

ワークスペースを設定したら、ソース コード エクスプローラーの **[ワークスペースの管理]** をクリックすることによって、変更または削除することができます。

![ワークスペースの管理](media/tfvc-workspace4.png)

## <a name="troubleshooting-and-known-issues"></a>トラブルシューティングと既知の問題

#### <a name="problems-using-basic-authentication"></a>基本認証の使用に関する問題

次のオプションを使用して、サーバーで認証できます。

- OAuth
- Basic
- Ntlm

基本認証を使用するには、以下の手順に従って、Azure DevOps Services で**代替認証資格情報**を有効にする必要があります。

1. 所有者として、Azure DevOps 組織にサインインします (https:\//dev.azure.com/{organization}/{project})。

2. 組織のツール バーの歯車アイコンを選択し、**[ポリシー]** を選択します。

    ![選択されたポリシー設定オプション](media/tfvc-auth2.png)

3. アプリケーションの接続設定を確認します。 セキュリティ ポリシーに基づいてこれらの設定を変更します。

    ![選択されたポリシー設定オプション](media/tfvc-auth.png)

#### <a name="i-do-not-see-anything-in-tfvc"></a>TFVC に何も表示されない

開発用コンピューターに Team Foundation バージョン管理 (TFVC) を設定するには、「[ワークスペースの管理](#managing-workspaces)」セクションの説明に従って、ワークスペースを作成する**必要があります**。

ソース管理エクスプローラーで、**[ワークスペースの管理]** ボタンをクリックします。 手順に従って、開発用コンピューター上にあるフォルダーに、プロジェクトをマップします。

#### <a name="i-do-not-see-any--all-of-my-projects"></a>一部/すべてのプロジェクトが表示されない

認証が済むと、プロジェクトの一覧が表示されるはずです。 既定では、TFS プロジェクトのみが表示されます。 他の種類のプロジェクトを表示するには、[See all projects]\(すべてのプロジェクトを表示する\) ボックスをオンにします。

適切な特権がない場合は、サーバー上にあるプロジェクトが表示されないことに注意してください。

##### <a name="i-am-getting-the-error-cannot-create-the-workspace-please-try-again"></a>次のような内容のエラーが表示される: "ワークスペースを作成できません。 もう一度お試しください"

[新しいワークスペースを作成](#creating-a-new-workspace)しようとするときは、次の条件が満たされていることを確認してください。

- ワークスペース名で無効な文字が使用されていない。
- 名前が 64 文字未満である。
- 他のワークスペースによってローカル パスが使用されていない。

### <a name="see-also"></a>関連項目

- [Visual Studio を使用して TFVC でコードを開発および共有する (Windows)](/azure/devops/repos/tfvc/share-your-code-in-tfvc-vs)