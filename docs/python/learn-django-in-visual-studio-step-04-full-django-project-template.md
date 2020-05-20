---
title: Visual Studio での Django 学習チュートリアル、手順 4、Web プロジェクト テンプレート
titleSuffix: ''
description: Visual Studio プロジェクトのコンテキストにおける Django の基本のチュートリアルです。具体的には、Django Web プロジェクト テンプレートによって提供される機能について取り上げます。
ms.date: 11/19/2018
ms.topic: tutorial
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: c778d830b20797962306700a5af938eb3a3bb142
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/20/2020
ms.locfileid: "62961692"
---
# <a name="step-4-use-the-full-django-web-project-template"></a>手順 4: Django Web プロジェクト テンプレートを使用する

**前の手順: [静的ファイルを提供し、ページを追加し、テンプレート継承を使用する](learn-django-in-visual-studio-step-03-serve-static-files-and-add-pages.md)**

Visual Studio の "空の Django Web プロジェクト" テンプレート上にアプリを構築して、Django の基本を確認したので、"Django Web プロジェクト" テンプレートで作成されるより完全なアプリを簡単に理解できるようになりました。

この手順では、次のことを学習します。

> [!div class="checklist"]
> - "Django Web プロジェクト" テンプレートを使用してより完全な Django Web アプリを作成し、プロジェクト構造を調べる (手順 4-1)
> - 基本のページ テンプレートを継承し、jQuery や Bootstrap などの静的 JavaScript ライブラリを採用した 3 つのページで構成される、プロジェクト テンプレートによって作成されたビューとページ テンプレートを理解する (手順 4-2)
> - テンプレートによって提供された URL ルーティングを理解する (手順 4-3)

また、テンプレートでは、手順 5 で取り上げる基本認証も提供されます。

## <a name="step-4-1-create-a-project-from-the-template"></a>手順 4-1: テンプレートからプロジェクトを作成する

1. Visual Studio で、**ソリューション エクスプローラー**に移動して、このチュートリアルで以前に作成した **LearningDjango** ソリューションを右クリックし、 **[追加]**  >  **[新しいプロジェクト]** を選択します (または、新しいソリューションを使用する場合は、代わりに **[ファイル]**  >  **[新規]**  >  **[プロジェクト]** の順に選択します)。

1. 新しいプロジェクトのダイアログで、**Django Web プロジェクト** テンプレートを検索して選択し、プロジェクトに "DjangoWeb" という名前を付けて、 **[OK]** をクリックします。

1. ここでも、テンプレートに *requirements.txt* ファイルが含まれているので、Visual Studio からそれらの依存関係をインストールする場所をたずねられます。 オプションを選択し、**仮想環境にインストール**して、 **[仮想環境の追加]** ダイアログで **[作成]** を選択して、既定値を受け入れます。

1. Visual Studio による仮想環境の設定が終了したら、*readme.html* に表示された指示に従って、Django スーパー ユーザー (つまり、管理者) を作成します。 Visual Studio プロジェクトを右クリックして、 **[Python]**  >  **[Django でスーパー ユーザーを作成する]** コマンドを選択して、プロンプトの指示に従います。 アプリの認証機能を利用するときに使うので、必ずユーザー名とパスワードを記録してください。

1. **ソリューション エクスプローラー**を右クリックし、**[スタートアップ プロジェクトとして設定]** を選択して、**DjangoWeb** プロジェクトを Visual Studio ソリューションの既定に設定します。 デバッガーを起動すると、太字で表示されているスタートアップ プロジェクトが実行されます。

    ![スタートアップ プロジェクトとして DjangoWeb プロジェクトを表示したソリューション エクスプローラー](media/django/step04-second-project-in-solution-set-as-startup-project.png)

1. **[デバッグ]**  >  **[デバッグの開始]** (**F5** キー) を選択するか、またはツールバーの **[Web サーバー]** ボタンを使用して、サーバーを実行します。

    ![Visual Studio の [Web サーバー] ツールバー ボタンを実行する](media/django/run-web-server-toolbar-button.png)

1. テンプレートで作成したアプリには [ホーム]、[About]\(詳細\)、[連絡先] という 3 つのページがあり、ナビゲーション バーを使用して各ページ間を移動できます。 アプリのさまざまな部分を調べるのに、1 ～ 2 分かかります。 **[ログイン]** コマンドを使ってアプリでの認証を行うために、前に作成したスーパーユーザーの資格情報を使用します。

    ![Django Web プロジェクト アプリの完全なブラウザー ビュー](media/django/step04-full-app-desktop-view.png)

