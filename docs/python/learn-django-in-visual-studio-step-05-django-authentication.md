---
title: Visual Studio での Django 学習チュートリアル、手順 5、認証
titleSuffix: ''
description: Visual Studio プロジェクトのコンテキストにおける Django の基本のチュートリアルです。具体的には、Django Web プロジェクト テンプレートによって提供される認証機能について取り上げます。
ms.date: 11/19/2018
ms.topic: tutorial
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: ea708c1721d85468d99a0ccc327f378042579f85
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99942491"
---
# <a name="step-5-authenticate-users-in-django"></a>手順 5: Django でユーザーを認証する

**前の手順:[Django Web プロジェクト テンプレートを使用する](learn-django-in-visual-studio-step-04-full-django-project-template.md)**

認証は Web アプリ共通のニーズであるため、"Django Web プロジェクト" テンプレートには基本認証フローが含まれています (このチュートリアルの手順 6. で説明する "ポーリング Django Web プロジェクト" テンプレートにも、同じフローが含まれています)。いずれかの Django プロジェクト テンプレートを使用する場合、Visual Studio には Django プロジェクトの *settings.py* での認証に必要なすべてのモジュールが含まれています。

この手順では、次のことを学習します。

> [!div class="checklist"]
> - Visual Studio テンプレートで提供される認証フローの使用方法 (手順 5-1)

## <a name="step-5-1-use-the-authentication-flow"></a>手順 5-1:認証フローを使用する

次の手順では、認証フローを利用して、プロジェクトの関連する部分について説明します。

1. プロジェクトのルートにある *readme.html* ファイルの指示に従ってスーパー ユーザー (管理者) アカウントをまだ作成していない場合は、すぐに作成します。

1. **[デバッグ]**  >  **[デバッグの開始]** (**F5** キー) を使用して、Visual Studio からアプリを実行します。 ブラウザーにアプリが表示されたら、ナビゲーション バーの右上に **[ログイン]** が表示されていることを確認します。

    ![Django Web プロジェクトのアプリ ページ上にある login コントロール](media/django/step05-login-control.png)

1. *templates/app/layout.html* を開き、`<div class="navbar ...>` 要素にタグ `{% include app/loginpartial.html %}` が含まれていることを確認します。 `{% include %}` タグは、含まれているテンプレートにこの時点でインクルードされているファイルの内容を組み入れるように、Django のテンプレート システムに指示します。

1. *templates/app/loginpartial.html* を開き、`{% else %}` タグと共に条件タグ `{% if user.is_authenticated %}` を使用して、ユーザーが認証済みかどうかに応じて異なる UI 要素を表示する方法を確認します。

    ```html
    {% if user.is_authenticated %}
    <form id="logoutForm" action="/logout" method="post" class="navbar-right">
        {% csrf_token %}
        <ul class="nav navbar-nav navbar-right">
            <li><span class="navbar-brand">Hello {{ user.username }}!</span></li>
            <li><a href="javascript:document.getElementById('logoutForm').submit()">Log off</a></li>
        </ul>
    </form>

    {% else %}

    <ul class="nav navbar-nav navbar-right">
        <li><a href="{% url 'login' %}">Log in</a></li>
    </ul>

    {% endif %}
    ```

