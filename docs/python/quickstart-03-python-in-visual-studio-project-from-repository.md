---
title: クイック スタート - Python コードのリポジトリをクローンする
description: このクイック スタートでは、Visual Studio チーム エクスプローラーを使用して Python Koans リポジトリをクローンすることで、Visual Studio で Python プロジェクトを作成します。
ms.date: 12/06/2018
ms.topic: quickstart
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: 55db74b2b2882aac12ac1587c4e972e31f7dfe10
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99902402"
---
# <a name="quickstart-clone-a-repository-of-python-code-in-visual-studio"></a>クイック スタート: Visual Studio で Python コードのリポジトリをクローンする

[Visual Studio に Python サポートをインストール](installing-python-support-in-visual-studio.md)すると、Visual Studio 向け GitHub 拡張を追加することができます。 この拡張機能を使用すると、Python コードのリポジトリを簡単にクローンし、これを使用して IDE 内からプロジェクトを作成することができます。 コマンドラインでも常にリポジトリをクローンして、それを Visual Studio で使用することができます。

## <a name="install-the-github-extension-for-visual-studio"></a>Visual Studio 用の GitHub 拡張機能のインストール

[!INCLUDE[install-github-extension](includes/install-github-extension.md)]

## <a name="work-with-github-in-visual-studio"></a>Visual Studio での GitHub の使用

1. Visual Studio を起動します。

1. **[表示]**  >  **[チーム エクスプローラー]** の順に選択し、 **[チーム エクスプローラー]** ウィンドウを開きます。ここでは、GitHub または Azure Repos に接続したり、リポジトリをクローンしたりできます。 (次に示す **[接続]** ページが表示されない場合は、上部ツールバーのプラグ アイコンを選択すると、そのページに進みます)。

    ![Azure Repos、GitHub、リポジトリのクローンを示すチーム エクスプローラー ウィンドウ](media/team-explorer.png)

1. **[ローカル Git リポジトリ]** で **[クローン]** コマンドを選択し、[URL] フィールドに「`https://github.com/gregmalcolm/python_koans`」と入力し、クローン元のファイルが格納されているフォルダーを入力し、 **[クローン]** ボタンを選択します。

    > [!Tip]
    > **チーム エクスプローラー** で指定するフォルダーは、クローンされたファイルを受け取るフォルダーです。 `git clone` コマンドとは異なり、**チーム エクスプローラー**でクローンを作成しても、リポジトリの名前のサブフォルダーは自動作成されません。

1. クローンが完了すると、リポジトリ名が **[ローカル Git リポジトリ]** の一覧に表示されます。 その名前をダブルクリックして、**チーム エクスプローラー**のリポジトリ ダッシュボードに移動します。

1. **[ソリューション]** の下で **[新規作成]** を選択します。

    ![[チーム エクスプローラー] ウィンドウ、クローンからの新しいプロジェクトの作成](media/team-explorer-new-project.png)

1. 表示された **[新しいプロジェクト]** ダイアログで、**Python** 言語に移動 (または "Python" を検索) し、 **[既存の Python コードから]** を選択し、プロジェクトの名前を指定し、 **[場所]** をリポジトリと同じフォルダーに設定し、 **[OK]** を選択します。 表示されたウィザードで、 **[完了]** を選択します。

1. メニューから **[表示]**  >  **[ソリューション エクスプローラー]** を選択します。

1. **ソリューション エクスプローラー** で **python3** ノードを展開し、**contemplate_koans.py** を右クリックし、 **[スタートアップ ファイルとして設定]** を選択します。 この手順により、プロジェクトの実行時に使用されるファイルが Visual Studio に指示されます。

1. メニューで **[プロジェクト]**  >  **[Koans プロパティ]** の順に選択し、 **[全般]** タブを選択し、 **[作業ディレクトリ]** を "python3" に設定します。 この手順が必要なのは、Visual Studio は既定では作業ディレクトリをスタートアップ ファイルの場所ではなく、プロジェクトのルートに設定するためです (*python3\contemplate_koans.py*。これはプロジェクトのプロパティでも確認できます)。 プログラム コードは、ファイル *koans.txt* を作業フォルダーから探すので、この値を変更しなくてもランタイム エラーは発生します。

    ![Python プロジェクトの作業ディレクトリの設定](media/projects-set-working-directory.png)

1. **Ctrl**+**F5** キーを押すか、 **[デバッグ]**  >  **[デバッグなしで開始]** の順に選択し、プログラムを実行します。 *koans.txt* の **FileNotFoundError** が表示される場合、前の手順の説明に従って作業ディレクトリの設定を再確認します。

1. プログラムが正常に実行されると、*python3/koans/about_asserts.py* の 17 行にアサーション エラーが表示されます。 これが意図的です。ユーザーが意図的なエラーをすべて修正することにより、プログラムでは、Python にそれが通知されるよう設計されています。 (詳細は、Python Koans にインスピレーションを与えた [Ruby Koans](https://rubykoans.com/) を参照してください。)

    ![Python Koans プログラムからの最初の出力](media/koans-output.png)

1. **ソリューション エクスプローラー** で *python3/koans/about_asserts.py* に移動してこれを開き、ファイルをダブルクリックします。 エディターには既定で行番号が表示されないことに注意してください。 これを変更するには、 **[ツール]**  >  **[オプション]** を選択し、ダイアログの下部の **[すべての設定を表示]** を選択し、 **[テキスト エディター]**  >  **[Python]**  >  **[全般]** に移動し、 **[行番号]** を選択します。

    ![Python ファイルの行番号の有効化](media/options-general-line-numbers.png)

1. 17 行の `False` 引数を `True` に変更することで、エラーを修正できます。 行を次のようにします。

    ```python
    self.assertTrue(True) # This should be True
    ```

1. 再びプログラムを実行します。 Visual Studio でエラーに関する警告が表示された場合は、 **[はい]** と応答して、コードの実行を続行します。 最初のチェックに合格し、プログラムが次の koan で停止することを確認します。 エラーの修正を続け、必要に応じてプログラムを再実行します。

> [!Important]
> このクイックスタートでは、GitHub の *python_koans* リポジトリのクローンを直接作成しました。 このようなリポジトリは、直接変更できないように作成者によって保護されているため、そのリポジトリに変更をコミットしようとすると失敗します。 実際には、開発者は、自分の GitHub アカウントにこのようなリポジトリをフォークした後、pull requests を作成して元のリポジトリにそれらの変更を送信します。 独自のフォークがある場合は、前に使用されていた元のリポジトリの URL の代わりにその URL を使用します。

## <a name="next-steps"></a>次の手順

> [!div class="nextstepaction"]
> [チュートリアル: Visual Studio での Python の使用](tutorial-working-with-python-in-visual-studio-step-01-create-project.md)

## <a name="see-also"></a>関連項目

- [既存の Python インタープリターを手動で識別する](managing-python-environments-in-visual-studio.md#manually-identify-an-existing-environment)
- [Windows の Visual Studio に Python サポートをインストールする方法](installing-python-support-in-visual-studio.md)
- [インストールする場所](installing-python-support-in-visual-studio.md#install-locations)
