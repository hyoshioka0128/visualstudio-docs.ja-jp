---
title: Git リポジトリのセットアップ
description: Visual Studio for Mac で Git および Subversion を使用します。
author: therealjohn
ms.author: johmil
ms.date: 05/13/2020
ms.assetid: E992FA1D-B2AD-4A28-ADC6-47E4FC471060
ms.topic: how-to
ms.openlocfilehash: bc981530f5493ce1899de1c888e20129c7ae0f8c
ms.sourcegitcommit: 2946d802aec1418e87bfa779d81834eeb7be5c9d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2020
ms.locfileid: "88214691"
---
# <a name="set-up-a-git-repository"></a>Git リポジトリのセットアップ

Git は、チームが同じドキュメントで同時に作業できるようにする分散型バージョン管理システムです。 つまり、すべてのファイルを含む 1 つのサーバーがありますが、この中央のソースからリポジトリがチェックアウトされるときには常に、リポジトリ全体がコンピューターにローカルでクローンされます。

Git をバージョン コントロールに使用できるリモート ホストは多数ありますが、GitHub が最も一般的です。 次の例では GitHub ホストを使用しますが、Visual Studio for Mac ではバージョン管理のために任意の Git ホストを使用できます。

GitHub を使用する場合は、アカウントの作成と構成を完了してから、この記事の手順を実行してください。

## <a name="creating-a-remote-repo-on-github"></a>GitHub でのリモート リポジトリの作成

次の例では GitHub ホストを使用しますが、Visual Studio for Mac ではバージョン管理のために任意の Git ホストを使用できます。

Git リポジトリをセットアップするには、次の手順を実行します。

1. github.com で新しい Git リポジトリを作成します。

    ![新しい Git リポジトリを作成する](media/version-control-git1-sml.png)

2. リポジトリの名前、説明、およびプライバシーを設定します。 リポジトリは初期化**しない**でください。 次のように、.gitignore とライセンスを None に設定します。

    ![Git リポジトリの詳細を設定する](media/version-control-git2.png)

3. 次のページには、HTTPS または SSH アドレスの表示と、作成したリポジトリへのコピーに関するオプションが表示されます。

    ![アドレスの表示とコピー](media/version-control-git3.png)

   Visual Studio for Mac にこのリポジトリを指す HTTPS アドレスが必要です。

## <a name="publishing-an-existing-project"></a>既存のプロジェクトの発行

バージョン管理にまだ_含まれていない_既存のプロジェクトがある場合は、Git のセットアップで次の手順を使用します。

1. Visual Studio for Mac でソリューション パッドからソリューション名を選択します。

2. メニュー バーで、 **[バージョン管理] > [バージョン管理で発行]** の順に選択して、 **[リポジトリの複製]** ダイアログを表示します。

    ![Visual Studio for Mac でチェックアウトを開始する](media/version-control-git4.png)

    このメニュー項目がメニューで灰色表示されている場合は、ソリューション名が選択されていることを確認してください。

3. 次のように、 **[Select from Registered] (登録済みのものから選択)** タブを選択し、 **[追加]** ボタンを押します。

    ![登録済みリポジトリのダイアログ ボックスを追加します。](media/version-control-git5.png)

4. ローカルで表示するリポジトリの名前を入力し、手順 3. の URL を貼り付けます。 リポジトリ構成ダイアログは次のようになります。 [OK] を押します。

    ![Git の詳細入力ダイアログ](media/version-control-git6.png)

    SSH を使用して Git に接続することもできます。

5. Git にアプリを発行してみる場合は、次のように、リポジトリを選択し、 **[モジュール名]** と **[メッセージ]** の両方のテキスト フィールドに入力されていることを確認します。

    ![Git にプロジェクトを発行してみる](media/version-control-git7.png)

6. **[OK]** をクリックし、警告ダイアログの **[発行]** をクリックします。

7. **[Git 資格情報]** ウィンドウに GitHub のユーザー名とパスワードを入力します。 

