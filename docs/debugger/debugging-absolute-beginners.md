---
title: 超初心者のためのコードのデバッグ
description: 初めてデバッグを行う場合は、いくつかの原則を理解していると、Visual Studio を使用してデバッグ モードでアプリを実行するときに役に立ちます
ms.date: 02/14/2020
ms.topic: tutorial
helpviewer_keywords:
- debugger
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5c3cf9d5e4d72ed316344d1bda930d0416e9efe5
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/20/2020
ms.locfileid: "77416397"
---
# <a name="how-to-debug-for-absolute-beginners"></a>超初心者でもわかるデバッグ方法

間違いなく、ソフトウェア開発者が記述したコードが意図したとおりに動くことはありません。 まったく違うことを行うときさえあります。 そのようなことが起きたときの次のタスクは、原因を究明することです。その場合、何時間もただコードを見つめてしまいがちですが、デバッグ用のツールつまりデバッガーを使用する方がはるかに簡単で効率的です。

残念ながら、デバッガーは、コードに存在するすべての問題つまり "バグ" を明らかにしてくれる魔法のようなものではありません。 "*デバッグ*" とは、Visual Studio のようなデバッグ ツールでコードを 1 ステップずつ実行し、プログラミングが間違っている箇所を正確に発見することです。 次に、行う必要があるコード修正を理解しますが、多くの場合、デバッグ ツールでは、プログラムの実行を続けながら、一時的に変更してみることができます。

デバッガーを効果的に使用することは、時間をかけて練習して習得しなければならないスキルですが、結局は、すべてのソフトウェア開発者にとって基本的なタスクです。 この記事では、デバッグの中核となる原則を紹介し、始めるためのヒントを提供します。

## <a name="clarify-the-problem-by-asking-yourself-the-right-questions"></a>適切な質問を自問して問題を明確化する

修正を試みる前に、直面している問題を明確にするのは役に立つことです。 既にコードで問題が発生していることでしょう。そうでなければ、ここでデバッグ方法を知ろうなどとしていないはずです。 ですから、デバッグを始める前に、解決しようとしている問題が明らかになっていることを確認してください。

* コードで何を行おうとしましたか?

* 代わりにどのようなことが発生しましたか?

    アプリの実行中にエラー (例外) が発生した場合、それは良いことである可能性があります。 例外とはコードを実行すると発生する予期しないイベントであり、通常は何らかの種類のエラーです。 デバッグ ツールを使用すると、例外が発生したコード内の場所を正確に特定でき、考えられる修正方法を調査するのに役立ちます。

    何か他のことが発生した場合は、問題はどのような症状ですか。 この問題が発生したコード内の場所に、既に心当たりがありますか。 たとえば、コードでテキストを表示していて、テキストが正しくない場合は、データが正しくないか、または表示するテキストを設定するコードに何らかのバグがあることがわかります。 デバッガーでコードをステップ実行することにより、変数に対するすべての変更を個別に調べて、正しくない値が割り当てられるタイミングと方法を正確に発見できます。

## <a name="examine-your-assumptions"></a>前提を調べる

バグまたはエラーを調査する前に、特定の結果を想定するに至った前提を考えてください。 隠れた前提や未知の前提があると、デバッガーで問題の原因を究明しようとしても、問題の識別が妨げられる可能性があります。 可能性のある前提のリストは長くなるかもしれません。 前提を検討するために自問してみるとよい質問をいくつか次に示します。

* 適切な API を使用していますか (つまり、正しいオブジェクト、関数、メソッド、プロパティ)。 意図したものとは異なることを行う API を使用しているかもしれません。 (デバッガーで API の呼び出しを調べた後、それを修正するため、ドキュメントに移動して正しい API を確認することが必要な場合があります。)

* API を正しく使用していますか。 正しい API を使用していても、使い方が正しくない可能性があります。

* コードにタイプミスが含まれていませんか。 変数名の単純なスペルミスのような一部のタイプミスは、発見するのが難しい場合があります。変数を使用する前に宣言する必要がない言語を使用している場合は、特にそうです。

* コードの変更を行っており、それは発生している問題に関係がないと想定しましたか。

* オブジェクトまたは変数に含まれると想定した特定の値 (または特定の型の値) が、実際に発生する値と異なっていましたか。

* コードの意図がわかっていますか。 通常、他の人のコードをデバッグする方が難しいものです。 自分のコードではない場合、効率よくデバッグするには、先に時間をかけてコードで行われていることを正確に理解することが必要になる場合があります。

    > [!TIP]
    > コードを作成するときは、小さくて動作するコードから始めるようにします。 (適切なコードの例を後で示します。)場合によっては、実現しようとしている中心的タスクを示すコードの小さなまとまりから始めた方が、大規模または複雑なコードのセットの修正が容易になります。 その後、段階的にコードを変更または追加し、各ポイントでエラーをテストできます。

