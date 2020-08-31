---
title: R の概要のチュートリアル
description: プロジェクトの作成、対話型ウィンドウ、コード編集、デバッグなど、Visual Studio での R の使用に関するチュートリアルです。
ms.date: 06/29/2017
ms.topic: tutorial
author: kraigb
ms.author: kraigb
manager: jillfra
ms.workload:
- data-science
ms.openlocfilehash: be0ba7b32af5247bb0dccccb68d900cb6797cc13
ms.sourcegitcommit: a801ca3269274ce1de4f6b2c3f40b58bbaa3f460
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/25/2020
ms.locfileid: "88801179"
---
# <a name="get-started-with-r-tools-for-visual-studio"></a>R Tools for Visual Studio の概要

R Tools for Visual Studio (RTVS) をインストールすると ([インストール](installing-r-tools-for-visual-studio.md)に関するページを参照してください)、ツールが提供するエクスペリエンスをすばやく確認できます。

## <a name="create-an-r-project"></a>R プロジェクトの作成

1. Visual Studio を開きます。
1. **[ファイル]**、**[新規作成]**、**[プロジェクト]** の順に選択します (**Ctrl**+**Shift**+**N**)。
1. **[テンプレート]** の **[R]** から "R Project" を選択し、プロジェクトに名前と場所を指定し、**[OK]** を選択します。

   ![Visual Studio 内の R (VS2017 の RTVS) の [新しいプロジェクト] ダイアログ ボックス](media/getting-started-01-new-project.png)

1. プロジェクトを作成すると、次のウィンドウが表示されます。

    - 右側には、Visual Studio ソリューション エクスプローラーがあり、ここには含まれる*ソリューション*内にプロジェクトが表示されます。 (ソリューションには、複数のさまざまな種類のプロジェクトを含めることができます。詳細については、[プロジェクト](r-projects-in-visual-studio.md)に関するページを参照してください。)
    - 左上には、新しい R ファイル (`script.R`) があり、ここでは、すべての Visual Studio の編集機能を使ってソース コードを編集することができます。
    - 左下には、 **[R インタラクティブ]** ウィンドウがあり、ここでは対話型でコードを開発およびテストすることができます。

> [!Note]
> プロジェクトを開かずに、別のプロジェクトの種類を読み込む場合にも、 **[R インタラクティブ]** ウィンドウを使用できます。 **[R Tools]**、**[Windows]**、**[R インタラクティブ]** の順に選択してください。

## <a name="explore-the-interactive-window-and-intellisense"></a>対話型ウィドウと IntelliSense の調査

1. 「`3 + 4`」と入力して **Enter** キーを押し、結果を表示して、対話型ウィンドウが動作していることをテストします。

    ![Visual Studio 2017 (VS2017) の R 対話型ウィンドウ](media/getting-started-02-interactive1.png)

1. 少し複雑な「`ds <- c(1.5, 6.7, 8.9) * 1:12`」を入力してから、「`ds`」を入力して結果を表示します。

    ![その他の Visual Studio の R 対話型の例](media/getting-started-03-interactive2.png)

1. 「`mean(ds)`」と入力しますが、「`m`」や「`me`」と入力すると、すぐに Visual Studio IntelliSense でオート コンプリートの候補が表示されます。 リストから目的のオート コンプリートを選択したら、**Tab** キーを押して挿入します。方向キーやマウスで選択を変更することができます。

    ![コードの入力時に表示される IntelliSense](media/getting-started-04-intellisense1.png)

1. `mean` が完成したら、先頭のかっこ「`(`」を入力すると、IntelliSense で関数に対するインライン ヘルプが示されることを確認できます。

    ![IntelliSense が示す関数のヘルプ](media/getting-started-05-intellisense2.png)

1. 行 `mean(ds)` を完成させ、Enter キーを押すと、結果が表示されます (`[1] 39.51667`)。

1. 対話型ウィンドウはヘルプと統合されているため、たとえば、「`?mean`」と入力すると、Visual Studio の **[R ヘルプ]** ウィンドウにその関数のヘルプが表示されます。 詳細については、「[R Tools for Visual Studio のヘルプ](getting-started-help.md)」を参照してください。

    ![Visual Studio の [R ヘルプ] ウィンドウ](media/getting-started-06-help.png)

1. 一部のコマンド (`plot(1:100)` など) では、出力が対話型ウィンドウに直接表示できない場合、Visual Studio 内に新しいウィンドウが開かれます。

    ![Visual Studio でのプロットの表示](media/getting-started-07-plot-window.png)

