---
title: '手順 6: タイマーの追加'
ms.date: 11/04/2016
ms.topic: tutorial
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
dev_langs:
- CSharp
- VB
ms.assetid: 09e7930b-cab6-4a22-9a6f-72e23f489585
author: ornellaalt
ms.author: ornella
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 23d050df688d4d1efec75245e6f48d748464170c
ms.sourcegitcommit: 2ae2436dc3484b9dfa10e0483afba1e5a02a52eb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/25/2020
ms.locfileid: "77579313"
---
# <a name="step-6-add-a-timer"></a>手順 6: タイマーの追加
次に、絵合わせゲームに <xref:System.Windows.Forms.Timer> コントロールを追加します。 タイマーは、指定されたミリ秒間待機してから、*ティック*と呼ばれるイベントを発生させます。 タイマーは、アクションを開始したり定期的に繰り返したりする場合に便利です。 ここではタイマーの使用例として、プレーヤーが 2 つのアイコンを選択し、アイコンが一致しない場合は、短時間の経過後にその 2 つのアイコンが再び非表示になるようにします。

## <a name="to-add-a-timer"></a>タイマーを追加するには

1. **Windows フォーム デザイナー**のツール ボックスから、( **[コンポーネント]** カテゴリ内の) **[タイマー]** を選択して **Enter** キーを押すか、タイマーをダブルクリックして、タイマー コントロールをフォームに追加します。 次の図で示されているように、タイマーのアイコンが **[Timer1]** という名前で、フォームの下の領域に表示されます。

     ![タイマー](../ide/media/express_timer.png)<br/>
***タイマー***

    > [!NOTE]
    > ツール ボックスが空の場合は、フォームのコードではなくフォーム デザイナーを選択してから、ツール ボックスを開いてください。

2. **[Timer1]** アイコンをクリックしてタイマーを選択します。 **[プロパティ]** ウィンドウで、表示イベントから表示プロパティに切り替えます。 次に、タイマーの **[Interval]** プロパティを **750** に設定します。ただし、その **[Enabled]** プロパティは **[False]** のままにします。 **[Interval]** プロパティは、*ティック*間の待機時間 (<xref:System.Windows.Forms.Timer.Tick> イベントのトリガーまでの待機時間) をタイマーに指示します。 このプロパティの値として 750 を指定すると、その Tick イベントを発生させるまでに 4 分の 3 秒 (750 ミリ秒) 待機するようタイマーに指示することになります。 <xref:System.Windows.Forms.Timer.Start> メソッドを呼び出して、プレーヤーが 2 つ目のラベルをクリックした後にのみタイマーが開始されるようにします。

3. **Windows フォーム デザイナー**でタイマー コントロール アイコンを選択して **Enter** キーを押すか、タイマーをダブルクリックして、空の Tick イベント ハンドラーを追加します。 次のコードを既存のコードと置き換えるか、手動でイベント ハンドラーに入力します。

     [!code-csharp[VbExpressTutorial4Step6#7](../ide/codesnippet/CSharp/step-6-add-a-timer_1.cs)]
     [!code-vb[VbExpressTutorial4Step6#7](../ide/codesnippet/VisualBasic/step-6-add-a-timer_1.vb)]

      > [!IMPORTANT]
      > このページの右上にあるプログラミング言語のコントロールを使用して、C# コード スニペットまたは Visual Basic コード スニペットのいずれかを表示します。<br><br>![Docs.Microsoft.com のプログラミング言語コントロール](../ide/media/docs-programming-language-control.png)

     Tick イベント ハンドラーは、3 つのことを実行します。まず、<xref:System.Windows.Forms.Timer.Stop> メソッドを呼び出してタイマーを停止します。 次に、2 つの参照変数 `firstClicked` および `secondClicked` を使用して、プレーヤーがクリックした 2 つのラベルを再び非表示にします。 最後に、`firstClicked` 参照変数と `secondClicked` 参照変数を `null` (C# の場合) または `Nothing` (Visual Basic の場合) にリセットします。 この手順は、プログラム自体がリセットされるしくみであるため重要です。 この時点では、<xref:System.Windows.Forms.Label> コントロールが追跡されておらず、プレーヤーはラベルを再びクリックできる状態になっています。

    > [!NOTE]
    > Timer オブジェクトには、タイマーを開始する `Start()` メソッドと、タイマーを停止する `Stop()` メソッドがあります。 **[プロパティ]** ウィンドウでタイマーの **[Enabled]** プロパティを **[True]** に設定した場合、タイマーはプログラムが起動するとすぐに時間を刻み始めます。 一方、 **[False]** に設定したままにした場合、その `Start()` メソッドが呼び出されるまでは時間の刻みは始まりません。 通常、タイマーは、**Interval** プロパティを使用して、次に時間を刻むまでに待機するミリ秒数を判断し、その Tick イベントを繰り返し発生させます。 ここでは、タイマーの `Stop()` メソッドが Tick イベント内で呼び出されるしくみになっています。 これにより、タイマーが*ワン ショット モード*になります。つまり、`Start()` メソッドが呼び出されると、タイマーは指定された間隔分の時間を待機し、Tick イベントを 1 回発生させた後に、停止するようになります。

4. 新しいタイマーの動作を確認するには、コード エディターに移動し、`label_Click()` イベント ハンドラー メソッドの上部と下部に次のコードを追加します (`if` ステートメントを、上部に 1 つ追加し、下部に 3 つ追加することになります。メソッドの他の部分は同じです)。

     [!code-csharp[VbExpressTutorial4Step6#8](../ide/codesnippet/CSharp/step-6-add-a-timer_2.cs)]
     [!code-vb[VbExpressTutorial4Step6#8](../ide/codesnippet/VisualBasic/step-6-add-a-timer_2.vb)]

     メソッドの上部のコードは、**Enabled** プロパティの値をチェックして、タイマーが開始されているかどうかをチェックします。 これにより、プレーヤーが 1 つ目と 2 つ目の Label コントロールをクリックした場合はタイマーが開始され、3 つ目のラベルをクリックした場合は何も実行されません。

     メソッドの下部のコードは、プレーヤーがクリックした 2 つ目の Label コントロールを追跡し、そのラベルのアイコンの色を黒に設定してアイコンを表示するように、`secondClicked` 参照変数を設定します。 これにより、タイマーがワン ショット モードで開始され、750 ミリ秒待機してから、Tick イベントを 1 回発生させるようになります。 その後で、タイマーの Tick イベント ハンドラーが 2 つのアイコンを非表示にし、`firstClicked` 参照変数と `secondClicked` 参照変数をリセットします。この時点で、プレーヤーはフォーム上で別の 1 組のアイコンをクリックできる状態になります。

5. プログラムを保存し、実行します。 アイコンをクリックすると、そのアイコンが表示されます。

6. 別のアイコンをクリックします。 そのアイコンが一時的に表示され、その後、両方のアイコンが非表示になります。 これを何度も繰り返します。 これで、フォームで、クリックした 1 つ目と 2 つ目のアイコンが追跡され、タイマーを使用して、少し時間をおいてからアイコンが非表示にされるようになりました。

## <a name="to-continue-or-review"></a>続行または確認するには

- チュートリアルの次の手順に進むには、「 **[手順 7:ペアの表示の維持](../ide/step-7-keep-pairs-visible.md)** 」をご覧ください。

- チュートリアルの前の手順に戻るには、「[手順 5:ラベルの参照の追加](../ide/step-5-add-label-references.md)」をご覧ください。
