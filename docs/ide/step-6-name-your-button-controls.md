---
title: '手順 6: ボタン コントロールの名前を設定する'
ms.date: 08/30/2016
ms.assetid: 56b3baa3-651e-4ad4-8942-e334c5c57158
ms.topic: tutorial
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
dev_langs:
- CSharp
- VB
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ff8c43e42d63208c1119f1f545697a57173fdd7a
ms.sourcegitcommit: 98b02f87c7aa1f5eb7f0d1c86bfa36efa8580c57
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72313978"
---
# <a name="step-6-name-your-button-controls"></a>手順 6: ボタン コントロールの名前を設定する

<xref:System.Windows.Forms.PictureBox> はフォームで 1 つだけ使用しています。 このコントロールには、追加したときに自動的に **pictureBox1**という名前が付けられています。 <xref:System.Windows.Forms.CheckBox> も 1 つだけで、**checkBox1** という名前が付けられています。 この後、コードを記述しますが、そのコードでは CheckBox と PictureBox を参照します。 これらのコントロールについては、どちらも 1 つだけであるため、コードで **pictureBox1** または **checkBox1** となっていても何を指しているのかがわかります。

> [!TIP]
> Visual Basic の場合は、どのコントロールの名前も既定で先頭文字が大文字になるため、名前は **PictureBox1**、 **CheckBox1**のようになります。

ボタンはフォームに 4 つあり、 **button1**、 **button2**、 **button3**、および **button4**という名前が付けられています。 現在の名前を見ただけでは、どれが **[Close]** ボタンでどれが **[Show a picture]** ボタンなのかわかりません。 そのため、ボタン コントロールにもっとわかりやすい名前を付けると便利です。

## <a name="to-name-your-button-controls"></a>ボタン コントロールの名前を設定するには

1. フォームで **[閉じる]** ボタンをクリックします (すべてのボタンが選択されたままになっている場合は、**Esc** キーを押して選択を取り消します)。 **[プロパティ]** ウィンドウで、 **(Name)** プロパティが表示されるまでスクロールします (プロパティがアルファベット順になっている場合は、 **(Name)** プロパティは上の方にあります)。次のスクリーンショットに示すように、名前を **closeButton** に変更します。

    ![closeButton という名前が表示された [プロパティ] ウィンドウ](../ide/media/express_setnameproperty.png)<br>***closeButton*** という "*名前*" が表示された ***[プロパティ]*** "*ウィンドウ*"

    > [!NOTE]
    > ボタンの名前を、"close" と "Button" の間に空白文字を含む「**close Button**」という名前に変更してみます。 これを行うと、IDE ではエラー メッセージが表示されます。IDE で "プロパティの値が無効です" というエラー メッセージが表示されます。 空白文字 (およびその他のいくつかの文字) は、コントロール名に使用できません。

1. 他の 3 つのボタンの名前を **backgroundButton**、 **clearButton**、および **showButton**に変更します。
名前を確認するには、 **[プロパティ]** ウィンドウにあるコントロール セレクターのドロップダウン リストをクリックします。 新しいボタン名が表示されます。

