---
title: Visual Studio での Flask 学習チュートリアル、手順 3、静的ファイルとページ
titleSuffix: ''
description: Visual Studio プロジェクトのコンテキストにおける Flask の基本のチュートリアルです。具体的には、静的ファイルを提供する方法、アプリにページを追加する方法、およびテンプレートの継承を使用する方法を示します。
ms.date: 01/07/2019
ms.topic: tutorial
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: 69fd704976ee941cb053d75040a3d3ec7871a380
ms.sourcegitcommit: d8609a78b460d4783f5d59c0c89454910a4dbd21
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2020
ms.locfileid: "88238743"
---
# <a name="step-3-serve-static-files-add-pages-and-use-template-inheritance-with-flask-app"></a>手順 3: Flask アプリで静的ファイルを提供し、ページを追加し、テンプレート継承を使用する

**前の手順:[ビューおよびページ テンプレートを使用して Flask アプリを作成する](learn-flask-visual-studio-step-02-create-app.md)**

このチュートリアルの前の手順では、自己完結型 HTML の単一のページを使って最小限の Flask アプリを作成する方法を学びました。 ただし、最新の Web アプリは通常、多数のページで構成されており、CSS や JavaScript ファイルなどの共有リソースを活用して、一貫したスタイル設定や動作を提供します。

この手順では、次の方法を学習します。

> [!div class="checklist"]
> - 便利なスケルトン コードによってさまざまな種類の新しいファイルを迅速に追加するための Visual Studio の項目テンプレートを使用する (手順 3-1)
> - コードから静的ファイルを提供する (手順 3-2、オプション)
> - アプリに追加ページを付け加える (手順 3-3)
> - テンプレートの継承を使用して、複数のページで使用されるヘッダーとナビゲーション バーを作成する (手順 3-4)

## <a name="step-3-1-become-familiar-with-item-templates"></a>手順 3-1:項目テンプレートを理解する

Flask アプリを開発する場合、通常、より多くの Python、HTML、CSS、および JavaScript ファイルを追加します。 Visual Studio では、(デプロイに必要になる可能性がある *web.config* のような他のファイルだけでなく) ファイルの種類ごとに、すぐに使用できる便利な[項目テンプレート](python-item-templates.md)を提供しています。

使用可能なテンプレートを確認するには、**ソリューション エクスプローラー**に移動して、項目を作成するフォルダーを右クリックし、**[追加]** > **[新しい項目]** の順に選択します。

![Visual Studio の新しい項目の追加ダイアログ](media/flask/step03-add-new-item-dialog.png)

テンプレートを使用するには、目的のテンプレートを選択して、ファイルの名前を指定し、**[OK]** をクリックします。 この方法で項目を追加すると、Visual Studio プロジェクトに自動的にファイルを追加して、ソース管理への変更にマーク付けされます。

### <a name="question-how-does-visual-studio-know-which-item-templates-to-offer"></a>質問:Visual Studio では、提供する項目テンプレートをどのように把握していますか。

回答:Visual Studio プロジェクト ファイル (*.pyproj*) には、Python プロジェクトとしてマーク付けするプロジェクト タイプ識別子が含まれます。 Visual Studio は、このタイプ識別子を使用して、プロジェクト タイプに適合する項目テンプレートのみを表示します。 このように、Visual Studio では、多数のプロジェクト タイプに対応する豊富な項目テンプレート セットを提供でき、項目テンプレートを毎回分類して調べる必要はありません。

## <a name="step-3-2-serve-static-files-from-your-app"></a>手順 3-2:アプリからの静的ファイルを提供する

Python を使って構築された Web アプリ (任意のフレームワークを使用する) では、Python ファイルは常に Web ホストのサーバー上で実行され、ユーザーのコンピューターに送信されることはありません。 しかし、CSS や JavaScript などの他のファイルは、これらのファイルが要求されたときに、ホスト サーバーから単純にそのまま配信されるように、ブラウザーで排他的に使用されます。 このようなファイルは "静的" ファイルと呼ばれ、Flask では、コードを記述しなくても自動的にこれらのファイルを配信できます。 たとえば、HTML ファイル内では、プロジェクトでの相対パスを使用するだけで静的ファイルを参照できます。 この手順の最初のセクションでは、既存のページ テンプレートに CSS ファイルを追加します。

