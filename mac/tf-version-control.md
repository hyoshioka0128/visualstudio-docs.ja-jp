---
title: Team Foundation バージョン管理 (TFVC)
description: TFVC と macOS に関するトラブルシューティング ガイド。
author: jmatthiesen
ms.author: jomatthi
ms.date: 09/02/2019
ms.technology: vs-ide-general
ms.assetid: 52D3D26A-4D01-4FD1-AAA1-AE7D7BD39746
ms.topic: troubleshooting
ms.openlocfilehash: 11b0788317cd0a20dd27159aa241db32e3818daf
ms.sourcegitcommit: 18729d7c99c999865cc2defb17d3d956eb3fe35c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2021
ms.locfileid: "98722127"
---
# <a name="does-visual-studio-for-mac-support-team-foundation-version-control"></a>Visual Studio for Mac は Team Foundation バージョン管理をサポートしていますか?

> [!CAUTION]
> Visual Studio for Mac の TFVC 拡張機能のプレビューは Visual Studio 2019 for Mac ではサポートされなくなります。


## <a name="alternative-version-control-options-in-visual-studio-for-mac"></a>Visual Studio for Mac の代替バージョン コントロール オプション

macOS 上での最善のバージョン コントロール エクスペリエンスのためには、Team Foundation バージョン管理 (TFVC) ではなく **Git** を使用することをお勧めします。 

Visual Studio for Mac では Git がサポートされており、Team Foundation Server (TFS)/Azure DevOps にホストされているリポジトリでの既定のオプションです。 TFS/Azure DevOps での Git の使用の詳細については、「[Setting up a Git Repository](./set-up-git-repository.md)」(Git リポジトリのセットアップ) のガイドをご覧ください。

## <a name="unsupported-workarounds-for-tfvc"></a>TFVC でサポートされていない回避策

Visual Studio for Mac は TFVC を正式にサポートしていませんが、このガイドの残りの部分では、macOS で TFVC を使用するための回避策について説明します。 現在、バージョン管理に TFVC を使用している場合は、TFVC にホストされているソース コードにアクセスするために、いくつかのソリューションを使用できます。

* 方法 1. [グラフィカル UI の場合、Visual Studio Code と Azure Repos 拡張機能を使用する](#use-visual-studio-code-and-the-azure-repos-extension)
* 方法 2. [Team Explorer Everywhere Command Line Client (TEE-CLC) を使用してお使いのリポジトリに接続する](#connecting-using-the-team-explorer-everywhere-command-line-client)

### <a name="option-1--use-visual-studio-code-and-the-azure-repos-extension"></a>方法 1. <a id="use-visual-studio-code-and-the-azure-repos-extension"></a> Visual Studio Code と Azure Repos 拡張機能を使用する

グラフィカル インターフェイスを操作してバージョン管理内のファイルを管理する場合、Visual Studio Code 対応の Azure Repos 拡張機能では、Microsoft からサポートされているソリューションを提供しています。 使用を開始するには、[Visual Studio Code](https://code.visualstudio.com) をダウンロードして、[Azure Repos 拡張機能を構成する](https://marketplace.visualstudio.com/items?itemName=ms-vsts.team)方法を確認します。

### <a name="option-2--connecting-using-the-team-explorer-everywhere-command-line-client"></a>方法 2. <a id="connecting-using-the-team-explorer-everywhere-command-line-client"></a> Team Explorer Everywhere Command Line Client を使用して接続する

> [!IMPORTANT]
> Team Explorer Everywhere の README にあるように、このプロジェクトは[管理されなくなりました](https://github.com/microsoft/team-explorer-everywhere)。

macOS ターミナルを快適に使用している場合、Team Explorer Everywhere Command Line Client (TEE-CLC) では、TFVC 内のソースに接続するためのサポートされた方法を提供しています。

以下の手順に従って、TFVC への接続を設定し変更をコミットできます。

#### <a name="setting-up-the-tee-clc"></a>TEE-CLC のセットアップ

TEE CLC のセットアップを行うには、2 つの方法があります。

* Homebrew を使用してクライアントをインストールする
* クライアントをダウンロードして手動でインストールする

最も簡単なソリューションは、macOS 用のパッケージ マネージャーである **HomeBrew を使用する** ことです。 この方法を使用してインストールするには、次の手順を実行します。

1. macOS ターミナルのアプリケーションを起動します。
1. ターミナルと [Homebrew ホーム ページ](https://brew.sh/)上の手順を使用して、Homebrew をインストールします。
1. Homebrew がインストールされたら、ご利用のターミナルから次のコマンドを実行します。`brew install tee-clc`

**TEE-CLC を手動でセットアップするには**:

1. Team Explorer Everywhere GitHub リポジトリのリリース ページから [ の最新バージョンをダウンロード](https://github.com/Microsoft/team-explorer-everywhere/releases)します (例えば、この記事の執筆時点では tee-clc-14.134.0.zip)。
1. .zip の内容をディスク上のフォルダーに抽出します。
1. macOS ターミナルのアプリを開き、`cd` コマンドを使用して前の手順で使用したフォルダーに切り替えます。
1. フォルダー内から、コマンド `./tf` を実行して、コマンド ライン クライアントが実行できることをテストします。Java またはその他の依存関係のインストールを求められる場合があります。

TEE-CLC がインストールされたら、コマンド `tf eula` を実行して、クライアント用のライセンス契約を表示して同意します。

最後に、お使いの TFS/Azure DevOps 環境による認証を行うために、サーバー上に個人用アクセス トークンを作成する必要があります。 詳しくは、「[Authenticating with personal access tokens (個人用アクセス トークンによる認証)](/azure/devops/integrate/get-started/authentication/pats?view=azure-devops&preserve-view=true)」をご覧ください。 TFVC によって使用される個人用アクセス トークンを作成する場合は、トークンの構成時に必ずフル アクセスを指定してください。

#### <a name="using-the-tee-clc-to-connect-to-your-repo"></a>TEE CLC を使用してリポジトリに接続する

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

#### <a name="committing-changes-using-the-tee-clc"></a>TEE CLC を使用して変更をコミットする

Visual Studio for Mac 内のファイルに変更を加えた後は、ターミナルに戻って編集内容をチェックインできます。 `tf add` コマンドは、チェックインされる保留中の変更一覧にファイルを追加するために使用され、`tf checkin` コマンドはサーバーへの実際のチェックインを実行します。 `checkin` コマンドには、コメントを追加したり、関連する作業項目を結び付けたりするためのパラメーターが含まれます。 次のコード スニペットでは、`WebApp.Services` フォルダーにあるすべてのファイルが、再帰的にチェックインに追加されます。 次に、コードはコメントと共にチェックインされ、ID "42" の作業項目と結び付けられます。

```bash
cd WebApp.Services
tf add * /recursive
tf checkin -comment:"Replaced 'Northwand' typos with the correct word Northwind" -associate:42
```

ここで説明したコマンドなどについて詳細を確認するには、ターミナルから次のコマンドを使用できます。

`tf help`

## <a name="see-also"></a>関連項目

- [Visual Studio を使用して TFVC でコードを開発および共有する (Windows)](/azure/devops/repos/tfvc/share-your-code-in-tfvc-vs)