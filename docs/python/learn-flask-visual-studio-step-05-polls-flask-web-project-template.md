---
title: Visual Studio での Flask 学習チュートリアル、手順 5、ポーリング プロジェクト テンプレート
titleSuffix: ''
description: Visual Studio プロジェクトのコンテキストにおける Flask の基本のチュートリアルです。具体的には、Polls Flask Web プロジェクトと Polls Flask/Jade Web プロジェクト テンプレートの機能について取り上げます。
ms.date: 01/07/2019
ms.topic: tutorial
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.custom: seodec18
monikerRange: vs-2017
ms.workload:
- python
- data-science
ms.openlocfilehash: fd67e527ccf62de17dc15a5415f573c9622a51e9
ms.sourcegitcommit: f1dff6c4532c43b0444aa12ea57e90bb7dba6fba
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/23/2021
ms.locfileid: "104805979"
---
# <a name="step-5-use-the-polls-flask-web-project-template"></a>手順 5: ポーリング Flask Web プロジェクト テンプレートを使用する

**前の手順: [完全な Flask Web プロジェクト テンプレートを使用する](learn-flask-visual-studio-step-04-full-flask-project-template.md)**

Visual Studio の "Flask Web プロジェクト" テンプレートについて理解したので、3 つ目の Flask テンプレートである "Polls Flask Web プロジェクト" について見てみましょう。これは同じコード ベースに基づいて構築されています。

この手順では、次の方法を学習します。

> [!div class="checklist"]
> - テンプレートからプロジェクトを作成し、データベースを初期化する (手順 5-1)
> - データ モデルを理解する (手順 5-2)
> - バッキング データ ストアを理解する (手順 5-3)
> - ポーリングの詳細と結果ビューを理解する (手順 5-4)