1. 最初にアプリを起動するときはどのユーザーも認証されていないので、このテンプレートのコードは、相対パス "login" への "ログイン" リンクのみを表示します。 (前のセクションで示したように) *urls.py* に指定されると、そのルートは `django.contrib.auth.views.login` ビューにマップされます。 そのビューは、次のデータを受け取ります。

    ```python
    {
        'template_name': 'app/login.html',
        'authentication_form': app.forms.BootstrapAuthenticationForm,
        'extra_context':
        {
            'title': 'Log in',
            'year': datetime.now().year,
        }
    }
    ```

    ここで、`template_name` は、ログイン ページ用のテンプレート (この場合は *templates/app/login.html*) を特定します。 `extra_context` プロパティは、テンプレートに指定された既定のコンテキスト データに追加されます。 最後に、`authentication_form` は、テンプレートに `form` オブジェクトとして示される、ログインに使用するフォーム クラスを定義します。 既定値は `AuthenticationForm` (`django.contrib.auth.views` より) です。Visual Studio プロジェクト テンプレートでは代わりに、アプリの *forms.py* ファイルに定義された次のフォームを使用します。

    ```python
    from django import forms
    from django.contrib.auth.forms import AuthenticationForm
    from django.utils.translation import ugettext_lazy as _

    class BootstrapAuthenticationForm(AuthenticationForm):
        """Authentication form which uses boostrap CSS."""
        username = forms.CharField(max_length=254,
                                   widget=forms.TextInput({
                                       'class': 'form-control',
                                       'placeholder': 'User name'}))
        password = forms.CharField(label=_("Password"),
                                   widget=forms.PasswordInput({
                                       'class': 'form-control',
                                       'placeholder':'Password'}))
    ```

    見てわかるように、このフォーム クラスは `AuthenticationForm` から派生し、明示的にユーザー名とパスワードのフィールドをオーバーライドして、プレースホルダ― テキストを追加します。 Visual Studio テンプレートには、パスワード強度の検証を追加するなど、必要に応じてフォームをカスタマイズすることを予想して、この明示的なコードが含まれています。

1. ログイン ページに移動すると、アプリは *login.html* テンプレートを表示します。 変数 `{{ form.username }}` および `{{ form.password }}` は、`BootstrapAuthenticationForm` から `CharField` フォームを表示します。 また、検証エラーを表示するための組み込みのセクションと、ソーシャル ログイン用にあらかじめ用意されている要素もあり、必要に応じてこれらのサービスを追加できます。

    ```html
    {% extends "app/layout.html" %}

    {% block content %}

    <h2>{{ title }}</h2>
    <div class="row">
        <div class="col-md-8">
            <section id="loginForm">
                <form action="." method="post" class="form-horizontal">
                    {% csrf_token %}
                    <h4>Use a local account to log in.</h4>
                    <hr />
                    <div class="form-group">
                        <label for="id_username" class="col-md-2 control-label">User name</label>
                        <div class="col-md-10">
                            {{ form.username }}
                        </div>
                    </div>
                    <div class="form-group">
                        <label for="id_password" class="col-md-2 control-label">Password</label>
                        <div class="col-md-10">
                            {{ form.password }}
                        </div>
                    </div>
                    <div class="form-group">
                        <div class="col-md-offset-2 col-md-10">
                            <input type="hidden" name="next" value="/" />
                            <input type="submit" value="Log in" class="btn btn-default" />
                        </div>
                    </div>
                    {% if form.errors %}
                    <p class="validation-summary-errors">Please enter a correct user name and password.</p>
                    {% endif %}
                </form>
            </section>
        </div>
        <div class="col-md-4">
            <section id="socialLoginForm"></section>
        </div>
    </div>

    {% endblock %}
    ```

1. フォームを送信すると、Django は資格情報 (スーパー ユーザーの資格情報など) の認証を試みます。 認証に失敗した場合、現在のページに留まりますが、`form.errors` は true に設定されます。 認証に成功した場合、Django は "next" フィールド `<input type="hidden" name="next" value="/" />` にある相対 URL に移動します。この例では、ホーム ページ (`/`) になっています。

1. ここで、ホーム ページが再表示されると、*loginpartial.html* テンプレートが表示されるときに、`user.is_authenticated` プロパティが true になります。 その結果、**Hello (<ユーザー名>)** メッセージと **[Log off]** が表示されます。 アプリの他の部分で `user.is_authenticated` を使用して、認証を確認できます。

    ![[Django Web プロジェクト] アプリ ページ上の Hello メッセージとログオフ コントロール](media/django/step05-logoff-control.png)

