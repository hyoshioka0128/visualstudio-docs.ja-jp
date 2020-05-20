---
title: Python コードの単体テスト
description: Visual Studio で Python コードの単体テストを設定し、テスト エクスプローラーの機能を最大限に活用してテストを検出、実行、デバッグします。
ms.date: 09/18/2019
ms.topic: include
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: 9843b47e38d5d33a25c455efe619dfcc033fb334
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "71933458"
---
## <a name="discover-and-view-tests"></a>テストを探索して表示する

規則により、Visual Studio はテストをその名前が `test` で始まるメソッドとして識別します。 この動作を確認するには、次の操作を行います。

1. Visual Studio に読み込まれた [Python プロジェクト](../../managing-python-projects-in-visual-studio.md)を開き、プロジェクトを右クリックして **[追加]**  >  **[新しい項目]** を選択し、 **[Python Unit Test (Python 単体テスト)]** に続けて **[追加]** を選択します。

1. このアクションにより、標準 `unittest` モジュールをインポートし、`unittest.TestCase` からテスト クラスを派生させ、スクリプトを直接実行する場合に `unittest.main()` を起動するコードを含む *test1.py* ファイルが作成されます。

    ```python

    import unittest

    class Test_test1(unittest.TestCase):
        def test_A(self):
            self.fail("Not implemented")

    if __name__ == '__main__':
        unittest.main()
    ```

1. 必要に応じてファイルを保存し、**[テスト]** > **[Windows]** > **[テスト エクスプローラー]** メニュー コマンドで**テスト エクスプローラー**を開きます。

1. **テスト エクスプローラー**は、テストするプロジェクトを検索し、それらを次のように表示します。 テストをダブルクリックすると、そのソース ファイルが開きます。

    ![既定の test_A を表示しているテスト エクスプローラー](../../media/unit-test-A.png)

1. 他のテストをプロジェクトに追加すると、ツール バーの**グループ化**メニューを使用して**テスト エクスプローラー**のビューを整理できます。

    ![テスト エクスプローラーのグループ化ツール バー メニュー](../../media/unit-test-group-menu.png)

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

デバッグを開始するには、コードに最初のブレークポイントを設定し、**テスト エクスプローラー**でテスト (または選択範囲) を右クリックし、 **[選択したテストのデバッグ]** を選択します。 アプリケーション コードの場合と同様に、Visual Studio が Python デバッガーを起動します。

![テストのデバッグ](../../media/unit-test-debugging.png)

**[選択されたテストのコード カバレッジの分析]** を使用することもできます。 詳細については、「[コード カバレッジを使用した、テストされるコード割合の確認](../../../test/using-code-coverage-to-determine-how-much-code-is-being-tested.md)」を参照してください。

### <a name="known-issues"></a>既知の問題

- デバッグを開始するときに、Visual Studio がデバッグを起動して停止してからもう一度開始するように見えます。 この動作は想定内です。
- 複数のテストをデバッグするときに、それぞれが個別に実行され、デバッグ セッションが中断されます。
- Visual Studio で、デバッグ時にテストの開始が断続的に失敗します。 通常は、もう一度テストをデバッグしようとすると成功します。
- デバッグ時に、テストを `unittest` 実装にステップ アウトできます。 通常は、次のステップはプログラムの最後まで実行されてデバッグを停止します。
