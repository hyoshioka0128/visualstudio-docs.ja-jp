---
title: Visual Studio での Flask 学習チュートリアル、手順 4、Web プロジェクト テンプレート
titleSuffix: ''
description: Visual Studio プロジェクトのコンテキストにおける Flask の基本のチュートリアルです。具体的には、Flask Web プロジェクトと Flask/Jade Web プロジェクト テンプレートの機能について取り上げます。
ms.date: 01/07/2019
ms.topic: tutorial
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: 9f4c165f3e882cea71ee4aaff9f2358c27ce6a2b
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/20/2020
ms.locfileid: "62957270"
---
# <a name="step-4-use-the-full-flask-web-project-template"></a>手順 4: 完全な Flask Web プロジェクト テンプレートを使用する

**前の手順: [静的ファイルを提供し、ページを追加し、テンプレート継承を使用する](learn-flask-visual-studio-step-03-serve-static-files-add-pages.md)**

Visual Studio の "空の Flask App プロジェクト" テンプレート上にアプリを構築して、Flask の基本を確認したので、"Flask Web プロジェクト" テンプレートで作成されるより完全なアプリを簡単に理解できるようになりました。

この手順では、次のことを学習します。

> [!div class="checklist"]
> - "Flask Web プロジェクト" テンプレートを使用してより完全な Flask Web アプリを作成し、プロジェクト構造を調べる (手順 4-1)
> - 基本のページ テンプレートを継承し、jQuery や Bootstrap などの静的 JavaScript ライブラリを採用した 3 つのページで構成される、プロジェクト テンプレートによって作成されたビューとページ テンプレートを理解する (手順 4-2)
> - テンプレートによって提供された URL ルーティングを理解する (手順 4-3)

この記事は、"Flask/Jade Web プロジェクト" テンプレートにも該当します。このテンプレートからは、Jinja の代わりに Jade テンプレート エンジンを利用し、"Flask Web プロジェクト" のアプリと同じアプリが作られます。 この記事の終わりには追加詳細を記載しています。

## <a name="step-4-1-create-a-project-from-the-template"></a>手順 4-1: テンプレートからプロジェクトを作成する

1. Visual Studio で、**ソリューション エクスプローラー**に移動し、本チュートリアルの前述の手順で作成した **LearningFlask** ソリューションを右クリックし、**[追加]** > **[新しいプロジェクト]** の順に選択します。 (または、新しいソリューションを使用する場合は、代わりに **[ファイル]** > **[新規]** > **[プロジェクト]** の順に選択します)。

1. [新しいプロジェクト] ダイアログで **Flask Web プロジェクト** テンプレートを探して選択し、プロジェクト "FlaskWeb" を呼び出して、**[OK]** を選択します。

1. ここでも、テンプレートに *requirements.txt* ファイルが含まれているので、Visual Studio からそれらの依存関係をインストールする場所をたずねられます。 オプションを選択し、**仮想環境にインストール**して、**[仮想環境の追加]** ダイアログで **[作成]** を選択して、既定値を受け入れます。

1. Visual Studio で仮想環境の設定が完了したら、**ソリューション エクスプローラー**でプロジェクトを右クリックし、**[スタートアップ プロジェクトに設定]** を選択する方法で **FlaskWeb** プロジェクトを Visual Studio ソリューションの既定に設定します。 デバッガーを起動すると、太字で表示されているスタートアップ プロジェクトが実行されます。

    ![ソリューション エクスプローラーでスタートアップ プロジェクトとして FlaskWeb プロジェクトが表示されます](media/flask/step04-second-project-in-solution-set-as-startup-project.png)

1. **[デバッグ]** > **[デバッグの開始]** (**F5** キー) を選択するか、またはツールバーの **[Web サーバー]** ボタンを使用して、サーバーを実行します。

    ![Visual Studio の [Web サーバー] ツールバー ボタンを実行する](media/flask/run-web-server-toolbar-button.png)

1. テンプレートで作成したアプリには [ホーム]、[About]\(詳細\)、[連絡先] という 3 つのページがあり、ナビゲーション バーを使用して各ページ間を移動できます。 アプリのさまざまな部分を調べるのに、1 ～ 2 分かかります。 **[ログイン]** コマンドを使ってアプリでの認証を行うために、前に作成したスーパーユーザーの資格情報を使用します。

    ![Flask Web プロジェクト アプリの完全なブラウザー ビュー](media/flask/step04-full-app-desktop-view.png)

1. "Flask Web プロジェクト" テンプレートで作成されたアプリでは、モバイル フォーム ファクターに対応したレスポンシブ レイアウトのために、Bootstrap を使用します。 この応答性を確認するために、コンテンツを縦長に表示してナビゲーション バーがメニュー アイコンに切り替わるように、ブラウザーの表示幅を縮小します。

    ![Flask Web プロジェクト アプリのモバイル (縮小幅) 表示](media/flask/step04-full-app-mobile-view.png)

