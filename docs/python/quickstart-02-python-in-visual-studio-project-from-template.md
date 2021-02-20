---
title: クイック スタート - テンプレートを使用して Python プロジェクトを作成する
description: このクイック スタートでは、基本的な Flask アプリ用の組み込みテンプレートを使用し、Python 向けの Visual Studio プロジェクトを作成します。
ms.date: 12/06/2018
ms.topic: quickstart
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: 81f337cf3feca517f46632e7fe08a9f5a62cd707
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99902455"
---
# <a name="quickstart-create-a-python-project-from-a-template-in-visual-studio"></a>クイック スタート: Visual Studio のテンプレートから Python プロジェクトを作成する

[Visual Studio に Python のサポートをインストール](installing-python-support-in-visual-studio.md)すると、さまざまなテンプレートを使用して新しい Python プロジェクトを簡単に作成できます。 このクイック スタートでは、テンプレートを利用し、簡単な Flask アプリを作成します。 結果的に生成されるプロジェクトは、「[クイック スタート - Flask での Web アプリの作成](../ide/quickstart-python.md)」で手動で作成するプロジェクトに似ています。

1. Visual Studio を起動します。

1. 一番上にあるメニュー バーから、**[ファイル]** > **[新規]** > **[プロジェクト]** の順に選択し、**[新しいプロジェクト]** ダイアログで "blank flask" を検索し、真ん中の一覧にある **Blank Flask Web Project** テンプレートを選択します。プロジェクトに名前を付け、**[OK]** を選択します。

    ![Blank Flask Web Project テンプレートで新しいプロジェクトを作成する](media/quickstart-python-06-blank-flask-template.png)

1. Visual Studio に **このプロジェクトには外部パッケージが必要です** というダイアログが表示されます。 このダイアログは、Flask に対する依存性を指定する *requirements.txt* ファイルがテンプレートに含まれているために表示されます。 Visual Studio では、パッケージを自動的にインストールできます。また、"*仮想環境*" へのインストールを選択できます。 仮想環境の利用はグローバル環境にインストールすることよりも推奨されます。**[Install into a virtual environment]\(仮想環境にインストールする\)** を選択して続行してください。

    ![仮想環境に Flask をインストールする](media/quickstart-python-07-install-into-virtual-environment.png)

1. Visual Studio に **[仮想環境の追加]** ダイアログが表示されます。 既定値をそのままにして **[作成]** を選択します。昇格要求があればそれに同意します。

    > [!Tip]
    > プロジェクトを開始するとき、すぐに仮想環境を作成することを強くお勧めします。ほとんどの Visual Studio テンプレートでそのように勧められます。 仮想環境では、時間の経過と共にライブラリを追加したり、削除したりしても、プロジェクトの厳密な要件が維持されます。 そのため、*requirements.txt* ファイルを簡単に生成できます。このファイルを利用し、(ソース管理を利用するとき) 他の開発コンピューターにそれらの依存関係を再インストールします。また、運用サーバーにプロジェクトを展開するときに再インストールします。 仮想環境とその長所については、「[仮想環境を使用する](../python/selecting-a-python-environment-for-a-project.md#use-virtual-environments)」と「[requirements.txt での必須パッケージの管理](../python/managing-required-packages-with-requirements-txt.md)」をご覧ください。

1. Visual Studio によってその環境が作成されたら、**ソリューション エクスプローラー** を調べて、*requirements.txt* と共に *app.py* ファイルが指定されていることを確認します。 *app.py* を開き、「[クイック スタート - Flask での Web アプリの作成](../ide/quickstart-python.md)」のものと似たコードがテンプレートによって指定されており、セクションがいくつか追加されていることを確認します。 以下に示すコードはすべてテンプレートで作成されるため、ユーザーが自分で *app.py* に貼り付ける必要はありません。

    コードは次のように必要なインポートで始まります。

    ```python
    from flask import Flask
    app = Flask(__name__)
    ```

    次の行は、アプリを Web ホストに展開するときに便利です。

    ```python
    wsgi_app = app.wsgi_app
    ```

    その後に、ビューを定義する単純な関数のルート デコレーターが続きます。

    ```python
    @app.route('/')
    def hello():
        """Renders a sample page."""
        return "Hello World!"
    ```

    最後に、以下のスタートアップ コードが示され、ハードコーディングするのではなく、環境変数によってホストとポートを設定できます。 このようなコードによって、コードを変更することなく、開発コンピューターと運用コンピューターの両方で構成を簡単に制御できます。

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

1. **[デバッグ]** > **[デバッグなしで開始]** を選択し、アプリを実行してブラウザーで `localhost:5555` を開きます。

**質問:Visual Studio には他にどのような Python テンプレートがありますか。**

**回答:** Python ワークロードをインストールすると、Visual Studio にはさまざまなプロジェクト テンプレートが用意されます。[Flask、Bottle、Django Web フレームワーク](../python/python-web-application-project-templates.md)、Azure クラウド サービス、さまざまな機械学習シナリオのためのテンプレートなどがあります。Python アプリを含む既存のフォルダー構造からプロジェクトを作成するテンプレートまであります。 テンプレートには、**Python** 言語ノードとその子ノードを選択することで、**[ファイル]** > **[新規]** > **[プロジェクト]** ダイアログからアクセスできます。

Visual Studio は、Python クラス、Python パッケージ、Python 単体テスト、*web.config* ファイルなどを簡単に作成するためのさまざまなファイルや "*項目テンプレート*" も備えています。 Python プロジェクトを開いているとき、**[プロジェクト]** > **[新しい項目の追加]** メニュー コマンドから項目テンプレートにアクセスできます。 [項目テンプレート](python-item-templates.md)のリファレンスを参照してください。

プロジェクトを開始するときやファイルを作成するとき、テンプレートを使用すると時間が大幅に節約されます。さまざまなアプリの種類やコードの構造について学習するための優れた方法でもあります。 さまざまなテンプレートからプロジェクトや項目を数分で作成できるということは、そのように作成したものでできることを知る上で便利なことです。

**質問:Cookiecutter テンプレートも使用できますか。**

**回答**:はい。 実際のところ、Visual Studio は Cookiecutter と直接統合できます。これについては、「[クイック スタート:Cookiecutter テンプレートからプロジェクトを作成する](../python/quickstart-04-python-in-visual-studio-project-from-cookiecutter.md)」で学習できます。

## <a name="next-steps"></a>次の手順

> [!div class="nextstepaction"]
> [チュートリアル: Visual Studio での Python の使用](tutorial-working-with-python-in-visual-studio-step-01-create-project.md)

## <a name="see-also"></a>関連項目

- [既存の Python インタープリターを手動で識別する](managing-python-environments-in-visual-studio.md#manually-identify-an-existing-environment)
- [Visual Studio 2015 以前の Python サポートをインストールする](installing-python-support-in-visual-studio.md)
- [インストールする場所](installing-python-support-in-visual-studio.md#install-locations)
