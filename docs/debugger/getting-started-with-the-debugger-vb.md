---
title: Visual Studio デバッガーを使用した Visual Basic コードのデバッグについて理解する
ms.description: Learn how to start the Visual Studio debugger, step through code, and inspect data.
ms.custom: debug-experiment
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
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 7f568c5785af1917827646d232ef3c6c8f0ad41b
ms.sourcegitcommit: d7f232a7596420e40ff8051d42cdf90203af4a74
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2018
ms.locfileid: "52825970"
---
# <a name="tutorial-learn-to-debug-visual-basic-code-using-visual-studio"></a>チュートリアル: Visual Studio を使用した Visual Basic コードのデバッグについて理解する

この記事では、ステップ バイ ステップのチュートリアルで Visual Studio デバッガーの機能を紹介します。 デバッガー機能の概要を確認したい場合は、[デバッガー機能のツアー](../debugger/debugger-feature-tour.md)に関するページを参照してください。 "*ご自分のアプリをデバッグする*" 場合、通常、それはデバッガーをアタッチした状態でご自分のアプリケーションを実行することを意味します。 これを行う場合、デバッガーには、ご自分のコードが実行されている間にそのコードによって何が行われているのかを確認するためのさまざまな方法が用意されています。 ご自分のコードをステップ実行して変数内に格納されている値を確認したり、変数に対してウォッチ式を設定して値が変わるタイミングを確認したり、コードの実行パスを調べたり、コードの分岐が実行されているかどうかを確認したりできます。 コードのデバッグを試みるのが今回初めてである場合は、この記事を先に進む前に[超初心者向けのデバッグ方法](../debugger/debugging-absolute-beginners.md)に関するページを参照することをお勧めします。