1. 認証済みユーザーに特定のリソースに対するアクセス権が付与されたかどうかを確認するには、ユーザー固有のアクセス許可をデータベースから取得する必要があります。 詳細については、[Django 認証システムの使用](https://docs.djangoproject.com/en/2.0/topics/auth/default/#permissions-and-authorization)に関するページ (Django docs) を参照してください。

1. 特に、ス―パー ユーザーまたは管理者は、相対 URL "/admin/" および "/admin/doc/" を使用して、組み込みの Django 管理者インターフェイスにアクセスします。 これらのインターフェイスを有効にするには、次の手順を実行します。

    1. 環境に docutils Python パッケージをインストールします。 そのためには、*requirements.txt* ファイルに "docutils" を追加し、**ソリューション エクスプローラー** でプロジェクトを展開し、 **[Python 環境]** ノードを選択してから、使用している環境を右クリックして **[requirements.txt からインストール]** を選択することをお勧めします。

    1. Django プロジェクトの *urls.py* を開き、次のエントリから既定のコメントを削除します。

        ```python
        from django.conf.urls import include
        from django.contrib import admin
        admin.autodiscover()

        # ...
        urlpatterns = [
            # ...
            url(r'^admin/doc/', include('django.contrib.admindocs.urls')),
            url(r'^admin/', include(admin.site.urls)),
        ]
        ```

    1. Django プロジェクトの *settings.py* ファイルで、`INSTALLED_APPS` コレクションに移動して `'django.contrib.admindocs'` を追加します。

    1. アプリを再起動したときに、"/admin/" および "/admin/doc/" に移動して、追加のユーザー アカウント作成などのタスクを実行できます。

        ![Django 管理者インターフェイス](media/django/step05-administrator-interface.png)

1. 認証フローの最後の部分は、ログオフです。 *loginpartial.html* でわかるように、 **[Log off]** リンクは単純に相対 URL "/login" に対する POST を実行します。これは、組み込みのビュー `django.contrib.auth.views.logout` によって処理されます。 このビューには UI が表示されず、ホーム ページへの移動のみを行います (*urls.py* の "^logout$" パターンで確認できます)。 ログオフ ページを表示する場合は、最初に、次のように URL パターンを変更して、"template_name" プロパティを追加し "next_page" プロパティを削除します。

    ```python
    url(r'^logout$',
        django.contrib.auth.views.logout,
        {
            'template_name': 'app/loggedoff.html',
            # 'next_page': '/',
        },
        name='logout')
    ```

    次に、以下の (最小限の) 内容で *templates/app/loggedoff.html* を作成します。

    ```html
    {% extends "app/layout.html" %}
    {% block content %}
    <h3>You have been logged off</h3>
    {% endblock %}
    ```

    結果として、次のように表示されます。

    ![追加されたログオフ ページ](media/django/step05-logged-off-page.png)

1. すべて完了したら、サーバーを停止し、もう一度ソース管理に変更をコミットします。

### <a name="question-what-is-the-purpose-of-the--csrf_token--tag-that-appears-in-the-form-elements"></a>質問:\<form\> 要素に表示される {% csrf_token %} タグの目的は何ですか?

回答:`{% csrf_token %}` タグには Django の組み込みの[クロスサイト リクエスト フォージェリ (csrf) 保護](https://docs.djangoproject.com/en/2.0/ref/csrf/) (Django docs) が含まれています。 このタグは通常、フォームなどの POST、PUT、または DELETE 要求のメソッドに関連する任意の要素に追加します。 その後、テンプレートのレンダリング関数 (`render`) により、必要な保護が挿入されます。

## <a name="next-steps"></a>次の手順

> [!div class="nextstepaction"]
> [ポーリング Django Web プロジェクト テンプレートを使用する](learn-django-in-visual-studio-step-06-polls-django-web-project-template.md)

## <a name="go-deeper"></a>詳しい説明

- [Django でのユーザー認証](https://docs.djangoproject.com/en/2.0/topics/auth/) (docs.djangoproject.com)
- GitHub のチュートリアルのソース コード:[Microsoft/python-sample-vs-learning-django](https://github.com/Microsoft/python-sample-vs-learning-django)
