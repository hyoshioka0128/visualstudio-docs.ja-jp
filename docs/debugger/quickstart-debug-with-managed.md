---
title: マネージド コードをデバッグする | Microsoft Docs
description: Visual Studio デバッガーを使用して C# または Visual Basic をデバッグする
ms.custom: mvc
ms.date: 03/18/2018
ms.technology: vs-ide-debug
ms.topic: quickstart
helpviewer_keywords:
- debugger
ms.assetid: f4cea2e1-08dc-47ac-aba2-3b8c338e607f
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- dotnet
ms.openlocfilehash: e35d102a30ffc7b80d39f359542bbdc4c00feff6
ms.sourcegitcommit: a7de99f36e9ead7ea9e9bac23c88d05ddfc38b00
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/20/2018
ms.locfileid: "52257187"
---
# <a name="quickstart-debug-with-c-or-visual-basic-using-the-visual-studio-debugger"></a>クイック スタート: Visual Studio デバッガーを使用して C# または Visual Basic でデバッグする

Visual Studio デバッガーでは、アプリのデバッグに役立つ多くの強力な機能が提供されます。 このトピックでは、基本的な機能のいくつかを簡単に紹介します。

## <a name="create-a-new-project"></a>新しいプロジェクトを作成する 

1. Visual Studio で、**[ファイル]、[新しいプロジェクト]** の順に選択します。

2. **[Visual C#]** または **[Visual Basic]** の下で、**[.NET Core]** を選択し、中央のウィンドウで **[コンソール アプリ (.NET Core)]** を選びます。

     **[Console App (.NET Core)]** プロジェクト テンプレートが表示されない場合は、**[新しいプロジェクト]** ダイアログ ボックスの左側のウィンドウにある **[Visual Studio インストーラーを開く]** リンクをクリックします。 Visual Studio インストーラーが起動します。 **[.NET デスクトップ開発]** と **[.NET Core]** ワークロードを選択し、**[変更]** を選びます。

3. 「**MyDbgApp**」のような名前を入力し、**[OK]** をクリックします。

    Visual Studio によってプロジェクトが作成されます。

4. *Program.cs* または *Module1.vb* で、次のコード

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

    を、次のコードで置換します。

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

*ブレークポイント*は、Visual Studio で実行コードが中断される場所を示すマーカーです。これにより、変数の値またはメモリの動作を確認したり、コードの分岐が実行されるかどうかを確認したりすることができます。 これが、デバッグの最も基本的な機能です。

1. ブレークポイントを設定するには、`doWork` 関数呼び出しの左側の余白をクリックします (またはコード行を選択して、**F9** キーを押します)。

    ![ブレークポイントを設定する](../debugger/media/dbg-qs-set-breakpoint-csharp.png "ブレークポイントを設定する")

2. ここで **F5** キーを押します (または **[デバッグ] > [デバッグの開始]** の順に選択します)。

    ![ブレークポイントに到達する](../debugger/media/dbg-qs-hit-breakpoint-csharp.png "ブレークポイントに到達する")

    ブレークポイントを設定した場所でデバッガーが一時停止します。 デバッガーとアプリの実行が一時停止されているステートメントが、黄色の矢印で示されます。 `doWork` 関数呼び出しがある行はまだ実行されていません。

    > [!TIP]
    > ループまたは再帰処理の中にブレークポイントがある場合、または頻繁にステップ実行するブレークポイントが数多くある場合、[条件付きブレークポイント](../debugger/using-breakpoints.md#BKMK_Specify_a_breakpoint_condition_using_a_code_expression)を使用して、特定の条件が満たされる場合にのみコードが中断されるようにしてください。 条件付きブレークポイントでは時間を節約でき、再現が難しい問題をより簡単にデバッグすることもできます。

## <a name="navigate-code"></a>コード間の移動

続行するようにデバッガーに指示するためのさまざまなコマンドがあります。 ここでは、Visual Studio 2017 の新しい機能である便利なコード ナビゲーション コマンドを示します。

ブレークポイントで一時停止している間に、緑色の **[クリックで実行]** ボタン ![[クリックで実行]](../debugger/media/dbg-tour-run-to-click.png "RunToClick") が表示されるまでステートメント `c1.AddLast(20)` をポイントし、表示されたら **[クリックで実行]** ボタンを押します。

![クリックで実行](../debugger/media/dbg-qs-run-to-click-csharp.png "クリックで実行")

アプリは引き続き実行され、`doWork` が呼び出され、ボタンをクリックしたコード行で一時停止します。

コードのステップ実行に使用される一般的なキーボード コマンドには、**F10** と **F11** が含まれます。 さらに詳しい手順については、[ビギナーズ ガイド](../debugger/getting-started-with-the-debugger.md)を参照してください。

## <a name="inspect-variables-in-a-datatip"></a>データヒントの変数を検査する

1. (黄色の実行ポインターでマークされた) コードの現在の行で、`c1` オブジェクトをマウスでポイントしてデータヒントを表示します。

    ![データヒントを表示する](../debugger/media/dbg-qs-data-tip-csharp.png "データヒントを表示する")

    データヒントでは、`c1` 変数の現在の値が示され、そのプロパティを検査することができます。 デバッグ中に、予期しない値が表示される場合は、先行するコード行または呼び出しているコード行にバグがある可能性があります。 

2. データヒントを展開して、`c1` オブジェクトの現在のプロパティ値を確認します。

3. コードを実行している間に `c1` の値を引き続き表示できるようにデータヒントをピン留めする場合は、小さいピン アイコンをクリックします  (ピン留めしたデータヒントを任意の場所に移動することができます)。

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
> [デバッガー機能ツアー](../debugger/debugger-feature-tour.md)
