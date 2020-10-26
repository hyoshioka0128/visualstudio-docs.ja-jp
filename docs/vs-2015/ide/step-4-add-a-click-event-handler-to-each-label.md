---
title: '手順 4: 各ラベルへの Click イベント ハンドラーの追加 | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
ms.assetid: 16bdbc7c-4129-411d-bace-f4a3e5375975
caps.latest.revision: 22
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 0b78a1757586dfaf6087711eaf1ed6001155a3b7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72671802"
---
# <a name="step-4-add-a-click-event-handler-to-each-label"></a>手順 4: 各ラベルへの Click イベント ハンドラーの追加
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

絵合わせゲームは、次のように動作します。

1. プレーヤーが、アイコンが非表示になっているいずれかの四角をクリックすると、アイコンの色が黒に変更され、プレーヤーにアイコンが表示されます。

2. 次に、プレーヤーが他の非表示のアイコンをクリックします。

3. アイコンが一致した場合は、表示されたままになります。 一致しない場合は、両方のアイコンが再び非表示になります。

   プログラムをこのように動作させるには、クリックされたラベルの色を変更させる Click イベント ハンドラーを追加します。

### <a name="to-add-a-click-event-handler-to-each-label"></a>各ラベルに Click イベント ハンドラーを追加するには

1. Windows フォーム デザイナーでフォームを開きます。 ソリューション エクスプローラーで Form1.cs または Form1.vb を選択します。 メニュー バーで [**表示**]、[**デザイナー**] の順にクリックします。

2. 最初のラベル コントロールをクリックして選択します。 次に、Ctrl キーを押しながら他のラベルを 1 つずつクリックして選択します。 すべてのラベルが選択されていることを確認します。

3. **[プロパティ]** ウィンドウのツール バーにある **[イベント]** をクリックして、 **[プロパティ]** ウィンドウに **[イベント]** ページを表示します。 **Click** イベントまで下へスクロールし、次の図に示すように、ボックスに「**label_Click**」と入力します。

     ![Click イベントを示すプロパティウィンドウ](../ide/media/express-labelclick.png "Express_labelClick") Click イベントを示すプロパティウィンドウ

4. Enter キーを押します。 IDE により、`label_Click()` という名前の Click イベント ハンドラーがコードに追加され、フォーム上の各ラベルにフックされます。

5. コードの残りの部分を次のように入力します。

     [!code-csharp[VbExpressTutorial4Step2_3_4#4](../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial4step2_3_4/cs/form1.cs#4)]
     [!code-vb[VbExpressTutorial4Step2_3_4#4](../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial4step2_3_4/vb/form1.vb#4)]

    > [!NOTE]
    > `label_Click()` コード ブロックを手動で入力せずにコピーして貼り付ける場合は、既存の `label_Click()` コードと置き換えてください。 置き換えないと、コード ブロックが重複することになります。

    > [!NOTE]
    > `object sender`イベントハンドラーの上部では、 [「チュートリアル 2: 時間指定の計算クイズの作成](../ide/tutorial-2-create-a-timed-math-quiz.md)」で使用したものと同じものとして認識できます。 単一のイベント ハンドラー メソッドに異なるラベル コントロールの Click イベントをフックしたため、ユーザーがどのラベルをクリックしたかにかかわらず、同じメソッドが呼び出されます。 イベント ハンドラー メソッドは、どのラベルがクリックされたのかを知る必要があるため、そのラベル コントロールに対して **sender** という名前を使用します。 メソッドの 1 行目は、sender が単なる汎用オブジェクトではなく、具体的にはラベル コントロールであること、さらに **clickedLabel** という名前を使用してラベルのプロパティとメソッドにアクセスすることをプログラムに通知します。

     このメソッドは、最初に **clickedLabel** がオブジェクトからラベル コントロールに正常に変換 (キャスト) されたかどうかをチェックします。 正常に変換されなかった場合は、値が `null` (C#) または `Nothing` (Visual Basic) となり、メソッドの残りのコードは実行されません。 次に、メソッドはラベルの **ForeColor** プロパティを使用して、クリックされたラベルのテキストの色をチェックします。 ラベルのテキストの色が黒になっている場合は、アイコンが既にクリックされていて、メソッドは実行されています  ( `return` このステートメントでは、メソッドの実行を停止するようにプログラムに指示します)。それ以外の場合、アイコンは選択されていないので、プログラムはラベルのテキストの色を黒に変更します。

6. メニュー バーで、[**ファイル**]、[**すべてを保存**] の順にクリックして、ここまでの進捗を保存したら、[**デバッグ**]、[**デバッグ開始**] の順にクリックしてプログラムを実行します。 青色の背景の空のフォームが表示されます。 フォーム内で任意のセルをクリックすると、いずれかのアイコンが表示されます。 フォーム内のさまざまな場所でクリックし続けます。 アイコンをクリックすると、そのアイコンが表示されます。

### <a name="to-continue-or-review"></a>続行または確認するには

- チュートリアルの次の手順に進むには、「 [手順 5: ラベル参照を追加](../ide/step-5-add-label-references.md)する」を参照してください。

- チュートリアルの前の手順に戻るには、「 [手順 3: 各ラベルへのランダムなアイコンの割り当て](../ide/step-3-assign-a-random-icon-to-each-label.md)」を参照してください。