1. フォームで **[Show a picture]** ボタンをダブルクリックします。 代わりに、フォームの **[Show a picture]** ボタンをクリックして、**Enter** キーを押すこともできます。 これを行うと、IDE では、**Form1.cs** という名前のメイン ウィンドウで追加タブが開きます。 (Visual Basic を使用している場合、タブの名前は **Form1.vb** になります)

   このタブは、次のスクリーンショットに示すように、フォームの背後にあるコード ファイルを示します。

    ![Visual C&#35; コードが表示された [Form1.cs] タブ](../ide/media/express_showbuttoncode.png)<br>
***[Form1.cs]*** *タブに含まれる C# コード*

    > [!NOTE]
    > [Form1.cs] または [Form1.vb] タブには、**ShowButton** ではなく、**showButton** と表示されることがあります。

1. コードの次の部分にフォーカスを設定します。

    ```csharp
        private void ShowButton_Click(object sender, EventArgs e)
    {
    }
    ```

    ```vb
        Private Sub showButton_Click() Handles showButton.Click

    End Sub
    ```

   [!INCLUDE [devlang-control-csharp-vb](./includes/devlang-control-csharp-vb.md)]

   `showButton_Click()` (または、`ShowButton_Click()`) という名前のコードを見ています。 **[showButton]** ボタンのコード ファイルを開いたときに、これがフォームのコードに追加されます。 デザイン時に、フォームでコントロールのコード ファイルを開いて、コードが存在しない場合はコントロール用のコードが生成されます。 アプリを実行して、コントロール (この場合は、 **[Show a picture]** ボタン) を選択すると、"*メソッド*" と呼ばれるこのコードが実行されます。

1. **Windows フォーム デザイナー**のタブをもう一度クリックし (**Form1.cs [Design]** )、 **[Clear the picture]** ボタンのコード ファイルを開いてフォームのコード内でメソッドを作成します。 残りの 2 つのボタンについてもこの手順を繰り返します。 それぞれについて、フォームのコード ファイルに新しいメソッドが追加されます。

1. メソッドをもう 1 つ追加するために、**Windows フォーム デザイナー**で **CheckBox** コントロールのコード ファイルを開きます。IDE で `checkBox1_CheckedChanged()` メソッドが追加されます。 このメソッドは、ユーザーがチェック ボックスのオンとオフを切り替えるたびに呼び出されます。

   > [!TIP]
   > アプリの作業を行うときは、コード エディターと **Windows フォーム デザイナー**を頻繁に切り替えることになりますが、 IDE ではプロジェクト内を簡単に移動することができます。 **ソリューション エクスプローラー**を使用して **Windows フォーム デザイナー**を開くには、C# の場合は *[Form1.cs]* 、Visual Basic の場合は *[Form1.vb]* をダブルクリックします。または、メニュー バーで **[表示]**  >  **[デザイナー]** の順に選択します。

    コード エディターに表示される新しいコードを次に示します。

    [!code-csharp[VbExpressTutorial1Step6_#2](../ide/codesnippet/CSharp/step-6-name-your-button-controls_2.cs)]

    [!code-vb[VbExpressTutorial1Step6_#2](../ide/codesnippet/VisualBasic/step-6-name-your-button-controls_2.vb)]

    > [!NOTE]
    > ご利用のコードでは、"camelCase" という文字にイベント ハンドラーが表示されない場合があります。

    追加した 5 つのメソッドは、イベントが発生するたびにアプリケーションで呼び出されることから (ユーザーがボタンをクリックしたときやチェック ボックスをオンにしたときなど)、"*イベント ハンドラー*" と呼ばれます。

    デザイン時に IDE でコントロールのコードを表示して、イベント ハンドラー メソッドが見つからないと Visual Studio はコントロールのためにこれを追加します。 たとえば、ボタンをダブルクリックすると、そのボタンの <xref:System.Windows.Forms.Control.Click> イベントに対するイベント ハンドラー (ユーザーがボタンをクリックするたびに呼び出されるイベント ハンドラー) が追加されます。 チェック ボックスをダブルクリックすると、そのチェック ボックスの <xref:System.Windows.Forms.CheckBox.CheckedChanged> イベントに対するイベント ハンドラー (ユーザーがチェック ボックスのオンとオフを切り替えるたびに呼び出されるイベント ハンドラー) が追加されます。

    コントロールのイベント ハンドラーを追加した後は、**Windows フォーム デザイナー**でコントロールをダブルクリックするか、またはメニュー バーで **[表示]**  >  **[コード]** の順に選択して、いつでもイベント ハンドラーに戻ることができます。

    名前は、プログラムを作成するときに重要になります。メソッド (イベント ハンドラーを含む) には任意の名前を付けることができます。 IDE でイベント ハンドラーを追加した場合は、コントロールの名前と処理されるイベントに基づいて名前が作成されます。

    たとえば、**showButton** というボタンの Click イベントのイベント ハンドラー メソッドには `showButton_Click()` (または、`ShowButton_Click()`) という名前が付けられます。 また、メソッドであることを示すために、通常はメソッド名の後に左かっこと右かっこ `()` が追加されます。

    コード変数名を変更する場合は、コードの変数を右クリックし、 **[リファクター]**  >  **[名前の変更]** の順に選択します。 コードのその変数のすべてのインスタンスの名前は変更されます。 詳細については、[名前の変更リファクタリング](../ide/reference/rename.md)に関するページを参照してください。

## <a name="next-steps"></a>次の手順

* チュートリアルの次の手順に進むには、「 **[手順 7: フォームへのダイアログ コンポーネントの追加](../ide/step-7-add-dialog-components-to-your-form.md)** 」を参照してください。

* チュートリアルの前の手順に戻るには、「[手順 5:フォームへのコントロールの追加](../ide/step-5-add-controls-to-your-form.md)」をご覧ください。

## <a name="see-also"></a>関連項目

* [チュートリアル 2: 制限時間ありの計算クイズの作成](tutorial-2-create-a-timed-math-quiz.md)
* [チュートリアル 3: 絵合わせゲームの作成](tutorial-3-create-a-matching-game.md)