前提を確認することにより、コード内の問題の発見に要する時間を短縮できます。 また、問題の解決にかかる時間も削減できます。

## <a name="step-through-your-code-in-debugging-mode-to-find-where-the-problem-occurred"></a>デバッグ モードでコードをステップ実行して問題の発生場所を発見する

アプリを普通に実行した場合、エラーや不正な結果はコードが実行された後でしか表示されません。 プログラムが理由を示すことなく予期せず終了する可能性もあります。

デバッガー内でアプリを実行すると ("*デバッグ モード*" とも呼ばれます)、プログラムの実行中に発生するすべてのことをデバッガーが能動的に監視します。 また、いつでもアプリを一時停止して状態を調べた後、コードを 1 行ずつステップ実行して発生するすべてのことを詳しく確認できます。

Visual Studio でデバッグ モードに入るには、**F5** キー (または、[デバッグ] ツール バーで **[デバッグ]**  >  **[デバッグの開始]** メニュー コマンドか、 **[デバッグの開始]** ボタン ![デバッグの開始](../debugger/media/dbg-tour-start-debugging.png "デバッグの開始")) を使用します。 例外が発生した場合、Visual Studio の例外ヘルパーによって、例外が発生した正確な地点に移動し、他の有用な情報が提供されます。 コード内で例外を処理する方法の詳細については、[デバッグのテクニックとツール](../debugger/write-better-code-with-visual-studio.md)に関するページを参照してください。

例外が発生しなかった場合は、おそらく、コード内で問題を探すべき場所について、開発者によい考えがあることでしょう。 その場合は、デバッガーで "*ブレークポイント*" を使用して、コードをより注意深く調べることができます。 ブレークポイントは、信頼できるデバッグの最も基本的で重要な機能です。 ブレークポイントは、Visual Studio が実行中のコードを一時停止する場所を示します。これにより、変数の値、メモリの動作、コード実行のシーケンスなどを確認できます。

Visual Studio では、コード行の左にある余白をクリックして、ブレークポイントを簡単に設定できます。 または、行にカーソルを置いて、**F9** キーを押します。

これらの概念を示すため、既にバグがいくつかあるコード例を使って説明します。 ここでは C# を使いますが、デバッグ機能は Visual Basic、C++、JavaScript、Python、その他のサポートされている言語にも適用されます。

### <a name="create-a-sample-app-with-some-bugs"></a>サンプル アプリを作成する (バグを含むもの)

次に、バグがいくつか含まれるアプリケーションを作成します。

