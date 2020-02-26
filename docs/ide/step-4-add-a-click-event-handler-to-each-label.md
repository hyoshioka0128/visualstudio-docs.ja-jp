---
title: '手順 4: 各ラベルに Click イベント ハンドラーを追加する'
ms.date: 11/04/2016
ms.topic: tutorial
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
dev_langs:
- CSharp
- vb
ms.assetid: 16bdbc7c-4129-411d-bace-f4a3e5375975
author: ornellaalt
ms.author: ornella
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7049271dddb4e763bf5ecb3760358bdd63e38df5
ms.sourcegitcommit: 2ae2436dc3484b9dfa10e0483afba1e5a02a52eb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/25/2020
ms.locfileid: "77579350"
---
# <a name="step-4-add-a-click-event-handler-to-each-label"></a>手順 4: 各ラベルに Click イベント ハンドラーを追加する

絵合わせゲームは、次のように動作します。

1. プレーヤーが、アイコンが非表示になっているいずれかの四角をクリックすると、アイコンの色が黒に変更され、プレーヤーにアイコンが表示されます。

2. 次に、プレーヤーが他の非表示のアイコンをクリックします。

3. アイコンが一致した場合は、表示されたままになります。 一致しない場合は、両方のアイコンが再び非表示になります。

   プログラムをこのように動作させるには、クリックされたラベルの色を変更させる <xref:System.Windows.Forms.Control.Click> イベント ハンドラーを追加します。

## <a name="to-add-a-click-event-handler-to-each-label"></a>各ラベルに Click イベント ハンドラーを追加するには

1. **Windows フォーム デザイナー**でフォームを開きます。 **ソリューション エクスプローラー**で *Form1.cs* または *Form1.vb* を選択します。 メニュー バーで **[表示]**  >  **[デザイナー]** の順にクリックします。

2. 最初のラベル コントロールをクリックして選択します。 次に、**Ctrl** キーを押しながら他のラベルを 1 つずつクリックして選択します。 すべてのラベルが選択されていることを確認します。

3. **[プロパティ]** ウィンドウのツール バーにある **[イベント]** をクリックして、 **[プロパティ]** ウィンドウに **[イベント]** ページを表示します。 **Click** イベントまで下へスクロールし、次のスクリーンショットに示すように、ボックスに「**label_Click**」と入力します。

     ![Click イベントが表示された [プロパティ] ウィンドウ](../ide/media/express_labelclick.png)

4. **Enter** キーを押します。 IDE により、`label_Click()` という名前の `Click` イベント ハンドラーがコードに追加され、フォーム上の各ラベルにフックされます。

5. コードの残りの部分を次のように入力します。

     [!code-csharp[VbExpressTutorial4Step2_3_4#4](../ide/codesnippet/CSharp/step-4-add-a-click-event-handler-to-each-label_1.cs)]
     [!code-vb[VbExpressTutorial4Step2_3_4#4](../ide/codesnippet/VisualBasic/step-4-add-a-click-event-handler-to-each-label_1.vb)]

     > [!IMPORTANT]
     > このページの右上にあるプログラミング言語のコントロールを使用して、C# コード スニペットまたは Visual Basic コード スニペットのいずれかを表示します。<br><br>![Docs.Microsoft.com のプログラミング言語コントロール](../ide/media/docs-programming-language-control.png)

    > [!NOTE]
    > `label_Click()` コード ブロックを手動で入力せずにコピーして貼り付ける場合は、既存の `label_Click()` コードと置き換えてください。 置き換えないと、コード ブロックが重複することになります。

    > [!NOTE]
    > 「[チュートリアル 2: 制限時間ありの計算クイズの作成](../ide/tutorial-2-create-a-timed-math-quiz.md)」チュートリアルで使用されているのと同じ  がイベント ハンドラーの上部にあります。 単一のイベント ハンドラー メソッドに異なるラベル コントロールの Click イベントをフックしたため、ユーザーがどのラベルをクリックしたかにかかわらず、同じメソッドが呼び出されます。 イベント ハンドラー メソッドは、どのラベルがクリックされたのかを知る必要があるため、そのラベル コントロールに対して `sender` という名前を使用します。 メソッドの 1 行目は、sender が単なる汎用オブジェクトではなく、具体的にはラベル コントロールであること、さらに `clickedLabel` という名前を使用してラベルのプロパティとメソッドにアクセスすることをプログラムに通知します。

     このメソッドは、最初に `clickedLabel` がオブジェクトからラベル コントロールに正常に変換 (キャスト) されたかどうかをチェックします。 正常に変換されなかった場合は、値が `null` (C#) または `Nothing` (Visual Basic) となり、メソッドの残りのコードは実行されません。 次に、メソッドはラベルの **ForeColor** プロパティを使用して、クリックされたラベルのテキストの色をチェックします。 ラベルのテキストの色が黒になっている場合は、アイコンが既にクリックされていて、メソッドは実行されています (これが `return` ステートメントが実行することです。メソッドの実行を停止するようにプログラムに指示します)。アイコンがクリックされていない場合、プログラムはそのテキストの色を黒に変更します。

6. メニュー バーで、 **[ファイル]**  >  **[すべてを保存]** の順にクリックして、ここまでの進捗を保存したら、 **[デバッグ]**  >  **[デバッグ開始]** の順にクリックしてプログラムを実行します。 青色の背景の空のフォームが表示されます。 フォーム内で任意のセルをクリックすると、いずれかのアイコンが表示されます。 フォーム内のさまざまな場所でクリックし続けます。 アイコンをクリックすると、そのアイコンが表示されます。

## <a name="to-continue-or-review"></a>続行または確認するには

- チュートリアルの次の手順に進むには、「 **[手順 5: ラベルの参照の追加](../ide/step-5-add-label-references.md)** 」を参照してください。

- チュートリアルの前の手順に戻るには、「[手順 3:各ラベルへのランダムなアイコンの割り当て](../ide/step-3-assign-a-random-icon-to-each-label.md)」を参照してください。
