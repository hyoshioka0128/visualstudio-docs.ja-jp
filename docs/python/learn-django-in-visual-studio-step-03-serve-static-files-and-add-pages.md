---
title: Visual Studio での Django 学習チュートリアル、手順 3、静的ファイルとページ
titleSuffix: ''
description: Visual Studio プロジェクトのコンテキストにおける Django の基本のチュートリアルです。具体的には、静的ファイルを提供する方法、アプリにページを追加する方法、およびテンプレートの継承を使用する方法を示します。
ms.date: 11/19/2018
ms.topic: tutorial
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: 7aabfa91f7f6c6204919c4a06d2d3080b5174c5f
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99942582"
---
# <a name="step-3-serve-static-files-add-pages-and-use-template-inheritance-with-django-app"></a>手順 3: Django アプリで静的ファイルを提供し、ページを追加し、テンプレート継承を使用する

**前の手順:[ビューおよびページ テンプレートを使用して Django アプリを作成する](learn-django-in-visual-studio-step-02-create-an-app.md)**

このチュートリアルの前の手順では、自己完結型 HTML の単一のページを使って最小限の Django アプリを作成する方法を学びました。 ただし、最新の Web アプリは通常、多数のページで構成されており、CSS や JavaScript ファイルなどの共有リソースを活用して、一貫したスタイル設定や動作を提供します。

この手順では、次の方法を学習します。

> [!div class="checklist"]
> - 便利なスケルトン コードによってさまざまな種類の新しいファイルを迅速に追加するための Visual Studio の項目テンプレートを使用する (手順 3-1)
> - Django プロジェクトを構成して静的ファイルを提供する (手順 3-2)
> - アプリに追加ページを付け加える (手順 3-3)
> - テンプレートの継承を使用して、複数のページで使用されるヘッダーとナビゲーション バーを作成する (手順 3-4)

## <a name="step-3-1-become-familiar-with-item-templates"></a>手順 3-1:項目テンプレートを理解する

Django アプリを開発する場合、通常、より多くの Python、HTML、CSS、および JavaScript ファイルを追加します。 Visual Studio では、(デプロイに必要になる可能性がある *web.config* のような他のファイルだけでなく) ファイルの種類ごとに、すぐに使用できる便利な [項目テンプレート](python-item-templates.md)を提供しています。

使用可能なテンプレートを確認するには、**ソリューション エクスプローラー** に移動して、項目を作成するフォルダーを右クリックし、 **[追加]**  >  **[新しい項目]** の順に選択します。

![Visual Studio の新しい項目の追加ダイアログ](media/django/step03-add-new-item-dialog.png)

テンプレートを使用するには、目的のテンプレートを選択して、ファイルの名前を指定し、 **[OK]** をクリックします。 この方法で項目を追加すると、Visual Studio プロジェクトに自動的にファイルを追加して、ソース管理への変更にマーク付けされます。

### <a name="question-how-does-visual-studio-know-which-item-templates-to-offer"></a>質問:Visual Studio では、提供する項目テンプレートをどのように把握していますか。

回答:Visual Studio プロジェクト ファイル ( *.pyproj*) には、Python プロジェクトとしてマーク付けするプロジェクト タイプ識別子が含まれます。 Visual Studio は、このタイプ識別子を使用して、プロジェクト タイプに適合する項目テンプレートのみを表示します。 このように、Visual Studio では、多数のプロジェクト タイプに対応する豊富な項目テンプレート セットを提供でき、項目テンプレートを毎回分類して調べる必要はありません。

## <a name="step-3-2-serve-static-files-from-your-app"></a>手順 3-2:アプリからの静的ファイルを提供する

Python を使って構築された Web アプリ (任意のフレームワークを使用する) では、Python ファイルは常に Web ホストのサーバー上で実行され、ユーザーのコンピューターに送信されることはありません。 しかし、CSS や JavaScript などの他のファイルは、これらのファイルが要求されたときに、ホスト サーバーから単純にそのまま配信されるように、ブラウザーで排他的に使用されます。 このようなファイルは "静的" ファイルと呼ばれ、Django では、コードを記述しなくても自動的にこれらのファイルを配信できます。

Django プロジェクトの *settings.py* にある以下の行のおかげで、Django プロジェクトでは既定で、アプリの *static* フォルダーから静的ファイルを提供するように構成されています。

```python
# Static files (CSS, JavaScript, Images)
# https://docs.djangoproject.com/en/1.9/howto/static-files/

STATIC_URL = '/static/'

STATIC_ROOT = posixpath.join(*(BASE_DIR.split(os.path.sep) + ['static']))
```

