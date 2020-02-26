---
title: '手順 5: フォームへのコントロールの追加'
ms.date: 08/30/2019
ms.assetid: dc2746f4-0b5c-4674-9ef7-f40f94150f52
ms.topic: tutorial
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
author: ornellaalt
ms.author: ornella
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 631def96fc7e4b5d7858ea3474492b41c526da65
ms.sourcegitcommit: 2ae2436dc3484b9dfa10e0483afba1e5a02a52eb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/25/2020
ms.locfileid: "77579352"
---
# <a name="step-5-add-controls-to-your-form"></a>手順 5: フォームへのコントロールの追加

この手順では、<xref:System.Windows.Forms.PictureBox> コントロールや <xref:System.Windows.Forms.CheckBox> コントロールなどのコントロールをフォームに追加します。 さらに、フォームに <xref:System.Windows.Forms.Button> コントロールを追加します。

## <a name="how-to-add-controls-to-your-form"></a>フォームにコントロールを追加する方法

1. Visual Studio IDE の左側にある **[ツールボックス]** タブを選択し (または、**Ctrl**+**Alt**+**X** キーを押して)、次に **[コモン コントロール]** グループを展開します。 フォームで使用する最も一般的なコントロールが表示されます。

1. **PictureBox** 項目をダブルクリックして、フォームに PictureBox コントロールを追加します。 TableLayoutPanel がフォーム全体にドッキングされているため、PictureBox コントロールは最初の空のセルに追加されます (左上隅)。

1. 新しい **PictureBox** コントロールを選択し、新しい PictureBox コントロール上の黒い三角形を選択して、次のスクリーンショットに示すように、タスク一覧を表示します。

    ![PictureBox タスク](../ide/media/express_pictureboxtasks.png)<br/>****PictureBox*** *タスク**

    > [!NOTE]
    > TableLayoutPanel に誤って違う種類のコントロールを追加した場合は、削除することができます。 コントロールを右クリックし、コンテキスト メニューの **[削除]** をクリックします。 また、メニュー バーを使用してフォームのコントロールを削除できます。 メニュー バーで、 **[編集]**  >  **[元に戻す]** 、または **[編集]**  >  **[削除]** の順にクリックします。

1. **PictureBox** コントロールの **[PictureBox タスク]** メニューで、 **[親コンテナーにドッキングする]** リンクを選択します。 これにより、PictureBox の **Dock** プロパティが自動的に **Fill** に設定されます。 これを確認するには、**PictureBox** コントロールをクリックし、 **[プロパティ]** ウィンドウに移動して、**Dock** プロパティが **Fill** に設定されていることを確認します。

1. PictureBox の **ColumnSpan** プロパティを変更して、PictureBox が両方のセルにまたがるようにします。 **PictureBox** で、**PictureBox** コントロールを選択し、**ColumnSpan** プロパティを **2** に設定します。 さらに、PictureBox が空の場合は空のフレームが表示されるようにします。 **BorderStyle** プロパティを **Fixed3D** に設定します。

    > [!NOTE]
    > PictureBox に **ColumnSpan** プロパティが表示されない場合は、PictureBox が TableLayoutPanel ではなくフォームに追加された可能性があります。 これを修正するには、**PictureBox** を選択して、削除し、**TableLayoutPanel** を選択して、新しい PictureBox を追加します。

1. フォームで **TableLayoutPanel** を選択し、フォームに CheckBox コントロールを追加します。 **ツールボックス**の **CheckBox** 項目をダブルクリックすると、新しい CheckBox コントロールがテーブル内の次の空いているセルに追加されます。 PictureBox が TableLayoutPanel の最初の 2 つのセルを使用しているため、CheckBox コントロールは左下のセルに追加されます。 **Text** プロパティを選択し、次の図に示すように、「**Stretch**」と入力します。

    ![Stretch プロパティのある TextBox コントロール](../ide/media/express_pictureviewercheckbox.png)<br/>"***Stretch*** *プロパティのある* ***TextBox*** *コントロール*"

