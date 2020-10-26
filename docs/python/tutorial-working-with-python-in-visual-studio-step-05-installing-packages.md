---
title: Visual Studio での Python チュートリアル、手順 5、パッケージのインストール
titleSuffix: ''
description: Visual Studio での Python 機能の中核となるチュートリアルの手順 5 では、Python 環境でパッケージを管理するための Visual Studio の機能について説明します。
ms.date: 03/09/2020
ms.topic: tutorial
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: 32e85f39c4acf9466def24bcfea59bbfd6807a1b
ms.sourcegitcommit: a801ca3269274ce1de4f6b2c3f40b58bbaa3f460
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/25/2020
ms.locfileid: "88801660"
---
# <a name="step-5-install-packages-in-your-python-environment"></a>手順 5: Python 環境へのパッケージのインストール

**前の手順:[デバッガーでコードを実行する](tutorial-working-with-python-in-visual-studio-step-04-debugging.md)**

Python 開発者コミュニティは、ユーザーが独自のプロジェクトに組み込むことのできる便利なパッケージを何千も作成してきました。 Visual Studio には、Python 環境内のパッケージを管理するための UI が用意されています。

## <a name="view-environments"></a>環境の表示

1. **[表示]**  >  **[その他のウィンドウ]**  >  **[Python 環境]** メニュー コマンドを選びます。 **ソリューション エクスプローラー**へのピアとして **[Python 環境]** ウィンドウが開き、利用可能なさまざまな環境が示されます。 この一覧には、Visual Studio インストーラーを使用してインストールした環境と、個別にインストールした環境の両方が表示されます。 これには、グローバル環境、仮想環境、および Conda 環境が含まれます。 太字で示されている環境は、新しいプロジェクトに使用される既定の環境です。 環境の使用方法の詳細については、[Visual Studio 環境で Python 環境を作成および管理する方法](managing-python-environments-in-visual-studio.md)に関する記事をご覧ください。

   ![[Python Environments (Python 環境)] ウィンドウ](media/environments/environments-default-view-2019.png)

   > [!NOTE]
   > [ソリューション エクスプローラー] ウィンドウを選択し、**Ctrl + K、Ctrl + `** キーボード ショートカットを使用して [Python 環境] ウィンドウを開くこともできます。 ショートカットが機能せず、メニューに [Python 環境] ウィンドウが見つからない場合は、Python ワークロードをインストールしていない可能性があります。 Python をインストールする方法については、[Visual Studio に Python サポートをインストールする方法](installing-python-support-in-visual-studio.md)に関する記事をご覧ください。

2. 環境の **[概要]** タブからは、環境の**対話型**ウィンドウと、環境のインストール フォルダーおよびインタープリターにすばやくアクセスできます。 たとえば、 **[対話型ウィンドウを開く]** を選択すると、その特定の環境の**対話型**ウィンドウが Visual Studio で表示されます。

3. 次に、 **[ファイル]**  >  **[新規]**  >  **[プロジェクト]** で、 **[Python アプリケーション]** テンプレートを選択して新しいプロジェクトを作成します。 表示されるコード ファイルに、次のコードを貼り付けます。これにより、前のチュートリアルの手順のように余弦波が作成されますが、今回はグラフィカルにプロットされるだけです。 または、前に作成したプロジェクトを使用して、そのコードを置き換えることもできます。

    ```python
    from math import radians
    import numpy as np     # installed with matplotlib
    import matplotlib.pyplot as plt

    def main():
        x = np.arange(0, radians(1800), radians(12))
        plt.plot(x, np.cos(x), 'b')
        plt.show()

    main()
    ```

4. Python プロジェクトを開いた状態で、ソリューション エクスプローラーから [Python 環境] ウィンドウを開くこともできます。それには、 **[Python 環境]** を右クリックし、 **[すべての Python 環境の表示]** を選択します

   ![環境](media/environments/environments-view-all-2019.png)

5. エディター ウィンドウでは、インポート ステートメント `numpy` と `matplotlib` にマウス ポインターを合わせると、それらが解決されていないことがわかります。 これは、そのパッケージが既定のグローバル環境にインストールされていないためです。

   ![未解決のパッケージ インポート](media/packages-unresolved-import.png)

## <a name="install-packages-using-the-python-environments-window"></a>[Python 環境] ウィンドウを使用したパッケージのインストール

1. [Python 環境] ウィンドウから、新しい Python プロジェクト用の既定の環境を選択し、 **[パッケージ]** タブを選択します。そうすると、現在環境にインストールされているパッケージの一覧が表示されます。

   ![環境にインストールされているパッケージ](media/environments/environments-installed-packages-2019.png)

2. `matplotlib` をインストールするには、検索フィールドにその名前を入力して、 **[次のコマンドを実行する: pip install matplotlib]** オプションを選択します。 これによって、`matplotlib` とそのすべての依存パッケージ (この場合は `numpy` が含まれます) がインストールされます。

   ![環境に matplotlib をインストールする](media/environments/environments-add-matplotlib-2019.png)

5. 昇格に同意するように求められた場合は、同意します。

6. パッケージがインストールされると、 **[Python 環境]** ウィンドウにそのパッケージが表示されます。 アンインストールするには、パッケージの右にある **[X]** 選択します。

   ![環境での matplotlib のインストール完了](media/environments/environments-add-matplotlib2-2019.png)

   > [!NOTE]
   > 環境の下に小さい進行状況バーが表示され、Visual Studio が新しくインストールしたパッケージに対して、IntelliSense データベースを構築していることが示される場合があります。 **[IntelliSense]** タブにはより詳細な情報も表示されます。 そのデータベースが完了するまで、エディターではそのパッケージのオートコンプリートや構文チェックなどの IntelliSense 機能がアクティブにならないことに注意してください。
   >
   > Visual Studio 2017 バージョン 15.6 以降では、高速で IntelliSense を操作する異なった方法が使用されています。その効果に関するメッセージが **[IntelliSense]** タブに表示されます。

## <a name="run-the-program"></a>プログラムを実行する

1. これで [matplotlib](https://matplotlib.org/) がインストールされたので、プログラムをデバッガーと共に実行 (**F5** キー) するか、デバッガーなしで実行 (**Ctrl** + **F5** キー) して、出力を確認します。

   ![matplotlib の出力例](media/environments/environments-add-matplotlib3.png)

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [Git の操作](tutorial-working-with-python-in-visual-studio-step-06-working-with-git.md)

## <a name="go-deeper"></a>詳しい説明

- [Python 環境](managing-python-environments-in-visual-studio.md)
- [Visual Studio での Django の詳細情報](learn-django-in-visual-studio-step-01-project-and-solution.md)
- [Visual Studio での Flask の詳細情報](learn-flask-visual-studio-step-01-project-solution.md)
