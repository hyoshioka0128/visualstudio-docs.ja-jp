---
title: '手順 5: NumericUpDown コントロールの Enter イベント ハンドラーの追加'
ms.date: 11/04/2016
ms.topic: tutorial
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
dev_langs:
- CSharp
- VB
ms.assetid: 45a99a5d-c881-4298-b74d-adb481dec5ee
author: ornellaalt
ms.author: ornella
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 17fb9ba8e82739ddb0a420f52b6f7f945a6454b8
ms.sourcegitcommit: 2ae2436dc3484b9dfa10e0483afba1e5a02a52eb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/25/2020
ms.locfileid: "77579832"
---
# <a name="step-5-add-enter-event-handlers-for-the-numericupdown-controls"></a>手順 5: NumericUpDown コントロールの Enter イベント ハンドラーの追加

このチュートリアルの第 5 部では、クイズ問題の解答の入力が少し楽になるように <xref:System.Windows.Forms.Control.Enter> イベント ハンドラーを追加します。 このコードは、クイズの受け手が選択して別の値の入力を開始するとすぐに、各 <xref:System.Windows.Forms.NumericUpDown> コントロールの現在の値を選択し、クリアします。

> [!NOTE]
> このトピックは、コーディングの基本概念に関するチュートリアル シリーズの一部です。 チュートリアルの概要については、「[チュートリアル 2:制限時間ありの計算クイズの作成](../ide/tutorial-2-create-a-timed-math-quiz.md)」を参照してください。

## <a name="to-verify-the-default-behavior"></a>既定の動作を確認するには

1. プログラムを実行し、クイズを開始します。

     加算問題の **NumericUpDown** コントロールで、カーソルが **0** (ゼロ) の横で点滅します。

2. 「**3**」と入力すると、コントロールが **30** を示すことに注意してください。

3. 「**5**」と入力すると **350** と表示されますが、その後すぐに **100** に変わります。

     この問題を修正する前に、状況をまとめておきましょう。 「**3**」を入力したときに **0** が消えなかった理由、および **350** が **100** にすぐに変化しなかった理由を検討します。

     この動作は不適切に見えますが、コードのロジックからすると当然です。 **[Start]** ボタンをクリックすると、**Enabled** プロパティが **False** に設定され、ボタンは淡色表示になり使用できません。 プログラムは、加算問題の NumericUpDown コントロールである、次に小さい TabIndex 値を持つコントロールに現在の選択 (フォーカス) を変更します。 **Tab** キーを使用して NumericUpDown コントロールに移動すると、カーソルはそのコントロールの先頭に自動的に移動します。このため、入力した数値が右ではなく左から入力されます。 100 に設定されている、**MaximumValue** プロパティの値を超える数を指定すると、入力した数はそのプロパティの値に置き換えられます。

## <a name="to-add-an-enter-event-handler-for-a-numericupdown-control"></a>NumericUpDown コントロールの Enter イベント ハンドラーを追加するには

1. フォームの最初の **NumericUpDown** コントロール ("sum") を選択し、次に、 **[プロパティ]** ダイアログ ボックスでツール バーの **[イベント]** アイコンをクリックします。

   ![プロパティ ツール バーのイベント ボタン](media/control-properties-events.png)

   **[プロパティ]** ダイアログ ボックスの **[イベント]** タブには、フォーム上で選択した項目に対して応答 (処理) できるイベントがすべて表示されます。 NumericUpDown コントロールを選択したため、そのコントロールに関係のあるすべてのイベントが一覧に表示されます。

2. **Enter** イベントを選択し、「`answer_Enter`」と入力して、**Enter** キーを押します。

   ![Enter イベント ハンドラーのメソッド名](media/enter-event.png)

   sum NumericUpDown コントロールの Enter イベント ハンドラーを追加し、そのハンドラーに **answer_Enter** という名前を付けます。

3. **answer_Enter** イベント ハンドラーのメソッドに、次のコードを追加します。

     [!code-vb[VbExpressTutorial3Step5_6#11](../ide/codesnippet/VisualBasic/step-5-add-enter-event-handlers-for-the-numericupdown-controls_1.vb)]
     [!code-csharp[VbExpressTutorial3Step5_6#11](../ide/codesnippet/CSharp/step-5-add-enter-event-handlers-for-the-numericupdown-controls_1.cs)]

     [!INCLUDE [devlang-control-csharp-vb](./includes/devlang-control-csharp-vb.md)]

     このコードは複雑に見えますが、順番に見ていけば理解できます。 まず、メソッドの先頭の部分 (C# の場合は `object sender`、Visual Basic の場合は `sender As System.Object`) を見てください。 このパラメーターは、sender と呼ばれる、イベントが発生しているオブジェクトを参照します。 この場合、sender オブジェクトは NumericUpDown コントロールです。 したがって、メソッドの 1 行目で、sender が汎用オブジェクトではなく、具体的に NumericUpDown コントロールであると指定します。 (NumericUpDown コントロールはいずれもオブジェクトですが、オブジェクトがすべて NumericUpDown コントロールであるとは限りません)。NumericUpDown コントロールはこのメソッドで **answerBox** と名付けられます。これは、sum NumericUpDown コントロールだけではなく、フォームのすべての NumericUpDown コントロールに使用されるためです。 このメソッドで answerBox 変数を宣言するため、そのスコープはこのメソッドにのみ適用されます。 つまり、変数はこのメソッド内でのみ使用できます。

     次の行では、answerBox がオブジェクトから NumericUpDown コントロールに正常に変換 (キャスト) されたかどうかを確認しています。 変換が成功しなかったときは、変数は `null` (C#) または `Nothing` (Visual Basic) の値になります。 3 行目は NumericUpDown コントロールに表示される解答の長さを取得し、4 行目はこの長さに基づいてコントロールの現在の値を選択します。 これで、クイズの受け手がコントロールを選択すると、Visual Studio がこのイベントを発生させ、現在の解答が選択されます。 クイズの受け手が別の解答の入力を開始するとすぐに、前の解答がクリアされて新しい解答に置き換えられます。

4. **Windows フォーム デザイナー**で、difference **NumericUpDown** コントロールを選択します。

5. **[プロパティ]** ダイアログ ボックスの **[イベント]** ページで、**Enter** イベントまでスクロールし、行の末尾にあるドロップダウン矢印をクリックし、追加した `answer_Enter` イベント ハンドラーを選択します。

6. product および quotient の各 NumericUpDown コントロールに対して、前の手順を繰り返します。

7. プログラムを保存し、実行します。

     **NumericUpDown** コントロールを選択すると、既存の値が自動的に選択され、別の値の入力を開始するとクリアされます。

## <a name="to-continue-or-review"></a>続行または確認するには

- チュートリアルの次の手順に進むには、「 **[手順 6: 減算問題を追加する](../ide/step-6-add-a-subtraction-problem.md)** 」を参照してください。

- チュートリアルの前の手順に戻るには、「[手順 4:CheckTheAnswer() メソッドの追加](../ide/step-4-add-the-checktheanswer-parens-method.md)」を参照してください。