Visual Studio は、同じアプリを生成しますが、Jinja テンプレート エンジンに Jade 拡張子を使用する "Polls Flask/Jade Web プロジェクト" テンプレートも提供します。 詳細については、「[Step 4 - The Flask/Jade Web Project template](learn-flask-visual-studio-step-04-full-flask-project-template.md#the-flaskjade-web-project-template)」 (手順 4 - Flask/Jade Web プロジェクト テンプレート) を参照してください。

## <a name="step-5-1-create-the-project"></a>手順 5-1: プロジェクトの作成

1. Visual Studio で、**ソリューション エクスプローラー** に移動し、本チュートリアルの前述の手順で作成した **LearningFlask** ソリューションを右クリックし、 **[追加]**  >  **[新しいプロジェクト]** の順に選択します。 (または、新しいソリューションを使用する場合は、代わりに **[ファイル]**  >  **[新規]**  >  **[プロジェクト]** の順に選択します)。

1. [新しいプロジェクト] ダイアログで **Polls Flask Web プロジェクト** テンプレートを探して選択し、プロジェクト "FlaskPolls" を呼び出して、 **[OK]** を選択します。

1. Visual Studio の他のプロジェクト テンプレートと同様に、"Polls Flask Web プロジェクト" テンプレートには *requirements.txt* ファイルが含まれており、Visual Studio ではこれらの依存関係のインストール先を確認するメッセージが表示されます。 オプションを選択し、**仮想環境にインストール** して、 **[仮想環境の追加]** ダイアログで **[作成]** を選択して、既定値を受け入れます。 (このテンプレートには、Flask の他に、azure-storage と pymongo のパッケージも必要です。"Polls Flask/Jade Web プロジェクト" には pyjade も必要でした。)

1. **ソリューション エクスプローラー** を右クリックし、**[スタートアップ プロジェクトに設定]** を選択して、**FlaskPolls** プロジェクトを Visual Studio ソリューションの既定に設定します。 デバッガーを起動すると、太字で表示されているスタートアップ プロジェクトが実行されます。

1. **[デバッグ]**  >  **[デバッグの開始]** (**F5** キー) を選択するか、またはツールバーの **[Web サーバー]** ボタンを使用して、サーバーを実行します。

    ![Visual Studio の [Web サーバー] ツールバー ボタンを実行する](media/django/run-web-server-toolbar-button.png)

1. テンプレートで作成したアプリには [ホーム]、[詳細]、[連絡先] という 3 つのページがあり、上部のナビゲーション バーを使用して各ページ間を移動できます。 1、2 分とって、アプリのさまざまな部分を確認してみましょう ([詳細] ページと [連絡先] ページは "Flask Web プロジェクト" とよく似ていますが、ここでは詳しく説明しません)。

    ![Polls Flask Web プロジェクト アプリの完全なビュー](media/flask/step06-full-app-view.png)

1. ホーム ページの **[Create Sample Polls]\(サンプル ポーリングの作成\)** ボタンは、*models/samples.json* ページに記載されている 3 つの異なるポーリングを使用して、アプリのデータ ストアを初期化します。 既定では、アプリは ([詳細] ページに表示されているように) メモリ内データベースを使用します。これはアプリを再起動するたびにリセットされます。 アプリには、Azure Storage と Mongo DB で機能するコードも含まれています。これについてはこの記事で後述します。

1. データ ストアを初期化すると、ホーム ページに示されているように (簡略化のためナビゲーション バーとフッターは省略されています)、さまざまなポーリングに投票することができます。

    ![データ ストアが初期化された後のポーリング アプリのビュー](media/flask/step06-polls-initialized.png)

1. ポーリングを選択すると、それ専用の選択肢が表示されます。

    ![ポーリングの投票インターフェイス](media/flask/step06-polls-voting-interface.png)

1. 投票すると、アプリにより結果ページが表示され、再度投票することができます。

    ![投票後の結果ビュー](media/flask/step06-polls-results.png)

1. 以降のセクションのために、アプリを実行したままにすることができます。

    アプリを停止して [ソース コントロールへの変更をコミットする](learn-flask-visual-studio-step-02-create-app.md#commit-to-source-control)場合、最初に **チーム エクスプローラー** で **[変更]** を開き、仮想環境のフォルダー (通常は **env**) を右クリックして、**[これらのローカル項目を無視]** を選択します。

### <a name="examine-the-project-contents"></a>プロジェクトの内容を確認する

前述のように、 Visual Studio で他のプロジェクト テンプレートを確認したことがある場合は、"Polls Flask Web プロジェクト" テンプレート (および "Polls Flask/Jade Web プロジェクト" テンプレート) から作成されたプロジェクトの多くの部分は見慣れているはずです。 この記事の追加手順では、データ モデルや追加のビューなど、より重要な変更や追加についてまとめています。

## <a name="step-5-2-understand-the-data-models"></a>手順 5-2: データ モデルを理解する

このアプリのデータ モデルは、*models/\_\_init\_\_.py* で定義されている Poll および Choice という名前の Python クラスです。 Poll は質問を表し、Choice インスタンスのコレクションはそれに対する使用可能な回答を表します。 Poll では、(すべての選択に対する) 投票の合計数と、ビューの生成に使用される統計を計算するメソッドも保持されます。

```python
class Poll(object):
    """A poll object for use in the application views and repository."""
    def __init__(self, key=u'', text=u''):
        """Initializes the poll."""
        self.key = key
        self.text = text
        self.choices = []
        self.total_votes = None

    def calculate_stats(self):
        """Calculates some statistics for use in the application views."""
        total = 0
        for choice in self.choices:
            total += choice.votes
        for choice in self.choices:
            choice.votes_percentage = choice.votes / float(total) * 100 \
                if total > 0 else 0
        self.total_votes = total

class Choice(object):
    """A poll choice object for use in the application views and repository."""
    def __init__(self, key=u'', text=u'', votes=0):
        """Initializes the poll choice."""
        self.key = key
        self.text = text
        self.votes = votes
        self.votes_percentage = None
```

これらのデータ モデルは、アプリのビューをさまざまな種類のバッキング データ ストア (次の手順で説明します) に対して動作できるようにする汎用の抽象化です。

## <a name="step-5-3-understand-the-backing-data-stores"></a>手順 5-3: バッキング データ ストアを理解する

"Polls Flask Web プロジェクト" テンプレートによって作成されたアプリは、メモリ、Azure テーブル ストレージ、または Mongo DB データベースのデータ ストアに対して実行できます。

データ ストレージのメカニズムは次のように機能します。

1. リポジトリの種類は `REPOSITORY_NAME` 環境変数で指定されます。この変数は、"memory"、"azuretablestore" または "mongodb" に設定することができます。 *settings.py* 内のコードのビットは、"memory" を既定値として使用して、名前を取得します。 バッキング ストアを変更する場合は、環境変数を設定してアプリを再起動する必要があります。

    ```python
    from os import environ
    REPOSITORY_NAME = environ.get('REPOSITORY_NAME', 'memory')
    ```

1. *settings.py* コードは次に `REPOSITORY_SETTINGS` オブジェクトを初期化します。 Azure テーブル ストアまたは Mondo DB を使用する場合は、まずこれらのデータ ストアを他の場所に初期化してから、ストアに接続する方法をアプリに指示するために必要な環境変数を設定する必要があります。

    ```python
    if REPOSITORY_NAME == 'azuretablestorage':
        REPOSITORY_SETTINGS = {
            'STORAGE_NAME': environ.get('STORAGE_NAME', ''),
            'STORAGE_KEY': environ.get('STORAGE_KEY', ''),
            'STORAGE_TABLE_POLL': environ.get('STORAGE_TABLE_POLL', 'polls'),
            'STORAGE_TABLE_CHOICE': environ.get('STORAGE_TABLE_CHOICE', 'choices'),
        }
    elif REPOSITORY_NAME == 'mongodb':
        REPOSITORY_SETTINGS = {
            'MONGODB_HOST': environ.get('MONGODB_HOST', None),
            'MONGODB_DATABASE': environ.get('MONGODB_DATABASE', 'polls'),
            'MONGODB_COLLECTION': environ.get('MONGODB_COLLECTION', 'polls'),
        }
    elif REPOSITORY_NAME == 'memory':
        REPOSITORY_SETTINGS = {}
    else:
        raise ValueError('Unknown repository.')
    ```

1. *views.py* では、アプリがファクトリ メソッドを呼び出して、データ ストアの名前と設定を使用して `Repository` オブジェクトを初期化します。

    ```python
    from FlaskPolls.models import PollNotFound
    from FlaskPolls.models.factory import create_repository
    from FlaskPolls.settings import REPOSITORY_NAME, REPOSITORY_SETTINGS

    repository = create_repository(REPOSITORY_NAME, REPOSITORY_SETTINGS)
    ```

1. `factory.create_repository` メソッドが (適切なリポジトリ モジュールを単にインポートする) *models\factory.py* で検出されると、`Repository` インスタンスを作成します。

    ```python
    def create_repository(name, settings):
        """Creates a repository from its name and settings. The settings
        is a dictionary where the keys are different for every type of repository.
        See each repository for details on the required settings."""
        if name == 'azuretablestorage':
            from .azuretablestorage import Repository
        elif name == 'mongodb':
            from .mongodb import Repository
        elif name == 'memory':
            from .memory import Repository
        else:
            raise ValueError('Unknown repository.')

        return Repository(settings)
    ```

1. 各データ ストアに固有の `Repository` クラスの実装は、*models\azuretablestorage.py*、*models\mongodb.py*、*models\memory.py* で見つかります。 Azure ストレージの実装では、azure-storage パッケージを使用します。Mongo DB の実装では、pymongo パッケージを使用します。 手順 5-1 に記載されているように、どちらのパッケージもプロジェクト テンプレートの *requirements.txt* ファイルに含まれています。 詳しい調査は読者の課題として残しておきます。

要するに、`Repository` クラスはデータ ストアの詳細を抽象化し、アプリは実行時に環境変数を使用して、3 つの実装のうち使用する実装を選択して構成します。

次の手順は、必要な場合に、プロジェクト テンプレートによって提供される 3 つのデータ ストアとは異なるデータ ストアのサポートを追加します。

1. `Repository` クラスの基本インターフェイスを得るため、*memory.py* を新しいファイルにコピーします。
1. 使用しているデータ ストア応じて、クラスの実装を変更します。
1. *factory.py* を変更して、追加したデータ ストアの名前を認識し、適切なモジュールをインポートする別の `elif` ケースを追加します。
1. *settings.py* を変更して、`REPOSITORY_NAME` 環境変数で別の名前を認識し、それに応じて `REPOSITORY_SETTINGS` を初期化します。

### <a name="seed-the-data-store-from-samplesjson"></a>samples.json からデータ ストアをシードする

最初は、選択したデータ ストアにはポーリングが含まれていないため、アプリのホーム ページに "**No polls available**" (使用可能なポーリングがありません) というメッセージが **[Create Sample Polls]\(サンプル ポーリングの作成\)** ボタンとともに表示されます。 ただし、ボタンを選択するとビューが変更され、使用可能なポーリングが表示されます。 この切り替えは、*templates\index.html* で条件タグを使用して行われます (簡略化のため、一部の空白行は省略されています)。

```html
{% extends "layout.html" %}
{% block content %}
<h2>{{title}}.</h2>

{% if polls %}
<table class="table table-hover">
    <tbody>
        {% for poll in polls %}
        <tr>
            <td>
                <a href="/poll/{{poll.key}}">{{poll.text}}</a>
            </td>
        </tr>
        {% endfor %}
    </tbody>
</table>
{% else %}
<p>No polls available.</p>
<br />
<form action="/seed" method="post">
    <button class="btn btn-primary" type="submit">Create Sample Polls</button>
</form>
{% endif %}
{% endblock %}
```

テンプレート内の `polls` 変数は `repository.get_polls` への呼び出しに由来しています。これは、データ ストアが初期化されるまで何も返しません。

**[Create Sample Polls]\(サンプル ポーリングの作成\)** ボタンを選択すると、/seed URL に移動します。 そのルートのハンドラーは、*views.py* で定義されています。

```python
@app.route('/seed', methods=['POST'])
def seed():
    """Seeds the database with sample polls."""
    repository.add_sample_polls()
    return redirect('/')
```

`repository.add_sample_polls()` への呼び出しは、選択したデータ ストアへの特定の `Repository` の実装のうちの 1 つになります。 実装ごとに *models\_\_init\_\_.py* で検出された `_load_samples_json` メソッドが呼び出され、*models\samples.json* ファイルがメモリに読み込まれます。次に、そのデータが反復処理され、データ ストア内に必要な `Poll` オブジェクトと `Choice` オブジェクトが作成されます。

この処理が完了すると、`seed` メソッドの `redirect('/')` ステートメントにより、ホーム ページに戻ります。 `repository.get_polls` でデータ オブジェクトが返されるようになったため、*templates\index.html* の条件タグはポーリングを含むテーブルをレンダリングするようになります。

### <a name="question-how-does-one-add-new-polls-to-the-app"></a>質問: アプリに新しいポーリングを追加するにはどうすればよいですか。

回答: プロジェクト テンプレートによって提供されるアプリには、ポーリングを追加または編集するための機能が含まれていません。 *models\samples.json* を変更して、新しい初期化データを作成することはできますが、これを行うことは、データ ストアがリセットされることを意味します。 編集機能を実装するには、メソッドを使用して `Repository` クラス インターフェイスを拡張して必要な `Choice` および `Poll`のインスタンスを作成してから、これらのメソッドを使用する追加ページに UI を実装します。

## <a name="step-5-4-understand-the-poll-detail-and-results-views"></a>手順 5-4: ポーリングの詳細と結果ビューを理解する

"Polls Flask Web プロジェクト" テンプレートおよび "Polls Flask/Jade Web プロジェクト" テンプレートで生成されるビュー ([詳細] ページや [連絡先] ページのビューなど) のほとんどは、このチュートリアルで使用した "Flask Web プロジェクト" (または "Flask/Jade Web プロジェクト") テンプレートによって作成されるビューとよく似ています。 前のセクションでは、初期化ボタンまたはポーリングの一覧のいずれかを示すため、ホーム ページがどのように実装されるかについても学習しました。

ここでは、投票 (詳細) と個々のポーリングの結果ビューを確認します。

ホーム ページからポーリングを選択すると、アプリは URL /poll/\<key\> に移動します。*key* はポーリングの一意の識別子です。 *views.py* では、`details` 関数が GET と要求の両方の URL ルーティングを処理するために割り当てられていることがわかります。 また、URL ルートでの `<key>` の使用によりそのフォームの任意のルートが同じ関数にマップされ、その同じ名前の関数への引数が生成されることもわかります。

```python
@app.route('/poll/<key>', methods=['GET', 'POST'])
def details(key):
    """Renders the poll details page."""
    error_message = ''
    if request.method == 'POST':
        try:
            choice_key = request.form['choice']
            repository.increment_vote(key, choice_key)
            return redirect('/results/{0}'.format(key))
        except KeyError:
            error_message = 'Please make a selection.'

    return render_template(
        'details.html',
        title='Poll',
        year=datetime.now().year,
        poll=repository.get_poll(key),
        error_message=error_message,
    )
```

ポーリング (GET 要求) を表示するため、この関数は *templates\details.html* を呼び出します。これは、ポーリングの `choices` 配列で反復処理行い、そのたびにラジオ ボタンを作成します。

```html
{% extends "layout.html" %}

{% block content %}

<h2>{{poll.text}}</h2>
<br />

{% if error_message %}
<p class="text-danger">{{error_message}}</p>
{% endif %}

<form action="/poll/{{poll.key}}" method="post">
    {% for choice in poll.choices %}
    <div class="radio">
        <label>
            <input type="radio" name="choice" id="choice{{choice.key}}" value="{{choice.key}}" />
            {{ choice.text }}
        </label>
    </div>
    {% endfor %}
    <br />
    <button class="btn btn-primary" type="submit">Vote</button>
</form>

{% endblock %}
```

**[投票]** ボタンには `type="submit"` があるため、選択すると、もう一度 `details` 関数にルーティングされるのと同じ URL に戻される POST 要求が生成されます。 しかし、今回は、フォーム データから選択肢が抽出され、/results/\<choice\> にリダイレクトされます。

その後、/results/\<key\> URL は *views.py* の `results` 関数にルーティングされます。これはその後、ポーリングの `calculate_stats` メソッドを呼び出し、レンダリングに *templates\results.html* を使用します。

```python
@app.route('/results/<key>')
def results(key):
    """Renders the results page."""
    poll = repository.get_poll(key)
    poll.calculate_stats()
    return render_template(
        'results.html',
        title='Results',
        year=datetime.now().year,
        poll=poll,
    )
```

一方、*results.html* テンプレートはポーリングの選択肢を単純に反復処理して、それぞれの進行状況バーを生成します。

```html
{% extends "layout.html" %}

{% block content %}

<h2>{{poll.text}}</h2>
<br />

{% for choice in poll.choices %}
<div class="row">
    <div class="col-sm-5">{{choice.text}}</div>
    <div class="col-sm-5">
        <div class="progress">
            <div class="progress-bar" role="progressbar" aria-valuenow="{{choice.votes}}" aria-valuemin="0" aria-valuemax="{{poll.total_votes}}" style="width: {{choice.votes_percentage}}%;">
                {{choice.votes}}
            </div>
        </div>
    </div>
</div>
{% endfor %}

<br />
<a class="btn btn-primary" href="/poll/{{poll.key}}">Vote again?</a>

{% endblock %}
```

## <a name="next-steps"></a>次のステップ

> [!Note]
> このチュートリアルの途中で Visual Studio ソリューションをソース コード管理にコミットした場合は、もう 1 つのコミットを実行することをお勧めします。 ソリューションは、GitHub [Microsoft/python-sample-vs-learning-flask](https://github.com/Microsoft/python-sample-vs-learning-flask) のチュートリアル ソース コードと一致するようにします。

Visual Studio で "Blank Flask Web プロジェクト"、"Flask[/Jade] Web プロジェクト"、"Polls Flask[/Jade] Web プロジェクト" の各テンプレートを全体的に確認しました。 Flask のすべての基本 (ビュー、テンプレート、ルーティングの使用など) を学習し、バッキング データ ストアの使用方法について確認しました。 これで、必要なビューとモデルがある独自の Web アプリの使用を開始できるようになったはずです。

開発用コンピューター上で Web アプリを実行することは、アプリを顧客に提供するための単なる 1 つの手順です。 今後の手順には、以下のようなタスクがあります。

- Web アプリを Azure App Service などの運用サーバーに展開します。 「[Azure App Service に発行する](publishing-python-web-applications-to-azure-from-visual-studio.md)」を参照してください。

- PostgreSQL、MySQL、SQL Server など (これらはいずれも Azure でホストできます) など、別の運用レベルのデータ ストアを使用するリポジトリの実装を追加します。 テーブルや BLOB のような Azure ストレージ サービスと Cosmos DB を使用する場合は、[Azure SDK for Python](/azure/python/) も使用できます。

- Azure DevOps などのサービスに対して、継続的インテグレーション/継続的配置パイプラインを設定します。 (Azure Repos、GitHub、または他の場所で) ソース コード管理を使用するだけでなく、リリースの前提条件として単体テストを自動的に実行するよう、Azure DevOps プロジェクトを構成することができます。また、運用環境にデプロイする前に、追加テストのためにステージング サーバーにデプロイするパイプラインを構成することもできます。 さらに、Azure DevOps は App Insights などの監視ソリューションと統合されているので、アジャイル計画ツールを使用してサイクル全体に対応することができます。 詳細については、「[Azure DevOps Projects を使用して Python 用の CI/CD パイプラインを作成する](/azure/devops-project/azure-devops-project-python?view=vsts&preserve-view=true)」、および一般的な [Azure DevOps ドキュメント](/azure/devops/?view=vsts&preserve-view=true)を参照してください。
