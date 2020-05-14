---
title: ASP.NET Core をデバッグする
description: Visual Studio デバッガーを使用して ASP.NET Core をデバッグする
ms.custom: mvc
ms.date: 08/06/2018
ms.topic: quickstart
helpviewer_keywords:
- debugger
ms.assetid: f4cea2e1-08dc-47ac-aba2-3b8c338e607f
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- aspnet
ms.openlocfilehash: bbe3d23301f0853626a930855acf4b595c6a2923
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/20/2020
ms.locfileid: "75847871"
---
# <a name="quickstart-debug-aspnet-core-with-the-visual-studio-debugger"></a>クイック スタート: Visual Studio デバッガーを使用して ASP.NET Core をデバッグする

Visual Studio デバッガーでは、アプリのデバッグに役立つ多くの強力な機能が提供されます。 このトピックでは、基本的な機能のいくつかを簡単に紹介します。

## <a name="create-a-new-project"></a>新しいプロジェクトを作成する

1. Visual Studio を開きます。

    ::: moniker range=">=vs-2019"
    **Esc** キーを押してスタート ウィンドウを閉じます。 **Ctrl + Q** キーを押して検索ボックスを開き、「**asp.net**」と入力し、 **[テンプレート]** を選択してから、 **[新しい ASP.NET Core Web アプリケーションの作成]** を選択します。 表示されたダイアログ ボックスで、 **[作成]** を選択します。
    ::: moniker-end
    ::: moniker range="vs-2017"
    上部のメニュー バーから、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** の順に選択します。 **[新しいプロジェクト]** の左側のウィンドウで、 **[Visual C#]** の下にある **[Web]** を選択し、次に、真ん中のウィンドウで **[ASP.NET Core Web アプリケーション]** を選択します。 「**MyDbgApp**」のような名前を入力し、 **[OK]** をクリックします。

    表示されたダイアログ ボックスの中央のウィンドウで、 **[Web アプリケーション]** を選択し、 **[OK]** をクリックします。

    ![Web アプリケーションを選ぶ](../debugger/media/dbg-qs-aspnet-choose-web-app.png)
    ::: moniker-end

    **[ASP.NET Core Web アプリケーション]** プロジェクト テンプレートが表示されない場合は、 **[ツール]**  >  **[ツールと機能を取得...]** に移動して、Visual Studio インストーラーを開きます。 **[ASP.NET と Web 開発]** ワークロードを選択してから **[変更]** を選択します。

    Visual Studio によってプロジェクトが作成されます。

1. ソリューション エクスプローラーで、(Pages/About.cshtml の下の) About.cshtml.cs を開き、次のコード

    ```csharp
    public void OnGet()
    {
        Message = "Your application description page.";
    }
    ```

    を、次のコードで置換します。

    ```csharp
    public void OnGet()
    {
        LinkedList<int> result = doWork();
        Message = "Result of work: " + result.First.Value + ", " + result.First.Value;
    }

    private static LinkedList<int> doWork()
    {
        LinkedList<int> c1 = new LinkedList<int>();

        c1.AddLast(10);
        c1.AddLast(20);

        LinkedList<int> c2 = new LinkedList<int>(c1);

        return c2;

    }
    ```

## <a name="set-a-breakpoint"></a>ブレークポイントの設定

*ブレークポイント*は、Visual Studio で実行コードが中断される場所を示すマーカーです。これにより、変数の値またはメモリの動作を確認したり、コードの分岐が実行されるかどうかを確認したりすることができます。 これが、デバッグの最も基本的な機能です。

1. ブレークポイントを設定するには、`doWork` 関数の左側の余白をクリックします (またはコード行を選択して、**F9** キーを押します)。

    ![ブレークポイントの設定](../debugger/media/dbg-qs-set-breakpoint-aspnet.png)

    ブレークポイントは左中かっこ (`{`) の左側に設定されます。

1. ここで **F5** キーを押します (または **[デバッグ] > [デバッグの開始]** の順に選択します)。

1. Web ページが読み込まれたら、Web ページの上部にある **[バージョン情報]** リンクをクリックします。

    ブレークポイントを設定した場所でデバッガーが一時停止します。 デバッガーとアプリの実行が一時停止されているステートメントが、黄色の矢印で示されます。 `doWork` 関数の宣言の後の左中かっこ (`{`) がある行はまだ実行されていません。

    ![ブレークポイントに到達する](../debugger/media/dbg-qs-hit-breakpoint-aspnet.png)

    > [!TIP]
    > ループまたは再帰処理の中にブレークポイントがある場合、または頻繁にステップ実行するブレークポイントが数多くある場合、[条件付きブレークポイント](../debugger/using-breakpoints.md#BKMK_Specify_a_breakpoint_condition_using_a_code_expression)を使用して、特定の条件が満たされる場合にのみコードが中断されるようにしてください。 これにより、時間が節約され、再現が難しい問題をより簡単にデバッグすることもできます。

## <a name="navigate-code"></a>コード間の移動

続行するようにデバッガーに指示するためのさまざまなコマンドがあります。 ここでは、Visual Studio 2017 以降で使用できる便利なコード ナビゲーション コマンドを示します。

ブレークポイントで一時停止している間に、緑色の **[クリックで実行]** ボタン ![[クリックで実行]](../debugger/media/dbg-tour-run-to-click.png) が表示されるまでステートメント `return c2` をポイントし、表示されたら **[クリックで実行]** ボタンを押します。

![クリックで実行](../debugger/media/dbg-qs-run-to-click-aspnet.png)

アプリは引き続き実行され、ボタンをクリックしたコード行で一時停止します。

コードのステップ実行に使用される一般的なキーボード コマンドには、**F10** と **F11** が含まれます。 詳しい手順については、「[デバッガーでのはじめに](../debugger/debugger-feature-tour.md)」をご覧ください。

## <a name="inspect-variables-in-a-datatip"></a>データヒントの変数を検査する

1. (黄色の実行ポインターでマークされた) コードの現在の行で、`c2` オブジェクトをマウスでポイントしてデータヒントを表示します。

    ![データヒントを表示する](../debugger/media/dbg-qs-data-tip-aspnet.png)

    データヒントでは、`c2` 変数の現在の値が示され、そのプロパティを検査することができます。 デバッグ中に、予期しない値が表示される場合は、先行するコード行または呼び出しているコード行にバグがある可能性があります。

2. データヒントを展開して、`c2` オブジェクトの現在のプロパティ値を確認します。

3. コードを実行している間に `c2` の値を引き続き表示できるようにデータヒントをピン留めする場合は、小さいピン アイコンをクリックします (ピン留めしたデータヒントを任意の場所に移動することができます)。

## <a name="edit-code-and-continue-debugging"></a>コードを編集してデバッグを続行する

デバッグ セッションの途中にコードでテストする変更を識別する場合は、そのようにすることもできます。

1. `OnGet` メソッドで、`result.First.Value` の 2 番目のインスタンスをクリックし、`result.First.Value` を `result.Last.Value` に変更します。

1. **F10** キー (または **[デバッグ] > [ステップ オーバー]** ) を数回押して、デバッガーを進めて編集したコードを実行します。

    ![エディット コンティニュ](../debugger/media/dbg-qs-edit-and-continue-aspnet.png "エディット コンティニュ")

    **F10** キーでは、デバッガーは一度に 1 ステートメントずつ進みますが、関数をステップインするのではなく、ステップ オーバーします (スキップしたコードがまだ実行される)。

エディット コンティニュの使用および機能制限の詳細については、[エディット コンティニュ](../debugger/edit-and-continue.md)に関するページを参照してください。

## <a name="next-steps"></a>次の手順

このチュートリアルでは、デバッガーを起動する方法、コードをステップ実行する方法、変数を確認する方法について学習しました。 必要に応じて、デバッガー機能の概要と、詳細情報へのリンクを取得します。

> [!div class="nextstepaction"]
> [デバッガーでのはじめに](../debugger/debugger-feature-tour.md)
