---
title: '手順 6: ボタン コントロールの名前の設定 | Microsoft ドキュメント'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
ms.assetid: 56b3baa3-651e-4ad4-8942-e334c5c57158
caps.latest.revision: 31
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: ebe3813ad01566e2994b0a16b4a3fdc735de8c8c
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74295708"
---
# <a name="step-6-name-your-button-controls"></a>手順 6: ボタン コントロールの名前の設定
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

PictureBox はフォームで 1 つだけ使用しています。 このコントロールには、追加したときに自動的に **pictureBox1**という名前が付けられています。 CheckBox も 1 つだけで、 **checkBox1**という名前が付けられています。 この後コードを記述しますが、そのコードでは CheckBox と PictureBox を参照します。 これらのコントロールについては、どちらも 1 つだけであるため、コードで **pictureBox1** または **checkBox1** となっていても何を指しているのかがわかります。

> [!NOTE]
> Visual Basic の場合は、どのコントロールの名前も既定で先頭文字が大文字になるため、名前は **PictureBox1**、 **CheckBox1**のようになります。

 ボタンはフォームに 4 つあり、 **button1**、 **button2**、 **button3**、および **button4**という名前が付けられています。 現在の名前を見ただけでは、どれが **[Close]** ボタンでどれが **[Show a picture]** ボタンなのかわかりません。 そのため、ボタン コントロールにもっとわかりやすい名前を付けると便利です。

 ![ビデオへのリンク](../data-tools/media/playvideo.gif "PlayVideo")このトピックのビデオ版については、「[チュートリアル 1: Visual Basic でのピクチャビューアーの作成-](https://go.microsoft.com/fwlink/?LinkId=205213)ビデオ3」または「[チュートリアル 1 C# : ピクチャビューアーの作成-ビデオ 3](https://go.microsoft.com/fwlink/?LinkId=205202)」を参照してください。 これらのビデオでは、旧バージョンの Visual Studio を使用しているため、一部のメニュー コマンドやその他のユーザー インターフェイス要素が若干異なります。 ただし、概念および手順は、現在のバージョンの Visual Studio でも同様です。

### <a name="to-name-your-button-controls"></a>ボタン コントロールの名前を設定するには

1. フォームで **[閉じる]** ボタンをクリックします (すべてのボタンが選択されている場合は、ESC キーを押して選択を取り消します)。 **[プロパティ]** ウィンドウで、 **(Name)** プロパティが表示されるまでスクロールします。 (プロパティがアルファベット順の場合、 **(Name)** プロパティは上部の近くにあります)。次の図に示すように、名前を**Closebutton**に変更します。

     ![CloseButton 名を使用したプロパティウィンドウ](../ide/media/express-setnameproperty.png "Express_SetNameProperty")CloseButton 名を使用したプロパティウィンドウ

    > [!NOTE]
    > ボタンの名前を、close と Button の間に空白文字を含む「 **closeButton**」という名前に変更しようとすると、IDE で "プロパティの値が無効です" というエラー メッセージが表示されます。 空白文字 (およびその他のいくつかの文字) は、コントロール名に使用できません。

2. 他の 3 つのボタンの名前を **backgroundButton**、 **clearButton**、および **showButton**に変更します。 名前を確認するには、 **[プロパティ]** ウィンドウにあるコントロール セレクターのドロップダウン リストをクリックします。 新しいボタン名が表示されます。

3. フォームで **[Show a picture]** ボタンをダブルクリックします。 代わりに、フォームの **[Show a picture]** ボタンをクリックして、Enter キーを押すこともできます。 これを行うと、IDE では **[Form1.cs]** (Visual Basic を使用している場合は **[Form1.vb]** ) というメイン ウィンドウで追加のタブが開きます。 このタブは、次の図に示すように、フォームの背後にあるコード ファイルを示します。

     ![Visual C&#35; code](../ide/media/express-showbuttoncode.png "Express_ShowButtonCode") Form1.cs タブC#が表示される [Form1.cs] タブ

4. コードの次の部分にフォーカスを設定します。 (Visual Basic を使用していてコードの Visual Basic バージョンを表示するには、次の **[VB]** タブをクリックします)。

     [!code-csharp[VbExpressTutorial1Step6#1](../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial1step6/cs/form1.cs#1)]
     [!code-vb[VbExpressTutorial1Step6#1](../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial1step6/vb/form1.vb#1)]

     `showButton_Click()`というコードが表示されています。 **[showButton]** ボタンのコード ファイルを開いたときに、これがフォームのコードに追加されます。 デザイン時に、フォームでコントロールのコード ファイルを開いて、コードが存在しない場合はコントロール用のコードが生成されます。 *メソッド*と呼ばれるこのコードは、プログラムを実行し、コントロール (この場合は、 **[Show a picture]** ) をクリックしたときに実行されます。

    > [!NOTE]
    > このチュートリアルでは、自動的に生成される Visual Basic コードのかっこ () で囲まれた部分をすべて削除して、コードを簡略化してあります。 このような場合は、コードの同じ部分を削除してかまいません。 いずれの場合もプログラムは正常に機能します。 チュートリアルの残りの部分では、自動的に生成されるコードについてはできる限り簡略化して示します。

5. Windows フォーム デザイナーのタブ (Visual C# の場合は **[Form1.cs [デザイン]]** 、Visual Basic の場合は **[Form1.vb [デザイン]]** ) をもう一度クリックし、 **[Clear the picture]** ボタンのコード ファイルを開いてフォーム コード内のメソッドを作成します。 残りの 2 つのボタンについてもこの手順を繰り返します。 それぞれについて、フォームのコード ファイルに新しいメソッドが追加されます。

6. メソッドをもう 1 つ追加するために、Windows フォーム デザイナーで CheckBox コントロールのコード ファイルを開きます。IDE で `checkBox1_CheckedChanged()` メソッドが追加されます。 このメソッドは、ユーザーがチェック ボックスのオンとオフを切り替えるたびに呼び出されます。

    > [!NOTE]
    > プログラムの作業を行うときは、コード エディターと Windows フォーム デザイナーを頻繁に切り替えることになりますが、 IDE ではプロジェクト内を簡単に移動することができます。 **ソリューション エクスプローラー** を使用して Windows フォーム デザイナーを開くには、Visual C# の場合は **[Form1.cs]** 、Visual Basic の場合は **[Form1.vb]** をダブルクリックします。または、メニュー バーで **[表示]** 、 **[デザイナー]** の順にクリックします。

     コード エディターに表示される新しいコードを次に示します。

     [!code-csharp[VbExpressTutorial1Step6#2](../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial1step6/cs/form1.cs#2)]
     [!code-vb[VbExpressTutorial1Step6#2](../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial1step6/vb/form1.vb#2)]

     追加した 5 つのメソッドは、(ユーザーがボタンをクリックしたときやチェック ボックスをオンにしたときなど) イベントが発生するたびにプログラムで呼び出されることから、 *イベント ハンドラー*と呼ばれます。

     デザイン時に IDE でコントロールのコードを表示して、イベント ハンドラー メソッドが見つからないと Visual Studio はコントロールのためにこれを追加します。 たとえば、ボタンをダブルクリックすると、そのボタンの Click イベントに対するイベント ハンドラー (ユーザーがボタンをクリックするたびに呼び出されるイベント ハンドラー) が追加されます。 チェック ボックスをダブルクリックすると、そのチェック ボックスの CheckedChanged イベントに対するイベント ハンドラー (ユーザーがチェック ボックスのオンとオフを切り替えるたびに呼び出されるイベント ハンドラー) が追加されます。

     コントロールのイベント ハンドラーを追加した後は、Windows フォーム デザイナーでコントロールをダブルクリックするか、またはメニュー バーで **[表示]** 、 **[コード]** の順にクリックして、いつでもイベント ハンドラーに戻ることができます。

     名前は、プログラムを作成するときに重要になります。メソッド (イベント ハンドラーを含む) には任意の名前を付けることができます。 IDE でイベント ハンドラーを追加した場合は、コントロールの名前と処理されるイベントに基づいて名前が作成されます。 たとえば、 **showButton** というボタンの Click イベントのイベント ハンドラー メソッドには `showButton_Click()` という名前が付けられます。 また、メソッドであることを示すために、通常はメソッド名の後に左かっこと右かっこ () が追加されます。 コード変数名を変更する場合は、コードの変数を右クリックし、 **[リファクター]** をクリックし、 **[名前の変更]** をクリックします。 コードのその変数のすべてのインスタンスの名前は変更されます。 詳細については、「[リファクタリングの名前変更 (C#)](../csharp-ide/rename-refactoring-csharp.md) 」または「[リファクタリングと名前の変更」ダイアログボックス](https://msdn.microsoft.com/library/001d2d81-9bb6-4e8e-ae3a-20c0daaa3959)を参照してください。

### <a name="to-continue-or-review"></a>続行または確認するには

- チュートリアルの次の手順に進むには、「[手順 7: フォームへのダイアログ コンポーネントの追加](../ide/step-7-add-dialog-components-to-your-form.md)」を参照してください。

- チュートリアルの前の手順に戻るには、「 [Step 5: Add Controls to Your Form](../ide/step-5-add-controls-to-your-form.md)」を参照してください。
