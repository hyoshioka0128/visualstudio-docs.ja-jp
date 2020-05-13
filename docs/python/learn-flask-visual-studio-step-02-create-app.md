---
title: Visual Studio 手順 2 のビューとテンプレートでは、Flask のチュートリアルについて説明します
titleSuffix: ''
description: Visual Studio プロジェクトのコンテキストにおける Flask の基本のチュートリアルです。具体的には、アプリの作成およびビューとテンプレートの使用に関する手順について取り上げます。
ms.date: 01/07/2019
ms.topic: tutorial
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: 03a0eb6808b2298e0727492978d9beb7cfaf2216
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/20/2020
ms.locfileid: "79300877"
---
# <a name="step-2-create-a-flask-app-with-views-and-page-templates"></a>手順 2: ビューおよびページ テンプレートを使用して Flask アプリを作成する

**前の手順:[Visual Studio プロジェクトとソリューションを作成する](learn-flask-visual-studio-step-01-project-solution.md)**

このチュートリアルの手順 1 では、ページが 1 つある Flask アプリを作成し、すべてのコードを 1 つのファイルに収めました。 今後の開発を可能にするために、コードをリファクタリングし、ページ テンプレートの構造を作成することをお勧めします。 特に、アプリのビューのコードを、スタートアップ コードなど、他の側面と切り離すことが望まれます。

この手順では、次の方法を学習します。

> [!div class="checklist"]
> - アプリのコードをリファクタリングし、ビューとスタートアップ コードを切り離す (手順 2-1)
> - ページ テンプレートを使用してビューを表示する (手順 2-2)

## <a name="step-2-1-refactor-the-project-to-support-further-development"></a>手順 2-1: 将来の開発のためにプロジェクトをリファクタリングする

"空の Flask Web プロジェクト" テンプレートで作成されたコードには、シングル ビューと共にスタートアップ コードが含まれる *app.py* ファイルが 1 つ与えられます。 今後、複数のビューとテンプレートでアプリを開発するためには、このような重要な項目を切り離すことをお勧めします。

1. プロジェクト フォルダーで、`HelloFlask` という名前のアプリ フォルダーを作成します (**ソリューション エクスプローラー**でプロジェクトを右クリックし、 **[追加]** 、 **[新しいフォルダー]** の順に選択します)。

2. *HelloFlask* フォルダーで、 *\_\_init\_\_.py* という名前のファイルを次の内容で作成します。`Flask` インスタンスが作成され、(次の手順で作成された) アプリのビューが読み込まれます。

    ```python
    from flask import Flask
    app = Flask(__name__)

    import HelloFlask.views
    ```

3. *HelloFlask* フォルダーで、*views.py* という名前のファイルを次の内容で作成します。 *views.py* という名前が重要になるのは、 *\_\_init\_\_.py* 内で `import HelloFlask.views` を使用したためです。名前が一致しない場合、実行時にエラーが表示されます。

    ```python
    from flask import Flask
    from HelloFlask import app

    @app.route('/')
    @app.route('/home')
    def home():
        return "Hello Flask!"
    ```

    関数とルートの名前を `home` に変更することに加え、このコードには *app.py* からのページ レンダリング コードが含まれ、 *\_\_init\_\_.py* で宣言されている `app` オブジェクトをインポートします。

4. *HelloFlask* に *templates* という名前のサブフォルダーを作成します。今のところは空のままです。

5. プロジェクトのルート フォルダーで、*app.py* の名前を *runserver.py* に変更し、コンテンツを次のコードに一致させます。

    ```python
    import os
    from HelloFlask import app    # Imports the code from HelloFlask/__init__.py

    if __name__ == '__main__':
        HOST = os.environ.get('SERVER_HOST', 'localhost')

        try:
            PORT = int(os.environ.get('SERVER_PORT', '5555'))
        except ValueError:
            PORT = 5555

        app.run(HOST, PORT)
    ```

6. プロジェクト構造は次の画像のようになります。

    ![コードのリファクタリング後のプロジェクト構造](media/flask/step02-project-structure.png)

7. **[デバッグ]**  >  **[デバッグの開始]** (**F5** キー) の順に選択するか、ツール バーの **[Web サーバー]** を使用して (表示されるブラウザーは異なる可能性があります)、アプリを起動し、ブラウザーを開きます。 URL ルートには / と /home の両方を試してください。

