---
title: Visual Studio での Django チュートリアル手順 6、ポーリング プロジェクト テンプレート
titleSuffix: ''
description: Visual Studio プロジェクトのコンテキストにおける Django の基本のチュートリアルです。具体的には、管理者用のカスタマイズなど、ポーリング Django Web プロジェクト テンプレートの機能について取り上げます。
ms.date: 11/19/2018
ms.topic: tutorial
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: 5e524232eed7e4044454c57fc4fcaa30c6e2a8a0
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99942478"
---
# <a name="step-6-use-the-polls-django-web-project-template"></a>手順 6: ポーリング Django Web プロジェクト テンプレートを使用する

**前の手順:[Django でユーザーを認証する](learn-django-in-visual-studio-step-05-django-authentication.md)**

Visual Studio の "Django Web Project" テンプレートについて理解したので、3 つ目の Django テンプレートである "ポーリング Django Web プロジェクト" について見てみましょう。これは同じコード ベースに基づいて構築されており、データベースの使用例がわかるテンプレートです。

この手順では、次の方法を学習します。

> [!div class="checklist"]
> - テンプレートからプロジェクトを作成し、データベースを初期化する (手順 6-1)
> - データ モデルを理解する (手順 6-2)
> - 移行を適用する (手順 6-3)
> - プロジェクト テンプレートによって作成されたビューとページ テンプレートを理解する (手順 6-4)
> - カスタム管理インターフェイスを作成する (手順 6-5)

