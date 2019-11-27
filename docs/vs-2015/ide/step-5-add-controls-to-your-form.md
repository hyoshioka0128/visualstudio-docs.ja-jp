---
title: '手順 5: フォームへのコントロールの追加 | Microsoft ドキュメント'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
ms.assetid: dc2746f4-0b5c-4674-9ef7-f40f94150f52
caps.latest.revision: 22
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 89ca4c02a1cbb1171619060b9478b5f2d3ccaa36
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74295722"
---
# <a name="step-5-add-controls-to-your-form"></a>手順 5: フォームへのコントロールの追加
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

この手順では、`PictureBox` コントロールや `CheckBox` コントロールなどのコントロールをフォームに追加します。 また、ボタンも追加します。

 ![ビデオへのリンク](../data-tools/media/playvideo.gif "PlayVideo")このトピックのビデオ版については、「[チュートリアル 1: Visual Basic でのピクチャビューアーの作成-](https://go.microsoft.com/fwlink/?LinkId=205211)ビデオ2」または「[チュートリアル 1 C# : ピクチャビューアーの作成-ビデオ 2](https://go.microsoft.com/fwlink/?LinkId=205200)」を参照してください。 これらのビデオでは、旧バージョンの Visual Studio を使用しているため、一部のメニュー コマンドやその他のユーザー インターフェイス要素が若干異なります。 ただし、概念および手順は、現在のバージョンの Visual Studio でも同様です。

### <a name="to-add-controls-to-your-form"></a>フォームにコントロールを追加するには

1. [ツールボックス] タブ (Visual Studio IDE の左側にある) に移動し、 **[コモン コントロール]** グループを展開します。 フォームで使用する最も一般的なコントロールが表示されます。

2. フォームの TableLayoutPanel コントロールを選択します。 TableLayoutPanel が選択されていることを確認するには、その名前が **[プロパティ]** ウィンドウの上部にあるボックスに表示されることを確認します。 また、 **[プロパティ]** ウィンドウの上部にあるボックスを使用してフォーム コントロールを選択できます。 多くの場合、この方法の方がマウスで小さいコントロールを選択するよりも簡単です。

3. **PictureBox** 項目をダブルクリックして、フォームに PictureBox コントロールを追加します。 TableLayoutPanel がフォーム全体にドッキングされているため、PictureBox コントロールは最初の空のセルに追加されます (左上隅)。

4. 新しい PictureBox コントロールを選択し、新しい PictureBox コントロール上の黒い三角形を選択して、次の図に示すように、タスク一覧を表示します。

     ![PictureBox タスク](../ide/media/express-pictureboxtasks.png "Express_PictureBoxTasks")PictureBox タスク

    > [!NOTE]
    > TableLayoutPanel に誤って違う種類のコントロールを追加した場合は、削除することができます。 コントロールを右クリックし、コンテキスト メニューの **[削除]** をクリックします。 また、メニュー バーを使用してフォームのコントロールを削除できます。 メニュー バーで、 **[編集]** 、 **[元に戻す]** 、または **[編集]** 、 **[削除]** の順にクリックします。

5. **[親コンテナーにドッキングする]** リンクをクリックします。 これにより、PictureBox の **Dock** プロパティが自動的に **Fill** に設定されます。 これを確認するには、PictureBox コントロールをクリックし、 **[プロパティ]** ウィンドウに移動して、**Dock** プロパティが **Fill** に設定されていることを確認します。

6. PictureBox の **ColumnSpan** プロパティを変更して、PictureBox が両方のセルにまたがるようにします。 PictureBox コントロールを選択し、**ColumnSpan** プロパティを **2** に設定します。 さらに、PictureBox が空の場合は空のフレームが表示されるようにします。 **BorderStyle** プロパティを **Fixed3D** に設定します。

    > [!NOTE]
    > PictureBox に **ColumnSpan** プロパティが表示されない場合は、PictureBox が TableLayoutPanel ではなくフォームに追加された可能性があります。 これを修正するには、PictureBox を選択して、削除し、TableLayoutPanel を選択して、新しい PictureBox を追加します。

7. フォームで TableLayoutPanel を選択し、フォームに **CheckBox** コントロールを追加します。 ツールボックスの **CheckBox** 項目をダブルクリックすると、新しい CheckBox コントロールがテーブル内の次の空いているセルに追加されます。 PictureBox が TableLayoutPanel の最初の 2 つのセルを使用しているため、CheckBox コントロールは左下のセルに追加されます。 **Text** プロパティを選択し、次の図に示すように、「**Stretch**」と入力します。

     ![Stretch プロパティのある TextBox コントロール](../ide/media/express-pictureviewercheckbox.png "Express_PictureViewerCheckbox")Stretch プロパティのある TextBox コントロール

8. フォームの TableLayoutPanel を選択し、ツールボックスの **[コンテナー]** グループ (TableLayoutPanel コントロールを取得したグループ) に移動し、**FlowLayoutPanel** 項目をダブルクリックして、新しいコントロールを PictureBox の最後のセル (右下) に追加します。 その後、TableLayoutPanel の FlowLayoutPanel をドッキングします (FlowLayoutPanel の黒い三角形のタスク一覧の **[親コンテナーにドッキングする]** をクリックするか、または FlowLayoutPanel の **Dock** プロパティを **Fill** に設定します)。

    > [!NOTE]
    > FlowLayoutPanel は、他のコントロールを直線状に順番に配置するコンテナーです。 FlowLayoutPanel のサイズを変更する際、すべてのコントロールが 1 行に収まる場合は 1 行にレイアウトされます。 1 行に収まらない場合は、上下に重なった複数の行に配置されます。 ここでは、4 つのボタンを保持するために FlowLayoutPanel を使用します。 追加するときにボタンを整列する場合は、ボタンを追加する前に FlowLayoutPanel が選択されていること確認します。 前に説明したように、各セルで保持できるコントロールは 1 つだけですが、TableLayoutPanel の右下のセルにはボタン コントロールが 4 つ含まれています。 これが可能なのは、他のコントロールを保持するコントロールをセルに配置できるからです。 このようなコントロールをコンテナーと呼び、FlowLayoutPanel は 1 つのコンテナーです。

### <a name="to-add-buttons"></a>ボタンを追加するには

1. 追加した新しい FlowLayoutPanel を選択します。 ツールボックスの **[コモン コントロール]** に移動し、**Button** 項目をダブルクリックします。**button1** というボタン コントロールが FlowLayoutPanel に追加されます。 この手順を繰り返して次のボタンを追加します。 既に **button1** というボタンがあることが IDE で認識され、次のボタンには **button2** という名前が付けられます。

2. 通常は他のボタンもツールボックスを使用して追加しますが、 ここでは、**button2** をクリックし、メニュー バーで、 **[編集]** 、 **[コピー]** の順にクリックします (または Ctrl キーを押しながら C キーを押します)。 メニュー バーで、 **[編集]** 、 **[貼り付け]** の順にクリックして (または Ctrl キーを押しながら V キーを押して)、コピーしたボタンを貼り付けます。 続けてもう一度貼り付けます。 これで、IDE により **button3** と **button4** が FlowLayoutPanel に追加されます。

    > [!NOTE]
    > コピーと貼り付けは、どのコントロールにも使用できます。 IDE では、論理的な方法で新しいコントロールに名前を付けて配置します。 コントロールをコンテナーに貼り付けると、IDE によって、配置できる次の論理的なスペースが選択されます。

3. 最初のボタンを選択し、**Text** プロパティを **Show a picture** に設定します。 次に、残りの 3 つのボタンの **Text** プロパティを、**Clear the picture**、**Set the background color**、および **Close** に設定します。

4. 次に、ボタンのサイズを設定し、パネルの右端に揃えてアラインします。 FlowLayoutPanel を選択し、**FlowDirection** プロパティを参照します。 変更して、**RightToLeft** に設定します。 これにより、ボタンがセルの右端に揃い、順序が逆になって **[Show a picture]** ボタンが右端になります。

    > [!NOTE]
    > ボタンの順序がまだ正しくない場合は、ボタンを FlowLayoutPanel 内でドラッグして、任意の順序で並べ替えることができます。 ボタンをクリックし、左または右にドラッグできます。

5. **[閉じる]** ボタンをクリックして選択します。 Ctrl キーを押しながら他の 3 つのボタンをクリックして、すべてのボタンを選択します。 すべてのボタンが選択された状態で、 **[プロパティ]** ウィンドウに移動し、**AutoSize** プロパティが表示されるまで上にスクロールします。 このプロパティを使用すると、テキスト全体が収まるようにボタンのサイズが自動的に変更されます。 このプロパティを **true** に設定します。 これで、ボタンのサイズと順序が適切に設定されました (4 つのボタンがすべて選択されていれば、4つの**AutoSize**プロパティすべてを同時に変更できます)。次の図は、4つのボタンを示しています。

     ![4 つのボタンがある Picture Viewer](../ide/media/express-autosize.png "Express_AutoSize")4つのボタンがある Picture Viewer

6. ここで、プログラムをもう一度実行して、フォームの新しいレイアウトを確認します。 ボタンおよびチェック ボックスをクリックしてもまだ何も実行されません。この後の手順で機能を設定していきます。

### <a name="to-continue-or-review"></a>続行または確認するには

- チュートリアルの次の手順に進むには、「[手順 6: ボタン コントロールの名前の設定](../ide/step-6-name-your-button-controls.md)」を参照してください。

- チュートリアルの前の手順に戻るには、「[手順 4: TableLayoutPanel コントロールを使用したフォームのレイアウトの設定](../ide/step-4-lay-out-your-form-with-a-tablelayoutpanel-control.md)」を参照してください。
