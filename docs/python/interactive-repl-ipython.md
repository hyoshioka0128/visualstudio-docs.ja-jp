---
title: IPython REPL (対話型ウィンドウ)
description: Visual Studio の IPython モードの対話型ウィンドウは、対話型の並列コンピューティング機能を備えた使いやすい対話形式の開発環境です。
ms.date: 01/28/2019
ms.topic: conceptual
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: 8b4510ed738fdd2b33389ab4242dbde86cffff8c
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "62957742"
---
# <a name="use-ipython-in-the-interactive-window"></a>対話型ウィンドウで IPython を使用する

Visual Studio の IPython モードの**対話型**ウィンドウは、対話型の並列コンピューティング機能を備えた、高度でありながら使いやすい対話形式の開発環境です。 この記事では、Visual Studio の**対話型**ウィンドウで IPython を使用する手順について説明します。IPython でも、通常の[対話型ウィンドウ](python-interactive-repl-in-visual-studio.md)機能をすべて使用できます。

このチュートリアルでは、IPython と必要なライブラリが含まれている [Anaconda](https://www.continuum.io) 環境をインストールする必要があります。

> [!Note]
> **Interactive オプション** フォームで選択できるにもかかわらず、IronPython では IPython はサポートされていません。 詳細については、[機能要求](https://github.com/Microsoft/PTVS/issues/84)のページを参照してください。

1. Visual Studio を開き、**Python 環境**ウィンドウに切り替え ( **[表示]**  >  **[その他のウィンドウ]**  >  **[Python 環境]** の順に選択)、Anaconda 環境を選びます。

2. その環境の **[パッケージ (Conda)]** タブ (**pip** または**パッケージ** と表示される場合があります) を調べ、`ipython` と `matplotlib` が一覧表示されていることを確認します。 表示されていない場合は、それらをここでインストールします。 (「[[Python 環境] ウィンドウ タブ リファレンス](python-environments-window-tab-reference.md)」を参照)。

3. **[概要]** タブを選択し、 **[IPython 対話モードを使用する]** を選びます (Visual Studio 2015 では、 **[Configure interactive options]\(対話オプションの構成\)** を選択して **[オプション]** ダイアログを開き、 **[インタラクティブ モード]** を **IPython** に設定し、 **[OK]** を選びます)。

4. **[対話型ウィンドウを開く]** を選択して、**対話型**ウィンドウを IPython モードで表示します。 対話型モードを変更した場合、ウィンドウのリセットが必要な場合があります。>>> プロンプトのみが表示されている場合は、**In [2]** のようなプロンプトを取得するために、**Enter** キーも押す必要がある場合があります。

    ![Python モードの対話型ウィンドウ](media/ipython-repl-03.png)

5. 次のコードを入力します。

   ```python
   import matplotlib.pyplot as plt
   import numpy as np

   x = np.linspace(0, 5, 10)
   y = x ** 2
   plt.plot(x, y, 'r', x, x ** 3, 'g', x, x ** 4, 'b')
   ```

6. 最後の行を入力した後、インライン グラフが表示されます (必要であれば、右下隅をドラッグしてサイズを変更できます)。

    ![対話型ウィンドウのインライン グラフ](media/ipython-repl-04.png)

7. REPL で入力する代わりに、エディターでコードを記述し、それを選んで右クリックして、 **[Interactive に送信]** コマンドを選択する (または **Ctrl**+**Enter** キーを押す) ことができます。 以下のコードをエディターの新しいファイルに貼り付け、**Ctrl**+**A** キーを使って選択し、**対話型**ウィンドウに送信してみてください (中間のグラフや部分的なグラフが表示されないように、Visual Studio からはコードが 1 つの単位として送信されます。 また、別の環境で開いた Python オブジェクトを選択していない場合、 **[Python 環境]** ウィンドウの既定としてどの環境が選択されている場合でも、Visual Studio では**対話型**ウィンドウが開きます)。

    ```python
    from mpl_toolkits.mplot3d import Axes3D
    import matplotlib.pyplot as plt
    import numpy as np
    fig = plt.figure()
    ax = fig.add_subplot(111, projection='3d')
    for c, z in zip(['r', 'g', 'b', 'y'], [30, 20, 10, 0]):
        xs = np.arange(20)
        ys = np.random.rand(20)
        # You can provide either a single color or an array. To demonstrate this,
        # the first bar of each set is colored cyan.
        cs = [c] * len(xs)
        cs[0] = 'c'
        ax.bar(xs, ys, zs=z, zdir='y', color=cs, alpha=0.8)

    ax.set_xlabel('X')
    ax.set_ylabel('Y')
    ax.set_zlabel('Z')
    plt.show()
    ```

    ![エディターから対話型ウィンドウへのコードの送信](media/ipython-repl-05.png)

8. **対話型**ウィンドウ以外にグラフを表示するには、 **[デバッグ]**  >  **[デバッグなしで開始]** コマンドを使用してコードを実行します。

IPython には、システム シェルのエスケープ、変数の代入、出力のキャプチャなどの便利な機能が多数あります。詳細については、[IPython のドキュメント](https://ipython.org/documentation.html)を参照してください。

## <a name="see-also"></a>関連項目

- Jupyter をインストールせずに簡単に使用するには、無料の [Azure Notebooks ホスト サービス](https://notebooks.azure.com/)を試してください。ノートブックを保存し、他のユーザーと共有することができます。

- [Azure Data Science Virtual Machine](/azure/machine-learning/data-science-virtual-machine/overview) も、他のさまざまなデータ サイエンス ツールと共に Jupyter ノートブックを実行するように事前に構成されています。