1. Visual Studio をインストールし、作成するアプリの種類に応じて、 **.NET デスクトップ開発**ワークロードまたは **.NET Core クロス プラットフォーム開発**ワークロードをインストールする必要があります。

    Visual Studio をまだインストールしていない場合は、 [Visual Studio のダウンロード](https://visualstudio.microsoft.com/downloads/)  ページに移動し、無料試用版をインストールしてください。

    Visual Studio は既にインストールされていて、ワークロードだけをインストールする必要がある場合は、 **[ツール]**  >  **[ツールと機能を取得]** の順にクリックします。 Visual Studio インストーラーが起動します。 **[.NET デスクトップ開発]** または **[.NET Core クロスプラットフォームの開発]** ワークロードを選択し、 **[変更]** を選択します。

1. Visual Studio を開きます。

    ::: moniker range=">=vs-2019"
    スタート ウィンドウで、 **[新しいプロジェクトの作成]** を選択します。 検索ボックスに「**コンソール**」と入力し、 **[コンソール アプリ (.NET Core)]** または **[コンソール アプリ (.NET Framework)]** のいずれかを選択します。 **[次へ]** をクリックします。 **ConsoleApp-FirstApp** のようなプロジェクト名を入力して、 **[作成]** をクリックします。
    ::: moniker-end
    ::: moniker range="vs-2017"
    上部のメニュー バーから、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** の順に選択します。 **[新しいプロジェクト]** ダイアログ ボックスの左側のウィンドウで、 **[Visual C#]** の下にある **[コンソール アプリ]** を選択し、次に真ん中のウィンドウで **[コンソール アプリ (.NET Framework)]** または **[コンソール アプリ (.NET Core)]** のいずれかを選択します。 **ConsoleApp-FirstApp** のような名前を入力して、 **[OK]** をクリックします。
    ::: moniker-end

    **[コンソール アプリ (.NET Framework)]** または **[コンソール アプリ (.NET Core)]** プロジェクト テンプレートが表示されない場合は、 **[ツール]**  >  **[ツールと機能を取得]** に移動して、Visual Studio インストーラーを開きます。 **[.NET Core クロスプラットフォームの開発]** ワークロードまたは **[.NET デスクトップ開発]** ワークロードのいずれかを選択して、 **[変更]** を選択します。

    Visual Studio によってコンソール プロジェクトが作成され、ソリューション エクスプローラーの右側のウィンドウに表示されます。

1. *Program.cs* で、既定のすべてのコードを次のコードに置き換えます。

    ```csharp
    using System;
    using System.Collections.Generic;

    namespace ConsoleApp_FirstApp
    {
        class Program
        {
            static void Main(string[] args)
            {
                Console.WriteLine("Welcome to Galaxy News!");
                IterateThroughList();
                Console.ReadKey();
            }

            private static void IterateThroughList()
            {
                var theGalaxies = new List<Galaxy>
            {
                new Galaxy() { Name="Tadpole", MegaLightYears=400, GalaxyType=new GType('S')},
                new Galaxy() { Name="Pinwheel", MegaLightYears=25, GalaxyType=new GType('S')},
                new Galaxy() { Name="Cartwheel", MegaLightYears=500, GalaxyType=new GType('L')},
                new Galaxy() { Name="Small Magellanic Cloud", MegaLightYears=.2, GalaxyType=new GType('I')},
                new Galaxy() { Name="Andromeda", MegaLightYears=3, GalaxyType=new GType('S')},
                new Galaxy() { Name="Maffei 1", MegaLightYears=11, GalaxyType=new GType('E')}
            };

                foreach (Galaxy theGalaxy in theGalaxies)
                {
                    Console.WriteLine(theGalaxy.Name + "  " + theGalaxy.MegaLightYears + ",  " + theGalaxy.GalaxyType);
                }

                // Expected Output:
                //  Tadpole  400,  Spiral
                //  Pinwheel  25,  Spiral
                //  Cartwheel, 500,  Lenticular
                //  Small Magellanic Cloud .2,  Irregular
                //  Andromeda  3,  Spiral
                //  Maffei 1,  11,  Elliptical
            }
        }

        public class Galaxy
        {
            public string Name { get; set; }

            public double MegaLightYears { get; set; }
            public object GalaxyType { get; set; }

        }

        public class GType
        {
            public GType(char type)
            {
                switch(type)
                {
                    case 'S':
                        MyGType = Type.Spiral;
                        break;
                    case 'E':
                        MyGType = Type.Elliptical;
                        break;
                    case 'l':
                        MyGType = Type.Irregular;
                        break;
                    case 'L':
                        MyGType = Type.Lenticular;
                        break;
                    default:
                        break;
                }
            }
            public object MyGType { get; set; }
            private enum Type { Spiral, Elliptical, Irregular, Lenticular}
        }
    }
    ```

    このコードの意図は、銀河の名前、銀河までの距離、銀河の種類をすべて一覧に表示することです。 デバッグするには、コードの意図を理解することが重要です。 出力で表示する一覧の 1 行の形式を次に示します。

    "*銀河の名前*", "*距離*", "*銀河の種類*"

### <a name="run-the-app"></a>アプリを実行する

1. **F5** キーを押すか、またはコード エディターの上にある [デバッグ] ツール バーの **[デバッグの開始]** ボタン ![デバッグの開始](../debugger/media/dbg-tour-start-debugging.png "デバッグの開始") を選択します。

    アプリが開始し、デバッガーでは例外は表示されません。 しかし、コンソール ウィンドウに表示される出力は、予想したものではありません。 予想される出力を次に示します。

    ```
    Tadpole  400,  Spiral
    Pinwheel  25,  Spiral
    Cartwheel, 500,  Lenticular
    Small Magellanic Cloud .2,  Irregular
    Andromeda  3,  Spiral
    Maffei 1,  Elliptical
    ```

    しかし、代わりに次のように表示されます。

    ```
    Tadpole  400,  ConsoleApp_FirstApp.GType
    Pinwheel  25,  ConsoleApp_FirstApp.GType
    Cartwheel, 500,  ConsoleApp_FirstApp.GType
    Small Magellanic Cloud .2,  ConsoleApp_FirstApp.GType
    Andromeda  3,  ConsoleApp_FirstApp.GType
    Maffei 1, 11,  ConsoleApp_FirstApp.GType
    ```

    出力とコードを調べると、`GType` が銀河の種類を格納しているクラスの名前であることがわかります。 表示しようとしているのは、実際の銀河の種類 ("Spiral" など) であって、クラス名ではありません。

### <a name="debug-the-app"></a>アプリをデバッグする

1. アプリを実行したまま、`Console.WriteLine` メソッドを呼び出している次のコード行の左側の余白をクリックして、ブレークポイントを設定します。

    ```csharp
    foreach (Galaxy theGalaxy in theGalaxies)
    {
        Console.WriteLine(theGalaxy.Name + "  " + theGalaxy.MegaLightYears + ",  " + theGalaxy.GalaxyType);
    }
    ```

    ブレークポイントを設定すると、左側の余白に赤い点が表示されます。

    出力に問題があるので、出力を設定する前記のコードをデバッガーで調べることによりデバッグを始めます。

1. [デバッグ] ツール バーの **[再起動]** ![アプリの再起動](../debugger/media/dbg-tour-restart.png "RestartApp") ボタンをクリックします (**Ctrl** + **Shift** + **F5** キー)。

    設定したブレークポイントでアプリが一時停止します。 黄色の強調表示は、デバッガーが一時停止していることを示します (黄色のコード行はまだ実行されていません)。

1. 右側の `GalaxyType` 変数をポイントし、レンチのアイコンの左側の `theGalaxy.GalaxyType` を展開します。 `GalaxyType` にはプロパティ `MyGType` が含まれ、プロパティの値が `Spiral` に設定されていることがわかります。

    ![変数を調べる](../debugger/media/beginners-inspect-variable.png)

    "Spiral" は、コンソールに出力することを想定していた実際に正しい値です。 アプリの実行中にこのコードのこの値にアクセスできるのは、良いスタートです。 このシナリオでは、正しくない API を使用しています。 デバッガーでコードを実行しながらこれを修正できるかどうかを見ていきます。

1. 同じコードで、まだデバッグしながら、カーソルを `theGalaxy.GalaxyType` の最後に置いて、`theGalaxy.GalaxyType.MyGType` に変更します。 この変更を行うことはできますが、コード エディターには、このコードをコンパイルできないことを示すエラーが表示されます。

    ![構文エラー](../debugger/media/beginners-edit.png)

1. **[エディット コンティニュ]** メッセージ ボックスで、 **[編集]** をクリックします。 **[エラー一覧]** ウィンドウにエラー メッセージが表示されるようになります。 エラーでは、`'object'` に `MyGType` の定義が含まれていないことが示されます。

    ![構文エラー](../debugger/media/beginners-no-definition.png)

    各銀河を `GType` 型のオブジェクト (`MyGType` プロパティを含みます) で設定しましたが、デバッガーは `theGalaxy` オブジェクトを `GType` 型のオブジェクトとして認識していません。 何が起こっているのでしょうか。 銀河の種類を設定しているコードを調べてみます。 そうすると、`GType` クラスには確かに `MyGType` のプロパティがありますが、どこかにおかしなところがあります。 `object` に関するエラー メッセージが手掛かりになります。言語インタープリターに対しては、種類は `GType` 型のオブジェクトではなく `object` 型のオブジェクトとして認識されています。

1. 銀河の種類の設定に関するコードを調べると、`Galaxy` クラスの `GalaxyType` プロパティが、`GType` ではなく `object` として指定されていることがわかります。

    ```csharp
    public object GalaxyType { get; set; }
    ```

1. 上記のコードを次のように変更します。

    ```csharp
    public GType GalaxyType { get; set; }
    ```

1. [デバッグ] ツール バーにある **[再起動]** ![アプリの再起動](../debugger/media/dbg-tour-restart.png "RestartApp") ボタンをクリックし (**Ctrl** + **Shift** + **F5** キー)、コードを再コンパイルして再起動します。

    デバッガーが `Console.WriteLine` で一時停止したら、`theGalaxy.GalaxyType.MyGType` をポイントして、値が正しく設定されていることを確認します。

1. 左側の余白でブレークポイントの円をクリックしてブレークポイントを削除し (または、右クリックして **[ブレークポイント]**  >  **[ブレークポイントの削除]** を選択)、**F5** キーを押して続行します。

    アプリが実行して、出力を表示します。 今度は問題ないようですが、1 つ気付いたことがあります。コンソール出力では Small Magellanic Cloud 銀河は Irregular 銀河として表示されるようにしたかったのですが、銀河の種類には何も表示されていません。

    ```
    Tadpole  400,  Spiral
    Pinwheel  25,  Spiral
    Cartwheel, 500,  Lenticular
    Small Magellanic Cloud .2,
    Andromeda  3,  Spiral
    Maffei 1,  Elliptical
    ```

1. このコード行にブレークポイントを設定します。

    ```csharp
    public GType(char type)
    ```

    このコードで銀河の種類を設定しているので、それを詳しく調べます。

1. [デバッグ] ツール バーの **[再起動]** ![アプリの再起動](../debugger/media/dbg-tour-restart.png "RestartApp") ボタンをクリックし (**Ctrl** + **Shift** + **F5** キー)、再起動します。

    ブレークポイントを設定したコード行で、デバッガーが一時停止します。

1. `type` 変数をポイントします。 `S` という値が (文字コードの後に) 表示されます。 銀河の種類 Irregular は `I` で表されることがわかっているので、この値に関心があります。

1. **F5** キーを押して、再び `type` 変数をポイントします。 `type` 変数の値が `I` になるまで、この手順を繰り返します。

    ![変数を調べる](../debugger/media/beginners-inspecting-data.png)

1. 次に、**F11** キーを押します ( **[デバッグ]**  >  **[ステップ イン]** またはデバッグ ツール バーの **[ステップ イン]** ボタン)。

    **F11** キーを押すと、デバッガーは一度に 1 ステートメント進みます (そしてコードを実行します)。 **F10** キー (**ステップ オーバー**) も似たコマンドであり、どちらもデバッガーの使用方法を学習するときに非常に役に立ちます。

1. **F11** キーを繰り返し押して、値 "I" に対する `switch` ステートメントでコード行を停止します。 ここで、タイプミスによって問題が発生していることがはっきりします。 `MyGType` を銀河の種類 Irregular に設定するコードに進んで欲しいのですが、デバッガーは代わりにこのコードを完全にスキップして、`switch` ステートメントの `default` セクションで一時停止します。

    ![タイプミスを探す](../debugger/media/beginners-typo.png)

    コードを調べると、`case 'l'` ステートメントにタイプミスがあることがわかります。 これは、`case 'I'` である必要があります。

1. `case 'l'` のコードをクリックして、`case 'I'` に置き換えます。

1. ブレークポイントを削除し、 **[再起動]** ボタンをクリックしてアプリを再起動します。

    バグが修正され、予期した出力が表示されます。

    任意のキーを押してアプリを終了します。

## <a name="summary"></a>まとめ

問題が見つかったら、デバッガーと **F10** や **F11** などの[ステップ コマンド](../debugger/navigating-through-code-with-the-debugger.md)を使用して、問題のあるコードの領域を探します。

> [!NOTE]
> 問題が発生しているコードの領域を特定するのが困難な場合は、問題が発生する前に実行されるコードにブレークポイントを設定した後、問題の兆候が現れるまでステップ コマンドを使用します。 [トレースポイント](../debugger/using-breakpoints.md#BKMK_Print_to_the_Output_window_with_tracepoints)を使用して、 **[出力]** ウィンドウにメッセージを表示することもできます。 表示されたメッセージを見る (そして、まだ表示されていないメッセージに注意する) ことで、多くの場合、問題のあるコードの領域を分離できます。 このプロセスを複数回繰り返して、絞り込むことが必要な場合があります。

問題のあるコードの領域が見つかったら、デバッガーを使用して調査します。 問題の原因を見つけるには、デバッガーでアプリを実行しながら問題のあるコードを調べます。

* [変数を検査](../debugger/view-data-values-in-data-tips-in-the-code-editor.md)し、含まれていなければならない型の値が含まれているかどうかを確認します。 不正な値が見つかった場合は、不正な値が設定された場所を探します (値が設定された場所を探すには、デバッガーの再起動、[呼び出し履歴](../debugger/how-to-use-the-call-stack-window.md)の確認、またはその両方が必要な場合があります)。

* アプリケーションで想定されたコードが実行されているかどうかを確認します。 (たとえば、サンプル アプリケーションでは、銀河の種類を Irregular に設定する switch ステートメントのコードが想定されましたが、タイプミスのためにアプリはそのコードをスキップしていました。)

> [!TIP]
> バグを見つけるにはデバッガーが役に立ちます。 デバッグ ツールは、コードの意図がわかっている場合にのみ、"*自動的に*" バグを発見できます。 開発者がその意図を表現した場合にのみ、ツールはコードの意図を認識できます。 それを行う方法は、[単体テスト](../test/improve-code-quality.md)を書くことです。

## <a name="next-steps"></a>次の手順

この記事では、いくつかの一般的なデバッグの概念を学びました。 次は、デバッガーに関する詳細の学習を開始できます。

> [!div class="nextstepaction"]
> [デバッガーでのはじめに](../debugger/debugger-feature-tour.md)