API エンドポイントの実装を使うなどしてコードから静的ファイルを提供する必要がある場合、Flask には、*static* (プロジェクト ルート内) という名前のフォルダー内の相対パスを使用してファイルを参照できる便利な方法が用意されています。 この手順の 2 番目のセクションでは、簡単な静的データ ファイルを使用する方法を示します。

どちらの場合も、*static* 下のファイルを好きなように編成できます。

### <a name="use-a-static-file-in-a-template"></a>テンプレートで静的ファイルを使用する

1. **ソリューション エクスプローラー**で、Visual Studio プロジェクトの **HelloFlask** フォルダーを右クリックして、**[追加]** > **[新しいフォルダー]** を選択して、フォルダーに `static` という名前を付けます。

1. **static** フォルダーを右クリックし、**[追加]** > **[新しい項目]** を選択します。 表示されたダイアログ ボックスで、**Stylesheet** テンプレートを選択して、ファイルに `site.css` という名前を付けて、**[OK]** をクリックします。 **site.css** ファイルがプロジェクトに表示され、エディターで開かれます。 次の画像のようなフォルダー構成が表示されます。

    ![ソリューション エクスプローラーに表示される静的ファイルの構造](media/flask/step03-static-file-structure.png)

1. *site.css* の内容を次のコードに置き換えて、ファイルを保存します。

    ```css
    .message {
        font-weight: 600;
        color: blue;
    }
    ```

1. アプリの *templates/index.html* ファイルの内容を次のコードに置き換えます。これにより、手順 2 で使用した `<strong>` 要素が `message` スタイル クラスを参照する `<span>` に置き換えられます。 この方法でスタイル クラスを使用すると、要素のスタイル設定をこれまで以上に柔軟に行えます 

    ```html
    <html>
        <head>
            <title>{{ title }}</title>
            <link rel="stylesheet" type="text/css" href="/static/site.css" />
        </head>
        <body>
            <span class="message">{{ message }}</span>{{ content }}
        </body>
    </html>
    ```

