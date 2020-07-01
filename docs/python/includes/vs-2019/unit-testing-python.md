---
title: Python コードの単体テスト
description: Visual Studio で Python コードの単体テストを設定し、テスト エクスプローラーの機能を最大限に活用してテストを検出、実行、デバッグします。
ms.date: 09/18/2019
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: 6b611657db104a4b74e784df8925627ff41f3c33
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85535333"
---
## <a name="select-the-test-framework-for-a-python-project"></a>Python プロジェクトのテスト フレームワークを選択する

Visual Studio では、Python 用に [unittest](https://docs.python.org/3/library/unittest.html) および [pytest](https://pytest.org/en/latest/) の 2 つのテスト フレームワークがサポートされています (Visual Studio 2019 バージョン 16.3 以降で利用可能)。 既定では、Python プロジェクトを作成するときにフレームワークは選択されません。 フレームワークを指定するには、ソリューション エクスプローラーでプロジェクト名を右クリックし、 **[プロパティ]** オプションを選択します。 プロジェクト デザイナーが開き、 **[テスト]** タブでテストを構成できます。このタブでは、プロジェクトに使用するテスト フレームワークを選択できます。 

* **unittest** フレームワークでは、プロジェクトのルート ディレクトリがテスト検出に使用されます。 この場所と、テストを識別するためのテキスト パターンは、 **[テスト]** タブで、ユーザーが指定した値に変更できます。
* **pytest** フレームワークでは、テストの場所やファイル名のパターンなどのテスト オプションは、標準の pytest .ini 構成ファイルを使用して指定します。 詳細については、[pytest のリファレンス ドキュメント](https://docs.pytest.org/en/latest/reference.html#ini-options-ref)をご覧ください。

フレームワークの選択と設定を保存すると、テスト エクスプローラーでテスト検出が開始されます。 [テスト エクスプローラー] ウィンドウがまだ開いていない場合は、ツール バーに移動して、 **[テスト]**  >  **[テスト エクスプローラー]** を選択します。

## <a name="configure-testing-for-python-without-a-project"></a>プロジェクトを使用せずに Python のテストを構成する
Visual Studio では、Python コードがある [フォルダーを開く](../../quickstart-05-python-visual-studio-open-folder.md)と、プロジェクトを使用せずに既存の Python コードを実行してテストすることができます。 このような場合は、**PythonSettings.json** ファイルを使用して、テストを構成する必要があります。 
1. **[ローカル フォルダーを開く]** オプションを使用して、既存の Python コードを開きます。 

   ![Visual Studio のスタートアップ画面](../../media/quickstart-open-folder/01-open-local-folder.png)

1. [ソリューション エクスプローラー] ウィンドウで、 **[すべてのファイルを表示]** アイコンをクリックして、現在のフォルダー内のすべてのファイルを表示します。

   ![[すべてのファイルを表示] ボタン](../../media/unit-test-show-files.png)

1. **ローカル設定**フォルダー内の **PythonSettings.json** ファイルに移動します。 このファイルが **ローカル設定**フォルダーに表示されない場合は、手動で作成します。
   
1. フィールド **TestFramework** を設定ファイルに追加し、使用するテスト フレームワークに応じて、**pytest** または **unittest** に設定します。

    ```json
    {
    "TestFramework": "unittest",
    "UnitTestRootDirectory": "testing",
    "UnitTestPattern": "test_*.py"
    }
    ```

    > [!Note]
    > **unittest** フレームワークの場合、フィールド **UnitTestRootDirectory** および **UnitTestPattern** が PythonSettings.json ファイルに指定されていないと、これらのフィールドは追加され、それぞれ既定値の "." と "test*.py" が割り当てられます。

1. テストが含まれるフォルダーとは別の **src** ディレクトリがフォルダーに含まれる場合は、**PythonSettings.json** ファイルの **SearchPaths** フィールドを使用して **src** フォルダーへのパスを指定します。

    ```json
    {
    "TestFramework": "unittest",
    "UnitTestRootDirectory": "testing",
    "UnitTestPattern": "test_*.py",
    "SearchPaths": [ ".\\src"]
    }
    ```

1. 変更内容を PythonSettings.json ファイルに保存して、指定されたフレームワークのテスト検出を開始します。 
   > [!Note]
   > [テスト エクスプローラー] ウィンドウが既に開いている場合は、**Ctrl** + **R、A** でも検出がトリガーされます。

## <a name="discover-and-view-tests"></a>テストを探索して表示する

既定では、Visual Studio では、**unittest** および **pytest** テストが、名前が `test` で始まるメソッドとして識別されます。 テスト検出を表示するには、次の手順を行います。

1. [Python プロジェクト](../../managing-python-projects-in-visual-studio.md)を開きます。

1. プロジェクトが Visual Studio に読み込まれたら、[ソリューション エクスプローラー] でプロジェクトを右クリックし、プロパティ **[テスト]** タブで **unittest** または **pytest** フレームワークを選択します。
   > [!Note]
   > pytest フレームワークを使用する場合、標準の pytest .ini 構成ファイルを使用して、テストの場所とファイル名のパターンを指定できます。 既定では、ワークスペース/プロジェクト フォルダーが使用され、パターンは `test_*py` および `*_test.py` です。 詳細については、[pytest のリファレンス ドキュメント](https://docs.pytest.org/en/latest/reference.html#ini-options-ref)をご覧ください。

1. フレームワークを選択したら、プロジェクトをもう一度右クリックし、 **[追加]**  >  **[新しい項目]** を選択してから、 **[Python 単体テスト]** に続けて **[追加]** を選択します。

1. このアクションにより、標準 `unittest` モジュールをインポートし、`unittest.TestCase` からテスト クラスを派生させ、スクリプトを直接実行する場合に `unittest.main()` を起動するコードを含む *test_1.py* ファイルが作成されます。

    ```python
    import unittest

    class Test_test1(unittest.TestCase):
        def test_A(self):
            self.fail("Not implemented")

    if __name__ == '__main__':
        unittest.main()
    ```

1. 必要に応じてファイルを保存し、 **[テスト]**  >  **[テスト エクスプローラー]** メニュー コマンドで**テスト エクスプローラー**を開きます。

1. **テスト エクスプローラー**は、テストするプロジェクトを検索し、それらを次のように表示します。 テストをダブルクリックすると、そのソース ファイルが開きます。

    ![既定の test_A を表示しているテスト エクスプローラー](../../media/unit-test-a-2.png) 

1. 他のテストをプロジェクトに追加すると、ツール バーの **[グループ化]** メニューを使用して**テスト エクスプローラー**のビューを整理できます。

    ![テスト エクスプローラーのグループ化ツール バー メニュー](../../media/unit-test-group-menu-2.png) 

1. **検索**フィールドにテキストを入力してテストを名前でフィルター処理することもできます。

`unittest` モジュールとテストの記述の詳細については、[Python 2.7 ドキュメント](https://docs.python.org/2/library/unittest.html)または [Python 3.7 ドキュメント](https://docs.python.org/3/library/unittest.html) (python.org) をご覧ください。

## <a name="run-tests"></a>テストの実行

**テスト エクスプローラー**では、さまざまな方法でテストを実行できます。

- **[Run All (すべて実行)]** は、表示されているすべてのテスト (フィルターの対象) を明確に実行します。
- **[実行]** メニューには、失敗、合格、または未実行のテストをグループとして実行するコマンドが用意されています。
- 1 つ以上のテストを選んで右クリックし、 **[選択したテストの実行]** を選択します。

テストはバックグラウンドで実行され、完了すると**テスト エクスプローラー**が各テストの状態を更新します。

- 合格したテストには、緑のチェックマークとテストの実行にかかった時間が表示されます。

    ![test_A の合格状態](../../media/unit-test-A-pass.png)

- 失敗したテストには、コンソール出力とテストの実行からの `unittest` 出力を示す **[出力]** リンクとともに赤い × 印が表示されます。

    ![test_A の失敗状態](../../media/unit-test-A-fail.png)

    ![test_A の失敗とその理由](../../media/unit-test-A-fail-reason.png)

## <a name="debug-tests"></a>テストのデバッグ

単体テストはコードの断片であるため、他のコードと同様にバグが発生することがあり、デバッガーでの実行が必要になることがあります。 デバッガーでは、ブレークポイントを設定し、変数を確認し、コードをステップ実行することができます。 Visual Studio には単体テストのための診断ツールも用意されています。

> [!Note]
> 既定では、テスト デバッグでは、Visual Studio 2017 (バージョン 15.8 以降) 用の ptvsd 4 デバッガーと Visual Studio 2019 (バージョン 16.5 以降) 用の debugpy が使用されます。 ptvsd 3 を代わりに使用する場合は、 **[ツール]**  >  **[オプション]**  >  **[Python]**  >  **[デバッグ]** で、 **[レガシ デバッガーを使用]** オプションを選択できます。 

デバッグを開始するには、コードに最初のブレークポイントを設定し、**テスト エクスプローラー**でテスト (または選択範囲) を右クリックし、 **[選択したテストのデバッグ]** を選択します。 アプリケーション コードの場合と同様に、Visual Studio が Python デバッガーを起動します。

![テストのデバッグ](../../media/unit-test-debugging.png)

**[選択されたテストのコード カバレッジの分析]** を使用することもできます。 詳細については、「[コード カバレッジを使用した、テストされるコード割合の確認](../../../test/using-code-coverage-to-determine-how-much-code-is-being-tested.md)」を参照してください。