対話型ウィンドウでは、履歴の確認、ワークスペースの読み込みと保存、デバッガーへのアタッチを行ったり、コピー/貼り付けを使用せずにソース コード ファイルを操作したりすることができます。 詳細については、「[Working with the R Interactive Window](interactive-repl-for-r-in-visual-studio.md)」 (対話型ウィンドウでの作業) を参照してください。

## <a name="experience-code-editing-features"></a>コード編集機能の体験

対話型ウィンドウでの簡単な作業例では、コード エディターでも動作する IntelliSense などの基本的な編集機能を紹介しました。 以前と同じコードを入力すると、同じオート コンプリートおよび IntelliSense のメッセージ画面が表示されますが、出力は行われません。

*.R* ファイルにコードを記述すると、すぐにすべてのコードが表示され、簡単に小さな変更を行い、対話型ウィンドウでコードをすばやく実行して結果を表示できます。 また、プロジェクトに必要なだけファイルを含めることもできます。 コードがファイル内にある場合は、デバッガーでステップごとに実行することもできます (この記事で後述します)。 これらの機能は、計算アルゴリズムを開発して、1 つ以上のデータセットを操作するためにコードを記述する場合、特にすべての中間結果を確認する必要がある場合に、非常に役立ちます。

例のように、次のステップでは、「[Central Limit Theorem](https://en.wikipedia.org/wiki/Central_limit_theorem)」 (中心極限定理) (Wikipedia) を調査する小さなコードを作成します。 (この例は、Paul Teetor による *R クックブック*から編集されています。)

1. `script.R` エディターで、次のコードを入力します。

    ```R
    mu <- 50
    stddev <- 1
    N <- 10000
    pop <- rnorm(N, mean = mu, sd = stddev)
    plot(density(pop), main = "Population Density", xlab = "X", ylab = "")
    ```

1. 結果をすばやく表示するには、すべてのコードを選択し (**Ctrl**+**A** キー)、**Ctrl**+**Enter** キーを押すか、右クリックして、 **[対話型で実行]** を選択します。 直接入力したかのように、選択したすべてのコードが対話型ウィンドウに入力され、結果がプロット ウィドウに表示されます。

    ![Visual Studio でのプロットの表示](media/getting-started-08-plot1.png)

1. 1 行の場合は、いつでも **Ctrl**+**Enter** キーを押すだけで、対話型ウィンドウで行を実行できます。

> [!Tip]
> すばやくコードを実行するために、編集を行って **Ctrl**+**Enter** キーを押す (または、**Ctrl**+**A** キーですべてを選択して **Ctrl**+**Enter** キーを押す) パターンについて説明します。 これは、同じ操作のためにマウスを使用するよりもはるかに効率的です。
>
> さらに、Visual Studio フレームの外部にあるプロット ウィンドウにドラッグ アンド ドロップし、ディスプレイ上の他の目的の場所に配置できます。 配置後は、必要なサイズにプロット ウィンドウのサイズを簡単に変更し、画像または PDF ファイルに保存できます。

1. 追加のコード行を少し追加して、2 つ目のプロットを含めます。

    ```R
    n <- 30
    samp.means <- rnorm(N, mean = mu, sd = stddev / sqrt(n))
    lines(density(samp.means))
    ```

1. もう一度 **Ctrl**+**A** キーと **Ctrl**+**Enter** キーを押し、コードを再実行します。次のような結果が生成されます。

    ![Visual Studio での更新されたデュアル プロット](media/getting-started-09-plot2.png)

1. 問題は、最初のプロットで垂直スケールが決定されるため、2 つ目のプロット (`lines` を含む) が収まらないことです。 この問題を解決するには、`plot` 呼び出しに `ylim` パラメーターを設定する必要がありますが、垂直方向の最大値を計算するには、適切にコードを追加する必要があります。 `plot` を呼び出す前に `samp.means` を使用するように、コードを再配置する必要があるため、対話型ウィンドウで 1 行ずつ実行するのは不便です。 コード ファイルで、簡単に適切な編集を行うことができます。

    ```R
    mu <- 50
    stddev <- 1
    N <- 10000
    pop <- rnorm(N, mean = mu, sd = stddev)

    n <- 30
    samp.means <- rnorm(N, mean = mu, sd = stddev / sqrt(n))
    max.samp.means <- max(density(samp.means)$y)

    plot(density(pop), main = "Population Density",
        ylim = c(0, max.samp.means),
        xlab = "X", ylab = "")
    lines(density(samp.means))
    ```

1. もう一度 **Ctrl**+**A** と **Ctrl**+**Enter** キーを押すと、結果が表示されます。

    ![適切にスケーリングされた Visual Studio の最新のデュアル プロット](media/getting-started-10-plot3.png)

エディターで操作できる内容は他にもあります。 詳細については、[R コードの編集](editing-r-code-in-visual-studio.md)、[IntelliSense](r-intellisense.md)、[コード スニペット](code-snippets-for-r.md)に関連するページを参照してください。

## <a name="debug-your-code"></a>コードをデバッグする

Visual Studio の主な強みの 1 つは、デバッグ UI です。 RTVS は、この強力な基盤の上にビルドされ、革新的な UI ([変数エクスプローラー](variable-explorer.md)など) を追加します。 ここでは、デバッグの概要を確認します。

1. 最初に、**[R Tools]**、**[セッション]** の順に選択し、**[リセット]** メニューを使用して、現在のワークスペースをリセットし、ここまでに実行したすべてをクリアします。 既定では、対話型ウィンドウで行うすべてが、現在のセッションに入り、これはデバッガーでも使用されます。 セッションをリセットすることで、既存のデータがない状態でデバッグ セッションを開始できます。 ただし、ソース ファイルはワークスペースの外部で管理および保存されるため、 **[リセット]** コマンドは *script.R* ソース ファイルに影響しません。

1. 前のセクションで作成された *script.R* ファイルを使用して、行にブレークポイントを設定します。行にキャレットを配置して **F9** キーを押すか、**[デバッグ]** から **[ブレークポイントの設定/解除]** メニューを選択すると、この行は `pop <-` で開始されます。 または、その行の左側の余白をクリックすると、ブレークポイントの赤いドットが表示されます。

    ![エディターでのブレークポイントの設定](media/getting-started-11-debug1.png)

1. ツール バーの **[Source startup file]\(ソース スタートアップ ファイル\)** ボタンを選択するか、**[デバッグ]**、**[Source startup file]\(ソース スタートアップ ファイル\)** メニュー アイテムの順に選択するか、**F5** キーを押すかのいずれかを行って、*script.R* のコードでデバッガーを起動します。 Visual Studio がデバッグ モードに切り替わり、コードの実行が開始されます。 ただし、ブレークポイントを設定した行で停止します。

    ![Visual Studio デバッガーのブレークポイントでの停止](media/getting-started-12-debug2.png)

1. Visual Studio には、デバッグ中にコード行をステップ実行する機能があります。 また、関数へのステップイン、関数のステップ オーバー、呼び出し元コンテキストへの関数のステップ アウトを行うこともできます。 これらの機能は、他の機能と共に **[デバッグ]** メニューに表示されます (エディターのコンテキスト メニューを右クリックして、[デバッグ] ツール バーを選択)。

    ![Visual Studio のデバッグ ツール バー](media/getting-started-13-debug3.png)

1. ブレークポイントで停止すると、変数の値を調べることができます。 Visual Studio で **[自動変数]** ウィンドウを検索して、 **[ローカル]** という名前の下部のタブを選択します。 **[ローカル]** ウィンドウには、プログラムの現在の位置でローカル変数が表示されます。 前に設定したブレークポイントで停止した場合、`pop` 変数がまだ定義されていないことがわかります。 **[デバッグ]** の **[ステップ オーバー]** (**F10** キー) を使用すると、`pop` の値が表示されます。

    ![Visual Studio の [ローカル] ウィンドウ](media/getting-started-14-debug4.png)

1. さまざまなスコープ (グローバル スコープとパッケージ スコープを含む) で変数を調べるには、[[変数エクスプローラー]](variable-explorer.md) を使用します。 また、変数エクスプローラーでも、並べ替え可能な列を含む表形式ビューに切り替え、CSV ファイルにデータをエクスポートする機能が提供されます。

    ![変数エクスプローラーの展開ビュー](media/variable-explorer-expanded-results.png)

1. 引き続き 1 行ずつプログラムをステップ実行したり、 **[続行]** (**F5**) を選択して完了 (次のブレークポイント) まで実行したりすることができます。

さらに詳細を確認するには、「[デバッグ](debugging-r-in-visual-studio.md)」と「[変数エクスプローラー](variable-explorer.md)」を参照してください。

## <a name="next-steps"></a>次の手順

このチュートリアルでは、Visual Studio で対話型ウィンドウを使用して、コードの編集およびデバッグを行い、R プロジェクトの基本について学習しました。 その他の機能を引き続き確認するには、以下の記事、および目次の内容を参照してください。

- [サンプル プロジェクト](getting-started-samples.md)
- [コードの編集](editing-r-code-in-visual-studio.md)
- [デバッグ](debugging-r-in-visual-studio.md)
- [ワークスペース](r-workspaces-in-visual-studio.md)
- [データの視覚化](visualizing-data-with-r-in-visual-studio.md)
