---
title: Python で CookieCutter テンプレートを使用する
description: Visual Studio では、Python コード用のテンプレートを見つけて、これらのテンプレートからプロジェクトを作成する、グラフィカルな Cookiecutter 拡張機能がサポートされています。
ms.date: 01/28/2019
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: 2d58462b90039e14ae98fe450812ca4cfdb6cbbd
ms.sourcegitcommit: a801ca3269274ce1de4f6b2c3f40b58bbaa3f460
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/25/2020
ms.locfileid: "88801582"
---
# <a name="use-the-cookiecutter-extension"></a>Cookiecutter 拡張機能の使用

[Cookiecutter](https://cookiecutter.readthedocs.io/en/latest/) は、テンプレートの検出、テンプレート オプションの入力、プロジェクトとファイルの作成を行うためのグラフィカル ユーザー インターフェイスを提供します。 Cookiecutter は Visual Studio 2017 以降に付属しており、Visual Studio の以前のバージョンにも個別にインストールできます。

Cookiecutter には、Python 3.3 以降 (32 ビットまたは 64 ビット) または Anaconda 3 4.2 以降 (32 ビットまたは 64 ビット) が必要です。 適切な Python インタープリターを使用できない場合、警告が Visual Studio に表示されます。 Visual Studio の実行中に Python インタープリターをインストールした場合は、Cookiecutter ツールバーの **[ホーム]** ボタンを選択すると、新しくインストールしたインタープリターが検出されます。 (環境全般の詳細については、「[Python 環境](managing-python-environments-in-visual-studio.md)」を参照してください。)

インストールしたら、 **[表示]**  >  **[Cookiecutter Explorer]** を選択して Cookiecutter のウィンドウを開きます。

![Cookiecutter のメイン ウィンドウ](media/cookiecutter-overview.png)

## <a name="cookiecutter-workflow"></a>Cookiecutter のワークフロー

Cookiecutter の操作は、テンプレートを参照して選択し、ローカル コンピューターに複製し、オプションを設定して、そのテンプレートからコードを作成するというプロセスです。以下のセクションで、このプロセスについて説明します。

### <a name="browse-templates"></a>テンプレートの参照

Cookiecutter のホーム ページにはテンプレートの一覧が次のグループに分けて表示され、一覧からテンプレートを選択できます。

| グループ | [説明] |
| --- | --- |
| **インストール済み** | ローカル コンピューターにインストール済みのテンプレートです。 オンライン テンプレートが使用されると、そのリポジトリが *~/.cookiecutters* のサブフォルダーに自動的に複製されます。 インストール済みテンプレートを選択して **Delete** キーを押すと削除できます。 |
| **推奨** | 推奨フィードから読み込まれたテンプレートです。 既定のフィードはマイクロソフトによって選別されます。 フィードをカスタマイズする方法の詳細については、後の「[Cookiecutter のオプション](#cookiecutter-options)」をご覧ください。 |
| **GitHub** | Cookiecutter キーワードの GitHub での検索結果です。 GitHub からの結果は改ページ調整されて返されます。さらに多くの結果がある場合は、一覧の最後に **[さらに読み込む]** が表示されます。 |
| **Custom** | カスタムの場所が検索ボックスに入力されると、このグループに表示されます。 GitHub リポジトリへの完全なパスを入力するか、ローカル ディスク上のフォルダーへの完全なパスを入力します。 |

### <a name="cloning"></a>複製

テンプレートを選択して **[次へ]** を選択すると、Cookiecutter によって作業用のローカル コピーが作成されます。

**[推奨]** または **[GitHub]** グループからテンプレートを選択するか、検索ボックスにカスタム URL を入力してそのテンプレートを選択した場合は、テンプレートが複製されてローカル コンピューターにインストールされます。 そのテンプレートが Visual Studio の以前のセッションでインストールされている場合は、自動的に削除され、最新のバージョンが複製されます。

**[インストール済み]** グループからテンプレートを選択するか、検索ボックスにカスタム フォルダーのパスを入力してそのテンプレートを選択した場合は、テンプレートが複製されずに Visual Studio に読み込まれます。

> [!Important]
> Cookiecutter のテンプレートは *~/.cookiecutters* という単一のフォルダーの下に複製されます。 各サブフォルダーの名前は git リポジトリの名前に従って付けられ、GitHub のユーザー名を含みません。 作成者が異なる、同じ名前の複数のテンプレートを複製すると、競合が発生する可能性があります。 その場合、Cookiecutter では、同じ名前の別のテンプレートで既存のテンプレートを上書きすることはできません。 他のテンプレートをインストールするには、先に既存のテンプレートを削除する必要があります。

### <a name="set-template-options"></a>テンプレート オプションの設定

テンプレートがローカルにインストールされると、Cookiecutter のオプション ページが表示され、Cookiecutter のファイルを生成する場所やその他のオプションを指定できます。

![Cookiecutter のオプション ページ](media/cookiecutter-template-options.png)

各 Cookiecutter テンプレートでは、独自のオプションのセットを定義し、各オプションの既定値 (各エントリ フィールドで推奨テキストとして表示される値) を指定します。 既定値はコード スニペットの場合もあります。これは主に、他のオプションを使用する動的な値である場合です。

各オプションの既定値はユーザー構成ファイルを使用してカスタマイズできます。 Cookiecutter 拡張機能はユーザー構成ファイルを検出すると、テンプレートの既定値をユーザー構成ファイルの既定値で上書きします。 この動作については、Cookiecutter ドキュメントの [User Config](https://cookiecutter.readthedocs.io/en/latest/advanced/user_config.html) に関するセクションで説明しています。

テンプレートでコード生成後に特定の Visual Studio タスクを実行するように指定した場合は、 **[Run additional tasks on completion (完了時に追加タスクを実行)]** オプションが表示されます。このオプションで、それらのタスクを実行しないように選択することもできます。 最も一般的なタスクの使用方法としては、Web ブラウザーを開く、エディターでファイルを開く、依存関係をインストールするなどがあります。

### <a name="create"></a>作成

オプションを設定したら、 **[作成]** を選択してコードを生成します (出力フォルダーが空ではない場合は警告が表示されます)。 テンプレートの出力に慣れていてファイルを上書きしても問題ない場合は、警告を無視してかまいません。 それ以外の場合は、 **[キャンセル]** を選択し、空のフォルダーを指定して、作成したファイルを空でない出力フォルダーに手動でコピーします。

ファイルが正常に作成されると、ファイルを**ソリューション エクスプローラー**で開くためのオプションが Cookiecutter に表示されます。

![ソリューション エクスプローラーのコマンドが表示された Cookiecutter](media/cookiecutter-files-created.png)

## <a name="cookiecutter-options"></a>Cookiecutter のオプション

Cookiecutter のオプションは、 **[ツール]**  >  **[オプション]**  >  **[Cookiecutter]** から表示できます。

![Cookiecutter のオプション](media/cookiecutter-tools-options.png)

| オプション | [説明] |
| --- | --- |
| **推奨されるフィード URL** | 推奨されるテンプレート フィードの場所です。 URL またはローカル ファイルへのパスを指定できます。 マイクロソフトによって選別された既定のフィードを使用する場合は、URL を空のままにします。 フィードでは、改行で区切られたテンプレートの場所の単純なリストが提供されます。 選別されたフィードの変更を要求するには、[GitHub 上のソース](https://github.com/Microsoft/PTVS/blob/master/Python/Product/Cookiecutter/CookiecutterFeed.txt)に対して pull request を行います。 |
| **ヘルプの表示** | Cookiecutter ウィンドウの上部にヘルプ情報のバーを表示するかどうかを指定します。 |

## <a name="optimize-cookiecutter-templates-for-visual-studio"></a>Visual Studio 向けの Cookiecutter テンプレートの最適化

Cookiecutter テンプレートの作成の基本については、[Cookiecutter のドキュメント](https://cookiecutter.readthedocs.io/en/latest/first_steps.html)をご覧ください。 Visual Studio の Cookiecutter 拡張機能は、Cookiecutter v1.4 用に作成されたテンプレートをサポートします。

テンプレート変数の既定のレンダリングは、データの型 (文字列またはリスト) によって異なります。

- 文字列: 変数名のラベル、値を入力するためのテキスト ボックス、既定値を表示するウォーターマーク。 テキスト ボックスのツールヒントには既定値が表示されます。
- リスト: 変数名のラベル、値を選択するためのコンボ ボックス。 コンボ ボックスのツールヒントには既定値が表示されます。

このレンダリングは、Visual Studio に固有の (Cookiecutter CLI では無視される) *cookiecutter.json* ファイルで追加のメタデータを指定することによって改善できます。 すべてのプロパティは省略可能です。

| プロパティ | [説明] |
| --- | --- |
| ラベル | エディターの上部に、変数名の代わりに変数に対して表示される内容を指定します。 |
| [説明] | 編集コントロールに、変数の既定値の代わりに表示されるツールヒントを指定します。 |
| URL | ラベルをハイパーリンクに変更し、URL を示したツールヒントとともに表示します。 ハイパーリンクを選択すると、ユーザーの既定のブラウザーでその URL が開きます。 |
| セレクター | 変数のエディターをカスタマイズできます。 現在、次のセレクターがサポートされています。<ul><li>`string`: 標準のテキスト ボックス (文字列の既定値)。</li><li>`list`: 標準のコンボ ボックス (リストの既定値)。</li><li>`yesno`: `y` と `n` のいずれかを選択するコンボ ボックス (文字列用)。</li><li>`odbcConnection`: データベース接続ダイアログを起動する **[...]** ボタンのあるテキスト ボックス。</li></ul> |

例:

```json
{
    "site_name": "web-app",
    "python_version": ["3.5.2", "2.7.12"],
    "use_azure": "y",

    "_visual_studio": {
        "site_name": {
            "label": "Site name",
            "description": "E.g. <site-name>.azurewebsites.net (can only contain alphanumeric characters and `-`)"
        },
        "python_version": {
            "label": "Python version",
            "description": "The version of Python to run the site on"
        },
        "use_azure" : {
            "label": "Use Azure",
            "description": "Include Azure deployment files",
            "selector": "yesno",
            "url": "https://azure.microsoft.com"
        }
    }
}
```

### <a name="run-visual-studio-tasks"></a>Visual Studio タスクの実行

Cookiecutter には、ファイルの生成後に任意の Python コードを実行できる *Post-Generate Hooks (生成後フック)* と呼ばれる機能があります。 この機能は柔軟ですが、Visual Studio への簡単なアクセスを許可しません。

たとえば、Visual Studio のエディターまたは Web ブラウザーでファイルを開くか、ユーザーに仮想環境を作成してパッケージの要件をインストールするように求める Visual Studio UI をトリガーする必要があるとします。

これらのシナリオを可能にするために、Visual Studio は、生成されたファイルをユーザーが**ソリューション エクスプローラー**で開いた後または既存のプロジェクトにファイルが追加された後に実行するコマンドについて説明した拡張メタデータを *cookiecutter.json* 内で探します。 (前述したように、ユーザーはテンプレート オプションの **[Run additional tasks on completion (完了時に追加タスクを実行)]** をオフにすることでタスクを実行しないよう選択できます)。

例:

```json
"_visual_studio_post_cmds": [
    {
        "name": "File.OpenFile",
        "args": "{{cookiecutter._output_folder_path}}\\readme.txt"
    },
    {
        "name": "Cookiecutter.ExternalWebBrowser",
        "args": "https://docs.microsoft.com"
    },
    {
        "name": "Python.InstallProjectRequirements",
        "args": "{{cookiecutter._output_folder_path}}\\dev-requirements.txt"
    }
]
```

コマンドは名前で指定し、Visual Studio のローカライズされたインストールで動作するように、ローカライズされていない (英語の) 名前を使用する必要があります。 Visual Studio の**コマンド** ウィンドウで、コマンド名のテストと検索を行うことができます。

1 つの引数を渡す場合は、前の例のように文字列として指定します。

引数を渡す必要がない場合は、空の文字列のままにするか、JSON から省略します。

```json
"_visual_studio_post_cmds": [
    {
        "name": "View.WebBrowser"
    }
]
```

複数の引数の場合は配列を使用します。 スイッチの場合には、正しく引用されるように、スイッチとその値を別の引数に分けます。 次に例を示します。

```json
"_visual_studio_post_cmds": [
    {
        "name": "File.OpenFile",
        "args": [
            "{{cookiecutter._output_folder_path}}\\read me.txt",
            "/e:",
            "Source Code (text) Editor"
        ]
    }
]
```

引数は他の Cookiecutter 変数を参照できます。 上の例では、生成されたファイルへの絶対パスを作成するために内部の `_output_folder_path` 変数が使用されています。

`Python.InstallProjectRequirements` コマンドは、既存のプロジェクトにファイルを追加する場合にのみ機能します。 **ソリューション エクスプローラー**の Python プロジェクトによって処理されますが、**ソリューション エクスプローラー** - **フォルダー ビュー**の表示中はメッセージを受け取るプロジェクトがないため、この制限が存在します。 今後のリリースでこの制限が解消され、**フォルダー ビュー**のサポート全般が改善される可能性があります。

## <a name="troubleshooting"></a>トラブルシューティング

### <a name="error-loading-template"></a>テンプレートの読み込みエラー

一部のテンプレートの *cookiecutter.json* 内で、ブール型などの無効なデータ型が使用されている場合があります。 このような場合は、[テンプレート情報] ウィンドウの **[問題]** リンクを選択してテンプレート作成者に報告してください。

### <a name="hook-script-failed"></a>フック スクリプトの失敗

一部のテンプレートで、Cookiecutter UI と互換性のない生成後スクリプトが使用されている場合があります。 たとえば、ユーザーに入力をクエリするスクリプトは、端末コンソールがないため失敗します。

### <a name="hook-script-not-supported-on-windows"></a>Windows でサポートされていないフック スクリプト

事後スクリプトが *.sh* の場合、ご使用の Windows コンピューター上のアプリケーションへの関連付けができない場合があります。 互換性のあるアプリケーションを Windows ストアで見つけるように求める Windows ダイアログが表示される可能性があります。

### <a name="templates-with-known-issues"></a>既知の問題があるテンプレート

複製エラー

- **wildfish/cookiecutter-django-crud** (サブフォルダー名に無効な文字 `|` が含まれている)
- **cookiecutter-pyvanguard** (サブフォルダー名に無効な文字 `|` が含まれている)

読み込みエラー

- **chrisdev/wagtail-cookiecutter-foundation** (*cookiecutter.json* でブール型を使用している)
- **quintoandar/cookiecutter-android** (テンプレート フォルダーが存在しない)

実行エラー

- **iknite/cookiecutter-ansible-role** (事後フック スクリプトにコンソール入力が必要)
- **benregn/cookiecutter-django-ansible** (Jinja エラー)

バッシュの使用 (致命的ではない)

- **openstack-dev/cookiecutter**