1. "Django Web プロジェクト" テンプレートで作成されたアプリでは、モバイル フォーム ファクターに対応したレスポンシブ レイアウトのために、Bootstrap を使用します。 この応答性を確認するために、コンテンツを縦長に表示してナビゲーション バーがメニュー アイコンに切り替わるように、ブラウザーの表示幅を縮小します。

    ![Django Web プロジェクト アプリのモバイル (縮小幅) 表示](media/django/step04-full-app-mobile-view.png)

1. 以降のセクションのために、アプリを実行したままにすることができます。

    アプリを停止して[ソース コントロールへの変更をコミットする](learn-django-in-visual-studio-step-02-create-an-app.md#commit-to-source-control)場合、最初に**チーム エクスプローラー**で **[変更]** を開き、仮想環境のフォルダー (通常は **env**) を右クリックして、**[これらのローカル項目を無視]** を選択します。

### <a name="examine-what-the-template-creates"></a>テンプレートによって作成されたものを確認する

広義では、"Django Web プロジェクト" テンプレートは次の構造を作成します。

- プロジェクト ルートにある次のファイル
  - *manage.py*: Django 管理ユーティリティ。
  - *db.sqlite3*: 既定の SQLite データベース。
  - *requirements.txt*: Django 1.x での依存関係を含む。
  - *readme.html*: プロジェクトの作成後に Visual Studio に表示されるファイル。 前のセクションで述べたように、このファイルの指示に従ってアプリのスーパー ユーザー (管理者) アカウントを作成します。
- *app* フォルダーには、ビュー、モデル、テスト、フォーム、テンプレート、静的ファイルなど、すべてのアプリ ファイルが含まれています (手順 4-2 を参照). 通常は、より区別しやすいアプリ名を使用するために、このフォルダー名を変更します。
- *DjangoWeb* (Django プロジェクト) フォルダーには、一般的な Django プロジェクト ファイルである *\_\_init\_\_.py*、*settings.py*、*urls.py*、*wsgi.py* が含まれています。 プロジェクト テンプレートを使用することで、*settings.py* は既にアプリおよびデータベース ファイル用に構成されており、*urls.py* は既にログイン フォームを含むすべてのアプリ ページへのルートを使って構成されています。

### <a name="question-is-it-possible-to-share-a-virtual-environment-between-visual-studio-projects"></a>質問: Visual Studio プロジェクト間で仮想環境を共有することは可能ですか。

回答: はい。ただし、異なるプロジェクトは時間の経過と共に異なるパッケージを使用する傾向があるため、共有した仮想環境には、使用するすべてのプロジェクトに対応するすべてのパッケージを含む必要があることを認識したうえで、共有してください。

それでもやはり、既存の仮想環境を使用するには、次の手順を実行します。

1. Visual Studio に依存関係をインストールするようメッセージが表示されたら、 **[I will install them myself]\(自分でインストールします\)** オプションを選択します。
1. **ソリューション エクスプローラー**で、 **[Python 環境]** ノードを右クリックして、 **[既存の仮想環境を追加する]** を選択します。
1. 仮想環境を含むフォルダーに移動して選択し、 **[OK]** をクリックします。

## <a name="step-4-2-understand-the-views-and-page-templates-created-by-the-project-template"></a>手順 4 2: プロジェクト テンプレートによって作成されたビューとページ テンプレートを理解する

プロジェクトを実行したときに確認すると、アプリには、[ホーム]、[About]\(詳細\)、[連絡先] という 3 つのビューが含まれています。 これらのビューに対応するコードは、*app/views* フォルダーにあります。 各ビューの関数では単に、テンプレートおよび単純なディクショナリ オブジェクトへのパスを使って、`django.shortcuts.render` を呼び出しています。 たとえば、[About]\(詳細\) ページは、`about` 関数で処理されています。

```python
def about(request):
    """Renders the about page."""
    assert isinstance(request, HttpRequest)
    return render(
        request,
        'app/about.html',
        {
            'title':'About',
            'message':'Your application description page.',
            'year':datetime.now().year,
        }
    )
```

テンプレートはアプリの *templates/app* フォルダー (通常は、*app* を実際のアプリの名前に変更します) に配置されています。 基本のテンプレートである *layout.html* は、最も拡張性に優れています。 このテンプレートは、すべての必要な静的ファイル (JavaScript および CSS) を参照し、他のページによってオーバーライドされる "content" という名前のブロックを定義し、"scripts" という名前のもう 1 つのブロックを提供しています。 次に示す *layout.html* からのコメント付きの抜粋は、これらの固有の領域を示しています。

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />

    <!-- Define a viewport for Bootstrap's responsive rendering -->
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{{ title }} - My Django Application</title>

    {% load staticfiles %}
    <link rel="stylesheet" type="text/css" href="{% static 'app/content/bootstrap.min.css' %}" />
    <link rel="stylesheet" type="text/css" href="{% static 'app/content/site.css' %}" />
    <script src="{% static 'app/scripts/modernizr-2.6.2.js' %}"></script>
</head>
<body>
    <!-- Navbar omitted -->

    <div class="container body-content">

<!-- "content" block that pages are expected to override -->
{% block content %}{% endblock %}
        <hr/>
        <footer>
            <p>&copy; {{ year }} - My Django Application</p>
        </footer>
    </div>

<!-- Additional scripts; use the "scripts" block to add page-specific scripts.  -->
    <script src="{% static 'app/scripts/jquery-1.10.2.js' %}"></script>
    <script src="{% static 'app/scripts/bootstrap.js' %}"></script>
    <script src="{% static 'app/scripts/respond.js' %}"></script>
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

また、*templates/app* フォルダーには、`{% include %}` を使用して *layout.html* に組み込まれる *loginpartial.html* と、4 番目のページである *login.html* もあります。 これらのテンプレート ファイルについては、手順 5 の認証に関するセクションで取り上げます。

### <a name="question-can--block--and--endblock--be-indented-in-the-django-page-template"></a>質問: {% block %} と {% endblock %} は Django ページ テンプレートでインデントできますか。

回答: はい。多くの場合、適切な親要素の中にこれらのタグを配置する目的で、ブロック タグをインデントしても、Django ページ テンプレートは有効です。 タグの配置場所が明確にわかるように、これらのタグは Visual Studio プロジェクト テンプレートで生成されたページ テンプレートではインデントされません。

## <a name="step-4-3-understand-the-url-routing-created-by-the-template"></a>手順 4-3: テンプレートによって作成された URL ルーティングを理解する

"Django Web プロジェクト" テンプレートで作成された Django プロジェクトの *urls.py* ファイルには、次のコードが含まれています。

```python
from datetime import datetime
from django.conf.urls import url
import django.contrib.auth.views

import app.forms
import app.views

urlpatterns = [
    url(r'^$', app.views.home, name='home'),
    url(r'^contact$', app.views.contact, name='contact'),
    url(r'^about$', app.views.about, name='about'),
    url(r'^login/$',
        django.contrib.auth.views.login,
        {
            'template_name': 'app/login.html',
            'authentication_form': app.forms.BootstrapAuthenticationForm,
            'extra_context':
            {
                'title': 'Log in',
                'year': datetime.now().year,
            }
        },
        name='login'),
    url(r'^logout$',
        django.contrib.auth.views.logout,
        {
            'next_page': '/',
        },
        name='logout'),
]
```

最初の 3 つの URL パターンは、アプリの *views.py* ファイルにある `home`、`contact`、`about` ビューに直接マップされます。 一方、パターン `^login/$` および `^logout$` では、アプリ定義のビューではなく、組み込みの Django ビューを使用します。 また、`url` メソッドの呼び出しには、ビューをカスタマイズするための追加のデータが含まれます。 手順 5 では、これらの呼び出しについて確認します。

### <a name="question-in-the-project-i-created-why-does-the-about-url-pattern-uses-about-instead-of-about-as-shown-here"></a>質問: 作成したプロジェクトでは、どうして "about" の URL パターンに、このページで示されている '^about$' ではなく '^about' を使用するのですか。

回答: 正規表現の末尾の '$' の欠如は、多くのバージョンのプロジェクト テンプレートでの単純なミスです。 URL パターンは "about" という名前のページでは完全に問題なく動作しますが、末尾の '$' が無い場合、URL パターンは "about=django"、"about09876", "aboutoflaughter" などの URL にも適合します。 "about" "*だけ*" に適合する URL パターンを作成するために、このページでは末尾の '$' が示されています。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [Django でユーザーを認証する](learn-django-in-visual-studio-step-05-django-authentication.md)

## <a name="go-deeper"></a>詳しい説明

- [Azure App Service への Web アプリの展開](publishing-python-web-applications-to-azure-from-visual-studio.md)
- [最初の Django アプリの作成、パート 4 - フォームと汎用ビュー](https://docs.djangoproject.com/en/2.0/intro/tutorial04/) (docs.djangoproject.com)
- GitHub 上のチュートリアルのソース コード: [Microsoft/python-sample-vs-learning-django](https://github.com/Microsoft/python-sample-vs-learning-django)