| | |
|---------|---------|
| ![ビデオのムービー カメラ アイコン](../install/media/video-icon.png "ビデオを見る") | デバッグに関する[ビデオを見る](https://mva.microsoft.com/en-US/training-courses-embed/getting-started-with-visual-studio-2017-17798/Debugger-Feature-tour-of-Visual-studio-2017-sqwiwLD6D_1111787171)。同様の手順が示されています。 |

このチュートリアルでは、次の作業を行います。

> [!div class="checklist"]
> * デバッガーを起動して、ブレークポイントにヒットします。
> * デバッガー内でコードをステップ実行するコマンドについて学習します。
> * データ ヒントおよびデバッガー ウィンドウ内で変数を確認します。
> * 呼び出し履歴を調べる

## <a name="prerequisites"></a>必須コンポーネント

* Visual Studio 2017 および **.NET デスクトップ開発**ワークロードをインストールしている必要があります。

    Visual Studio をまだインストールしていない場合は、 [Visual Studio のダウンロード](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)  ページに移動し、無料試用版をインストールしてください。

    ワークロードをインストールする必要があるが、既に Visual Studio を所有している場合は、(**[ファイル]** > **[新規作成]** > **[プロジェクト]** の順に選択し) **[新しいプロジェクト]** ダイアログ ボックスの左側のウィンドウにある **[Visual Studio インストーラーを開く]** リンクをクリックします。 Visual Studio インストーラーが起動します。 **[.NET デスクトップ開発]** ワークロードを選択し、**[変更]** を選びます。

## <a name="create-a-project"></a>プロジェクトを作成する

1. Visual Studio で、**[ファイル]、[新しいプロジェクト]** の順に選択します。

2. **[Visual Basic]** の下で **[Windows デスクトップ]** を選択し、真ん中のウィンドウで **[コンソール アプリ]** を選択します。

    **[コンソール アプリケーション]** プロジェクト テンプレートが表示されない場合は、**[新しいプロジェクト]** ダイアログ ボックスの左側のウィンドウにある **[Visual Studio インストーラーを開く]** リンクをクリックします。 Visual Studio インストーラーが起動します。 *[.NET デスクトップ開発]** ワークロードを選択し、**[変更]** を選びます。

3. 「**get-started-debugging**」ような名前を入力し、**[OK]** をクリックします。

    Visual Studio によってプロジェクトが作成されます。

4. *Program.cs* で、下記のコード

    ```vb
    Module Module1

        Sub Main()
        End Sub

    End Module
    ```

    を、次のコードで置換します。

    ```vb
    Imports System
    Imports System.Collections.Generic

    Public Class Shape

      ' A few example members
        Public Property X As Integer
            Get
                Return X
            End Get
            Set
            End Set
        End Property

        Public Property Y As Integer
            Get
                Return Y
            End Get
            Set
            End Set
        End Property

        Public Property Height As Integer
            Get
                Return Height
            End Get
            Set
            End Set
        End Property

        Public Property Width As Integer
            Get
                Return Width
            End Get
            Set
            End Set
        End Property

        ' Virtual method
        Public Overridable Sub Draw()
            Console.WriteLine("Performing base class drawing tasks")
        End Sub
    End Class

    Public Class Circle
        Inherits Shape

        Public Overrides Sub Draw()
            ' Code to draw a circle...
            Console.WriteLine("Drawing a circle")
            MyBase.Draw()
        End Sub
    End Class

    Public Class Rectangle
        Inherits Shape

        Public Overrides Sub Draw()
            ' Code to draw a rectangle...
            Console.WriteLine("Drawing a rectangle")
            MyBase.Draw()
        End Sub
    End Class

    Public Class Triangle
        Inherits Shape

        Public Overrides Sub Draw()
            ' Code to draw a triangle...
            Console.WriteLine("Drawing a trangle")
            MyBase.Draw()
        End Sub
    End Class

    Module Module1

        Sub Main(ByVal args() As String)

            Dim shapes = New List(Of Shape) From
            {
                New Rectangle,
                New Triangle,
                New Circle
            }

            For Each shape In shapes
                shape.Draw()
            Next
            ' Keep the console open in debug mode.
            Console.WriteLine("Press any key to exit.")
            Console.ReadKey()

        End Sub

    End Module

    ' Output:
    '    Drawing a rectangle
    '    Performing base class drawing tasks
    '    Drawing a triangle
    '    Performing base class drawing tasks
    '    Drawing a circle
    '    Performing base class drawing tasks
    ```

## <a name="start-the-debugger"></a>デバッガーを起動する

1. **F5** キーを押す (**[デバッグ] > [デバッグの開始]**) か、またはデバッグ ツールバーの **[デバッグの開始]** ボタン![デバッグの開始](../debugger/media/dbg-tour-start-debugging.png "デバッグの開始")を選択します。

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

2. 赤色の停止![デバッグの停止](../debugger/media/dbg-tour-stop-debugging.png "デバッグの停止")ボタンを押して、デバッガーを停止します。

## <a name="set-a-breakpoint-and-start-the-debugger"></a>ブレークポイントを設定し、デバッガーを開始する

1. `Main` 関数の `For Each` ループ内で、ブレークポイントを設定します。そのためには、次のコード行の左余白をクリックします。

    `shape.Draw()`

    ブレークポイントを設定した場所に赤い円が表示されます。

    ![ブレークポイントの設定](../debugger/media/get-started-set-breakpoint-vb.png)

    ブレークポイントは、信頼できるデバッグの最も基本的で重要な機能です。 ブレークポイントは、Visual Studio が実行コードを中断する場所を示します。これにより、変数の値またはメモリの動作を確認したり、コードの分岐が実行されるかどうかを確認したりすることができます。 

2. **F5** キーを押すか、または **[デバッグの開始]** ボタン ![デバッグの開始](../debugger/media/dbg-tour-start-debugging.png "デバッグの開始" をクリックします。アプリが起動され、デバッガーが実行されてブレークポイントを設定したコード行まで進みます。

    ![ブレークポイントに到達する](../debugger/media/get-started-hit-breakpoint-vb.png)

    黄色の矢印はデバッガーが一時停止しているステートメントを表します。デバッガーの一時停止によってアプリの実行も同じポイントで中断されます (このステートメントはまだ実行されていません)。

     アプリがまだ実行されていない場合、**F5** キーを押すとデバッガーが起動し、最初のブレークポイントで停止します。 それ以外の場合、**F5** キーを押すと、アプリの実行が続行され、次のブレークポイントまで進みます。

    ブレークポイントは、詳細に調べたいコード行またはコード セクションがわかっている場合に便利な機能です。

## <a name="navigate-code-in-the-debugger-using-step-commands"></a>ステップ コマンドを使用してデバッガーでコード内を移動する

ほとんどの場合、ここではキーボード ショートカットを使用します。それはデバッガーでご自分のアプリをすばやく実行するのに便利な方法だからです (コマンド メニューなどの対応するコマンドはかっこ内に示します)。

1. `Main` 関数内の `shape.Draw` メソッド呼び出しで一時停止している間に、**F11** キーを押して (または **[デバッグ] > [ステップ イン]** の順に選択して)、`Rectangle` クラスのコードに進みます。

     ![F11 キーを使用して、コードにステップ インする](../debugger/media/get-started-f11-vb.png "F11 キーによるステップ イン")

     F11 キーは **[ステップ イン]** コマンドであり、アプリの実行が一度に 1 ステートメント進められます。 F11 キーは実行フローを最も詳しく確認することができる便利な方法です。 (他にコード内をより速く移動するためのオプションについても紹介します)既定では、非ユーザー コードはデバッガーによってスキップされます (詳細については、[マイ コードのみ](../debugger/just-my-code.md)に関するページを参照)。

2. `MyBase.Draw` メソッド呼び出し上でデバッガーが停止するまで数回 **F10** キーを押し (または **[デバッグ] > [ステップ オーバー]** の順に選択し)、次にもう一度 **F10** キーを押します。

     ![F10 キーを使用してコードをステップ オーバーする](../debugger/media/get-started-step-over-vb.png "F10 キーによるステップ オーバー")

     今回は、デバッガーが基本クラス (`Shape`) の `Draw` メソッドにステップ インしていないことに注目してください。 **F10** キーを押すと、ご利用のアプリのコード内の関数またはメソッドにステップ インすることなく、デバッガーが進められます (コードはまだ実行されています)。 `MyBase.Draw` メソッド呼び出し上で F10 キーを押すことによって (**F11** キーではなく)、`MyBase.Draw` 用の実装コードをスキップしました (現時点で関係ないと思われるため)。

## <a name="navigate-code-using-run-to-click"></a>[クリックで実行] を使用してコード内を移動する

1. コード エディター内で下方にスクロールして `Triangle` クラス内の `Console.WriteLine` メソッドにカーソルを合わせ、それによって左側に緑色の **[クリックで実行]** ボタン![クリックで実行](../debugger/media/dbg-tour-run-to-click.png "クリックで実行")が表示されるのを確認します。

     ![[クリックで実行] 機能を使用する](../debugger/media/get-started-run-to-click-vb.png "[クリックで実行]")

   > [!NOTE]
   > **[クリックで実行]** ボタンは [!include[vs_dev15](../misc/includes/vs_dev15_md.md)] の新機能です。 緑色の矢印ボタンが表示されない場合、この例では代わりに **F11** キーを使用してデバッガーを適切な場所まで進めます。

2. **[クリックで実行]** ボタン![クリックで実行](../debugger/media/dbg-tour-run-to-click.png "クリックで実行")をクリックします。

    このボタンを使用することは、一時的なブレークポイントを設定することに似ています。 **[クリックで実行]** はアプリ コードの表示領域内をすばやく移動するのに便利です (開いている任意のファイル内でクリックすることができます)。

    デバッガーは `Triangle` クラスの `Console.WriteLine` メソッド実装に進みます。

    一時停止したところで、入力ミスがあることに気づきました。 出力 "Drawing a trangle" にはスペルの誤りがあります。 デバッガーでアプリを実行しながら、ここでスペルミスを修正することができます。

## <a name="edit-code-and-continue-debugging"></a>コードを編集してデバッグを続行する

1. "Drawing a trangle" 内をクリックし、"trangle" を "triangle" に変更するという修正を加えます。

1. **F11** キーを 1 回押します。デバッガーが再び前に進むのがわかります。

    > [!NOTE]
    > デバッガー内で編集するコードの種類によっては、警告メッセージが表示される場合があります。 一部のシナリオでは、続行する前にコードを再コンパイルする必要があります。

## <a name="step-out"></a>ステップ アウト

たとえば、`Triangle` クラス内の `Draw` メソッドの確認を終了しました。そこで、この関数からは抜け出したいけれども、デバッガーには留まっていたいとします。 これを行うには、**[ステップ アウト]** コマンドを使用します。

1. **Shift** + **F11** キーを押します (または **[デバッグ] > [ステップ アウト]** の順に選択します)。

     このコマンドを使用すると、アプリの実行が再開され (そしてデバッガーが前へ進められ)、現在の関数から制御が戻るまで続けられます。

     `Main` メソッド内の `For Each` ループに戻る必要があります。

## <a name="restart-your-app-quickly"></a>アプリを簡単に再起動する

デバッグ ツールバーにある **[再起動]** ![アプリの再起動](../debugger/media/dbg-tour-restart.png "RestartApp") ボタンをクリックします (**Ctrl** + **Shift** + **F5**)。

**[再起動]** を押すと、アプリを停止してからデバッガーを再起動する場合と比較して時間の節約になります。 デバッガーは、コードを実行すると最初にヒットするブレークポイントで一時停止します。

`shape.Draw()` メソッド上で設定したブレークポイントでデバッガーが再び停止します。

## <a name="inspect-variables-with-data-tips"></a>データ ヒントを使用して変数を確認する

変数を調べることができる機能は、デバッガーの機能の中でも最も便利な機能の 1 つに挙げられ、それを行うにはさまざまな方法を利用できます。 多くの場合、問題のデバッグを試みるときは、特定のタイミングで変数に期待する値がそのとおりに変数に格納されているかどうかの確認を試みます。

1. `shape.Draw()` メソッド上で一時停止しているときに、`shapes` オブジェクトにカーソルを合わせます。すると、そのプロパティの既定値 (`Count` プロパティ) が表示されます。

1. `shapes` オブジェクトを展開してそのプロパティをすべて表示します。たとえば、`Rectangle` の値が含まれる配列 `[0]` の最初のインデックスなどが表示されます。

     ![データ ヒントを表示する](../debugger/media/get-started-data-tip-vb.png "データ ヒントを表示する")

    さらにオブジェクトを展開することで、四角形の `Height` プロパティなどのプロパティを表示することができます。

    多くの場合、デバッグを行うときは、オブジェクト上のプロパティ値を簡単な方法で確認したいと思います。データ ヒントは、これに適した方法です。

## <a name="inspect-variables-with-the-autos-and-locals-windows"></a>[自動変数] ウィンドウと [ローカル] ウィンドウを使用して変数を確認する

1. コード エディターの下部にある **[自動変数]** ウィンドウを見てください。

     ![[自動変数] ウィンドウで変数を確認する](../debugger/media/get-started-autos-window-vb.png "[自動変数] ウィンドウ")

    **[自動変数]** ウィンドウには、変数とその現在の値が表示されます。 **[自動変数]** ウィンドウには、現在の行または前の行で使用されるすべての変数が表示されます (言語固有の動作についてはドキュメントを参照してください)。

2. 次に、**[自動変数]** ウィンドウの隣にあるタブ内の **[ローカル]** ウィンドウを見てください。

    **[ローカル]** ウィンドウを確認すれば、現在の[スコープ](https://www.wikipedia.org/wiki/Scope_(computer_science)) (現在の実行コンテキスト) に含まれている変数がわかります。

## <a name="set-a-watch"></a>ウォッチ式を設定する

1. メインのコード エディター ウィンドウで、`shapes` オブジェクトを右クリックして、**[ウォッチ式の追加]** を選択します。

    コード エディターの下部に **[ウォッチ]** ウィンドウが表示されます。 **[ウォッチ]** ウィンドウを使用することで、監視する変数 (または式) を指定できます。

    `shapes` オブジェクトに対してウォッチ式が設定されたので、デバッガー内を移動しながらその値の変化を確認することができます。 その他の変数ウィンドウとは異なり、**[ウォッチ]** ウィンドウには監視対象の変数が常に表示されます (対象外のときは淡色表示となります)。

## <a name="examine-the-call-stack"></a>呼び出し履歴を調べる

1. `For Each` ループ内で一時停止しているときに、**[呼び出し履歴]** ウィンドウをクリックします。このウィンドウは既定では右下ペイン内に表示されます。

2. コード エディター内でデバッガーが `Rectangle` クラスの `MyBase.Draw` メソッド内で一時停止するのを確認できるまで、**F11** キーを数回押します。 **[呼び出し履歴]** ウィンドウを見てください。

    ![呼び出し履歴を調べる](../debugger/media/get-started-call-stack-vb.png "ExamineCallStack")

    **[呼び出し履歴]** ウィンドウには、メソッドおよび関数が呼び出されている順番が表示されます。 先頭行には、現在の関数が表示されます (このアプリでは `Rectangle.Draw` メソッド)。 2 行目には、`Rectangle.Draw` が `Main` 関数から呼び出されたことが表示されます。3 行目以降にも同様の内容が表示されます。

   > [!NOTE]
   > **[呼び出し履歴]** ウィンドウは、Eclipse のような一部の IDE におけるデバッグ パースペクティブに似ています。

    呼び出し履歴は、アプリの実行フローを調査して理解するのに優れた方法です。

    コード行をダブルクリックすることで、ソース コードに移動できます。また、それによって、デバッガーで検査されている現在のスコープを変更することもできます。 このアクションを行っても、デバッガーは前に進みません。

    **[呼び出し履歴]** ウィンドウから右クリック メニューを使用して他の操作を行うこともできます。 たとえば、指定した関数にブレークポイントを挿入したり、**[カーソル行の前まで実行]** を使用してデバッガーを進めたり、ソース コードの調査を開始したりできます。 詳細については、[呼び出し履歴を調べる方法](../debugger/how-to-use-the-call-stack-window.md)に関するページを参照してください。

## <a name="change-the-execution-flow"></a>実行フローを変更する

1. `Rectangle` クラスの `MyBase.Draw` メソッド呼び出し内でデバッガーが一時停止した状態で、マウスを使用して左側にある黄色の矢印 (実行ポインター) をつかみ、その黄色の矢印を 1 行上にある `Console.WriteLine` メソッド呼び出しまで移動します。

1. **F11** キーを押します。

    デバッガーにより `Console.WriteLine` メソッドが返されます (コンソール ウィンドウの出力に重複する出力が表示されます)。

    実行フローを変更することにより、さまざまなコード実行パスをテストしたり、デバッガーを再起動することなくコードを再実行したりできます。

    > [!WARNING]
    > 多くの場合、この機能には注意する必要があり、ツールヒントに警告が表示されます。 他の警告が表示される場合もあります。 ポインターを移動しても、ご利用のアプリを以前のアプリ状態に戻すことはできません。

1. **F5** キーを押してアプリの実行を続行します。

    これでこのチュートリアルは完了です。

## <a name="next-steps"></a>次の手順

このチュートリアルでは、デバッガーを起動する方法、コードをステップ実行する方法、変数を確認する方法について学習しました。 必要に応じて、デバッガー機能の概要と、詳細情報へのリンクを取得します。

> [!div class="nextstepaction"]
> [デバッガーでのはじめに](../debugger/debugger-feature-tour.md)
