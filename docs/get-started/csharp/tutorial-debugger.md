---
title: 'チュートリアル: C# のコードをデバッグする'
description: Visual Studio デバッガーを起動し、コードをステップ実行し、データを検査する方法について説明します。
ms.custom: debug-experiment, seodec18, get-started
ms.date: 11/27/2018
ms.technology: vs-ide-debug
ms.topic: tutorial
dev_langs:
- CSharp
helpviewer_keywords:
- debugger
ms.assetid: 62734c0d-a75a-4576-8f73-0e97c19280e1
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1c7237d8d8bf66273078049a41a3193af0026792
ms.sourcegitcommit: 697f2ab875fd789685811687387e9e8e471a38c4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "74830026"
---
# <a name="tutorial-learn-to-debug-c-code-using-visual-studio"></a>チュートリアル: Visual Studio を使用した C# のデバッグについて理解する

この記事では、ステップ バイ ステップのチュートリアルで Visual Studio デバッガーの機能を紹介します。 デバッガー機能の概要を確認したい場合は、「[デバッガーでのはじめに](../../debugger/debugger-feature-tour.md)」を参照してください。 "*ご自分のアプリをデバッグする*" 場合、通常、それはデバッガーをアタッチした状態でご自分のアプリケーションを実行することを意味します。 これを行う場合、デバッガーには、ご自分のコードが実行されている間にそのコードによって何が行われているのかを確認するためのさまざまな方法が用意されています。 ご自分のコードをステップ実行して変数内に格納されている値を確認したり、変数に対してウォッチ式を設定して値が変わるタイミングを確認したり、コードの実行パスを調べたり、コードの分岐が実行されているかどうかを確認したりできます。 コードのデバッグを試みるのが今回初めてである場合は、この記事を先に進む前に[超初心者向けのデバッグ方法](../../debugger/debugging-absolute-beginners.md)に関するページを参照することをお勧めします。

デモ アプリは C# ですが、ほとんどの機能は C++、Visual Basic、F#、Python、JavaScript、および Visual Studio でサポートされているその他の言語にも適用されます (F# はエディット コンティニュをサポートしていません。 F# および JavaScript は、 **[自動変数]** ウィンドウをサポートしていません)。 スクリーン ショットは C# になっています。

このチュートリアルでは、次の作業を行います。

> [!div class="checklist"]
> * デバッガーを起動して、ブレークポイントにヒットします。
> * デバッガー内でコードをステップ実行するコマンドについて学習します。
> * データ ヒントおよびデバッガー ウィンドウ内で変数を確認します。
> * 呼び出し履歴を調べる

## <a name="prerequisites"></a>必須コンポーネント

::: moniker range=">=vs-2019"

Visual Studio 2019 および **.NET デスクトップ開発**ワークロードをインストールしている必要があります。

::: moniker-end
::: moniker range="vs-2017"

Visual Studio 2017 および **.NET デスクトップ開発**ワークロードをインストールしている必要があります。

::: moniker-end

::: moniker range="vs-2017"

Visual Studio をまだインストールしていない場合は、[Visual Studio のダウンロード](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download) ページに移動し、無料試用版をインストールしてください。

::: moniker-end

::: moniker range="vs-2019"

