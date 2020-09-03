---
title: '手順 3: カウントダウン タイマーの追加 | Microsoft ドキュメント'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
ms.assetid: 62670a2b-efdc-45c6-9646-9b17eeb33dcb
caps.latest.revision: 25
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: bae5b4a81864cc591491c21218a5d8253dfc61bb
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72671839"
---
# <a name="step-3-add-a-countdown-timer"></a>手順 3: カウントダウン タイマーの追加
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このチュートリアルの第 3 部では、クイズの受け手が完了するまでの残り秒数を追跡するためのカウントダウン タイマーを追加します。

> [!NOTE]
> このトピックは、コーディングの基本概念に関するチュートリアル シリーズの一部です。 チュートリアルの概要については、「 [チュートリアル 2: 時間指定の計算クイズの作成](../ide/tutorial-2-create-a-timed-math-quiz.md)」を参照してください。

### <a name="to-add-a-countdown-timer"></a>カウントダウン タイマーを追加するには

1. 前の手順と同様に、**timeLeft** という名前の整数変数を追加します。 コードは次のようになります。

     [!code-csharp[VbExpressTutorial3Step3#5](../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial3step3/cs/form1.cs#5)]
     [!code-vb[VbExpressTutorial3Step3#5](../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial3step3/vb/form1.vb#5)]

     次に、指定した時間の後にイベントを生成する、タイマーのような、実際に秒をカウントするメソッドが必要になります。

2. デザイン ウィンドウで、ツールボックスの **[コンポーネント]** カテゴリから `Timer` コントロールをフォームに移動します。

     このコントロールは、デザイン ウィンドウの下部にある灰色の領域に表示されます。

3. フォーム上で、追加した **[timer1]** アイコンをクリックし、**Interval** プロパティを **1000** に設定します。

     間隔の値はミリ秒であるため、値が 1000 の場合は Tick イベントが毎秒生成されます。

4. フォーム上で、Timer コントロールをダブルクリックするか、または Timer コントロールをクリックして Enter キーを押します。

     コード エディターが開き、追加した Tick イベント ハンドラーのメソッドが表示されます。

5. 次のステートメントを新しいイベント ハンドラー メソッドに追加します。

     [!code-csharp[VbExpressTutorial3Step3#6](../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial3step3/cs/form1.cs#6)]
     [!code-vb[VbExpressTutorial3Step3#6](../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial3step3/vb/form1.vb#6)]

     追加されたステートメントに基づいて、タイマーは毎秒、**timeLeft** 整数変数が 0 より大きいかどうかを確認することで、残り時間がなくなっていないかどうかを確認します。 0 より大きい場合、時間はそのまま残ります。 タイマーは、まず timeLeft から 1 を減算し、次に残り秒数をクイズの受け手に示すために `timeLabel` コントロールの **Text** プロパティを更新します。

     残り時間がなくなると、タイマーは停止し、"**Time's up!**" と表示されるように `timeLabel` コントロールのテキストを変更します。 メッセージ ボックスはクイズが終了したことを知らせ、この場合、解答は addend1 と addend2 を加算することによって表示されます。 `startButton` コントロールの **Enabled** プロパティは、クイズの受け手が別の問題を開始できるように `true` に設定されます。

     ここでは、`if else` ステートメントを追加しました。これは、プログラムで条件判断を行うように指定するためのステートメントです。 `if else` ステートメントは次のようになります。

    > [!NOTE]
    > 次の例は例示のみを目的としています。プロジェクトに追加しないでください。

    ```vb
    If (something that your program will check) Then
        ' One or more statements that will run
        ' if what the program checked is true.
    Else
        ' One or more statements that will run
        ' if what the program checked is false.
    End If
    ```

    ```csharp
    if (something that your program will check)
    {
        // One or more statements that will run
        // if what the program checked is true.
    }
    else
    {
        // One or more statements that will run
        // if what the program checked is false.
    }
    ```

     加算問題の解答を表示するために `else` ブロックに追加したステートメントについて詳しく見てみましょう。

     [!code-csharp[VbExpressTutorial3Step3#24](../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial3step3/cs/form1.cs#24)]
     [!code-vb[VbExpressTutorial3Step3#24](../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial3step3/vb/form1.vb#24)]

     ステートメント `addend1 + addend2` は 2 つの変数の値を加算します。 最初の部分 (`sum.Value`) は、sum `NumericUpDown` コントロールの **Value** プロパティを使用して正しい解答を表示します。 クイズの解答を確認するために後で同じプロパティを使用します。

     `NumericUpDown` コントロールを使用するとクイズの受け手がさらに簡単に数値を入力できるので、これを計算問題の解答のために使用します。 解答となる可能性があるものはすべて、0 ～ 100 の整数です。 **[最小値]** 、 **[最大値]** 、および **[DecimalPlaces]** の各プロパティの既定値を残しておくと、クイズの受け手は小数、負の値、大きすぎる数を入力できなくなります (クイズの受け手が 3.141 は入力できるが、3.1415 は入力できないようにする場合は、**DecimalPlaces** プロパティを 3 に設定します)。

6. `StartTheQuiz()` メソッドの最後に 3 行のコードを追加します。コードは次のようになります。

     [!code-csharp[VbExpressTutorial3Step3#7](../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial3step3/cs/form1.cs#7)]
     [!code-vb[VbExpressTutorial3Step3#7](../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial3step3/vb/form1.vb#7)]

     これで、クイズの開始時に、**timeLeft** 変数が 30 に設定され、`timeLabel` コントロールの **Text** プロパティが 30 seconds に変更されます。 次に、`Timer` コントロールの `Start()` メソッドがカウントダウンを開始します  (解答の確認は次の手順で設定するため、まだ行われません)。

7. プログラムを保存し、実行して、フォームの **[Start]** ボタンをクリックします。

     タイマーはカウント ダウンを開始します。 残り時間がなくなると、クイズが終了し、答えが表示されます。 次の図は実行中のクイズを示します。

     ![実行中の計算クイズ](../ide/media/express-addcountdown.png "Express_AddCountdown") 実行中の計算クイズ

### <a name="to-continue-or-review"></a>続行または確認するには

- チュートリアルの次の手順に進むには、「 [手順 4: CheckTheAnswer () メソッドの追加](../ide/step-4-add-the-checktheanswer-parens-method.md)」を参照してください。

- チュートリアルの前の手順に戻るには、「 [手順 2: ランダムな加算問題の作成](../ide/step-2-create-a-random-addition-problem.md)」を参照してください。
