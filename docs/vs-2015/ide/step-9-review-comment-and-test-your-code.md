---
title: '手順 9: レビュー、コメントの追加、およびコードのテスト | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
ms.assetid: f26f79ba-c91b-4164-b87f-679a1b231c09
caps.latest.revision: 31
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 090aeb83f6d0480c511acd808498953ae6c01940
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/10/2020
ms.locfileid: "75851102"
---
# <a name="step-9-review-comment-and-test-your-code"></a>手順 9: レビュー、コメントの追加、およびコードのテスト
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

次に、コードにコメントを追加します。 コメントは、プログラムの動作には影響しないメモです。 コメントを追加すると、コードを読む人が動作内容を理解しやすくなります。 コードにコメントを追加することをお勧めします。 行をコメントとしてマークするには、Visual C# では 2 つのスラッシュ (//) を使用します。 Visual Basic では、単一引用符 (') を使用してコメントとしてマークします。 コメントを追加したら、プログラムをテストします。 プロジェクトで作業している間にコードを頻繁に実行してテストすることをお勧めします。これによって、コードが複雑になる前に、問題を早期に見つけて修正することができます。 これは*反復テスト*と呼ばれます。

 一部の機能を作成しただけで、まだ完成はしていませんが、既にピクチャを読み込むことはできます。 コードへのコメントの追加とテストを行う前に、頻繁に使用することになるコードの概念についてここで確認しておきましょう。

- Windows フォーム デザイナーで **[Show a picture]** ボタンをダブルクリックしたとき、プログラムのコードに自動的に*メソッド*が追加されました。

- メソッドはコードを整理する 1 つの方法で、これを使用してコードをまとめることができます。

- ほとんどの場合、メソッドではいくつかの処理を特定の順序で行います。たとえば、ここで作成した `showButton_Click()` メソッドでは、ダイアログ ボックスを表示してから、ピクチャを読み込みます。

- メソッドは、コード *ステートメント*、またはコード行で構成されます。 コード ステートメントをまとめたものがメソッドであると考えることができます。