8. コードのさまざまな部分にブレークポイントを設定し、アプリを再開し、スタートアップ シーケンスを続行することもできます。 たとえば、*runserver.py* と *HelloFlask\_* init *_.py* の最初の行と *views.py* の行 `return "Hello Flask!"` にブレークポイントを設定します。 その後、アプリを再開し ( **[デバッグ]**  >  **[再開]** の順に選択するか、**Ctrl**+**F5** キーを押すか、下の画像にあるツール ボタンをクリックします)、コードをステップ実行するか (**F10** キー)、**F5** キーを使って各ブレークポイントから実行します。

    ![Visual Studio のデバッグ ツールバーにある再起動ボタン](media/debugging-restart-toolbar-button.png)

9. 完了したら、アプリを停止します。

### <a name="commit-to-source-control"></a>ソース管理へのコミット

コードに変更を加え、テストが正常に終了したので、このタイミングで、変更を確認してソース管理に追加します。 このチュートリアルの以降の手順で、ソース管理にコミットする適切なタイミングについてもう一度触れる機会があるので、このセクションに戻って参照してください。

1. Visual Studio の下部にある変更ボタン (以下の円印) を選択すると、**チーム エクスプローラー**に移動します。

    ![Visual Studio ステータス バーにあるソース管理の変更ボタン](media/flask/step02-source-control-changes-button.png)

1. **チーム エクスプローラー**で "Refactor code" などのコミット メッセージを入力し、 **[すべてコミット]** を選択します。 コミットが完了すると、" **\<hash> のコミットがローカルで作成されました。変更をサーバーと共有するには、同期を使用してください。** " というメッセージが表示されます。 リモート リポジトリに変更をプッシュする場合は、 **[同期]** を選択して、 **[出力方向のコミット]** にある **[プッシュ]** を選択します。 リモートにプッシュする前に、複数のローカル コミットを蓄積しておくことも可能です。

    ![チーム エクスプローラーでリモートにコミットをプッシュする](media/flask/step02-source-control-push-to-remote.png)

### <a name="question-how-frequently-should-one-commit-to-source-control"></a>質問: ソース管理にはどのくらいの頻度でコミットすべきですか。

回答:ソース管理に変更をコミットすると、変更ログにレコードが作成され、必要に応じてリポジトリを元に戻すためのポイントが作成されます。 各コミットはその特定の変更について調べることもできます。 Git のコミットは高コストではないため、大量の変更を蓄積して 1 回でコミットするより頻繁にコミットすることをお勧めします。 明白なことですが、個々のファイルの細かな変更を逐一コミットする必要はありません。 一般的に、機能を追加したとき、この手順で行ったように構造を変更したとき、コードをリファクタリングしたときにコミットします。 また、コミットの詳細度について、皆にとって最適になるよう、チームの全員に確認します。

コミットする頻度とリモート リポジトリにコミットをプッシュする頻度の 2 つが重要な項目となります。 リモート リポジトリにプッシュする前にローカル リポジトリに複数のコミットを蓄積することもできます。 繰り返しになりますが、コミットする頻度はチームのリポジトリ管理方針に依存します。

## <a name="step-2-2-use-a-template-to-render-a-page"></a>手順 2-2: テンプレートを使用してページをレンダリングする

*views.py* に既にある `home` 関数では、ページに対するプレーンテキストの HTTP 応答以外は生成されません。 ただし、現実のほとんどの Web ページは、ライブ データを頻繁に取り込む豊富な HTML ページを使って応答します。 実際、関数を使用してビューを定義する主な理由はコンテンツを動的に生成することにあります。

ビューの戻り値は単なる文字列であるため、動的コンテンツを利用し、文字列内で任意の HTML を構築できます。 ただし、マークアップとデータを分離することが望まれるため、テンプレートにマークアップを、コードにデータを置くと効率的になります。

1. 手始めに、*views.py* を編集して次のコードを含めます。このコードでは、動的コンテンツを一部含むページにインライン HTML が使用されます。

    ```python
    from datetime import datetime
    from flask import render_template
    from HelloFlask import app

    @app.route('/')
    @app.route('/home')
    def home():
        now = datetime.now()
        formatted_now = now.strftime("%A, %d %B, %Y at %X")

        html_content = "<html><head><title>Hello Flask</title></head><body>"
        html_content += "<strong>Hello Flask!</strong> on " + formatted_now
        html_content += "</body></html>"

        return html_content
    ```

1. アプリを実行してページを数回更新し、日付/時刻が更新されていることを確認します。 完了したら、アプリを停止します。

1. テンプレートを使用するようにページ レンダリングを変換するには、次のような内容で *templates* フォルダーに *index.html* という名前のファイルを作成します。`{{ content }}` はプレースホルダーまたは置換トークン ("*テンプレート変数*" とも呼ばれます) であり、これにコードの値を指定します。

    ```html
    <html>
        <head><title>Hello Flask</title></head>

        <body>
            {{ content }}
        </body>
    </html>
    ```

