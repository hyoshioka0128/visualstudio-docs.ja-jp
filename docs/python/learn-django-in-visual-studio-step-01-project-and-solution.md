---
title: Visual Studio での Django チュートリアル手順 1、Django の基本
titleSuffix: ''
description: Visual Studio プロジェクトのコンテキストでの Django の基礎に関するチュートリアルでは、Visual Studio が Django 開発のために提供するサポートについて説明します。
ms.date: 11/19/2018
ms.topic: tutorial
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: afde24347237ed3fc87d7a00ebdf21787d78909c
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99942661"
---
# <a name="tutorial-get-started-with-the-django-web-framework-in-visual-studio"></a>チュートリアル: Visual Studio での Django Web フレームワークの概要

[Django](https://www.djangoproject.com/) は、高速、安全、スケーラブルな Web 開発用に設計されたハイレベルの Python フレームワークです。 このチュートリアルでは、Visual Studio が Django ベースの Web アプリの作成を合理化するために提供するプロジェクト テンプレートのコンテキストで Django フレームワークについて説明します。

このチュートリアルでは、以下の内容を学習します。

> [!div class="checklist"]
> - "空の Django Web プロジェクト" テンプレートを使用して Git リポジトリに基本的な Django プロジェクトを作成する (手順 1)
> - 1 つのページがある Django アプリを作成し、テンプレートを使用してそのページをレンダリングする (手順 2)
> - 静的ファイルを提供し、ページを追加し、テンプレート継承を使用する (手順 3)
> - Django Web プロジェクト テンプレートを使用して、複数のページを持つ応答性に優れたデザインのアプリを作成する (手順 4)
> - ユーザーを認証する (手順 5)
> - ポーリング Django Web プロジェクト テンプレートを使用して、モデル、データベースの移行、管理インターフェイスのカスタマイズを使用するアプリを作成する (手順 6)

## <a name="prerequisites"></a>前提条件

- Windows 用の Visual Studio 2017 以降は次のオプションを備えています。
  - **Python 開発ワークロード** (インストーラーの **[ワークロード]** タブ)。 手順については、[Visual Studio での Python サポートのインストール](installing-python-support-in-visual-studio.md)に関するページをご覧ください。
  - **Windows 向け Git** と **Visual Studio 向け GitHub 拡張** ( **[個別のコンポーネント]** タブの **[コード ツール]** )。

Django プロジェクト テンプレートは Python Tools for Visual Studio のすべての旧バージョンにも含まれていますが、詳細は、このチュートリアルの説明と異なる場合があります (特に、Django フレームワークの旧バージョンでは異なります)。

現在、Visual Studio for Mac では Python 開発はサポートされていません。 Mac および Linux では、[Visual Studio Code で Python 拡張](https://code.visualstudio.com/docs/python/python-tutorial)を使用します。

### <a name="visual-studio-projects-and-django-projects"></a>"Visual Studio プロジェクト" と "Django プロジェクト"

Django の用語では、"Django プロジェクト" は、複数のサイト レベル構成ファイルと、完全な Web アプリケーションを作成するために Web ホストにデプロイする 1 つ以上の "アプリ" から構成されます。 Django プロジェクトには複数のアプリを含めることができ、同じアプリを複数の Django プロジェクトに含めることができます。

Visual Studio プロジェクトには、Django プロジェクトと複数のアプリを含めることができます。 わかりやすくするために、このチュートリアルで単に "プロジェクト" と呼ぶ場合、それは Visual Studio プロジェクトを表しています。 Web アプリケーションの "Django プロジェクト" 部分を表す場合は、明示的に "Django プロジェクト" を使用します。

この一連のチュートリアルでは、3 つの独立した Django プロジェクトを含む単一の Visual Studio ソリューションを作成します。各 Django プロジェクトに単一の Django アプリが含まれます。 同じソリューション内にプロジェクトを保持することで、異なるファイル間を簡単に切り替えて比較できます。

## <a name="step-1-1-create-a-visual-studio-project-and-solution"></a>手順 1-1: Visual Studio プロジェクトとソリューションを作成する

コマンド ラインから Django を使用する場合、通常は `django-admin startproject <project_name>` コマンドを実行してプロジェクトを開始します。 Visual Studio で、"空の Django Web プロジェクト" テンプレートを使用して、Visual Studio プロジェクトおよびソリューション内に同じ構造を提供します。

1. Visual Studio で、 **[ファイル]**  >  **[新規]**  >  **[プロジェクト]** の順に選択し、"Django" を検索して、"**空の Django Web プロジェクト**" テンプレートを選択します (テンプレートは、左側の一覧の **[Python]**  >  **[Web]** にもあります)。

    ![Visual Studio での空の Django Web プロジェクト用の [新しいプロジェクト] ダイアログ ボックス](media/django/step01-new-blank-project.png)

1. ダイアログの下部にあるフィールドで、(前の図に示したように) 次の情報を入力し、 **[OK]** を選択します。

    - **名前**: Visual Studio プロジェクトの名前を「**BasicProject**」に設定します。 この名前は Django プロジェクトにも使用されます。
    - **場所**: Visual Studio ソリューションとプロジェクトを作成する場所を指定します。
    - **ソリューション**: このコントロールは既定の **[新しいソリューションの作成]** オプションに設定したままにします。
    - **ソリューション名**: このチュートリアルでは複数プロジェクトのコンテナーとしてのソリューションに適した **LearningDjango** に設定します。
    - **ソリューションのディレクトリを作成**: オンのままにします (既定)。
    - **新しい Git リポジトリの作成**: ソリューションの作成時に Visual Studio でローカルの Git リポジトリが作成されるように、このオプション (既定ではオフ) をオンにします。 このオプションが表示されない場合は、Visual Studio インストーラーを実行し、**[コード ツール]** の **[個別のコンポーネント]** タブで **Windows 用 Git** および **Visual Studio 用 GitHub 拡張機能** を追加します。

1. しばらくすると、Visual Studio に (次に示すように) "**このプロジェクトには外部パッケージが必要です**" というダイアログが表示されます。 テンプレートには、最新の Django 1.x パッケージを参照する *requirements.txt* ファイルが含まれているため、このダイアログが表示されます (正確な依存関係を確認するには **[必要なパッケージを表示]** を選択します)。

    ![プロジェクトに外部パッケージが必要であることを示すプロンプト](media/django/step01-requirements-prompt-install-myself.png)

1. オプション **[I will install them myself]\(自分でインストールする\)** を選択します。 仮想環境を簡単に作成し、ソース管理から除外されていることを確認します (環境はいつでも *requirements.txt* から作成できます)。

## <a name="step-1-2-examine-the-git-controls-and-publish-to-a-remote-repository"></a>手順 1-2: Git コントロールを確認し、リモート リポジトリに発行する

**[新しいプロジェクト]** ダイアログで **[新しい Git リポジトリの作成]** を選択したため、作成プロセスが完了するとすぐに、プロジェクトは既にローカル ソース管理にコミットされています。 この手順では、Visual Studio の Git コントロールと、ソース管理を操作する **[チーム エクスプローラー]** ウィンドウについて理解します。

1. Visual Studio のメイン ウィンドウの下隅にある Git コントロールを確認します。 これらのコントロールは、左から右の順に、確定されていないコミット、確定されていない変更、リポジトリの名前、現在のブランチを示します。

    ![Visual Studio ウィンドウの Git コントロール](media/django/step01-git-controls.png)

    > [!Note]
    > **[新しいプロジェクト]** ダイアログで **[新しい Git リポジトリの作成]** を選択しない場合、Git コントロールには、ローカル リポジトリを作成する **[Add to source control]\(ソース管理に追加\)** コマンドのみが表示されます。
    >
    > ![リポジトリを作成していない場合、Visual Studio には [Add to source control]\(ソース管理に追加\) が表示される](media/django/step01-git-add-to-source-control.png)

1. 変更ボタンをクリックすると、Visual Studio の **[変更]** ページに **[チーム エクスプローラー]** ウィンドウが開きます。 新しく作成されたプロジェクトは既にソース管理に自動的にコミットされているので、保留中の変更は表示されません。

    ![[変更] ページの [チーム エクスプローラー] ウィンドウ](media/django/step01-team-explorer-changes.png)

1. Visual Studio のステータス バーで、確定されていないコミット ボタン (**2** と表示された上向きの矢印) をクリックして、**[チーム エクスプローラー]** で **[同期]** ページを開きます。 ローカル リポジトリのみがあるため、ページには、リポジトリを別のリモート リポジトリに発行する簡単なオプションがあります。

    ![ソース管理に使用できる Git リポジトリ オプションを表示している [チーム エクスプローラー] ウィンドウ](media/django/step01-team-explorer.png)

    自身のプロジェクトにどちらのサービスでも選択できます。 このチュートリアルでは、GitHub の使用方法を示します。GitHub では、チュートリアルの完全なサンプル コードが [Microsoft/python-sample-vs-learning-django](https://github.com/Microsoft/python-sample-vs-learning-django) リポジトリに保持されます。

1. いずれかの **[発行]** コントロールを選択すると、 **[チーム エクスプローラー]** から詳細情報を要求されます。 たとえば、このチュートリアルのサンプルを発行する場合は、リポジトリ自体を最初に作成する必要があります。その場合、 **[Push to Remote Repository]\(リモート リポジトリにプッシュ\)** オプションがリポジトリの URL と共に使用されました。

    ![既存のリモート リポジトリにプッシュする [チーム エクスプローラー] ウィンドウ](media/django/step01-push-to-github.png)

    既存のリポジトリがない場合は、 **[Publish to GitHub]\(GitHub に発行\)** オプションと **[Azure DevOps へプッシュ]** オプションを使用して、Visual Studio から直接作成できます。

1. このチュートリアルを進めるときに、Visual Studio のコントロールを定期的に使用して変更をコミットおよびプッシュする習慣を付けてください。 このチュートリアルでは、適切な時点で通知します。

> [!Tip]
> **[チーム エクスプローラー]** 内をすばやく移動するには、ヘッダー (上の図では "**変更**" または "**プッシュ**" と表示されています) を選択して、使用可能なページのポップアップ メニューを表示します。

### <a name="question-what-are-some-advantages-of-using-source-control-from-the-beginning-of-a-project"></a>質問: プロジェクトの最初からソース管理を使用する利点は何ですか?

回答: まず、ソース管理を最初から使用すると、リモート リポジトリも使用する場合は特に、プロジェクトの定期的なオフサイト バックアップが提供されます。 ローカル ファイル システムだけでプロジェクトを保持するのとは異なり、ソース管理では完全な変更履歴も提供されるので、1 つのファイルまたはプロジェクト全体を以前の状態に簡単に戻すことができます。 変更履歴は回帰 (テスト不合格) の原因の特定に役立ちます。 さらに、ソース管理は上書きを管理し、競合の解決を提供するので、複数の人がプロジェクトを作業している場合に重要です。 最後に、基本的にオートメーションの 1 つの形式であるソース管理は、ビルド、テスト、リリース管理の自動化も可能にします。 プロジェクトで DevOps を使用する際のまさに最初の手順であり、使用開始の障壁はかなり低いので、最初からソース管理を使用しない理由はありません。

オートメーションとしてのソース管理について詳しくは、MSDN マガジンの記事「[The Source of Truth: The Role of Repositories in DevOps](/archive/msdn-magazine/2016/september/mobile-devops-the-source-of-truth-the-role-of-repositories-in-devops)」(信頼できる情報源: DevOps でのリポジトリの役割) をご覧ください。この記事はモバイル アプリ用に記述されていますが、Web アプリにも適用されます。

### <a name="question-can-i-prevent-visual-studio-from-auto-committing-a-new-project"></a>質問: Visual Studio が新しいプロジェクトを自動コミットしないようにすることはできますか?

回答: はい。 自動コミットを無効にするには、**[チーム エクスプローラー]** の **[設定]** ページに移動し、**[Git]** > **[グローバル設定]** を選択し、**[Commit changes after merge by default]\(既定では、マージ後に変更をコミット\)** というラベルの付いたオプションをオフにしてから **[更新]** を選択します。

## <a name="step-1-3-create-the-virtual-environment-and-exclude-it-from-source-control"></a>手順 1-3: 仮想環境を作成し、ソース管理から除外する

プロジェクトのソース管理を構成したら、プロジェクトに必要な Django パッケージを含む仮想環境を作成できることに注意してください。 その後、 **[チーム エクスプローラー]** を使用して、環境のフォルダーをソース管理から除外できます。

1. **ソリューション エクスプローラー** で **[Python 環境]** ノードを右クリックし、 **[仮想環境を追加]** を選択します。

    ![ソリューション エクスプローラーの [仮想環境の追加] コマンド](media/django/step01-add-virtual-environment-command.png)

1. **[仮想環境の追加]** ダイアログが開き、"**requirements.txt ファイルが見つかりました**" というメッセージが表示されます。 このメッセージは、Visual Studio がそのファイルを使用して仮想環境を構成することを示します。

    ![requirements.txt メッセージが表示された [仮想環境の追加] ダイアログ](media/django/step01-add-virtual-environment-found-requirements.png)

1. **[作成]** を選択して既定値を受け入れます (必要に応じて仮想環境の名前を変更できます (サブフォルダーの名前を変更するだけです) が、`env` が標準規則です)。

1. プロンプトが表示されたら管理者特権に同意します。Visual Studio がパッケージをダウンロードし、インストールするまで数分かかります。Django の場合、任意の数のサブフォルダーに数千のファイルが展開されます。 Visual Studio の **[出力]** ウィンドウで進行状況を確認できます。 待っている間、次の質問のセクションについて熟考してください。

1. (ステータス バーの) Visual Studio Git コントロールで、変更インジケーター (**99&#42;** と表示されます) を選択します。これにより、**[チーム エクスプローラー]** に **[変更]** ページが開きます。

    仮想環境の作成によって何千もの変更が生じましたが、あなた (またはプロジェクトをクローンしている他のすべてのユーザー) は *requirements.txt* からいつでも環境を再作成できるので、そのいずれもソース管理に含める必要はありません。

    仮想環境を除外するには、**env** フォルダーを右クリックし、 **[これらのローカル項目を無視]** を選択します。

    ![ソース管理の変更で仮想環境を無視する](media/django/step01-ignore-local-items.png)

1. 仮想環境を除外した後、残りの変更はプロジェクト ファイルと *.gitignore* に対するものだけです。 *.gitignore* ファイルには、仮想環境フォルダーの追加エントリが含まれています。 ファイルをダブルクリックして差分を確認できます。

1. コミット メッセージを入力し、 **[すべてコミット]** を選択してから、必要に応じてコミットをリモート リポジトリにプッシュします。

### <a name="question-why-do-i-want-to-create-a-virtual-environment"></a>質問: 仮想環境を作成する理由は何ですか?

回答: 仮想環境は、アプリの正確な依存関係を特定する優れた方法です。 このような特定により、グローバル Python 環境内での競合が回避され、テストとコラボレーションの両方が支援されます。 長い時間をかけて、アプリを開発するときに、多くの役立つ Python パッケージを必ず取り込むことになります。 プロジェクトに固有の仮想環境にパッケージを保持することで、ソース管理に含まれている、環境を説明するプロジェクトの *requirements.txt* ファイルを簡単に更新できます。 プロジェクトがビルド サーバー、展開サーバー、その他の開発用コンピューターなどの他のコンピューターにコピーされると、*requirements.txt* だけを使用して環境を簡単に作成し直すことができます (そのため、環境をソース管理する必要はありません)。 詳細については、「[仮想環境を使用する](selecting-a-python-environment-for-a-project.md#use-virtual-environments)」を参照してください。

### <a name="question-how-do-i-remove-a-virtual-environment-thats-already-committed-to-source-control"></a>質問: ソース管理に既にコミットされている仮想環境を削除するにはどうすればよいですか?

回答: 最初に、 *.gitignore* ファイルを編集してフォルダーを除外します。末尾にコメント `# Python Tools for Visual Studio (PTVS)` があるセクションを探し、`/BasicProject/env` などの仮想環境のフォルダー用の新しい行を追加します (Visual Studio ではファイルが **ソリューション エクスプローラー** に表示されないので、 **[ファイル]**  >  **[開く]**  >  **[ファイル]** メニュー コマンドを使用して直接開きます。 **[チーム エクスプローラー]** からファイルを開くこともできます。**[設定]** ページで、**[リポジトリ設定]** を選択し、**[無視および属性ファイル]** セクションに移動し、**.gitignore** の横の **[編集]** リンクを選択します)。

次に、コマンド ウィンドウを開き、*env* などの仮想環境のフォルダーを含む *BasicProject* のようなフォルダーに移動し、`git rm -r env` を実行します。 さらに、コマンドラインからこれらの変更をコミットするか (`git commit -m 'Remove venv'`)、**[チーム エクスプローラー]** の **[変更]** ページからコミットします。

## <a name="step-1-4-examine-the-boilerplate-code"></a>手順 1-4: 定型コードを確認する

プロジェクトの作成が完了したら、定型 Django プロジェクト コードを確認します (これは CLI コマンド `django-admin startproject <project_name>` によって生成されるコードと同じです)。

1. プロジェクトのルートには *manage.py* があります。これは、Visual Studio によってプロジェクトのスタートアップ ファイルとして自動的に設定される Django コマンドライン管理ユーティリティです。 コマンドラインで `python manage.py <command> [options]` を使用してユーティリティを実行します。 Django の一般的なタスクの場合、Visual Studio は便利なメニュー コマンドを提供します。 **ソリューション エクスプローラー** でプロジェクトを右クリックし、 **[Python]** を選択して一覧を表示します。 このチュートリアルの過程では、これらのコマンドの一部が見られます。

    ![Python プロジェクトのコンテキスト メニューの Django コマンド](media/django/step01-django-commands-menu.png)

2. プロジェクトでは、フォルダーの名前はプロジェクトと同じです。 これには基本的な Django プロジェクト ファイルが含まれています。

   - *__init.py*: このフォルダーが Python パッケージであることを Python に通知する空のファイルです。
   - *wsgi.py*: プロジェクトを処理する WSGI 互換 Web サーバーのエントリ ポイントです。 通常、このファイルは実稼働 Web サーバーのフックを提供するため、現状のままにします。
   - *settings.py*: Web アプリの開発の過程で変更する Django プロジェクトの設定が含まれています。
   - *urls.py*: 同様に開発の過程で変更する Django プロジェクトの目次が含まれています。

     ![ソリューション エクスプローラーでの Django プロジェクト ファイル](media/django/step01-django-project-in-solution-explorer.png)

3. 前に示したように、Visual Studio テンプレートは Django パッケージの依存関係を指定する *requirements.txt* ファイルもプロジェクトに追加します。 このファイルの存在は、プロジェクトを最初に作成するときに仮想環境の作成を求めるものです。

### <a name="question-can-visual-studio-generate-a-requirementstxt-file-from-a-virtual-environment-after-i-install-other-packages"></a>質問: Visual Studio では、他のパッケージをインストールした後に仮想環境から requirements.txt ファイルを生成できますか?

回答: はい。 **[Python 環境]** ノードを展開し、仮想環境を右クリックして、 **[requirements.txt を生成]** を選択します。 環境を変更するときにこのコマンドを定期的に使用し、その環境に依存するその他のコード変更と共に *requirements.txt* に対する変更をソース管理にコミットすることをお勧めします。 ビルド サーバーに継続的インテグレーションを設定する場合は、環境を変更するたびに、ファイルを生成し、変更をコミットする必要があります。

## <a name="step-1-5-run-the-empty-django-project"></a>手順 1-5: 空の Django プロジェクトを実行する

1. Visual Studio で、 **[デバッグ]**  >  **[デバッグの開始]** (**F5** キー) を選択するか、ツール バーの **[Web サーバー]** を使用します (表示されるブラウザーは異なる可能性があります)。

    ![Visual Studio の [Web サーバー] ツールバー ボタンを実行する](media/django/run-web-server-toolbar-button.png)

1. サーバーの実行は、Django の組み込み開発サーバーを起動するコマンド`manage.py runserver <port>` の実行を意味します。 Visual Studio に、スタートアップ ファイルがないことに関するメッセージと共に "**デバッガーを開始できませんでした**" と表示される場合は、**ソリューション エクスプローラー** で **manage.py** を右クリックし、**[スタートアップ ファイルとして設定]** を選択します。

1. サーバーを起動すると、サーバー ログも表示するコンソール ウィンドウが開きます。 Visual Studio では、ブラウザーで自動的に `http://localhost:<port>` が開きます。 ただし、Django プロジェクトにはアプリがないので、Django には、これまで正常に動作していることを確認する既定のページのみが表示されます。

    ![Django プロジェクトの既定のビュー](media/django/step01-first-run-success.png)

1. 完了したら、コンソール ウィンドウを閉じるか Visual Studio の **[デバッグ]**  >  **[デバッグの停止]** を使用してサーバーを停止します。

### <a name="question-is-django-a-web-server-as-well-as-a-framework"></a>質問: Django は Web サーバーおよびフレームワークですか?

回答: はい、そしていいえです。 Django には、開発目的で使用される組み込みの Web サーバーがあります。 この Web サーバーは、Visual Studio でデバッグする場合など、Web アプリをローカルで実行するときに使用されます。 一方、Web ホストにデプロイする場合、Django はホストの Web サーバーを代わりに使用します。 Django プロジェクトの *wsgi.py* モジュールは、実稼働サーバーへのフックに対処します。

### <a name="question-whats-the-difference-between-using-the-debug-menu-commands-and-the-server-commands-on-the-projects-python-submenu"></a>質問: [デバッグ] メニュー コマンドとプロジェクトの Python サブメニュー上のサーバー コマンドの使用にはどのような違いがありますか?

回答: **[デバッグ]** メニュー コマンドとツール バー ボタンに加えて、プロジェクトのコンテキスト メニューの **[Python]**  >  **[Run server]\(サーバーの実行\)** または **[Python]**  >  **[Run debug server]\(デバッグ サーバーの実行\)** を使用してサーバーを起動することもできます。 どちらのコマンドも、実行中のサーバーのローカル URL (localhost:port) を表示するコンソール ウィンドウを開きます。 ただし、その URL を使用してブラウザーを手動で開く必要があり、デバッグ サーバーを実行しても、Visual Studio デバッガーは自動的に起動しません。 **[デバッグ]**  >  **[プロセスにアタッチ]** を使用して、必要に応じてデバッガーを実行中のプロセスに後でアタッチできます。

## <a name="next-steps"></a>次のステップ

現時点では、基本的な Django プロジェクトにはアプリが含まれません。 次の手順では、アプリを作成します。 通常は Django プロジェクトよりも Django アプリを使用することが多いので、現時点では定型ファイルについて詳しく知る必要はありません。

> [!div class="nextstepaction"]
> [ビューおよびページ テンプレートを使用して Django アプリを作成する](learn-django-in-visual-studio-step-02-create-an-app.md)

## <a name="go-deeper"></a>詳しい説明

- Django プロジェクト コード: [最初の Django アプリの作成、パート 1](https://docs.djangoproject.com/en/2.0/intro/tutorial01/) (docs.djangoproject.com)
- 管理ユーティリティ: [django-admin と manage.py](https://docs.djangoproject.com/en/2.0/ref/django-admin/) (docs.djangoproject.com)
- GitHub 上のチュートリアルのソース コード: [Microsoft/python-sample-vs-learning-django](https://github.com/Microsoft/python-sample-vs-learning-django)