任意のフォルダー構造を使用して目的の *static* 内にファイルを編成し、そのフォルダー内で相対パスを使用してファイルを参照できます。 このプロセスを示すために、次の手順では CSS ファイルをアプリに追加して、*index.html* テンプレートに該当のスタイルシートを使用しています。

1. **ソリューション エクスプローラー** で、Visual Studio プロジェクトの **HelloDjangoApp** フォルダーを右クリックして、 **[追加]**  >  **[新しいフォルダー]** を選択して、フォルダーに `static` という名前を付けます。

1. **static** フォルダーを右クリックし、 **[追加]**  >  **[新しい項目]** を選択します。 表示されたダイアログ ボックスで、**Stylesheet** テンプレートを選択して、ファイルに `site.css` という名前を付けて、 **[OK]** をクリックします。 **site.css** ファイルがプロジェクトに表示され、エディターで開かれます。 次の画像のようなフォルダー構成が表示されます。

    ![ソリューション エクスプローラーに表示される静的ファイルの構造](media/django/step03-static-file-structure.png)

1. *site.css* の内容を次のコードに置き換えて、ファイルを保存します。

    ```css
    .message {
        font-weight: 600;
        color: blue;
    }
    ```

1. アプリの *templates/HelloDjangoApp/index.html* ファイルの内容を次のコードに置き換えます。これにより、手順 2 で使用した `<strong>` 要素が `message` スタイル クラスを参照する `<span>` に置き換えられます。 この方法でスタイル クラスを使用すると、要素のスタイル設定をこれまで以上に柔軟に行えます (VS 2017 15.7 以前の使用時、*index.html* を *templates* 内のサブフォルダーに移動済みの場合、手順 2-4 の [テンプレートの名前空間の設定](learn-django-in-visual-studio-step-02-create-an-app.md#template-namespacing)に関する記述を参照してください)。

    ```html
    <html>
        <head>
            <title>{{ title }}</title>
            {% load staticfiles %} <!-- Instruct Django to load static files -->
            <link rel="stylesheet" type="text/css" href="{% static 'site.css' %}" />
        </head>
        <body>
            <span class="message">{{ message }}</span>{{ content }}
        </body>
    </html>
    ```

1. プロジェクトを実行して、結果を確認します。 終わったらサーバーを停止し、([手順 2](learn-django-in-visual-studio-step-02-create-an-app.md#commit-to-source-control) の説明にあるように) 必要に応じてソース管理に対する変更をコミットします。

### <a name="question-what-is-the-purpose-of-the--load-staticfiles--tag"></a>質問:{% load staticfiles %} タグの目的は何ですか。

回答:`<head>` や `<body>` のような要素で静的ファイルを参照する前に、`{% load staticfiles %}` 行が必要です。 このセクションで示した例では、"staticfiles" はカスタム Django テンプレート タグ設定を参照します。これにより、`{% static %}` 構文を使って静的ファイルを参照できます。  `{% load staticfiles %}` がないと、アプリが実行されたときに例外が表示されます。

### <a name="question-are-there-any-conventions-for-organizing-static-files"></a>質問:静的ファイルを編成するにあたって、何らかの規則はありますか。

回答:*static* フォルダーには、他の CSS、JavaScript、HTML ファイルを自由に追加できます。 静的ファイルを編成する一般的な方法は、*fonts*、*scripts*、*content* (スタイルシートとその他のファイル用) という名前のサブフォルダーを作成することです。 どの場合も、`{% static %}` 参照のファイルへの相対パスにこれらのフォルダーを必ず含めてください。

### <a name="question-can-i-complete-the-same-task-without-using-the--load-staticfiles--tag"></a>質問:{% load staticfiles %} タグを使用せずに同じタスクを完了することはできますか。

回答:はい、できます。

```html
<html>
    <head>
        <title>{{ title }}</title>
        <link rel="stylesheet" type="text/css" href="../../static/site.css" />
    </head>
    <body>
        <span class="message">{{ message }}</span>{{ content }}
    </body>
</html>
```

## <a name="step-3-3-add-a-page-to-the-app"></a>手順 3-3:アプリにページを追加する

アプリに別のページを追加することには、次のような意味があります。

- ビューを定義する Python 関数を追加する。
- ページのマークアップのためにテンプレートを追加する。
- Django プロジェクトの *urls.py* ファイルに必要なルーティングを追加する。

次の手順では、"HelloDjangoApp" プロジェクトに "About"\(詳細\) ページと、ホーム ページからこのページへのリンクを追加します。

1. **ソリューション エクスプローラー** で、**templates/HelloDjangoApp** フォルダーを右クリックし、 **[追加]**  >  **[新しい項目]** を選択し、 **[HTML ページ]** 項目テンプレートを選択して、ファイルに `about.html` という名前を付けて、 **[OK]** をクリックします。

    > [!Tip]
    > **[新しい項目]** コマンドが **[追加]** メニューに表示されない場合、Visual Studio がデバッグ モードを終了できるようにサーバーを停止済みであることを確認してください。

1. *about.html* の内容を次のマークアップに置き換えます (手順 3-4 で、ホーム ページへの明示的なリンクをシンプルなナビゲーション バーに置き換えます)。

    ```html
    <html>
        <head>
            <title>{{ title }}</title>
            {% load staticfiles %}
            <link rel="stylesheet" type="text/css" href="{% static 'site.css' %}" />
        </head>
        <body>
            <div><a href="home">Home</a></div>
            {{ content }}
        </body>
    </html>
    ```

1. アプリの *views.py* ファイルを開き、次のテンプレートを使用する `about` という名前の関数を追加します。

    ```python
    def about(request):
        return render(
            request,
            "HelloDjangoApp/about.html",
            {
                'title' : "About HelloDjangoApp",
                'content' : "Example app page for Django."
            }
        )
    ```

1. Django プロジェクトの *urls.py* ファイルを開き、次の行を `urlPatterns` 配列に追加します。

    ```python
    url(r'^about$', HelloDjangoApp.views.about, name='about'),
    ```

1. *templates/HelloDjangoApp/index.html* ファイルを開き、`<body>` 要素の下に次の行を追加して、About ページにリンクします (繰り返しになりますが、このリンクは手順 3-4 でナビゲーション バーに置き換えます)。

    ```html
    <div><a href="about">About</a></div>
    ```

1. **[ファイル]**  >  **[すべて保存]** メニュー コマンドを使用するか、または単純に **Ctrl**+**Shift**+**S** キーを押して、すべてのファイルを保存します (技術的には、Visual Studio でプロジェクトを実行するとファイルが自動的に保存されるので、この手順は必要ありませんが、 知っておくとよいコマンドです)。

1. プロジェクトを実行して結果を確認し、ページ間の移動をチェックします。 終わったら、サーバーを閉じます。

### <a name="question-i-tried-using-index-for-the-link-to-the-home-page-but-it-didnt-work-why"></a>質問:ホーム ページへのリンクに "index" の使用を試みましたが、機能しませんでした。 なぜでしょうか。

回答:*views.py* のビュー関数が `index` という名前であっても、Django プロジェクトの *urls.py* ファイルにある URL ルーティング パターンは、文字列 "index" と一致する正規表現を含みません。 この文字列と一致させるには、パターン `^index$` に対応する別のエントリを追加する必要があります。

次のセクションで示すように、ページ テンプレートで `{% url '<pattern_name>' %}` タグを使用して、パターンの *名前* を参照する方が優れた方法です。この場合、Django は状況に見合った URL を作成します。 たとえば、*about.html* の `<div><a href="home">Home</a></div>` を `<div><a href="{% url 'index' %}">Home</a></div>` に置き換えます。 *urls.py* にある最初の URL パターンは実際、(`name='index'` 引数の特性により) 'index' という名前になるため、ここでは 'index' の使用が有効です。 また、2 番目のパターンを参照するには、'home' を使用することもできます。

## <a name="step-3-4-use-template-inheritance-to-create-a-header-and-nav-bar"></a>手順 3-4:テンプレートの継承を使ってヘッダーとナビゲーション バーを作成する

最新の Web アプリでは通常、各ページに明示的なナビゲーション リンクを保持するのではなく、最も重要なページ リング、ポップアップ メニューなどを提供するブランド ヘッダーとナビゲーション バーを使用します。 しかし、ヘッダーとナビゲーション バーをすべてのページで確実に同じにするために、各ページ テンプレートで同じコードを繰り返したくはありません。 代わりに、すべてのページの共通部分を 1 つの場所に定義します。

Django のテンプレート システムでは、複数のテンプレート間で特定の要素を再利用するために、インクルードと継承という 2 つの方法を提供しています。

- *インクルード* とは、構文 `{% include <template_path> %}` を使用して参照元テンプレートの特定の場所に挿入する他のページ テンプレートのことです。 また、コード内で動的にパスを変更する場合、変数を使用することもできます。 インクルードは通常、ページ上の特定の場所に共有テンプレートを組み入れるために、ページの本文で使用されます。

- *継承* は、ページ テンプレートの冒頭で `{% extends <template_path> %}` を使用して、参照元テンプレートが構築される共有の基本テンプレートを指定します。 継承は一般的に、アプリのページの共有レイアウト、ナビゲーション バー、およびその他の構造を定義するために使用されます。これにより、参照元テンプレートで必要になるのは、*ブロック* と呼ばれる基本テンプレートの特定の領域を追加または修正することだけです。

どちらの場合も、`<template_path>` はアプリの *templates* フォルダーへの相対です (`../` または `./` も許可されます)。

基本テンプレートでは、`{% block <block_name> %}` と `{% endblock %}` タグを使用してブロックを表現します。 参照元テンプレートで同じブロック名のタグを使用している場合、基本テンプレートの内容は、そのブロックの内容でオーバーライドされます。

次の手順では、継承を例示します。

1. アプリの *templates/HelloDjangoApp* フォルダーで、*layout.html* という新しい HTML ファイルを作成し ( **[追加]**  >  **[新しい項目]** コンテキスト メニュー、または **[追加]**  >  **[HTML ページ]** を使用)、その内容を以下のマークアップに置き換えます。 このテンプレートが含む "content" というブロックは、参照元ページで置き換える必要があることがわかります。

    ```html
    <!DOCTYPE html>
    <html>
    <head>
        <meta charset="utf-8" />
        <title>{{ title }}</title>
        {% load staticfiles %}
        <link rel="stylesheet" type="text/css" href="{% static 'site.css' %}" />
    </head>

    <body>
        <div class="navbar">
           <a href="/" class="navbar-brand">Hello Django</a>
           <a href="{% url 'home' %}" class="navbar-item">Home</a>
           <a href="{% url 'about' %}" class="navbar-item">About</a>
        </div>

        <div class="body-content">
    {% block content %}{% endblock %}
            <hr/>
            <footer>
                <p>&copy; 2018</p>
            </footer>
        </div>
    </body>
    </html>
    ```

1. 次のスタイルをアプリの *static/site.css* ファイルに追加します (このチュートリアルでは、レスポンシブ設計を示すことを意図していません。以下に示したスタイルは単純に、面白い結果を生成します)。

    ```css
    .navbar {
        background-color: lightslategray;
        font-size: 1em;
        font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
        color: white;
        padding: 8px 5px 8px 5px;
    }

    .navbar a {
        text-decoration: none;
        color: inherit;
    }

    .navbar-brand {
        font-size: 1.2em;
        font-weight: 600;
    }

    .navbar-item {
        font-variant: small-caps;
        margin-left: 30px;
    }

    .body-content {
        padding: 5px;
        font-family:'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    }
    ```

1. 基本テンプレートを参照して content ブロックをオーバーライドするように、*templates/HelloDjangoApp/index.html* を変更します。 継承を使用することで、このテンプレートがシンプルになることがわかります。

    ```html
    {% extends "HelloDjangoApp/layout.html" %}
    {% block content %}
    <span class="message">{{ message }}</span>{{ content }}
    {% endblock %}
    ```

1. また、基本テンプレートを参照して content ブロックをオーバーライドするように、*templates/HelloDjangoApp/about.html* を次のように変更します。

    ```html
    {% extends "HelloDjangoApp/layout.html" %}
    {% block content %}
    {{ content }}
    {% endblock %}
    ```

1. サーバーを実行して、結果を確認します。 終わったら、サーバーを閉じます。

    ![ナビゲーション バーを表示するアプリを実行する](media/django/step03-nav-bar.png)

1. アプリに十分な変更を加えたので、このタイミングで再び[ソース管理に変更をコミットする](learn-django-in-visual-studio-step-02-create-an-app.md#commit-to-source-control)ことが適切です。

## <a name="next-steps"></a>次の手順

> [!div class="nextstepaction"]
> [Django Web プロジェクト テンプレートを使用する](learn-django-in-visual-studio-step-04-full-django-project-template.md)

## <a name="go-deeper"></a>詳しい説明

- [Azure App Service への Web アプリの展開](publishing-python-web-applications-to-azure-from-visual-studio.md)
- [最初の Django アプリの作成、パート 3 (ビュー)](https://docs.djangoproject.com/en/2.0/intro/tutorial03/) (docs.djangoproject.com)
- 制御フローなど Django テンプレートの詳細な機能について、「[The Django template language](https://docs.djangoproject.com/en/2.0/ref/templates/language/)」(Django テンプレート言語) (docs.djangoproject.com) を確認する
- `{% url %}` タグの使用に関する完全な詳細について、Django テンプレート リファレンスの「[Built-in template tags and filters](https://docs.djangoproject.com/en/2.0/ref/templates/builtins/)」(組み込みのテンプレート タグとフィルター) (docs.djangoproject.com) にある [URL](https://docs.djangoproject.com/en/2.0/ref/templates/builtins/#url) を確認する
- GitHub のチュートリアルのソース コード:[Microsoft/python-sample-vs-learning-django](https://github.com/Microsoft/python-sample-vs-learning-django)