> [!NOTE]
> ご自分のアカウントで 2 要素認証 (2FA) が有効になっている場合は、パスワードの代わりに使用するアクセス トークンを作成する必要があります。 アクセス トークンを作成していない場合は、Git の[アクセス トークン](https://help.github.com/articles/creating-an-access-token-for-command-line-use/)に関するドキュメントの手順を実行してください。

8. ユーザー名と個人用アクセス トークンを入力して、 **[OK]** を押します。

    ![Git のユーザー名とパスワードを入力する](media/version-control-git9-sml.png)

9. 数秒後に、初回コミットでソリューションが発行されます。 [バージョン コントロール] メニュー項目を参照して発行されたことを確認します。この時点で、次のように多くのオプションが示されます。

    ![バージョン管理メニュー](media/version-control-git10.png)

10. 追加の変更を開始したら、まず **[バージョン管理] > [確認してコミット]** メニューを使用して状態ビューを開きます。 変更を選択してコミットした後、 **[プッシュ]** を選択してリモート リポジトリに変更をプッシュします。 これで、適切なすべてのユーザーが github.com で表示できるようになります。

    ![リモート リポジトリに変更をプッシュする](media/version-control-git11.png)

## <a name="publishing-a-new-project"></a>新しいプロジェクトの発行

新しいプロジェクト ダイアログを使用すると、ローカル git リポジトリがある新しいプロジェクトを作成できます。 これを有効にするには、次のスクリーンショットのとおりに、 **[Use git for version control]** \(バージョン管理に git を使用する\) チェック ボックスをオンにします。 これでリポジトリが初期化され、オプションの .gitignore ファイルが追加されます。

![git サポートを使用した新しいプロジェクトの作成](media/version-control-git-publish-new1.png)

新しい GitHub リポジトリに新しいローカル リポジトリをプッシュするには、次の手順を実行します。

> [!NOTE]
> GitHub リポジトリをまだ作成していない場合は、「[GitHub でのリモート リポジトリの作成](#creating-a-remote-repo-on-github)」のセクションを参照してください。

1. メニュー バーの **[バージョン管理] > [確認してコミット]** に移動し、最初のコミットを行います。

2. [状態] タブで、左上の **[コミット]** を選択します。

3. たとえば、「最初のコミット」などのコミット メッセージを記述し、 **[コミット]** をクリックします。

    ![最初の変更の git リポジトリへのコミット](media/version-control-git-publish-new2.png)

4. 次いで、メニュー バーの **[バージョン管理] > [ブランチとリモートを管理する]** に移動します。

5. **[リモート ソース]** タブに移動し、 **[追加]** をクリックします。

6. **[リモート ソース]** ウィンドウで前に作成した GitHub リポジトリの詳細を追加し、 **[OK]** をクリックします。

    ![git リポジトリ用のリモート ソースの構成](media/version-control-git-publish-new3.png)

7. **[Git リポジトリの構成]** ウィンドウを閉じ、メニュー バーの **[バージョン管理] > [変更をプッシュ]** に移動します。

8. **[リポジトリへプッシュ]** ウィンドウで **[変更をプッシュ]** ボタンをクリックします。

    ![リモート リポジトリへの変更のプッシュ](media/version-control-git-publish-new4.png)

9. 求められたら、GitHub のユーザー名とパスワードを入力します。

> [!NOTE]
> ご自分のアカウントで 2 要素認証 (2FA) が有効になっている場合は、パスワードの代わりに使用するアクセス トークンを作成する必要があります。 アクセス トークンを作成していない場合は、Git の[アクセス トークン](https://help.github.com/articles/creating-an-access-token-for-command-line-use/)に関するドキュメントの手順を実行してください。

これで Visual Studio for Mac によって、ご使用のリモート GitHub リポジトリに変更がプッシュされます。

![[プッシュ操作は正常に完了しました] の確認](media/version-control-git11.png)

## <a name="clone-an-existing-repository"></a>既存のリポジトリを複製する

ローカル コンピューター上にない、リモートにのみ存在する GitHub リポジトリを使用しなければならなくなる可能性があります。 Visual Studio for Mac ではこのリポジトリをすばやく複製できます。 お使いのコンピューターに複製するには、次の手順に従います。

1. メニュー バーで、 **[バージョン管理] > [リポジトリの複製]** の順に選択します。

2. **[Connect with Url] (URL での接続)** タブが表示されます。

    ![詳細が入力された [Connect with Url] (URL での接続) タブ](media/version-control-git13.png)

3. リモート リポジトリの GitHub ページで、 **[Clone or download]\(クローンまたはダウンロード\)** ボタンを押して、提供された URL をコピーします。

    ![URL が表示された github](media/version-control-git14.png)

4. **[Connect with Url] (URL での接続)** タブの **[URL]** エントリ フィールド内のすべてのテキストを置き換えます。手順 2 の画像に示すように、これによりこのタブの他のほとんどのフィールドに自動的に入力されます。

5. リポジトリの複製先のディレクトリを入力し、 **[複製]** を押します。

> [!NOTE]
> リポジトリのサイズが 4 GB を超えている場合は、問題が発生する可能性があります。

## <a name="troubleshooting"></a>トラブルシューティング

空のリモート リポジトリでプロジェクトを初期化する際に問題が発生した場合は、次の手順を試すことができます。

1. ソリューション フォルダーに移動します。
1. **Command + Shift + .** キーを押して、 非表示のファイルとフォルダーを表示します。
1. **.git** フォルダーがある場合は、それを削除します。
1. **gitignore** ファイルがある場合は、それを削除します。
1. **Command + Shift + .** キーを押して、 ファイルとフォルダーを非表示にします。
1. VS for Mac でソリューションを開きます。
1. Solution Pad で、ソリューション ノードを選択します。
1. バージョン管理メニューを参照し、 **[バージョン管理で発行]** を選択します。
1. 上記のチュートリアルの手順 6. 以降の手順に従います。

## <a name="see-also"></a>関連項目

- [Visual Studio でのバージョン コントロール (Windows)](/visualstudio/version-control/)