1. 以降のセクションのために、アプリを実行したままにすることができます。

    アプリを停止して[ソース コントロールへの変更をコミットする](learn-flask-visual-studio-step-02-create-app.md#commit-to-source-control)場合、最初に**チーム エクスプローラー**で **[変更]** を開き、仮想環境のフォルダー (通常は **env**) を右クリックして、**[これらのローカル項目を無視]** を選択します。

### <a name="examine-what-the-template-creates"></a>テンプレートによって作成されたものを確認する

"Flask Web プロジェクト" によって以下の構造が作成されます。 コンテンツは前の手順で作成したものに非常に似ています。 違いは、"Flask Web プロジェクト" テンプレートの場合、*static* フォルダーの構成が多いことです。応答性に優れた設計のための jQuery と Bootstrap が含まれているためです。 このテンプレートによって [お問い合わせ] ページも追加されます。 全体として、このチュートリアルの前手順を完了している場合、テンプレートの内容はどれも見たことがあるはずです。

- プロジェクト ルートにある次のファイル
  - *runserver.py*。開発サーバーでアプリを実行するスクリプト。
  - *requirements.txt*。Flask 0.x での依存関係を含む。
- *FlaskWeb* フォルダーにはすべてのアプリ ファイルが含まれています。
  - *\_\_init.py\_\_* はアプリ コードを Python モジュールとしてマークし、Flask オブジェクトを作成し、アプリのビューをインポートします。
  - *views.py* には、ページをレンダリングするためのコードが含まれています。
  - *static* フォルダーには、*content* (CSS ファイル)、*fonts* (フォント ファイル)、*scripts* (JavaScript ファイル) という名前のサブフォルダーが含まれています。
  - *templates* フォルダーには、*layout.html* 基本テンプレートと共に、*layout.html* を拡張するページのための *about.html*、*contact.html*、*index.html* が含まれています。

### <a name="question-is-it-possible-to-share-a-virtual-environment-between-visual-studio-projects"></a>質問: Visual Studio プロジェクト間で仮想環境を共有することは可能ですか。

回答: はい。ただし、異なるプロジェクトは時間の経過と共に異なるパッケージを使用する傾向があるため、共有した仮想環境には、使用するすべてのプロジェクトに対応するすべてのパッケージを含む必要があることを認識したうえで、共有してください。

それでもやはり、既存の仮想環境を使用するには、次の手順を実行します。

1. Visual Studio に依存関係をインストールするようメッセージが表示されたら、**[I will install them myself]\(自分でインストールします\)** オプションを選択します。
1. **ソリューション エクスプローラー**で、**[Python 環境]** ノードを右クリックして、**[既存の仮想環境を追加する]** を選択します。
1. 仮想環境を含むフォルダーに移動して選択し、 **[OK]** をクリックします。

## <a name="step-4-2-understand-the-views-and-page-templates-created-by-the-project-template"></a>手順 4 2: プロジェクト テンプレートによって作成されたビューとページ テンプレートを理解する

プロジェクトを実行したときに確認すると、アプリには、[ホーム]、[About]\(詳細\)、[連絡先] という 3 つのビューが含まれています。 これらのビューに対応するコードは、*FlaskWeb/views.py* フォルダーにあります。 テンプレートに値を与えるために、各ビューの関数はテンプレートのパスと引数の変数一覧を利用して `flask.render_template` を呼び出します。 たとえば、[バージョン情報] ページは `about` 関数によって処理されます (そのデコレーターによって URL ルーティングが与えられます)。

```python
@app.route('/about')
def about():
    """Renders the about page."""
    return render_template(
        'about.html',
        title='About',
        year=datetime.now().year,
        message='Your application description page.'
    )
```

`home` 関数と `contact` 関数はほとんど同じです。デコレーターが同類で、引数が多少異なります。

テンプレートはアプリの *templates* フォルダーにあります。 基本のテンプレートである *layout.html* は、最も拡張性に優れています。 このテンプレートは、すべての必要な静的ファイル (JavaScript および CSS) を参照し、他のページによってオーバーライドされる "content" という名前のブロックを定義し、"scripts" という名前のもう 1 つのブロックを提供しています。 次に示す *layout.html* からのコメント付きの抜粋は、これらの固有の領域を示しています。

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />

    <!-- Define a viewport for Bootstrap's responsive rendering -->
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{{ title }} - My Flask Application</title>

    <link rel="stylesheet" type="text/css" href="/static/content/bootstrap.min.css" />
    <link rel="stylesheet" type="text/css" href="/static/content/site.css" />
    <script src="/static/scripts/modernizr-2.6.2.js"></script>
</head>

<body>
    <!-- Navbar omitted -->

    <div class="container body-content">
        <!-- "content" block that pages are expected to override -->
        {% block content %}{% endblock %}
        <hr />
        <footer>
            <p>&copy; {{ year }} - My Flask Application</p>
        </footer>
    </div>

    <!-- Additional scripts; use the "scripts" block to add page-specific scripts.  -->
    <script src="/static/scripts/jquery-1.10.2.js"></script>
    <script src="/static/scripts/bootstrap.js"></script>
    <script src="/static/scripts/respond.js"></script>
    {% block scripts %}{% endblock %}

</body>
</html>
```

個々のページ テンプレート *about.html*、*contact.html*、*index.html* はそれぞれ、基本のテンプレートである *layout.html* を拡張します。 *about.html* は最もシンプルで、次のように `{% extends %}` および `{% block content %}` タグを表示します。

```html
{% extends "app/layout.html" %}

{% block content %}

<h2>{{ title }}.</h2>
<h3>{{ message }}</h3>

<p>Use this area to provide additional information.</p>

{% endblock %}
```

*index.html* および *contact.html* は、同じ構造を使用して、"content" ブロックでより長い内容を提供します。

## <a name="the-flaskjade-web-project-template"></a>Flask/Jade Web プロジェクト テンプレート

この記事の冒頭でお話ししたように、Visual Studio には "Flask/Jade Web プロジェクト" テンプレートがあります。このテンプレートによって、"Flask Web プロジェクト" で生成されるものと見た目が同じアプリケーションが作成されます。 主な違いは、Jade テンプレート エンジンの使用です。これは Jinja の拡張であり、同じ概念をより簡潔な言語で実行します。 具体的には、たとえば、Jade は {% %} 区切り記号で囲まれたタグの代わりにキーワードが使用され、キーワードを利用して CSS スタイルや HTML 要素を参照できます。

Jade を有効にするために、プロジェクト テンプレートは最初に *requirements.txt* に pyjade パッケージを含めます。

アプリの *\_\_init\_\_.py* ファイルには次の行が含まれています。

```python
app.jinja_env.add_extension('pyjade.ext.jinja.PyJadeExtension')
```

*templates* フォルダーには、*.html* テンプレートではなく *.jade* ファイルが表示されます。*views.py* のビューは、`flask.render_template` の呼び出しでこれらのファイルを参照します。 それ以外の点では、ビュー コードは同じです。

*.jade* ファイルの 1 つを開くと、テンプレートがより簡潔に表現されていることがわかります。 たとえば、"Flask/Jade Web プロジェクト" テンプレートで作成された *templates/layout.jade* の内容は次のようになります。

```jade
doctype html
html
  head
    meta(charset='utf-8')
    meta(name='viewport', content='width=device-width, initial-scale=1.0')
    title #{title} - My Flask/Jade Application
    link(rel='stylesheet', type='text/css', href='/static/content/bootstrap.min.css')
    link(rel='stylesheet', type='text/css', href='/static/content/site.css')
    script(src='/static/scripts/modernizr-2.6.2.js')
  body
    .navbar.navbar-inverse.navbar-fixed-top
      .container
        .navbar-header
          button.navbar-toggle(type='button', data-toggle='collapse', data-target='.navbar-collapse')
            span.icon-bar
            span.icon-bar
            span.icon-bar
          a.navbar-brand(href='/') Application name
        .navbar-collapse.collapse
          ul.nav.navbar-nav
            li
              a(href='/') Home
            li
              a(href='/about') About
            li
              a(href='/contact') Contact
    .container.body-content
      block content
      hr
      footer
        p &copy; #{year} - My Flask/Jade Application

    script(src='/static/scripts/jquery-1.10.2.js')
    script(src='/static/scripts/bootstrap.js')
    script(src='/static/scripts/respond.js')

    block scripts
```

*templates/about.jade* の内容は次のようになります。プレースホルダーに `#{ <name>}` が使用されています。

```jade
extends layout

block content
  h2 #{title}.
  h3 #{message}
  p Use this area to provide additional information.
```

Jinja と Jade の構文をいろいろ試し、自分にとって何が最適か見つけてください。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [Polls Flask Web プロジェクト テンプレート](learn-flask-visual-studio-step-05-polls-flask-web-project-template.md)

## <a name="go-deeper"></a>詳しい説明

- [最初の Flask アプリの作成、パート 4 - フォームと汎用ビュー](https://docs.djangoproject.com/en/2.0/intro/tutorial04/) (docs.djangoproject.com)
- [GitHub の Jade (ドキュメント)](https://github.com/liuliqiang/pyjade) (github.com)
- GitHub 上のチュートリアルのソース コード: [Microsoft/python-sample-vs-learning-flask](https://github.com/Microsoft/python-sample-vs-learning-flask)
