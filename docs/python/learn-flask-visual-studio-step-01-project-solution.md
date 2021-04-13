---
title: Visual Studio での Flask 学習チュートリアル、手順 1、Flask 基本
titleSuffix: ''
description: Visual Studio プロジェクトにおける Flask の基本のチュートリアル。前提条件、Git、仮想環境など。
ms.date: 01/07/2019
ms.topic: tutorial
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: 89a84198256657ae7f94d0a923780163bee73e48
ms.sourcegitcommit: 5c0e20fc6005bc1f8ca38f4122378c4ac21ba89a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/01/2021
ms.locfileid: "106110611"
---
# <a name="tutorial-get-started-with-the-flask-web-framework-in-visual-studio"></a>チュートリアル: Visual Studio での Flask Web フレームワークの概要

[Flask](https://palletsprojects.com/p/flask/) は Web アプリケーション用の軽量 Python フレームワークであり、URL のルーティングとページのレンダリングの基礎を提供します。

Flask は、フォームの検証、データベースの抽象化、認証などの機能を直接提供しないため、"マイクロ" フレームワークと呼ばれます。 このような機能は、Flask "*拡張機能*" と呼ばれる特別な Python パッケージによって代わりに提供されます。 拡張機能は Flask とシームレスに統合するので、Flask 自体の一部であるかのように見えます。 たとえば、Flask 自体ではページ テンプレート エンジンは提供されません。 テンプレートは、このチュートリアルで紹介するように Jinja や Jade などの拡張機能によって提供されます。

::: moniker range="vs-2017"
このチュートリアルでは、以下の内容を学習します。
- "空の Flask Web プロジェクト" テンプレートを使用して Git リポジトリに基本的な Flask プロジェクトを作成する (手順 1)
- 1 つのページがある Flask アプリを作成し、テンプレートを使用してそのページをレンダリングする (手順 2)
- 静的ファイルを提供し、ページを追加し、テンプレート継承を使用する (手順 3)
- Flask Web プロジェクト テンプレートを使用して、複数のページを持つ応答性に優れたデザインのアプリを作成する (手順 4)
- Polls Flask Web プロジェクト テンプレートを使用して、さまざまなストレージ オプション (Azure Storage、MongoDB、またはメモリ) を使用するポーリング アプリを作成する

一連の手順に従って、3 つの独立したプロジェクトを含む 1 つの Visual Studio ソリューションを作成します。 Visual Studio に含まれる異なる Flask プロジェクト テンプレートを使用して、プロジェクトを作成します。 同じソリューション内にプロジェクトを保持することで、異なるファイル間を簡単に切り替えて比較できます。
::: moniker-end

::: moniker range=">=vs-2019"

このチュートリアルでは、以下の内容を学習します。
- "空の Flask Web プロジェクト" テンプレートを使用して Git リポジトリに基本的な Flask プロジェクトを作成する (手順 1)
- 1 つのページがある Flask アプリを作成し、テンプレートを使用してそのページをレンダリングする (手順 2)
- 静的ファイルを提供し、ページを追加し、テンプレート継承を使用する (手順 3)
- Flask Web プロジェクト テンプレートを使用して、複数のページを持つ応答性に優れたデザインのアプリを作成する (手順 4)

一連の手順に従って、2 つの独立したプロジェクトを含む 1 つの Visual Studio ソリューションを作成します。 Visual Studio に含まれる異なる Flask プロジェクト テンプレートを使用して、プロジェクトを作成します。 同じソリューション内にプロジェクトを保持することで、異なるファイル間を簡単に切り替えて比較できます。
::: moniker-end

> [!Note]
> [Flask クイック スタート](../ide/quickstart-python.md?toc=/visualstudio/python/toc.json&bc=/visualstudio/python/_breadcrumb/toc.json)とは異なり、このチュートリアルでは、Flask の機能についていっそう詳しく説明すると共に、独自のプロジェクトの広範な起点となるさまざまな Flask プロジェクト テンプレートの使用方法を示します。 たとえば、プロジェクトを作成すると、プロジェクト テンプレートによって Flask パッケージが自動的にインストールされます。クイック スタートで示されているように手動でパッケージをインストールする必要はありません。

## <a name="prerequisites"></a>前提条件

- Windows 用の Visual Studio 2017 以降は次のオプションを備えています。
  - **Python 開発ワークロード** (インストーラーの **[ワークロード]** タブ)。 手順については、[Visual Studio での Python サポートのインストール](installing-python-support-in-visual-studio.md)に関するページをご覧ください。
  - **Windows 向け Git** と **Visual Studio 向け GitHub 拡張** ( **[個別のコンポーネント]** タブの **[コード ツール]** )。

Flask プロジェクト テンプレートは Python Tools for Visual Studio のすべての旧バージョンに含まれていますが、詳細は、このチュートリアルの説明と異なる場合があります。

現在、Visual Studio for Mac では Python 開発はサポートされていません。 Mac および Linux では、[Visual Studio Code で Python 拡張](https://code.visualstudio.com/docs/python/python-tutorial)を使用します。

## <a name="step-1-1-create-a-visual-studio-project-and-solution"></a>手順 1-1: Visual Studio プロジェクトとソリューションを作成する

1. Visual Studio で、 **[ファイル]**  >  **[新規]**  >  **[プロジェクト]** の順に選択し、"Flask" を検索して、 **[Blank Flask Web プロジェクト]** テンプレートを選択します (テンプレートは、左側の一覧の **[Python]**  >  **[Web]** にもあります)。

    ![Visual Studio での Blank Flask Web プロジェクト用の [新しいプロジェクト] ダイアログ ボックス](media/flask/step01-new-blank-project.png)

1. ダイアログの下部にあるフィールドで、(前の図に示したように) 次の情報を入力し、 **[OK]** を選択します。

    - **名前**: Visual Studio プロジェクトの名前を「**BasicProject**」に設定します。 この名前は Flask プロジェクトにも使用されます。
    - **場所**: Visual Studio ソリューションとプロジェクトを作成する場所を指定します。
    - **ソリューション名**: このチュートリアルでは複数プロジェクトのコンテナーとしてのソリューションに適した「**LearningFlask**」に設定します。
    - **ソリューションのディレクトリを作成**: オンのままにします (既定)。
    - **新しい Git リポジトリの作成**: ソリューションの作成時に Visual Studio でローカルの Git リポジトリが作成されるように、このオプション (既定ではオフ) をオンにします。 このオプションが表示されない場合は、Visual Studio インストーラーを実行し、**[コード ツール]** の **[個別のコンポーネント]** タブで **Windows 用 Git** および **Visual Studio 用 GitHub 拡張機能** を追加します。

1. しばらくすると、Visual Studio に (次に示すように) "**このプロジェクトには外部パッケージが必要です**" というダイアログが表示されます。 テンプレートには、最新の Flask 1.x パッケージを参照する *requirements.txt* ファイルが含まれているため、このダイアログが表示されます (正確な依存関係を確認するには **[必要なパッケージを表示]** を選択します)。

    ![プロジェクトに外部パッケージが必要であることを示すプロンプト](media/tutorials-common/step01-requirements-prompt-install-myself.png)

1. オプション **[I will install them myself]\(自分でインストールする\)** を選択します。 仮想環境を簡単に作成し、ソース管理から除外されていることを確認します (環境はいつでも *requirements.txt* から作成できます)。

## <a name="step-1-2-examine-the-git-controls-and-publish-to-a-remote-repository"></a>手順 1-2: Git コントロールを確認し、リモート リポジトリに発行する

**[新しいプロジェクト]** ダイアログで **[新しい Git リポジトリの作成]** を選択したため、作成プロセスが完了するとすぐに、プロジェクトは既にローカル ソース管理にコミットされています。 この手順では、Visual Studio の Git コントロールと、ソース管理を操作する **[チーム エクスプローラー]** ウィンドウについて理解します。

1. Visual Studio のメイン ウィンドウの下隅にある Git コントロールを確認します。 これらのコントロールは、左から右の順に、確定されていないコミット、確定されていない変更、リポジトリの名前、現在のブランチを示します。

    ![Visual Studio ウィンドウの Git コントロール](media/flask/step01-git-controls.png)

    > [!Note]
    > **[新しいプロジェクト]** ダイアログで **[新しい Git リポジトリの作成]** を選択しない場合、Git コントロールには、ローカル リポジトリを作成する **[Add to source control]\(ソース管理に追加\)** コマンドのみが表示されます。
    >
    > ![リポジトリを作成していない場合、Visual Studio には [Add to source control]\(ソース管理に追加\) が表示される](media/tutorials-common/step01-git-add-to-source-control.png)

1. 変更ボタンをクリックすると、Visual Studio の **[変更]** ページに **[チーム エクスプローラー]** ウィンドウが開きます。 新しく作成されたプロジェクトは既にソース管理に自動的にコミットされているので、保留中の変更は表示されません。

    ![[変更] ページの [チーム エクスプローラー] ウィンドウ](media/flask/step01-team-explorer-changes.png)

1. Visual Studio のステータス バーで、確定されていないコミット ボタン (**2** と表示された上向きの矢印) をクリックして、**[チーム エクスプローラー]** で **[同期]** ページを開きます。 ローカル リポジトリのみがあるため、ページには、リポジトリを別のリモート リポジトリに発行する簡単なオプションがあります。

    ![ソース管理に使用できる Git リポジトリ オプションを表示している [チーム エクスプローラー] ウィンドウ](media/flask/step01-team-explorer.png)

    自身のプロジェクトにどちらのサービスでも選択できます。 このチュートリアルでは、GitHub の使用方法を示します。GitHub では、チュートリアルの完全なサンプル コードが [Microsoft/python-sample-vs-learning-flask](https://github.com/Microsoft/python-sample-vs-learning-flask) リポジトリに保持されます。

1. いずれかの **[発行]** コントロールを選択すると、 **[チーム エクスプローラー]** から詳細情報を要求されます。 たとえば、このチュートリアルのサンプルを発行する場合は、リポジトリ自体を最初に作成する必要があります。その場合、 **[Push to Remote Repository]\(リモート リポジトリにプッシュ\)** オプションがリポジトリの URL と共に使用されました。

    ![既存のリモート リポジトリにプッシュする [チーム エクスプローラー] ウィンドウ](media/flask/step01-push-to-github.png)

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

プロジェクトのソース管理を構成したら、プロジェクトに必要な Flask パッケージの仮想環境を作成できます。 その後、 **[チーム エクスプローラー]** を使用して、環境のフォルダーをソース管理から除外できます。

1. **ソリューション エクスプローラー** で **[Python 環境]** ノードを右クリックし、 **[仮想環境を追加]** を選択します。

    ![ソリューション エクスプローラーの [仮想環境の追加] コマンド](media/flask/step01-add-virtual-environment-command.png)

1. **[仮想環境の追加]** ダイアログが開き、"**requirements.txt ファイルが見つかりました**" というメッセージが表示されます。 このメッセージは、Visual Studio がそのファイルを使用して仮想環境を構成することを示します。

    ![requirements.txt メッセージが表示された [仮想環境の追加] ダイアログ](media/tutorials-common/step01-add-virtual-environment-found-requirements.png)

1. **[作成]** を選択して既定値を受け入れます (必要に応じて仮想環境の名前を変更できます (サブフォルダーの名前を変更するだけです) が、`env` が標準規則です)。

1. プロンプトが表示されたら管理者特権に同意します。Visual Studio がパッケージをダウンロードし、インストールするまで数分かかります。Flask とその依存関係の場合、100 以上のサブフォルダーに数千のファイルが展開されます。 Visual Studio の **[出力]** ウィンドウで進行状況を確認できます。 待っている間、次の質問のセクションについて熟考してください。 Flask の依存関係の説明については、[Flask インストール](https://flask.palletsprojects.com/en/1.0.x/installation/#installation)のページ (flask.pcocoo.org) でも確認できます。

1. (ステータス バーの) Visual Studio Git コントロールで、変更インジケーター (**99&#42;** と表示されます) を選択します。これにより、**[チーム エクスプローラー]** に **[変更]** ページが開きます。

    仮想環境の作成によって何百もの変更が生じましたが、あなた (またはプロジェクトをクローンしている他のすべてのユーザー) は *requirements.txt* からいつでも環境を再作成できるので、そのいずれもソース管理に含める必要はありません。

    仮想環境を除外するには、**env** フォルダーを右クリックし、 **[これらのローカル項目を無視]** を選択します。

    ![ソース管理の変更で仮想環境を無視する](media/flask/step01-ignore-local-items.png)

1. 仮想環境を除外した後、残りの変更はプロジェクト ファイルと *.gitignore* に対するものだけです。 *.gitignore* ファイルには、仮想環境フォルダーの追加エントリが含まれています。 ファイルをダブルクリックして差分を確認できます。

1. コミット メッセージを入力し、 **[すべてコミット]** を選択してから、必要に応じてコミットをリモート リポジトリにプッシュします。

### <a name="question-why-do-i-want-to-create-a-virtual-environment"></a>質問: 仮想環境を作成する理由は何ですか?

回答: 仮想環境は、アプリの正確な依存関係を特定する優れた方法です。 このような特定により、グローバル Python 環境内での競合が回避され、テストとコラボレーションの両方が支援されます。 長い時間をかけて、アプリを開発するときに、多くの役立つ Python パッケージを必ず取り込むことになります。 プロジェクトに固有の仮想環境にパッケージを保持することで、ソース管理に含まれている、環境を説明するプロジェクトの *requirements.txt* ファイルを簡単に更新できます。 プロジェクトがビルド サーバー、展開サーバー、その他の開発用コンピューターなどの他のコンピューターにコピーされると、*requirements.txt* だけを使用して環境を簡単に作成し直すことができます (そのため、環境をソース管理する必要はありません)。 詳細については、「[仮想環境を使用する](selecting-a-python-environment-for-a-project.md#use-virtual-environments)」を参照してください。

### <a name="question-how-do-i-remove-a-virtual-environment-thats-already-committed-to-source-control"></a>質問: ソース管理に既にコミットされている仮想環境を削除するにはどうすればよいですか?

回答: 最初に、 *.gitignore* ファイルを編集してフォルダーを除外します。末尾にコメント `# Python Tools for Visual Studio (PTVS)` があるセクションを探し、`/BasicProject/env` などの仮想環境のフォルダー用の新しい行を追加します (Visual Studio ではファイルが **ソリューション エクスプローラー** に表示されないので、 **[ファイル]**  >  **[開く]**  >  **[ファイル]** メニュー コマンドを使用して直接開きます。 **[チーム エクスプローラー]** からファイルを開くこともできます。**[設定]** ページで、**[リポジトリ設定]** を選択し、**[無視および属性ファイル]** セクションに移動し、**.gitignore** の横の **[編集]** リンクを選択します)。

次に、コマンド ウィンドウを開き、*env* などの仮想環境のフォルダーを含む *BasicProject* のようなフォルダーに移動し、`git rm -r env` を実行します。 さらに、コマンドラインからこれらの変更をコミットするか (`git commit -m 'Remove venv'`)、**[チーム エクスプローラー]** の **[変更]** ページからコミットします。

## <a name="step-1-4-examine-the-boilerplate-code"></a>手順 1-4: 定型コードを確認する

1. プロジェクトの作成が完了すると、**ソリューション エクスプローラー** にソリューションとプロジェクトが表示されますが、プロジェクトに含まれるファイルは *app.py* と *requirements.txt* の 2 つだけです。

    ![ソリューション エクスプローラーでの Blank Flask プロジェクト ファイル](media/flask/step01-blank-flask-project-in-solution-explorer.png)

1. 前に説明したように、*requirements.txt* ファイルでは Flask パッケージの依存関係が指定されています。 このファイルの存在は、プロジェクトを最初に作成するときに仮想環境の作成を求めるものです。

1. 1 つの *app.py* ファイルに 3 つの部分が含まれます。 1 番目の部分は Flask の `import` ステートメントであり、`Flask` クラスのインスタンスを作成した後 (インスタンスは変数 `app` に割り当てられます)、`wsgi_app` 変数を割り当てます (これは Web ホストを配置するときに便利ですが、現時点では使用されていません)。

    ```python
    from flask import Flask
    app = Flask(__name__)

    # Make the WSGI interface available at the top level so wfastcgi can get it.
    wsgi_app = app.wsgi_app
    ```

1. ファイルの最後にある 2 番目の部分は省略可能なコードであり、環境変数から取得された特定のホストとポートの値 (既定値は localhost:5555) を使用して Flask 開発サーバーを起動します。

    ```python
    if __name__ == '__main__':
        import os
        HOST = os.environ.get('SERVER_HOST', 'localhost')
        try:
            PORT = int(os.environ.get('SERVER_PORT', '5555'))
        except ValueError:
            PORT = 5555
        app.run(HOST, PORT)
    ```

1. 3 番目の部分は、URL に関数を割り当てる短いコードです。この関数は、URL によって識別されるリソースを提供します。 Flask の `@app.route` デコレーターを使用してルートを定義します。引数は、サイトのルートからの相対 URL です。 コードを見るとわかるように、この関数はテキスト文字列のみを返します。ブラウザーのレンダリングにはこれで十分です。 後に続く手順では、さらに豊富な内容のページを HTML でレンダリングします。

    ```python
    @app.route('/')
    def hello():
        """Renders a sample page."""
        return "Hello World!"
    ```

### <a name="question-what-is-the-purpose-of-the-__name__-argument-to-the-flask-class"></a>質問: Flask クラスに対する __name__ 引数の目的は何ですか?

回答: この引数はアプリのモジュールまたはパッケージの名前であり、アプリに属するテンプレート、静的ファイル、他のリソースを検索する場所を Flask に指示します。 1 つのモジュールに含まれているアプリの場合、`__name__` は常に適切な値です。 また、デバッグ情報を必要とする拡張機能にも重要です。 詳細およびその他の引数については、[Flask のクラスのドキュメント](https://flask.palletsprojects.com/en/1.0.x/api/#flask.Flask) (flask.pocoo.org) をご覧ください。

### <a name="question-can-a-function-have-more-than-one-route-decorator"></a>質問: 1 つの関数で複数のルート デコレーターを使用できますか?

回答: はい。同じ関数が複数のルートを提供している場合、必要なだけいくつでもデコレーターを使用できます。 たとえば、"/" と "/hello" の両方に対して `hello` 関数を使用するには、次のようなコードを使用します。

```python
@app.route('/')
@app.route('/hello')
def hello():
    """Renders a sample page."""
    return "Hello World!"
```

<a name="qa-url-variables"></a>

### <a name="question-how-does-flask-work-with-variable-url-routes-and-query-parameters"></a>質問: Flask は変数の URL ルートとクエリ パラメーターをどのように処理しますか?

応答: ルートでは、変数を `<variable_name>` でマークします。Flask は、URL パスの名前付き引数を使用して変数を関数に渡します。 たとえば、`/hello/<name>` 形式のルートの場合、`name` という名称の文字列引数が関数に生成されます。 クエリ パラメーターが `request.args` プロパティを通じて (具体的には `request.args.get` メソッド) 使用できます。 詳しくは、Flask のドキュメントで [Request オブジェクト](https://flask.palletsprojects.com/en/1.1.x/quickstart/#the-request-object)に関する説明をご覧ください。

```python
# URL: /hello/<name>?message=Have%20a%20nice%20day
@app.route('/hello/<name>')
def hello(name):
    msg = request.args.get('message','')
    return "Hello " + name + "! "+ msg + "."
```

型を変更するには、変数の前に `int`、`float`、`path` (フォルダー名を区切るためのスラッシュを受け付けます)、`uuid` を付加します。 詳しくは、Flask のドキュメントで[変数のルール](https://flask.palletsprojects.com/en/1.0.x/quickstart/#variable-rules)に関する説明をご覧ください。

### <a name="question-can-visual-studio-generate-a-requirementstxt-file-from-a-virtual-environment-after-i-install-other-packages"></a>質問: Visual Studio では、他のパッケージをインストールした後に仮想環境から requirements.txt ファイルを生成できますか?

回答: はい。 **[Python 環境]** ノードを展開し、仮想環境を右クリックして、 **[requirements.txt を生成]** を選択します。 環境を変更するときにこのコマンドを定期的に使用し、その環境に依存するその他のコード変更と共に *requirements.txt* に対する変更をソース管理にコミットすることをお勧めします。 ビルド サーバーに継続的インテグレーションを設定する場合は、環境を変更するたびに、ファイルを生成し、変更をコミットする必要があります。

## <a name="step-1-5-run-the-project"></a>手順 1-5: プロジェクトを実行する

1. Visual Studio で、 **[デバッグ]**  >  **[デバッグの開始]** (**F5** キー) を選択するか、ツール バーの **[Web サーバー]** を使用します (表示されるブラウザーは異なる可能性があります)。

    ![Visual Studio の [Web サーバー] ツールバー ボタンを実行する](media/tutorials-common/run-web-server-toolbar-button.png)

1. いずれのコマンドも、PORT 環境変数にランダムなポート番号を割り当ててから、`python app.py` を実行します。 コードは、Flask の開発サーバー内でそのポートを使用してアプリを起動します。 Visual Studio に、スタートアップ ファイルがないことに関するメッセージと共に "**デバッガーを開始できませんでした**" と表示される場合は、**ソリューション エクスプローラー** で **app.py** を右クリックし、**[スタートアップ ファイルとして設定]** を選択します。

1. サーバーが起動すると、コンソール ウィンドウが開いてサーバー ログが表示されます。 Visual Studio によってブラウザーで `http://localhost:<port>` が自動的に開かれ、`hello` 関数でレンダリングされたメッセージが表示されます。

    ![Flask プロジェクトの既定のビュー](media/flask/step01-first-run-success.png)

1. 完了したら、コンソール ウィンドウを閉じるか Visual Studio の **[デバッグ]**  >  **[デバッグの停止]** を使用してサーバーを停止します。

### <a name="question-whats-the-difference-between-using-the-debug-menu-commands-and-the-server-commands-on-the-projects-python-submenu"></a>質問: [デバッグ] メニュー コマンドとプロジェクトの Python サブメニュー上のサーバー コマンドの使用にはどのような違いがありますか?

回答: **[デバッグ]** メニュー コマンドとツール バー ボタンに加えて、プロジェクトのコンテキスト メニューの **[Python]**  >  **[Run server]\(サーバーの実行\)** または **[Python]**  >  **[Run debug server]\(デバッグ サーバーの実行\)** を使用してサーバーを起動することもできます。 どちらのコマンドも、実行中のサーバーのローカル URL (localhost:port) を表示するコンソール ウィンドウを開きます。 ただし、その URL を使用してブラウザーを手動で開く必要があり、デバッグ サーバーを実行しても、Visual Studio デバッガーは自動的に起動しません。 **[デバッグ]**  >  **[プロセスにアタッチ]** を使用して、必要に応じてデバッガーを実行中のプロセスに後でアタッチできます。

## <a name="next-steps"></a>次のステップ

この時点で、基本的な Flask プロジェクトには、スタートアップ コードとページ コードが同じファイルに含まれています。 これら 2 つは分けた方がよく、HTML とデータもテンプレートを使用して分離するのが最善の方法です。

> [!div class="nextstepaction"]
> [ビューおよびページ テンプレートを使用して Flask アプリを作成する](learn-flask-visual-studio-step-02-create-app.md)

## <a name="go-deeper"></a>詳しい説明

- [Flask クイック スタート](https://flask.palletsprojects.com/en/1.0.x/quickstart/)(flask.pocoo.org)
- GitHub 上のチュートリアルのソース コード: [Microsoft/python-sample-vs-learning-flask](https://github.com/Microsoft/python-sample-vs-learning-flask)