1. プロジェクトを実行して、結果を確認します。 終わったらアプリを停止し、([手順 2](learn-flask-visual-studio-step-02-create-app.md#commit-to-source-control) の説明にあるように) 必要に応じてソース管理に対する変更をコミットします。

### <a name="serve-a-static-file-from-code"></a>コードから静的ファイルを提供する

Flask で提供されている `serve_static_file` という名前の関数をコードから呼び出して、プロジェクトの *static* フォルダー内の任意のファイルを参照できます。 次のプロセスは、静的データ ファイルを返す簡単な API エンドポイントを作成します。

1. まだ行っていない場合は、次のようにして *static* フォルダーを作成します。**ソリューション エクスプローラー**で、Visual Studio プロジェクトの **HelloFlask** フォルダーを右クリックして、**[追加]** > **[新しいフォルダー]** を選択して、フォルダーに `static` という名前を付けます。

1. *static* フォルダーに、次のような内容 (意味のないサンプル データです) で *data.json* という名前の静的 JSON データ ファイルを作成します。

    ```json
    {
        "01": {
            "note" : "Data is very simple because we're demonstrating only the mechanism."
        }
    }
    ```

1. *views.py* に、`send_static_file` メソッドを使用して静的データ ファイルを返す関数とルート /api/data を追加します。

    ```python
    @app.route('/api/data')
    def get_data():
      return app.send_static_file('data.json')
    ```

1. アプリを実行して /api/data エンドポイントに移動し、静的ファイルが返されることを確認します。 完了したら、アプリを停止します。

### <a name="question-are-there-any-conventions-for-organizing-static-files"></a>質問:静的ファイルを編成するにあたって、何らかの規則はありますか。

回答:*static* フォルダーには、他の CSS、JavaScript、HTML ファイルを自由に追加できます。 静的ファイルを編成する一般的な方法は、*fonts*、*scripts*、*content* (スタイルシートとその他のファイル用) という名前のサブフォルダーを作成することです。

### <a name="question-how-do-i-handle-url-variables-and-query-parameters-in-an-api"></a>質問:API では URL 変数とクエリ パラメーターをどのように処理すればよいですか。

回答:「[質問:Flask は変数の URL ルートとクエリ パラメーターをどのように処理しますか?](learn-flask-visual-studio-step-01-project-solution.md#qa-url-variables)」については、手順 1-4 の回答をご覧ください。

## <a name="step-3-3-add-a-page-to-the-app"></a>手順 3-3:アプリにページを追加する

アプリに別のページを追加することには、次のような意味があります。

- ビューを定義する Python 関数を追加する。
- ページのマークアップのためにテンプレートを追加する。
- Flask プロジェクトの *urls.py* ファイルに必要なルーティングを追加する。

次の手順では、"HelloFlask" プロジェクトに "About" ページと、ホーム ページからこのページへのリンクを追加します。

1. **ソリューション エクスプローラー**で、**templates** フォルダーを右クリックし、**[追加]** > **[新しい項目]** を選択し、**[HTML ページ]** 項目テンプレートを選択して、ファイルに `about.html` という名前を付けて、**[OK]** をクリックします。

    > [!Tip]
    > **[新しい項目]** コマンドが **[追加]** メニューに表示されない場合、Visual Studio がデバッグ モードを終了できるようにアプリを停止済みであることを確認してください。

1. *about.html* の内容を次のマークアップに置き換えます (手順 3-4 で、ホーム ページへの明示的なリンクをシンプルなナビゲーション バーに置き換えます)。

    ```html
    <html>
        <head>
            <title>{{ title }}</title>
            <link rel="stylesheet" type="text/css" href="/static/site.css" />
        </head>
        <body>
            <div><a href="home">Home</a></div>
            {{ content }}
        </body>
    </html>
    ```

1. アプリの *views.py* ファイルを開き、次のテンプレートを使用する `about` という名前の関数を追加します。

    ```python
    @app.route('/about')
    def about():
        return render_template(
            "about.html",
            title = "About HelloFlask",
            content = "Example app page for Flask.")
    ```

1. *templates/index.html* ファイルを開き、`<body>` 要素のすぐ内部に次の行を追加して、About ページにリンクします (繰り返しになりますが、このリンクは手順 3-4 でナビゲーション バーに置き換えます)。

    ```html
    <div><a href="about">About</a></div>
    ```

1. **[ファイル]** > **[すべて保存]** メニュー コマンドを使用するか、または単純に **Ctrl**+**Shift**+**S** キーを押して、すべてのファイルを保存します  (技術的には、Visual Studio でプロジェクトを実行するとファイルが自動的に保存されるので、この手順は必要ありませんが、 知っておくとよいコマンドです)。

1. プロジェクトを実行して結果を確認し、ページ間の移動をチェックします。 終わったらアプリを停止します。

### <a name="question-does-the-name-of-a-page-function-matter-to-flask"></a>質問:Flask ではページ関数の名前は重要ですか。

回答:いいえ。Flask が関数を呼び出して応答を生成するための URL を決定する `@app.route` デコレーターなので、重要ではありません。 通常は関数名をルートと同じにしますが、一致させる必要はありません。

## <a name="step-3-4-use-template-inheritance-to-create-a-header-and-nav-bar"></a>手順 3-4:テンプレートの継承を使ってヘッダーとナビゲーション バーを作成する

最新の Web アプリでは通常、各ページに明示的なナビゲーション リンクを保持するのではなく、最も重要なページ リング、ポップアップ メニューなどを提供するブランド ヘッダーとナビゲーション バーを使用します。 しかし、ヘッダーとナビゲーション バーをすべてのページで確実に同じにするために、各ページ テンプレートで同じコードを繰り返したくはありません。 代わりに、すべてのページの共通部分を 1 つの場所に定義します。

Flask のテンプレート システム (既定では Jinja) では、複数のテンプレート間で特定の要素を再利用するために、インクルードと継承という 2 つの方法を提供しています。

- *インクルード*とは、構文 `{% include <template_path> %}` を使用して参照元テンプレートの特定の場所に挿入する他のページ テンプレートのことです。 また、コード内で動的にパスを変更する場合、変数を使用することもできます。 インクルードは通常、ページ上の特定の場所に共有テンプレートを組み入れるために、ページの本文で使用されます。

- *継承*は、ページ テンプレートの冒頭で `{% extends <template_path> %}` を使用して、参照元テンプレートが構築される共有の基本テンプレートを指定します。 継承は一般的に、アプリのページの共有レイアウト、ナビゲーション バー、およびその他の構造を定義するために使用されます。これにより、参照元テンプレートで必要になるのは、*ブロック*と呼ばれる基本テンプレートの特定の領域を追加または修正することだけです。

どちらの場合も、`<template_path>` はアプリの *templates* フォルダーへの相対です (`../` または `./` も許可されます)。

基本テンプレートでは、`{% block <block_name> %}` タグと `{% endblock %}` タグを使用して、"*ブロック*" を表現します。 参照元テンプレートで同じブロック名のタグを使用している場合、基本テンプレートの内容は、そのブロックの内容でオーバーライドされます。

次の手順では、継承を例示します。

1. アプリの *templates* フォルダーで、*layout.html* という新しい HTML ファイルを作成し (**[追加]** > **[新しい項目]** コンテキスト メニュー、または **[追加]** > **[HTML ページ]** を使用)、その内容を以下のマークアップに置き換えます。 このテンプレートが含む "content" というブロックは、参照元ページで置き換える必要があることがわかります。

    ```html
    <!DOCTYPE html>
    <html>
    <head>
        <meta charset="utf-8" />
        <title>{{ title }}</title>
        <link rel="stylesheet" type="text/css" href="/static/site.css" />
    </head>

    <body>
        <div class="navbar">
            <a href="/" class="navbar-brand">Hello Flask</a>
            <a href="{{ url_for('home') }}" class="navbar-item">Home</a>
            <a href="{{ url_for('about') }}" class="navbar-item">About</a>
        </div>

        <div class="body-content">
            {% block content %}
            {% endblock %}
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

1. 基本テンプレートを参照して content ブロックをオーバーライドするように、*templates/index.html* を変更します。 継承を使用することで、このテンプレートがシンプルになることがわかります。

    ```html
    {% extends "layout.html" %}
    {% block content %}
    <span class="message">{{ message }}</span>{{ content }}
    {% endblock %}
    ```

1. また、基本テンプレートを参照して content ブロックをオーバーライドするように、*templates/about.html* を次のように変更します。

    ```html
    {% extends "layout.html" %}
    {% block content %}
    {{ content }}
    {% endblock %}
    ```

1. サーバーを実行して、結果を確認します。 終わったら、サーバーを閉じます。

    ![ナビゲーション バーを表示するアプリを実行する](media/flask/step03-nav-bar.png)

1. アプリに十分な変更を加えたので、このタイミングで再び[ソース管理に変更をコミットする](learn-django-in-visual-studio-step-02-create-an-app.md#commit-to-source-control)ことが適切です。

## <a name="next-steps"></a>次の手順

> [!div class="nextstepaction"]
> [完全な Flask Web プロジェクト テンプレートを使用する](learn-flask-visual-studio-step-04-full-flask-project-template.md)

## <a name="go-deeper"></a>詳しい説明

- [Azure App Service への Web アプリの展開](publishing-python-web-applications-to-azure-from-visual-studio.md)
- 制御フローなど、Jinja テンプレートの他の機能については、[Jinja Template Designer のドキュメント](http://jinja.palletsprojects.com/en/2.10.x/templates/) (jinja.pocoo.org) をご覧ください
- `url_for` の使用方法について詳しくは、Flask アプリケーション オブジェクトのドキュメント (flask.pocoo.org) で [url_for](https://flask.palletsprojects.com/en/1.0.x/api/#flask.url_for) をご覧ください
- GitHub のチュートリアルのソース コード:[Microsoft/python-sample-vs-learning-flask](https://github.com/Microsoft/python-sample-vs-learning-flask)