- メソッドを実行する (*呼び出す*) と、メソッド内のステートメントが最初のものから順番に 1 つずつ実行されます。

   ステートメントの例を次に示します。

  ```csharp
  pictureBox1.Load(openFileDialog1.FileName);
  ```

  ```vb
  pictureBox1.Load(openFileDialog1.FileName)
  ```

   ステートメントは、プログラムに処理を実行させる指示にあたります。 Visual C# の場合、ステートメントは必ずセミコロンで終わります。 Visual Basic の場合は、行の末尾がステートメントの末尾になります (Visual Basic にセミコロンは必要ありません)。前のステートメントは、ユーザーが**OpenFileDialog**コンポーネントで選択したファイルを読み込むように `PictureBox` コントロールに指示します。

  ![ビデオへのリンク](../data-tools/media/playvideo.gif "PlayVideo")このトピックのビデオ版については、「[チュートリアル 1: Visual Basic でのピクチャビューアーの作成-](https://msdn.microsoft.com/vbasic/gg315356.aspx)ビデオ5」または「[チュートリアル 1 C# : ピクチャビューアーの作成-ビデオ 5](https://msdn.microsoft.com/vcsharp/gg278413.aspx)」を参照してください。 これらのビデオでは、旧バージョンの Visual Studio を使用しているため、一部のメニュー コマンドやその他のユーザー インターフェイス要素が若干異なります。 ただし、概念および手順は、現在のバージョンの Visual Studio でも同様です。

### <a name="to-add-comments"></a>コメントを追加するには

1. コードに次のコメントを追加します。

     [!code-csharp[VbExpressTutorial1Step9_10#1](../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial1step9_10/cs/form1.cs#1)]
     [!code-vb[VbExpressTutorial1Step9_10#1](../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial1step9_10/vb/form1.vb#1)]

    > [!NOTE]
    > これで **showButton** ボタンの Click イベント ハンドラーが完成し、使用できる状態になりました。 コードの記述を開始するとき、最初に `if` ステートメントを記述しました。 `if` ステートメントは、"ある条件を確認し、それに当てはまる場合に処理を実行する" ようにプログラムに指示するステートメントです。 ここでは、 **[ファイルを開く]** ダイアログ ボックスを開き、ユーザーがファイルを選択して **[OK]** をクリックした場合にそのファイルを PictureBox に読み込むように指示しています。

    > [!TIP]
    > IDE はコードを簡単に記述できるように設計されており、そのための方法の 1 つとして*コード スニペット*が用意されています。 スニペットは、小さなコードのブロックに展開されるショートカットです。
    >
    >  使用可能なすべてのスニペットを表示できます。 メニュー バーで、 **[ツール]** 、 **[コード スニペット マネージャー]** の順にクリックします。 Visual C# の場合、`if` スニペットは **[Visual C#]** にあります。 Visual Basic の場合、`if` スニペットは **[条件とループ]** 、 **[コード パターン]** にあります。 このマネージャーを使用して、既存のスニペットを参照したり独自のスニペットを追加したりすることができます。
    >
    >  コードの入力時にスニペットをアクティブにするには、そのスニペットを入力して Tab キーを押します。 多くのスニペットは **IntelliSense** ウィンドウに表示されます。Tab キーを 2 回押すのは、1 回目で **IntelliSense** ウィンドウからスニペットを選択し、2 回目でそのスニペットを使用するように IDE に指示するためです (IntelliSense は `if` スニペットはサポートしますが、`ifelse` スニペットはサポートしません)。

2. プログラムを実行する前に、ツール バーの **[すべてを保存]** (次の図を参照) をクリックしてプログラムを保存します。

     ![[すべて保存] ツールバーボタン](../ide/media/express-iconsaveall.png "Express_IconSaveAll")[すべて保存] ボタン

     または、メニュー バーで、 **[ファイル]** 、 **[すべてを保存]** の順にクリックしてプログラムを保存します。 早めに、かつ頻繁に保存することをお勧めします。

     実行中のプログラムは次の図のようになります。

     ![画像ビューアー](../ide/media/express-pictureviewerdonerun.png "Express_PictureViewerDoneRun")画像ビューアー

### <a name="to-test-your-program"></a>プログラムをテストするには

1. F5 キーを押すか、ツール バーの **[デバッグ開始]** をクリックします。

2. **[Show a picture]** をクリックして、記述したコードを実行します。 最初に、 **[ファイルを開く]** ダイアログ ボックスが開きます。 ダイアログ ボックスの下部にある **[ファイルの種類]** ボックスにフィルターが表示されることを確認します。 次に、ピクチャがある場所に移動して、そのピクチャを開きます。 通常、Windows オペレーティング システムに付属しているサンプルのピクチャが **My Documents** フォルダーの **My Pictures\Sample Pictures** フォルダーにあります。

    > [!NOTE]
    > **[Select a picture file]** ダイアログ ボックスにイメージが表示されない場合は、ダイアログ ボックスの右下のボックスで All files (*.\*) フィルターが選択されていることを確認します。

3. ピクチャを読み込みます。ピクチャが PictureBox に表示されます。 その後、境界線をドラッグしてフォームのサイズを変更してみてください。 フォーム内にドッキングした TableLayoutPanel 内に PictureBox をドッキングしてあるため、ピクチャの領域が、幅はフォームと同じで、高さはフォームの上部 90% に収まるようにサイズ変更されます。 TableLayoutPanel コンテナーと FlowLayoutPanel コンテナーを使用したのはそのためです。これらのコンテナーを使用することで、ユーザーがフォームのサイズを変更したときに適切なサイズが維持されます。

     この時点では、大きなピクチャはピクチャ ビューアーの境界線を超えます。 次の手順では、ウィンドウに合ったピクチャを作成するコードを追加します。

### <a name="to-continue-or-review"></a>続行または確認するには

- チュートリアルの次の手順に進むには、「[手順 10: その他のボタンおよびチェック ボックスに対するコードの記述](../ide/step-10-write-code-for-additional-buttons-and-a-check-box.md)」を参照してください。

- チュートリアルの前の手順に戻るには、「[手順 8: [Show a Picture] ボタンのイベント ハンドラーのコードの記述](../ide/step-8-write-code-for-the-show-a-picture-button-event-handler.md)」を参照してください。