1. フォームの **TableLayoutPanel** を選択し、**ツールボックス**の **[コンテナー]** グループ (TableLayoutPanel コントロールを取得したグループ) に移動し、**FlowLayoutPanel** 項目をダブルクリックして、新しいコントロールを最後のセル (右下) に追加します。 次に、FlowLayoutPanel を TableLayoutPanel にドッキングします。 それには、FlowLayoutPanel の黒い三角形のタスク一覧で **[親コンテナーにドッキングする]** を選択するか、または FlowLayoutPanel の **Dock** プロパティを **Fill** に設定します。

    > [!NOTE]
    > <xref:System.Windows.Forms.FlowLayoutPanel> は、他のコントロールを順番に行に配置するコンテナーです。 FlowLayoutPanel のサイズを変更すると、余裕がある場合は、すべてのコントロールが 1 行にレイアウトされます。 1 行に収まらない場合は、上下に重なった複数の行に配置されます。 <br/><br/>ここでは、FlowLayoutPanel を使用して 4 つのボタンを保持します。 追加するときにボタンを上下に整列する場合は、ボタンを追加する前に FlowLayoutPanel を選択します。 <br/><br/>(通常、各セルには 1 つのコントロールしか含まれません。 この例では、TableLayoutPanel の右下のセルに 4 つのボタン コントロールが含まれています。 なぜでしょうか。  FlowLayoutPanel はコンテナー コントロールであり、他のコントロールを保持するセル内のコントロールであるためです。)

## <a name="to-add-buttons"></a>ボタンを追加するには

1. 追加した新しい FlowLayoutPanel を選択します。 **ツールボックス**の **[コモン コントロール]** に移動し、**Button** 項目をダブルクリックします。**button1** というボタン コントロールが FlowLayoutPanel に追加されます。 この手順を繰り返して次のボタンを追加します。 既に **button1** というボタンがあることが IDE で認識され、次のボタンには **button2** という名前が付けられます。

1. 通常は、他のボタンも**ツールボックス**を使用して追加します。 ここでは、**button2** を選択し、メニュー バーから **[編集]**  >  **[コピー]** を選択します (または、**Ctrl**+**C** キーを押します)。 次に、メニュー バーから **[編集]**  >  **[貼り付け]** を選択して (または、**Ctrl**+**V** キーを押して)、コピーしたボタンを貼り付けます。 続けてもう一度貼り付けます。 IDE により **button3** と **button4** が FlowLayoutPanel に追加されることに注意してください。

    > [!NOTE]
    > コピーと貼り付けは、どのコントロールにも使用できます。 IDE では、論理的な方法で新しいコントロールに名前を付けて配置します。 コントロールをコンテナーに貼り付けると、IDE によって、配置できる次の論理的なスペースが選択されます。

1. 最初のボタンを選択し、**Text** プロパティを **Show a picture** に設定します。 次に、残りの 3 つのボタンの **Text** プロパティを、**Clear the picture**、**Set the background color**、および **Close** に設定します。

1. ボタンのサイズを設定し、パネルの右端に揃えて配置してみましょう。 **FlowLayoutPanel** を選択し、**FlowDirection** プロパティを参照します。 変更して、**RightToLeft** に設定します。

   ボタンがセルの右端に揃い、順序が逆になって **[Show a picture]** ボタンが右端になります。

    > [!NOTE]
    > ボタンの順序がまだ正しくない場合は、ボタンを FlowLayoutPanel 内でドラッグして、任意の順序で並べ替えることができます。 ボタンをクリックし、左または右にドラッグできます。

1. **[閉じる]** ボタンをクリックして選択します。 次に、残りのボタンを一度に選択するには、**Ctrl** キーを押しながら選択します。

   すべてのボタンを選択した後、 **[プロパティ]** ウィンドウに移動し、**AutoSize** プロパティが表示されるまで上にスクロールします。 このプロパティを使用すると、テキスト全体が収まるようにボタンのサイズが自動的に変更されます。 それを **True** に設定します。

   これで、ボタンのサイズと順序が適切に設定されました (4 つすべてのボタンを選択していれば、4 つすべての **AutoSize** プロパティを同時に変更することができます)。4 つのボタンは次の図のようになります。

    ![4 つのボタンがある Picture Viewer](../ide/media/express_autosize.png)<br/>"*4 つのボタンがある* ***Picture Viewer***"

1. 次に、プログラムを再度実行して、変更を確認します。

   ボタンとチェック ボックスでは、まだ何も行われないことに注意してください &mdash; ただし、すぐに行われるようになります。

## <a name="to-continue-or-review"></a>続行または確認するには

* チュートリアルの次の手順に進むには、「 **[手順 6: ボタン コントロールの名前を設定する](../ide/step-6-name-your-button-controls.md)** 」を参照してください。

* チュートリアルの前の手順に戻るには、「[手順 4:TableLayoutPanel コントロールを使用してフォームのレイアウトを設定する](../ide/step-4-lay-out-your-form-with-a-tablelayoutpanel-control.md)」を参照してください。

## <a name="see-also"></a>関連項目

* [チュートリアル 2: 制限時間ありの計算クイズの作成](tutorial-2-create-a-timed-math-quiz.md)
* [チュートリアル 3: 絵合わせゲームの作成](tutorial-3-create-a-matching-game.md)