1. `render_template` を利用してテンプレートを読み込み、"コンテンツ" の値を入力するように `home` 関数を変更します。値は、プレースホルダーの名前に一致する名前付き引数を使用することで入力されます。 Flask は自動的に *templates* フォルダーでテンプレートを探します。そのため、テンプレートのパスはそのフォルダーの相対パスとなります。

    ```python
    def home():
        now = datetime.now()
        formatted_now = now.strftime("%A, %d %B, %Y at %X")

        return render_template(
            "index.html",
            content = "<strong>Hello, Flask!</strong> on " + formatted_now)
    ```

1. アプリを実行して結果を確認します。`content` 値のインライン HTML が HTML *として*レンダリングされないことを確認します。これは、テンプレート エンジン (Jinja) は自動的に HTML コンテンツをエスケープするためです。 自動エスケープによって、インジェクション攻撃に対する偶発的な脆弱性を防ぎます。開発者は、1 つのページから入力を収集し、テンプレートのプレースホルダーを介して別のページの値として使用することがよくあります。 エスケープは、HTML をコードとは別に保存する方法が最善であることを思い出すためにも役立ちます。

    適宜、*templates\index.html* を見直し、マークアップ内にデータ別のプレースホルダーが含まれていることを確認します。

    ```html
    <html>
        <head>
            <title>{{ title }}</title>
        </head>
        <body>
            <strong>{{ message }}</strong>{{ content }}
        </body>
    </html>
    ```

    次に、`home` 関数を更新し、すべてのプレースホルダーの値を入力します。

    ```python
    def home():
        now = datetime.now()
        formatted_now = now.strftime("%A, %d %B, %Y at %X")

        return render_template(
            "index.html",
            title = "Hello Flask",
            message = "Hello, Flask!",
            content = " on " + formatted_now)
    ```

1. アプリをもう一度実行し、出力が正しく表示されていることを確認します。

    ![テンプレートを使用してアプリを実行する](media/flask/step02-result.png)

1. ソース管理への変更をコミットし、必要に応じて[手順 2-1](#commit-to-source-control) の説明に従って、リモート リポジトリを更新します。

### <a name="question-do-page-templates-have-to-be-in-a-separate-file"></a>質問:ページ テンプレートを別のファイルにする必要はありますか。

回答:通常、テンプレートは別の HTML ファイルで保持されていますが、インライン テンプレートも使用できます。 ただし、マークアップとコード間の明確な分離を維持するために、別個のファイルを使用することが推奨されています。

### <a name="question-must-templates-use-the-html-file-extension"></a>質問:テンプレートには、.html ファイルの拡張子を使用する必要がありますか。

回答:`render_template` 関数の最初の引数にファイルへの正確な相対パスを常に指定するため、ページ テンプレート ファイルの *.html* 拡張子は完全にオプションです。 ただし、Visual Studio (および、その他のエディター) では通常、 *.html* ファイルでのコード補完や構文の色付けなどの機能を提供しており、このことは、ページ テンプレートが厳密に HTML ではないという事実よりも重要です。

実際に、Flask プロジェクトを操作していると、Visual Studio では、編集中の HTML ファイルが実際には Flask テンプレートである場合を自動検出して、特定のオートコンプリート機能を提供します。 たとえば、Flask ページ テンプレートのコメント `{#` の入力を開始すると、Visual Studio では終了の `#}` 文字を自動的に提示します。 また、 **[選択範囲のコメント]** および **[選択範囲のコメントを解除]** コマンド ( **[編集]**  >  **[詳細]** メニューおよびツールバー上にある) では、HTML コメントではなく、テンプレート コメントを使用します。

### <a name="question-can-templates-be-organized-into-further-subfolders"></a>質問:サブフォルダーをさらに追加してテンプレートを整理できますか。

回答: はい。サブフォルダーを使用し、`render_template` の呼び出しで *templates* 下の相対パスを参照できます。 これは、テンプレートの名前空間を効果的に作成する方法として優れています。

## <a name="next-steps"></a>次の手順

> [!div class="nextstepaction"]
> [静的ファイルを提供し、ページを追加し、テンプレート継承を使用する](learn-flask-visual-studio-step-03-serve-static-files-add-pages.md)

## <a name="go-deeper"></a>詳しい説明

- [Flask クイックスタート - レンダリング テンプレート](https://flask.palletsprojects.com/en/1.0.x/quickstart/#rendering-templates) (flask.pocoo.org)
- GitHub のチュートリアルのソース コード:[Microsoft/python-sample-vs-learning-flask](https://github.com/Microsoft/python-sample-vs-learning-flask)