このテンプレートを使用して作成されるプロジェクトは、Django ドキュメントの「[Writing your first Django app](https://docs.djangoproject.com/en/2.0/intro/tutorial01/)」(最初の Django アプリを作成する) チュートリアルに従った場合のプロジェクトと似ています。この Web アプリは、ユーザーが投票を表示し、投票することができるパブリック サイトと、投票を管理できる管理インターフェイスから構成されています。 以下のセクションで説明するように、"Django Web プロジェクト" テンプレートと同じ認証システムを使用し、Django モデルを実装してデータベースをより活用しています。

## <a name="step-6-1-create-the-project-and-initialize-the-database"></a>手順 6-1:プロジェクトを作成し、データベースを初期化する

1. Visual Studio で、**ソリューション エクスプローラー** に移動して、このチュートリアルで以前に作成した **LearningDjango** ソリューションを右クリックし、 **[追加]**  >  **[新しいプロジェクト]** を選択します (または、新しいソリューションを使用する場合は、代わりに **[ファイル]**  >  **[新規]**  >  **[プロジェクト]** の順に選択します)。

1. [新しいプロジェクト] ダイアログで **Django ポーリング Web プロジェクト** テンプレートを探して選択し、 **[OK]** を選択します。

1. Visual Studio の他のプロジェクト テンプレートと同様に、"ポーリング Django Web プロジェクト" テンプレートには *requirements.txt* ファイルが含まれており、Visual Studio ではこれらの依存関係のインストール先を確認するメッセージが表示されます。 オプションを選択し、**仮想環境にインストール** して、 **[仮想環境の追加]** ダイアログで **[作成]** を選択して、既定値を受け入れます。

1. Python による仮想環境の設定が終了したら、*readme.html* に表示された指示に従って、データベースを初期化し、Django スーパー ユーザー (つまり、管理者) を作成します。 そのために、まず **ソリューション エクスプローラー** で **DjangoPolls** プロジェクトを右クリックし、 **[Python]**  >  **[Django 移行]** コマンドを選択し、もう一度プロジェクトを右クリックして **[Python]**  >  **[Django でスーパー ユーザーを作成する]** コマンドを選択し、プロンプトに従います (初めてスーパー ユーザーを作成する場合、データベースが初期化されていないため、エラーが表示されます)。

1. **ソリューション エクスプローラー** を右クリックし、 **[スタートアップ プロジェクトに設定]** を選択して、**DjangoPolls** プロジェクトを Visual Studio ソリューションの既定に設定します。 デバッガーを起動すると、太字で表示されているスタートアップ プロジェクトが実行されます。

1. **[デバッグ]**  >  **[デバッグの開始]** (**F5** キー) を選択するか、またはツールバーの **[Web サーバー]** ボタンを使用して、サーバーを実行します。

    ![Visual Studio の [Web サーバー] ツールバー ボタンを実行する](media/django/run-web-server-toolbar-button.png)

1. テンプレートで作成したアプリには [ホーム]、[詳細]、[連絡先] という 3 つのページがあり、上部のナビゲーション バーを使用して各ページ間を移動できます。 1、2 分とって、アプリのさまざまな部分を確認してみましょう ([詳細] ページと [連絡先] ページは Django Web プロジェクトとよく似ていますが、ここでは詳しく説明しません)。

    ![ポーリング Django Web プロジェクト アプリの全体的なブラウザー ビュー](media/django/step06-full-app-view.png)

1. また、ナビゲーション バーの **[管理]** リンクを選択すると、ログイン画面が表示され、認証された管理者のみが管理インターフェイスを使用できることが示されます。 スーパー ユーザーの資格情報を使用すると、このプロジェクト テンプレートを使用するときに既定で有効になっている "/admin" ページにルーティングされます。

    ![ポーリング Django Web プロジェクト アプリの管理ビュー](media/django/step06-polls-administrative-interface.png)

1. 以降のセクションについては、アプリにそのまま実行させることができます。

    アプリを停止して [ソース コントロールへの変更をコミットする](learn-django-in-visual-studio-step-02-create-an-app.md#commit-to-source-control)場合、最初に **チーム エクスプローラー** で **[変更]** を開き、仮想環境のフォルダー (通常は **env**) を右クリックして、 **[これらのローカル項目を無視]** を選択します。

### <a name="examine-the-project-contents"></a>プロジェクトの内容を確認する

前述のように、 Visual Studio で他のプロジェクト テンプレートを確認したことがある場合は、"ポーリング Django Web プロジェクト" テンプレートから作成されたプロジェクトの多くの部分は見慣れているはずです。 この記事の追加手順では、データ モデルや追加のビューなど、より重要な変更や追加についてまとめています。

### <a name="question-what-does-the-django-migrate-command-do"></a>質問:[Django 移行] は何を実行するコマンドですか

回答: **[Django 移行]** コマンドは、具体的には `manage.py migrate` コマンドを実行します。これは、以前に実行されたことがないスクリプトが *app/migrations* フォルダー内にあれば実行するコマンドです。 この例では、そのフォルダー内の *0001_initial.py* スクリプトが実行され、データベース内の必要なスキーマが設定されます。

移行スクリプト自体は `manage.py makemigrations` コマンドによって作成されます。このコマンドを実行すると、アプリの *models.py* ファイルがスキャンされ、データベースの現在の状態と比較され、現在のモデルに合うようにデータベース スキーマを移行するために必要なスクリプトが生成されます。 いずれはモデルを更新し、変更することになるので、この Django の機能は非常に強力です。 移行を生成して実行することで、モデルとデータベースの同期状態を簡単に維持することができます。

移行は、この記事で後述する手順 6-3 で使用します。

## <a name="step-6-2-understand-data-models"></a>手順 6-2:データ モデルを理解する

このアプリのモデルである Poll と Choice は、*app/models.py* で定義されています。 各モデルは `django.db.models.Model` から派生し、`CharField` や `IntegerField` のような `models` クラスのメソッドを使用してモデル内のフィールドを定義する Python クラスです (これらのフィールドはデータベースの列にマップされます)。

```python
from django.db import models
from django.db.models import Sum

class Poll(models.Model):
    """A poll object for use in the application views and repository."""
    text = models.CharField(max_length=200)
    pub_date = models.DateTimeField('date published')

    def total_votes(self):
        """Calculates the total number of votes for this poll."""
        return self.choice_set.aggregate(Sum('votes'))['votes__sum']

    def __unicode__(self):
        """Returns a string representation of a poll."""
        return self.text

class Choice(models.Model):
    """A poll choice object for use in the application views and repository."""
    poll = models.ForeignKey(Poll)
    text = models.CharField(max_length=200)
    votes = models.IntegerField(default=0)

    def votes_percentage(self):
        """Calculates the percentage of votes for this choice."""
        total = self.poll.total_votes()
        return self.votes / float(total) * 100 if total > 0 else 0

    def __unicode__(self):
        """Returns a string representation of a choice."""
        return self.text
```

ご覧のように、Poll は `text` フィールドに説明を、`pub_date` に公開日を保持します。 これらのフィールドは、データベース内の Poll のためにのみ存在するフィールドです。`total_votes` フィールドは実行時に計算されます。

Choice は `poll` フィールドを介して Poll と関連しており、`text` には説明が含まれ、`votes` には選択肢の数が保持されます。 `votes_percentage` フィールドは実行時に計算され、データベース内には存在しません。

フィールドの種類をすべて挙げると、`CharField` (制限ありのテキスト) `TextField` (無制限のテキスト)、`EmailField`、`URLField`、`DateTimeField`、`IntegerField`、`DecimalField`、`BooleanField`、`ForeignKey`、および `ManyToMany` があります。 各フィールドには、`max_length` のような属性があります。 `blank=True` 属性はフィールドが省略可能であることを意味します。`null=true` は値が省略可能であることを意味します。 値を、データ値または表示値タプルの配列に含まれる値に制限する `choices` 属性もあります (Django ドキュメントの「[Model field reference](https://docs.djangoproject.com/en/2.0/ref/models/fields/)」(Model フィールド リファレンス) を参照してください)。

[SQLite ブラウザー](https://sqlitebrowser.org/)のようなツールを使用してプロジェクトの *db.sqlite3* ファイルを調べることで、データベースに保存されている内容を正確に確認することができます。 データベース内には、Choice モデルの `poll` のような外部キー フィールドが `poll_id` として格納されていることがわかります。Django はこのマッピングを自動的に処理します。

一般的に、Django でデータベースを操作するということは、Django がユーザーの代わりに基のデータベースを管理できるように、モデルを介して排他的に操作することを意味します。

### <a name="seed-the-database-from-samplesjson"></a>samples.json からデータベースをシードする

最初は、データベースには投票が含まれていません。 "/admin" URL の管理インターフェイスを使用して手動で投票を追加することができます。また、実行中のサイトの "/seed" ページにアクセスして、アプリの *samples.json* ファイルに定義されている投票でデータベースのシードを追加することもできます。

Django プロジェクトの *urls.py* には追加の URL パターン `url(r'^seed$', app.views.seed, name='seed'),` があります。 *app/views.py* の `seed` ビューには *samples.json* ファイルが読み込まれ、必要なモデル オブジェクトが作成されます。 Django で、基のデータベース内の一致するレコードが自動的に作成されます。

`@login_required` デコレーターを使用は、ビューの承認レベルを示すことに注意してください。

```python
@login_required
def seed(request):
    """Seeds the database with sample polls."""
    samples_path = path.join(path.dirname(__file__), 'samples.json')
    with open(samples_path, 'r') as samples_file:
        samples_polls = json.load(samples_file)

    for sample_poll in samples_polls:
        poll = Poll()
        poll.text = sample_poll['text']
        poll.pub_date = timezone.now()
        poll.save()

        for sample_choice in sample_poll['choices']:
            choice = Choice()
            choice.poll = poll
            choice.text = sample_choice
            choice.votes = 0
            choice.save()

    return HttpResponseRedirect(reverse('app:home'))
```

影響を確認するために、まずアプリを実行して投票がまだ存在しないことを確認します。 次に "/seed" URL にアクセスします。アプリがホーム ページに戻ると、投票を使用できるようになったことがわかります。 ここでも [SQLite ブラウザー](https://sqlitebrowser.org/)のようなツールを使って *db.sqlite3* の生ファイルを調べてみてください。

![シードされたデータベースを使用したポーリング Django Web プロジェクト アプリ](media/django/step06-app-with-seeded-database.png)

### <a name="question-is-it-possible-to-initialize-the-database-using-the-django-administrative-utility"></a>質問:Django 管理ユーティリティを使用してデータベースを初期化することはできますか

回答:はい。[django-admin loaddata コマンド](https://docs.djangoproject.com/en/2.0/ref/django-admin/#loaddata)を使用して、アプリのシード処理ページと同じタスクを実行できます。 完成した Web アプリ上で作業する場合は、2 つの方法を組み合わせて使用することができます。コマンド ラインからデータベースを初期化してから、ハードコーディングしたファイルに頼らずに他の任意の JSON に送信できる API にこのシード ページを変換するという方法です。

## <a name="step-6-3-use-migrations"></a>手順 6-3:移行を使用する

プロジェクトの作成後に (Visual Studio のコンテキスト メニューを使用して) `manage.py makemigrations` コマンドを実行した場合、Django によってファイル *app/migrations/0001_initial.py* が作成されます。 このファイルには、初期データベース テーブルを作成するスクリプトが含まれています。

いずれはモデルに変更を加えることになるので、Django でこれらのモデルを使用すると、基のデータベース スキーマを簡単に最新の状態に保つことができます。 一般的なワークフローは次のとおりです。

1. *models.py* ファイルのモデルに変更を加えます。
1. Visual Studio の **ソリューション エクスプローラー** でプロジェクトを右クリックし、 **[Python]**  >  **[Django で移行を実行する]** コマンドを選択します。 前述のように、このコマンドは *app/migrations* にスクリプトを生成し、データベースを現在の状態から新しい状態に移行します。
1. スクリプトを実際のデータベースに適用するには、もう一度プロジェクトを右クリックし、 **[Python]**  >  **[Django 移行]** を選択します。

Django では、移行コマンドの実行時に必要な移行が適用されるように、各データベースに適用された移行が追跡されます。 たとえば、新しい空のデータベースを作成する場合、移行コマンドを実行すると、すべての移行スクリプトが適用され、現在のモデルを使用して最新の状態になります。 同様に、開発用コンピューター上で複数のモデルを変更し、移行を生成する場合は、運用サーバー上で移行コマンドを実行して、累積的な移行を運用データベースに適用することができます。 Django は、運用データベースの最後の移行以降に生成された移行スクリプトのみを改めて適用します。

モデルの変更の影響を確認するには、次の手順を実行します。

1. `pub_date` フィールドの後に次の行を追加して、*app/models.py* の Poll モデルに省略可能な `author` フィールドを追加します。

    ```python
    author = models.CharField(max_length=100, blank=True)
    ```

1. ファイルを保存し、**ソリューション エクスプローラー** で **DjangoPolls** プロジェクトを右クリックし、 **[Python]**  >  **[Django で移行を実行する]** コマンドを選択します。
1. **[プロジェクト]**  >  **[すべてのファイルを表示]** コマンドを選択すると、**migrations** フォルダーに名前が **002_auto_** で始まる新しく生成されたスクリプトが表示されます。 ファイルを右クリックし、 **[プロジェクトに含める]** を選択します。 もう一度 **[プロジェクト]**  >  **[すべてのファイルを表示]** コマンドを選択すると、元のビューに戻ります (この手順の詳細については、以下の 2 つ目の質問を参照してください)。
1. 必要に応じてそのファイルを開き、Django によって以前のモデル状態から新しい状態への変更がどのようにスクリプト化されたかを確認します。
1. もう一度 Visual Studio プロジェクトを右クリックし、 **[Python]**  >  **[Django 移行]** を選択して変更をデータベースに適用します。
1. 必要に応じて、適切なビューアーでデータベースを開いて変更を確認します。

全体的に見ると、Django の移行機能があれば、データベース スキーマを手動で管理する必要がないことがわかります。 モデルを変更し、移行スクリプトを生成し、移行コマンドを使用して適用するだけで済みます。

### <a name="question-what-happens-if-i-forget-to-run-the-migrate-command-after-making-changes-to-models"></a>質問:モデルを変更した後で移行コマンドを実行し忘れた場合はどうなりますか

回答:モデルがデータベースの内容と一致しない場合、実行時に適切な例外がスローされ、Django は失敗します。 たとえば、前のセクションで示したモデルの変更を移行し忘れた場合、**no such column: app_poll.author** というエラーが表示されます。

![モデルの変更が移行されなかったときに表示されるエラー](media/django/step06-exception-when-forgetting-to-migrate.png).

### <a name="question-why-doesnt-solution-explorer-show-newly-generated-scripts-after-running-django-make-migrations"></a>質問:[Django で移行を実行する] を実行した後、ソリューション エクスプローラーに新しく生成されたスクリプトが表示されないのはなぜですか

回答:新しく生成されたスクリプトは *app/migrations* フォルダーにあり、 **[Django 移行]** コマンドを実行すると適用されますが、Visual Studio プロジェクトに追加されていないので、自動的には **ソリューション エクスプローラー** に表示されません。 表示するには、まず **[プロジェクト]**  >  **[すべてのファイルを表示]** メニュー コマンドまたは次の図で示されているツール バーのボタンを選択します。 このコマンドを実行すると、**ソリューション エクスプローラー** にプロジェクト フォルダー内のすべてのファイルが表示されます。そのプロジェクトに追加されていない項目には、輪郭が点線のアイコンが使用されます。 追加するファイルを右クリックし、 **[プロジェクトに含める]** を選択します。こうすると、次回のコミットでソース管理にも含まれます。

![ソリューション エクスプローラーの [プロジェクトに含める] コマンド](media/django/step06-include-migrations-script-in-project.png)

### <a name="question-can-i-see-what-migrations-would-be-applied-before-running-the-migrate-command"></a>質問:移行コマンドを実行する前に、どのような移行が適用されるかを確認できますか

回答:はい。[django-admin showmigrations コマンド](https://docs.djangoproject.com/en/2.0/ref/django-admin/#showmigrations)を使用してください。

## <a name="step-6-4-understand-the-views-and-page-templates-created-by-the-project-template"></a>手順 6-4:プロジェクト テンプレートによって作成されたビューとページ テンプレートを理解する

"ポーリング Django Web プロジェクト" テンプレートで生成されるビュー ([詳細] ページや [連絡先] ページのビューなど) のほとんどは、このチュートリアルで使用した "Django Web プロジェクト" テンプレートによって作成されるビューとよく似ています。 ポーリング アプリの違いは、ホーム ページでモデルを利用している点と、投票を実行し、投票結果を表示するためのページがいくつか追加されている点です。

まず、Django プロジェクトの *urls.py* ファイル内にある `urlpatterns` 配列の最初の行は、単なるアプリ ビューへのルーティングではなく、 アプリ固有の *urls.py* ファイルを取得します。

```python
from django.conf.urls import url, include
import app.views

urlpatterns = [
    url(r'^', include('app.urls', namespace="app")),
    # ..
]
```

*app/urls.py* ファイルには、さらに興味深いルーティング コードがあります (説明コメントが追加されています)。

```python
urlpatterns = [
    # Home page routing
    url(r'^$',
        app.views.PollListView.as_view(
            queryset=Poll.objects.order_by('-pub_date')[:5],
            context_object_name='latest_poll_list',
            template_name='app/index.html',),
        name='home'),

    # Routing for a poll page, which use URLs in the form <poll_id>/,
    # where the id number is captured as a group named "pk".
    url(r'^(?P<pk>\d+)/$',
        app.views.PollDetailView.as_view(
            template_name='app/details.html'),
        name='detail'),

    # Routing for <poll_id>/results pages, again using a capture group
    # named pk.
    url(r'^(?P<pk>\d+)/results/$',
        app.views.PollResultsView.as_view(
            template_name='app/results.html'),
        name='results'),

    # Routing for <poll_id>/vote pages, with the capture group named
    # poll_id this time, which becomes an argument passed to the view.
    url(r'^(?P<poll_id>\d+)/vote/$', app.views.vote, name='vote'),
]
```

ここで使用されている複雑な正規表現に慣れていない場合は、正規表現を [regex101.com](https://regex101.com/) に貼り付けて、わかりやすい説明を確認することができます (スラッシュ `/` をエスケープするには、その前にバック スラッシュ `\` を追加する必要があります。Python では、文字列に "raw (生)" を意味する `r` プレフィックスがあるため、エスケープする必要はありません)。

Django では、構文 `?P<name>pattern` で `name` というグループが作成されます。これは出現順でビューの引数として渡されます。 前述のコードでは、`PollsDetailView` と `PollsResultsView` は `pk` という引数を受け取り、`app.views.vote` は `poll_id` という引数を受け取ります。

また、ほとんどのビューは *app/views.py* のビュー関数に対する直接参照ではありません。 ほとんどは `django.views.generic.ListView` または `django.views.generic.DetailView` から派生した同じファイル内のクラスを参照していることがわかります。 基底クラスには `as_view` メソッドがあります。このメソッドは、テンプレートを識別する `template_name` 引数を受け取ります。 `ListView` 基底クラスは、ホーム ページに使用されます。この基底クラスには、データを含む `queryset` プロパティと、テンプレート内のデータを参照する変数名 (この場合は `latest_poll_list`) が指定された `context_object_name` プロパティも必要です。

ホーム ページの `PollListView` を確認できるようになりました。これは、*app/views.py* で次のように定義されています。

```python
class PollListView(ListView):
    """Renders the home page, with a list of all polls."""
    model = Poll

    def get_context_data(self, **kwargs):
        context = super(PollListView, self).get_context_data(**kwargs)
        context['title'] = 'Polls'
        context['year'] = datetime.now().year
        return context
```

ここでは、ビューが使用するモデル (Poll) を特定し、`get_context_data` メソッドをオーバーライドして `title` と `year` の値をコンテキストに追加する処理が行われています。

テンプレート (*templates/app/index.html*) の中心部分は次のとおりです。

```html
{% if latest_poll_list %}
<table class="table table-hover">
    <tbody>
        {% for poll in latest_poll_list %}
        <tr>
            <td>
                <a href="{% url 'app:detail' poll.id %}">{{poll.text}}</a>
            </td>
        </tr>
        {% endfor %}
    </tbody>
</table>
{% else %}
<!-- ... other content omitted ... -->
{% endif %}
```

簡単に説明すると、このテンプレートは `latest_poll_list` で Poll オブジェクトのリストを受け取り、そのリストに対して、投票の `text` 値を使用して各投票のリンクを含むテーブル行を作成する反復処理を実行しています。 `{% url %}` タグの "app:detail" は、引数として `poll.id` を使用する、"detail" という *app/urls.py* の URL パターンを指します。 この結果、Django では適切なパターンを使用して URL が作成され、それがリンクに使用されます。 つまり、今後は、この URL パターンをいつでも変更できます。また、生成されるリンクは、変更に合わせて自動的に更新されます。

*app/views.py* の `PollDetailView` クラスと `PollResultsView` クラス (ここには示されていません) は、代わりに `DetailView` から派生している点を除いて `PollListView` とほとんど同じです。 それぞれのテンプレート *app/templates/details.html* と *app/templates/results.html* は、さまざまな HTML コントロール内のモデルから適切なフィールドを配置します。 *details.html* に独自の点の 1 つは、送信時に /vote URL に対して POST が実行される HTML フォーム内に、投票の選択肢が含まれていることです。 前述のように、この URL パターンは `app.views.vote` にルーティングされます。これは次のように実装されます (ここでも、`poll_id` 引数は、このビューのルーティングで使用される正規表現の名前付きグループです)。

```python
def vote(request, poll_id):
    """Handles voting. Validates input and updates the repository."""
    poll = get_object_or_404(Poll, pk=poll_id)
    try:
        selected_choice = poll.choice_set.get(pk=request.POST['choice'])
    except (KeyError, Choice.DoesNotExist):
        return render(request, 'app/details.html', {
            'title': 'Poll',
            'year': datetime.now().year,
            'poll': poll,
            'error_message': "Please make a selection.",
    })
    else:
        selected_choice.votes += 1
        selected_choice.save()
        return HttpResponseRedirect(reverse('app:results', args=(poll.id,)))
```

この例では、ビューには他のページのような固有の対応するテンプレートがありません。 代わりに、選択された投票を検証し、(誰かが "vote/1a2b3c" のような URL を入力した場合に備えて) 投票が存在しない場合に 404 を表示します。 次に、投票した選択肢がその投票で有効であることを確認します。 有効でない場合、`except` ブロックはエラー メッセージが記載された詳細ページを改めて表示します。 選択肢が有効な場合、ビューに投票が集計され、結果ページにリダイレクトされます。

## <a name="step-6-5-create-a-custom-administration-interface"></a>手順 6-5:カスタム管理インターフェイスを作成する

"ポーリング Django Web プロジェクト" テンプレートの最後の部分は、この記事の手順 6-1 で説明したように、既定の Django 管理インターフェイスのカスタム拡張です。 ユーザーとグループの管理用に既定のインターフェイスが用意されていますが、それ以上の機能はありません。 ポーリング プロジェクト テンプレートでは、投票も管理できる機能を追加しています。

まず、Django プロジェクトの *urls.py* の URL パターンには、既定で `url(r'^admin/', include(admin.site.urls)),` が含まれています。"admin/doc" パターンもコメント アウトされた状態で含まれています。

このアプリには *admin.py* ファイルが含まれています。*settings.py* の `INSTALLED_APPS` 配列に `django.contrib.admin` が含まれているため、管理インターフェイスにアクセスしたときに、このファイルは Django によって自動的に実行されます。 プロジェクト テンプレートに含まれているこのファイルのコードは次のとおりです。

```python
from django.contrib import admin
from app.models import Choice, Poll

class ChoiceInline(admin.TabularInline):
    """Choice objects can be edited inline in the Poll editor."""
    model = Choice
    extra = 3

class PollAdmin(admin.ModelAdmin):
    """Definition of the Poll editor."""
    fieldsets = [
        (None, {'fields': ['text']}),
        ('Date information', {'fields': ['pub_date']}),
    ]
    inlines = [ChoiceInline]
    list_display = ('text', 'pub_date')
    list_filter = ['pub_date']
    search_fields = ['text']
    date_hierarchy = 'pub_date'

admin.site.register(Poll, PollAdmin)
```

ご覧のように、`PollAdmin` クラスは `django.contrib.admin.ModelAdmin` から派生し、管理する `Poll` モデルの名前を使用して複数のフィールドをカスタマイズします。 これらのフィールドについては、Django ドキュメントの「[ModelAdmin options](https://docs.djangoproject.com/en/2.0/ref/contrib/admin/#modeladmin-options)」(ModelAdmin のオプション) を参照してください。

`admin.site.register` を呼び出すと、そのクラスはモデル (`Poll`) に接続され、管理インターフェイスに追加されます。 全体的な結果は次のとおりです。

![ポーリング Django Web プロジェクト アプリの管理ビュー](media/django/step06-polls-administrative-interface.png)

## <a name="next-steps"></a>次の手順

> [!Note]
> このチュートリアルの途中で Visual Studio ソリューションをソース コード管理にコミットした場合は、もう 1 つのコミットを実行することをお勧めします。 ソリューションは、GitHub ([Microsoft/python-sample-vs-learn-django](https://github.com/Microsoft/python-sample-vs-learning-django)) のチュートリアル ソース コードと一致するようにします。

Visual Studio で "空の Django Web プロジェクト"、"Django Web プロジェクト"、"ポーリング Django Web プロジェクト" の各テンプレートを全体的に確認しました。 ビューとテンプレートの使用方法など、Django のすべての基本を学習し、ルーティング、認証、データベース モデルの使用方法を確認しました。 これで、必要なビューとモデルがある独自の Web アプリを作成できるようになったはずです。

開発用コンピューター上で Web アプリを実行することは、アプリを顧客に提供するための単なる 1 つの手順です。 今後の手順には、以下のようなタスクがあります。

- Web アプリを Azure App Service などの運用サーバーに展開します。 「[Azure App Service に発行する](publishing-python-web-applications-to-azure-from-visual-studio.md)」を参照してください。

- *templates/404.html* というテンプレートを作成して、404 ページをカスタマイズします。 このテンプレートがある場合、Django は既定のテンプレートではなくこのテンプレートを使用します。 詳細については、Django ドキュメントの「[Error views](https://docs.djangoproject.com/en/2.0/ref/views/#error-views)」(エラー ビュー) を参照してください。

- *tests.py* で単体テストを作成します。Visual Studio プロジェクト テンプレートには、そのための出発点が用意されています。詳細については、Django ドキュメントの「[Writing your first Django app, part 5 - testing](https://docs.djangoproject.com/en/2.0/intro/tutorial05/)」(最初の Django アプリを作成する、パート 5 - テスト) と「[Testing in Django](https://docs.djangoproject.com/en/2.0/topics/testing/)」(Django のテスト) を参照してください。

- SQLite から、PostgreSQL、MySQL、SQL Server など (これらはいずれも Azure でホストできます) の運用レベルのデータ ストアにアプリを変更します。 「[When to use SQLite](https://www.sqlite.org/whentouse.html)」(SQLite を使用する場合) (sqlite.org) で説明されているように、SQLite は、1 日あたり 100,000 ヒット未満のトラフィックが中小規模のサイトには適していますが、高ボリュームのサイトにはお勧めできません。 また、単一のコンピューターに制限されているため、負荷分散処理や geo レプリケーションなど、マルチサーバーのシナリオには使用できません。 他のデータベースに対する Django のサポートについては、「[Database setup](https://docs.djangoproject.com/en/2.0/intro/tutorial02/#database-setup)」(データベースの設定) を参照してください。 テーブルや BLOB のような Azure ストレージ サービスを使用する場合は、[Azure SDK for Python](/azure/python/) も使用できます。

- Azure DevOps などのサービスに対して、継続的インテグレーション/継続的配置パイプラインを設定します。 (Azure Repos、GitHub、または他の場所で) ソース コード管理を使用するだけでなく、リリースの前提条件として単体テストを自動的に実行するよう、Azure DevOps プロジェクトを構成することができます。また、運用環境にデプロイする前に、追加テストのためにステージング サーバーにデプロイするパイプラインを構成することもできます。 さらに、Azure DevOps は App Insights などの監視ソリューションと統合されているので、アジャイル計画ツールを使用してサイクル全体に対応することができます。 詳細については、「[Azure DevOps プロジェクトで Python 用の CI/CD パイプラインを作成する](/azure/devops-project/azure-devops-project-python?view=vsts&preserve-view=true)」、および一般的な [Azure DevOps ドキュメント](/azure/devops/?view=vsts&preserve-view=true)を参照してください。
