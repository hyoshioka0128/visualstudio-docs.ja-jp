---
title: マネージド コードをデバッグする | Microsoft Docs
description: Visual Studio デバッガーを使用して C# または Visual Basic をデバッグする
ms.custom: mvc
ms.date: 03/18/2018
ms.topic: quickstart
helpviewer_keywords:
- debugger
ms.assetid: f4cea2e1-08dc-47ac-aba2-3b8c338e607f
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- dotnet
ms.openlocfilehash: f790d30dc97d5549737c3c1cd003086477ce984f
ms.sourcegitcommit: 5654b7a57a9af111a6f29239212d76086bc745c9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/03/2021
ms.locfileid: "101683019"
---
# <a name="quickstart-debug-with-c-or-visual-basic-using-the-visual-studio-debugger"></a>クイック スタート: Visual Studio デバッガーを使用して C# または Visual Basic でデバッグする

Visual Studio デバッガーでは、アプリのデバッグに役立つ多くの強力な機能が提供されます。 このトピックでは、基本的な機能のいくつかを簡単に紹介します。

## <a name="create-a-new-project"></a>新しいプロジェクトを作成する

1. Visual Studio を起動し、新しいプロジェクトを作成します。

    ::: moniker range=">=vs-2019"
    スタート ウィンドウが開いていない場合は、 **[ファイル]**  >  **[スタート ウィンドウ]** を選択します。 スタート ウィンドウで、 **[新しいプロジェクトの作成]** を選択します。

    **[新しいプロジェクトの作成]** ウィンドウで、検索ボックスに「*コンソール*」と入力またはタイプします。 次に、言語のリストから **[C#]** を選択して、プラットフォームのリストから **[Windows]** を選択します。

    言語およびプラットフォームのフィルターを適用してから、.NET Core 用の **[コンソール アプリ]** テンプレートを選択して、 **[次へ]** を選択します。

    推奨されるターゲット フレームワーク (.NET Core 3.1) または .NET 5 を選択し、 **[作成]** を選択します。

    .NET Core 用の **[コンソール アプリ]** プロジェクト テンプレートが表示されない場合は、 **[ツール]**  >  **[ツールと機能を取得...]** に移動して、Visual Studio インストーラーを開きます。 **[.NET Core クロスプラットフォームの開発]** ワークロードを選択し、 **[変更]** を選択します。
    ::: moniker-end
    ::: moniker range="vs-2017"
    上部のメニュー バーから、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** の順に選択します。 **[新しいプロジェクト]** の左側のウィンドウで、**[Visual C#]** の下にある **[.NET Core]** を選択し、次に、真ん中のウィンドウで **[コンソール アプリ (.NET Core)]** を選択します。 次に、「**MyDbgApp**」のような名前を入力し、**[OK]** をクリックします。

    **[コンソール アプリ (.NET Core)]** プロジェクト テンプレートが表示されない場合は、**[ツール]** > **[ツールと機能を取得...]** に移動して、Visual Studio インストーラーを開きます。 **[.NET Core クロスプラットフォームの開発]** ワークロードを選択し、 **[変更]** を選択します。
    ::: moniker-end

    Visual Studio によってプロジェクトが作成されます。

1. *Program.cs* または *Module1.vb* で、次のコード

    ```csharp
    class Program
    {
        static void Main(string[] args)
        {
        }
    }
    ```

    ```vb
    Module Module1
        Sub Main()
        End Sub
    End Module
    ```

    次のコードに置き換えます。

    ```csharp
    class Program
    {
        private static void doWork()
        {
            LinkedList<int> c1 = new LinkedList<int>();

            c1.AddLast(10);
            c1.AddLast(20);

            LinkedList<int> c2 = new LinkedList<int>(c1);
            int i = c2.First.Value;
            int j = c2.First.Value;
            Console.Write("The first element is ");
            Console.Write(i);
            Console.Write("\n");
            Console.Write("The second element is ");
            Console.Write(j);
            Console.Write("\n");

        }

        static int Main()
        {
            // using namespace std;
            doWork();
            return 0;

        }
    }
    ```

    ```vb
    Imports System.Collections.Generic

    Namespace MyDbgApp
        Class Program
            Private Shared Sub doWork()
                Dim c1 As New LinkedList(Of Integer)()

                c1.AddLast(10)
                c1.AddLast(20)

                Dim c2 As New LinkedList(Of Integer)(c1)
                Dim i As Integer = c2.First.Value
                Dim j As Integer = c2.First.Value
                Console.Write("The first element is ")
                Console.Write(i)
                Console.Write(vbLf)
                Console.Write("The second element is ")
                Console.Write(j)
                Console.Write(vbLf)

            End Sub

            Public Shared Function Main() As Integer
                ' using namespace std;
                doWork()
                Return 0

            End Function
        End Class
    End Namespace
    ```

    > [!NOTE]
    > Visual Basic で、スタートアップ オブジェクトが `Sub Main` に設定されていることを確認します (**[プロパティ]、[アプリケーション]、[スタートアップ オブジェクト]**)。

## <a name="set-a-breakpoint"></a>ブレークポイントの設定

*ブレークポイント* は、Visual Studio で実行コードが中断される場所を示すマーカーです。これにより、変数の値またはメモリの動作を確認したり、コードの分岐が実行されるかどうかを確認したりすることができます。 これが、デバッグの最も基本的な機能です。

1. ブレークポイントを設定するには、`doWork` 関数呼び出しの左側の余白をクリックします (またはコード行を選択して、**F9** キーを押します)。

    ![ブレークポイントを設定する](../debugger/media/dbg-qs-set-breakpoint-csharp.png "ブレークポイントの設定")

2. ここで **F5** キーを押します (または **[デバッグ] > [デバッグの開始]** の順に選択します)。

    ![ブレークポイントに到達する](../debugger/media/dbg-qs-hit-breakpoint-csharp.png "ブレークポイントに到達する")

    ブレークポイントを設定した場所でデバッガーが一時停止します。 デバッガーとアプリの実行が一時停止されているステートメントが、黄色の矢印で示されます。 `doWork` 関数呼び出しがある行はまだ実行されていません。

    > [!TIP]
    > ループまたは再帰処理の中にブレークポイントがある場合、または頻繁にステップ実行するブレークポイントが数多くある場合、[条件付きブレークポイント](../debugger/using-breakpoints.md#BKMK_Specify_a_breakpoint_condition_using_a_code_expression)を使用して、特定の条件が満たされる場合にのみコードが中断されるようにしてください。 条件付きブレークポイントでは時間を節約でき、再現が難しい問題をより簡単にデバッグすることもできます。

## <a name="navigate-code"></a>コード間の移動

続行するようにデバッガーに指示するためのさまざまなコマンドがあります。 ここでは、Visual Studio 2017 以降で使用できる便利なコード ナビゲーション コマンドを示します。

ブレークポイントで一時停止している間に、緑色の **[クリックで実行]** ボタン ![[クリックで実行]](../debugger/media/dbg-tour-run-to-click.png "RunToClick") が表示されるまでステートメント `c1.AddLast(20)` をポイントし、表示されたら **[クリックで実行]** ボタンを押します。

![クリックで実行](../debugger/media/dbg-qs-run-to-click-csharp.png "クリックで実行")

アプリは引き続き実行され、`doWork` が呼び出され、ボタンをクリックしたコード行で一時停止します。

コードのステップ実行に使用される一般的なキーボード コマンドには、**F10** と **F11** が含まれます。 詳しい手順については、「[デバッガーでのはじめに](../debugger/debugger-feature-tour.md)」をご覧ください。

## <a name="inspect-variables-in-a-data-tip"></a>データ ヒントで変数を検査する

1. (黄色の実行ポインターでマークされた) 現在のコード行で、`c1` オブジェクトをマウスでポイントしてデータ ヒントを表示します。

    ![データ ヒントを表示する](../debugger/media/dbg-qs-data-tip-csharp.png "データ ヒントを表示する")

    データ ヒントには `c1` 変数の現在の値が表示され、そのプロパティを調べることができます。 デバッグ中に、予期しない値が表示される場合は、先行するコード行または呼び出しているコード行にバグがある可能性があります。

2. データ ヒントを展開して、`c1` オブジェクトの現在のプロパティ値を確認します。

3. コードを実行している間に `c1` の値を引き続き表示できるようにデータ ヒントをピン留めする場合は、小さいピン アイコンをクリックします。 (ピン留めしたデータ ヒントを任意の場所に移動することができます。)

## <a name="edit-code-and-continue-debugging"></a>コードを編集してデバッグを続行する

デバッグ セッションの途中にコードでテストする変更を識別する場合は、そのようにすることもできます。

1. `c2.First.Value` の 2 番目のインスタンスをクリックし、`c2.First.Value` を `c2.Last.Value` に変更します。

2. **F10** キー (または **[デバッグ] > [ステップ オーバー]**) を数回押して、デバッガーを進めて編集したコードを実行します。

    ![エディット コンティニュ](../debugger/media/dbg-qs-edit-and-continue-csharp.gif "エディット コンティニュ")

    **F10** キーでは、デバッガーは一度に 1 ステートメントずつ進みますが、関数をステップインするのではなく、ステップ オーバーします (スキップしたコードがまだ実行される)。

エディット コンティニュの使用および機能制限の詳細については、[エディット コンティニュ](../debugger/edit-and-continue.md)に関するページを参照してください。

## <a name="next-steps"></a>次の手順

このチュートリアルでは、デバッガーを起動する方法、コードをステップ実行する方法、変数を確認する方法について学習しました。 必要に応じて、デバッガー機能の概要と、詳細情報へのリンクを取得します。

> [!div class="nextstepaction"]
> [デバッガーでのはじめに](../debugger/debugger-feature-tour.md)