Visual Studio をまだインストールしていない場合は、[Visual Studio のダウンロード](https://visualstudio.microsoft.com/downloads) ページに移動し、無料試用版をインストールしてください。

::: moniker-end

Visual Studio は既にあり、ワークロードだけをインストールする必要がある場合は、 **[ツール]**  >  **[ツールと機能を取得]** に移動すると、Visual Studio インストーラーが開きます。 Visual Studio インストーラーが起動します。 **.NET デスクトップ開発**ワークロードを選択し、 **[変更]** を選択します。

## <a name="create-a-project"></a>プロジェクトを作成する

1. Visual Studio を開きます。

    ::: moniker range=">=vs-2019"
    **Esc** キーを押してスタート ウィンドウを閉じます。 **Ctrl + Q** キーを押して検索ボックスを開き、「**コンソール**」と入力して、 **[テンプレート]** を選択した後、 **[新しいコンソール アプリ (.NET Core) プロジェクトの作成]** 、 **[Create new Console App (.NET Framework) project]\(新しいコンソール アプリ (.NET Framework) プロジェクトの作成\)** のいずれかを選択します。 表示されたダイアログ ボックスで、**get-started-debugging** のような名前を入力して、 **[作成]** をクリックします。
    ::: moniker-end
    ::: moniker range="vs-2017"
    上部のメニュー バーで、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** の順に選択します。 **[新しいプロジェクト]** ダイアログ ボックスの左側のウィンドウで、 **[Visual C#]** の下にある **[Windows デスクトップ]** を選択し、次に真ん中のウィンドウで **[コンソール アプリ (.NET Framework)]** を選択します。 次に、「**get-started-debugging**」ような名前を入力し、 **[OK]** をクリックします。
    ::: moniker-end

    **[コンソール アプリ (.NET Framework)]** プロジェクト テンプレートが表示されない場合は、 **[ツール]**  >  **[ツールと機能を取得...]** に移動して、Visual Studio インストーラーを開きます。 **.NET デスクトップ開発**ワークロードを選択し、 **[変更]** を選択します。

    Visual Studio によってプロジェクトが作成されます。

1. *Program.cs* で、すべての既定のコード

    ```csharp
    using System;
    // ...

    namespace get_started_debugging
    {
        class Program
        {
            static void Main(string[] args)
            {
            }
        }
    }
    ```

    を、次のコードで置換します。

    ```csharp
    using System;
    using System.Collections.Generic;

    public class Shape
    {
        // A few example members
        public int X { get; private set; }
        public int Y { get; private set; }
        public int Height { get; set; }
        public int Width { get; set; }

        // Virtual method
        public virtual void Draw()
        {
            Console.WriteLine("Performing base class drawing tasks");
        }
    }

    class Circle : Shape
    {
        public override void Draw()
        {
            // Code to draw a circle...
            Console.WriteLine("Drawing a circle");
            base.Draw();
        }
    }

    class Rectangle : Shape
    {
        public override void Draw()
        {
            // Code to draw a rectangle...
            Console.WriteLine("Drawing a rectangle");
            base.Draw();
        }
    }

    class Triangle : Shape
    {
        public override void Draw()
        {
            // Code to draw a triangle...
            Console.WriteLine("Drawing a trangle");
            base.Draw();
        }
    }

    class Program
    {
        static void Main(string[] args)
        {

            var shapes = new List<Shape>
            {
                new Rectangle(),
                new Triangle(),
                new Circle()
            };

            foreach (var shape in shapes)
            {
                shape.Draw();
            }

            // Keep the console open in debug mode.
            Console.WriteLine("Press any key to exit.");
            Console.ReadKey();
        }

    }

    /* Output:
        Drawing a rectangle
        Performing base class drawing tasks
        Drawing a triangle
        Performing base class drawing tasks
        Drawing a circle
        Performing base class drawing tasks
    */
    ```

## <a name="start-the-debugger"></a>デバッガーを起動する

1. **F5** キー ( **[デバッグ] > [デバッグの開始]** ) を押すか、デバッグ ツールバーの **[デバッグの開始]** ボタン ![デバッグの開始](../../debugger/media/dbg-tour-start-debugging.png "デバッグの開始") を押します。

     **F5** キーを押すと、デバッガーがアプリ プロセスにアタッチされた状態でアプリが起動されますが、現時点で、コードを調べるために特別なことは何も行っていません。 したがって、アプリが読み込まれたにすぎず、コンソール出力が表示されます。

    ```cmd
    Drawing a rectangle
    Performing base class drawing tasks
    Drawing a triangle
    Performing base class drawing tasks
    Drawing a circle
    Performing base class drawing tasks
    ```

     このチュートリアルでは、デバッガーを使用してこのアプリを詳しく見て行くと共に、デバッガーの機能についても説明します。

2. 赤色の停止 ![デバッグの停止](../../debugger/media/dbg-tour-stop-debugging.png "デバッグ中に診断ツールを有効にします") ボタンを押して、デバッガーを停止します。

## <a name="set-a-breakpoint-and-start-the-debugger"></a>ブレークポイントを設定し、デバッガーを開始する

1. `Main` 関数の `foreach` ループ内で、ブレークポイントを設定します。そのためには、次のコード行の左余白をクリックします。

    `shape.Draw()`

    ブレークポイントを設定した場所に赤い円が表示されます。

    ブレークポイントは、信頼できるデバッグの最も基本的で重要な機能です。 ブレークポイントは、Visual Studio が実行コードを中断する場所を示します。これにより、変数の値またはメモリの動作を確認したり、コードの分岐が実行されるかどうかを確認したりすることができます。

2. **F5** キーを押すか、 **[デバッグの開始]** ボタン ![デバッグの開始](../../debugger/media/dbg-tour-start-debugging.png "デバッグの開始") を押します。アプリが起動され、ブレークポイントを設定したコード行までデバッガーが実行されます。

    ![ブレークポイントを設定してそこにヒットする](../csharp/media/get-started-set-breakpoint.gif)

    黄色の矢印はデバッガーが一時停止しているステートメントを表します。デバッガーの一時停止によってアプリの実行も同じポイントで中断されます (このステートメントはまだ実行されていません)。

     アプリがまだ実行されていない場合、**F5** キーを押すとデバッガーが起動し、最初のブレークポイントで停止します。 それ以外の場合、**F5** キーを押すと、アプリの実行が続行され、次のブレークポイントまで進みます。

    ブレークポイントは、詳細に調べたいコード行またはコード セクションがわかっている場合に便利な機能です。

## <a name="navigate-code-in-the-debugger-using-step-commands"></a>ステップ コマンドを使用してデバッガーでコード内を移動する

ほとんどの場合、ここではキーボード ショートカットを使用します。それはデバッガーでご自分のアプリをすばやく実行するのに便利な方法だからです (コマンド メニューなどの対応するコマンドはかっこ内に示します)。

1. `Main` メソッド内の `shape.Draw` メソッド呼び出しで一時停止している間に、**F11** キーを押して (または **[デバッグ] > [ステップ イン]** の順に選択して)、`Rectangle` クラスのコードに進みます。

     ![F11 キーを使用してコードにステップ インする](../csharp/media/get-started-f11.png "F11 ステップ イン")

     F11 キーは **[ステップ イン]** コマンドであり、アプリの実行が一度に 1 ステートメント進められます。 F11 キーは実行フローを最も詳しく確認することができる便利な方法です。 (他にコード内をより速く移動するためのオプションについても紹介します)既定では、非ユーザー コードはデバッガーによってスキップされます (詳細については、[マイ コードのみ](../../debugger/just-my-code.md)に関するページを参照)。

2. `base.Draw` メソッド呼び出し上でデバッガーが停止するまで数回 **F10** キーを押し (または **[デバッグ] > [ステップ オーバー]** の順に選択し)、次にもう一度 **F10** キーを押します。

     ![F10 キーを使用してコードをステップ オーバーする](../csharp/media/get-started-step-over.png "F10 ステップ オーバー")

     今回は、デバッガーが基本クラス (`Shape`) の `Draw` メソッドにステップ インしていないことに注目してください。 **F10** キーを押すと、ご利用のアプリのコード内の関数またはメソッドにステップ インすることなく、デバッガーが進められます (コードはまだ実行されています)。 `base.Draw` メソッド呼び出し上で (**F11** キーではなく) **F10** キーを押して、`base.Draw` 用の実装コードをスキップしました (現時点で関係ないと思われるため)。

## <a name="navigate-code-using-run-to-click"></a>[クリックで実行] を使用してコード内を移動する

1. コード エディター内で下方にスクロールして `Triangle` クラス内の `Console.WriteLine` メソッドにカーソルを合わせ、それによって左側に緑色の **[クリックで実行]** ボタン ![クリックで実行](../../debugger/media/dbg-tour-run-to-click.png "RunToClick") が表示されるのを確認します。 ボタンのヒントには、[ここまで実行します] と表示されます。

     ![[クリックで実行] 機能を使用する](../csharp/media/get-started-run-to-click.png "[Run To Click (クリックで実行)]")

   > [!NOTE]
   > **[クリックで実行]** ボタンは [!include[vs_dev15](../../misc/includes/vs_dev15_md.md)] の新機能です。 緑色の矢印ボタンが表示されない場合、この例では代わりに **F11** キーを使用してデバッガーを適切な場所まで進めます。

2. **[クリックで実行]** ボタン ![クリックで実行](../../debugger/media/dbg-tour-run-to-click.png "RunToClick") をクリックします。

    このボタンを使用することは、一時的なブレークポイントを設定することに似ています。 **[クリックで実行]** はアプリ コードの表示領域内をすばやく移動するのに便利です (開いている任意のファイル内でクリックすることができます)。

    デバッガーは `Triangle` クラスの `Console.WriteLine` メソッド実装に進みます。 (前に設定したブレークポイントで先にデバッガーが一時停止する場合は、もう一度 **[クリックで実行]** を使用して `Console.WriteLine` までデバッガーを進めます。)

    一時停止したところで、入力ミスがあることに気づきました。 出力 "Drawing a trangle" にはスペルの誤りがあります。 デバッガーでアプリを実行しながら、ここでスペルミスを修正することができます。

## <a name="edit-code-and-continue-debugging"></a>コードを編集してデバッグを続行する

1. "Drawing a trangle" 内をクリックし、"trangle" を "triangle" に変更するという修正を加えます。

1. **F11** キーを 1 回押します。デバッガーが再び前に進むのがわかります。

    > [!NOTE]
    > デバッガー内で編集するコードの種類によっては、警告メッセージが表示される場合があります。 一部のシナリオでは、続行する前にコードを再コンパイルする必要があります。

## <a name="step-out"></a>ステップ アウト

たとえば、`Triangle` クラス内の `Draw` メソッドの確認を終了しました。そこで、この関数からは抜け出したいけれども、デバッガーには留まっていたいとします。 これを行うには、 **[ステップ アウト]** コマンドを使用します。

1. **Shift** + **F11** キーを押します (または **[デバッグ] > [ステップ アウト]** の順に選択します)。

     このコマンドを使用すると、アプリの実行が再開され (そしてデバッガーが前へ進められ)、現在の関数から制御が戻るまで続けられます。

     `Main` メソッド内の `foreach` ループに戻る必要があります。 そうでない場合は、もう一度 **Shift** + **F11** キーを押します。

## <a name="restart-your-app-quickly"></a>アプリを簡単に再起動する

[デバッグ] ツール バーの **[再起動]** ![アプリの再起動](../../debugger/media/dbg-tour-restart.png "RestartApp") ボタンをクリックします (**Ctrl** + **Shift** + **F5** キー)。

**[再起動]** を押すと、アプリを停止してからデバッガーを再起動する場合と比較して時間の節約になります。 デバッガーは、コードを実行すると最初にヒットするブレークポイントで一時停止します。

`shape.Draw()` メソッド上で設定したブレークポイントでデバッガーが再び停止します。

## <a name="inspect-variables-with-data-tips"></a>データ ヒントを使用して変数を確認する

変数を調べることができる機能は、デバッガーの機能の中でも最も便利な機能の 1 つに挙げられ、それを行うにはさまざまな方法を利用できます。 多くの場合、問題のデバッグを試みるときは、特定のタイミングで変数に期待する値がそのとおりに変数に格納されているかどうかの確認を試みます。

1. `shape.Draw()` メソッド上で一時停止しているときに、`shape` オブジェクトにカーソルを合わせます。すると、そのプロパティの既定値 (オブジェクトの種類 `Rectangle`) が表示されます。

1. `shape` オブジェクトを展開すると、そのプロパティ (`Height` プロパティなど) が表示されます。この値は 0 です。

1. **F10** キーを何回か押して (または **[デバッグ]**  >  **[ステップ オーバー]** の順に選択して)、`foreach` ループを 1 回反復処理し、`shape.Draw()` で再度一時停止します。

1. マウス ポインターをもう一度、図形オブジェクトの上に移動すると、今度は種類が `Triangle` の新しいオブジェクトが作成されたことが表示されます。

     ![データ ヒントを表示する](../csharp/media/get-started-data-tip.gif "データ ヒントを表示する")

    デバッグ時に、変数のプロパティ値に期待どおりの値が格納されているかどうかをすばやく確認したい場合がよくあります。データ ヒントはそれを行うのに適した方法です。

## <a name="inspect-variables-with-the-autos-and-locals-windows"></a>[自動変数] ウィンドウと [ローカル] ウィンドウを使用して変数を確認する

1. コード エディターの下部にある **[自動変数]** ウィンドウを見てください。

    ウィンドウが閉じている場合は、デバッガーが一時停止している間に、 **[デバッグ]**  >  **[ウィンドウ]**  >  **[自動変数]** の順に選択します。

1. `shapes` オブジェクトを展開します。

     ![[自動変数] ウィンドウで変数を検査する](../csharp/media/get-started-autos-window.png "[自動変数] ウィンドウ")

    **[自動変数]** ウィンドウには、変数とその現在の値が表示されます。 **[自動変数]** ウィンドウには、現在の行または前の行で使用されるすべての変数が表示されます (言語固有の動作についてはドキュメントを参照してください)。

1. 次に、 **[自動変数]** ウィンドウの隣にあるタブ内の **[ローカル]** ウィンドウを見てください。

    **[ローカル]** ウィンドウを確認すれば、現在の[スコープ](https://www.wikipedia.org/wiki/Scope_(computer_science)) (現在の実行コンテキスト) に含まれている変数がわかります。

## <a name="set-a-watch"></a>ウォッチ式を設定する

1. メインのコード エディター ウィンドウで、`shapes` オブジェクトを右クリックして、 **[ウォッチ式の追加]** を選択します。

    コード エディターの下部に **[ウォッチ]** ウィンドウが表示されます。 **[ウォッチ]** ウィンドウを使用することで、監視する変数 (または式) を指定できます。

    `shapes` オブジェクトに対してウォッチ式が設定されたので、デバッガー内を移動しながらその値の変化を確認することができます。 その他の変数ウィンドウとは異なり、 **[ウォッチ]** ウィンドウには監視対象の変数が常に表示されます (対象外のときは淡色表示となります)。

## <a name="examine-the-call-stack"></a>呼び出し履歴を調べる

1. `foreach` ループ内で一時停止しているときに、 **[呼び出し履歴]** ウィンドウをクリックします。このウィンドウは既定では右下ペイン内に表示されます。

    ウィンドウが閉じている場合は、デバッガーが一時停止している間に、 **[デバッグ]**  >  **[ウィンドウ]**  >  **[呼び出し履歴]** の順に選択します。

2. コード エディター内でデバッガーが `Triangle` クラスの `Base.Draw` メソッド内で一時停止するのを確認できるまで、**F11** キーを数回押します。 **[呼び出し履歴]** ウィンドウを見てください。

    ![呼び出し履歴を調べる](../csharp/media/get-started-call-stack.png "ExamineCallStack")

    **[呼び出し履歴]** ウィンドウには、メソッドおよび関数が呼び出されている順番が表示されます。 先頭行には、現在の関数が表示されます (このアプリでは `Triangle.Draw` メソッド)。 2 行目には、`Triangle.Draw` が `Main` メソッドから呼び出されたことが表示され、後もこのような具合に表示されます。

   > [!NOTE]
   > **[呼び出し履歴]** ウィンドウは、Eclipse のような一部の IDE におけるデバッグ パースペクティブに似ています。

    呼び出し履歴は、アプリの実行フローを調査して理解するのに優れた方法です。

    コード行をダブルクリックすることで、ソース コードに移動できます。また、それによって、デバッガーで検査されている現在のスコープを変更することもできます。 このアクションを行っても、デバッガーは前に進みません。

    **[呼び出し履歴]** ウィンドウから右クリック メニューを使用して他の操作を行うこともできます。 たとえば、指定した関数にブレークポイントを挿入したり、 **[カーソル行の前まで実行]** を使用してデバッガーを進めたり、ソース コードの調査を開始したりできます。 詳細については、[呼び出し履歴を調べる](../../debugger/how-to-use-the-call-stack-window.md)」を参照してください。

## <a name="change-the-execution-flow"></a>実行フローを変更する

1. `Circle.Draw` メソッド呼び出し内でデバッガーが一時停止した状態で、マウスを使用して左側にある黄色の矢印 (実行ポインター) をつかみ、その黄色の矢印を 1 行上にある `Console.WriteLine` メソッド呼び出しまで移動します。

1. **F11** キーを押します。

    デバッガーにより `Console.WriteLine` メソッドが返されます (これはコンソール ウィンドウの出力に表示されます)。

    実行フローを変更することにより、さまざまなコード実行パスをテストしたり、デバッガーを再起動することなくコードを再実行したりできます。

    > [!WARNING]
    > 多くの場合、この機能には注意する必要があり、ツールヒントに警告が表示されます。 他の警告が表示される場合もあります。 ポインターを移動しても、ご利用のアプリを以前のアプリ状態に戻すことはできません。

1. **F5** キーを押してアプリの実行を続行します。

    これでこのチュートリアルは完了です。

## <a name="next-steps"></a>次の手順

このチュートリアルでは、デバッガーを起動する方法、コードをステップ実行する方法、変数を確認する方法について学習しました。 必要に応じて、デバッガー機能の概要と、詳細情報へのリンクを取得します。

> [!div class="nextstepaction"]
> [デバッガーでのはじめに](../../debugger/debugger-feature-tour.md)
