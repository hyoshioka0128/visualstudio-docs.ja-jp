---
title: '手順 3: 各ラベルへのランダムなアイコンの割り当て'
description: ゲームで毎回、同じアイコンが同じセルに表示されないように、各ラベルにランダムなアイコンを割り当てる方法を説明します。
ms.custom: SEO-VS-2020
ms.date: 03/21/2020
ms.topic: tutorial
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
dev_langs:
- CSharp
- VB
ms.assetid: 0ba5ed7a-9aaa-41f4-95d2-e3c2d567bc79
author: ornellaalt
ms.author: ornella
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 3254a986fb21c5a562d0d9a3c7f098d2b560dbfd
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106214292"
---
# <a name="step-3-assign-a-random-icon-to-each-label"></a>手順 3: 各ラベルへのランダムなアイコンの割り当て

ゲームで毎回、同じアイコンが同じセルに表示されていたのでは、やりがいがありません。 これを避けるには、`AssignIconsToSquares()` メソッドを使用して、フォームのラベル コントロールにアイコンをランダムに割り当てます。

## <a name="to-assign-a-random-icon-to-each-label"></a>各ラベルにランダムなアイコンを割り当てるには

1. 次のコードを追加する前に、メソッドのしくみについて検討します。 新しいキーワード `foreach` (C# の場合) および `For Each` (Visual Basic の場合) があります。 (1 つの行は意図的にコメント アウトされています。これについてはこの手順の最後に説明します)。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial4step2_3_4/cs/form1.cs" id="Snippet2":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial4step2_3_4/vb/form1.vb" id="Snippet2":::

      > [!IMPORTANT]
      > このページの右上にあるプログラミング言語のコントロールを使用して、C# コード スニペットまたは Visual Basic コード スニペットのいずれかを表示します。<br><br>![Docs.Microsoft.com のプログラミング言語コントロール](../ide/media/docs-programming-language-control.png)

2. 前の手順で示されているように、`AssignIconsToSquares()` メソッドを追加します。 このメソッドを、「[手順 2:Random オブジェクトおよびアイコンのリストの追加](../ide/step-2-add-a-random-object-and-a-list-of-icons.md)」をご覧ください。

     前に説明したように、`AssignIconsToSquares()` メソッドに新しいものが含まれています。つまり、`foreach` ループ (C# の場合) および `For Each` (Visual Basic の場合) です。 `For Each` ループは、同じ処理を繰り返し実行する必要がある場合にいつでも使用できます。 ここでは、次のコードで説明されているように、<xref:System.Windows.Forms.TableLayoutPanel> のラベルごとに同じステートメントを実行する必要があります。 最初の行では、`control` という名前の変数を作成し、その変数に一度に 1 つずつコントロールを格納して、そのコントロールに対してループ内のステートメントを実行します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial4step2_3_4/cs/form1.cs" id="Snippet14":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial4step2_3_4/vb/form1.vb" id="Snippet14":::

    > [!NOTE]
    > "iconLabel" および "control" という名前が使用されているのは、わかりやすくするためです。 これらの名前を任意の名前に置き換えても、コードはまったく同じように動作します (ただしループ内の各ステートメントで名前を変更する必要はあります)。

     `AssignIconsToSquares()` メソッドは、TableLayoutPanel の各ラベル コントロールを反復処理し、それぞれに対し同じステートメントを実行します。 これらのステートメントは、「[手順 2:Random オブジェクトおよびアイコンのリストの追加](../ide/step-2-add-a-random-object-and-a-list-of-icons.md)」をご覧ください。 これらの各アイコンは Webdings フォントの文字であるため、このメソッドではテキストとして表現されます。 ランダムなラベル コントロールにアイコンのペアが割り当てられるように、リストに各アイコンを 2 つずつ含めています。

     `foreach` または `For Each` ループ内で実行されるコードを詳しく見てみましょう。 次に示しているのは前に示したコードの一部です。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial4step2_3_4/cs/form1.cs" id="Snippet16":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial4step2_3_4/vb/form1.vb" id="Snippet16":::

     最初の行では、**control** 変数を **iconLabel** という名前のラベルに変換しています。 その次の行は、変換が成功したかどうかを確認する `if` ステートメントです。 変換が成功した場合は、`if` ステートメント内のステートメントが実行されます (前のチュートリアルでも説明したように、`if` ステートメントは、指定した任意の条件を評価するために使用されます)。`if` ステートメントの最初の行では、**randomNumber** という名前の変数を作成し、icons リスト内の項目のいずれかに対応する乱数をこの変数に格納します。 そのために、前に作成した <xref:System.Random.Next> オブジェクトの <xref:System.Random> メソッドを使用します。 `Next` メソッドは乱数を返します。 またこの行では、**icons** リストの <xref:System.Collections.Generic.List%601.Count> プロパティを使用して、乱数を選択する範囲を決定しています。 次の行では、icons リストのいずれかの項目をラベルの <xref:System.Windows.Forms.Label.Text> プロパティに割り当てています。 コメントアウトしている行は、このトピックの後半で説明します。 最後に、`if` ステートメントの最終の行で、フォームに追加したアイコンをリストから削除しています。

     コード内にわからない部分があれば、コード要素の上にマウス ポインターを合わせると、関連するヒントが表示されます。 Visual Studio デバッガーを使用して、プログラムの実行中にコードの各行をステップ実行することもできます。 詳しくは、「[How Do I:Step with The Debugger in Visual Studio?](https://msdn.microsoft.com/vstudio/ee672313.aspx)」 (操作方法: Visual Studio のデバッガーでステップ実行する) または「[デバッガーでのコード間の移動](../debugger/navigating-through-code-with-the-debugger.md)」をご覧ください。

3. ゲーム ボードをアイコンで埋めるには、プログラムが起動したらすぐに `AssignIconsToSquares()` メソッドを呼び出す必要があります。 C# を使用している場合は、**Form1** "_コンストラクター_" の `InitializeComponent()` メソッドの呼び出しのすぐ下にステートメントを追加し、フォームが新しいメソッドを呼び出してフォーム自体の設定後に表示されるようにします。 新しいオブジェクト (クラスや構造体など) を作成するときは、コンストラクターを呼び出します。 詳しくは、「[コンストラクター (C# プログラミング ガイド)](/dotnet/csharp/programming-guide/classes-and-structs/constructors)」または「[コンストラクターとデストラクターの使用方法](/previous-versions/visualstudio/visual-studio-2008/2z08e49e\(v\=vs.90\))」(Visual Basic の場合) をご覧ください。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial4step2_3_4/cs/form1.cs" id="Snippet13":::

     Visual Basic の場合は、`AssignIconsToSquares()` メソッドの呼び出しを `Form1_Load` メソッドに追加します。コードは次のようになります。

    ```vb
    Private Sub Form1_Load(sender As Object, e As EventArgs) Handles MyBase.Load
        AssignIconsToSquares()
    End Sub
    ```

4. プログラムを保存し、実行します。 各ラベルに割り当てられたランダムなアイコンを備えたフォームが表示されます。 

5. いったんプログラムを終了して、再び実行します。 次の図に示すように、各ラベルに別のアイコンが割り当てられています。 

     ![ランダムなアイコンが表示された絵合わせゲーム](../ide/media/express_tut4step3.png)<br/>
*ランダムなアイコンが表示された絵合わせゲーム*

     アイコンは、まだ非表示に設定されていないため、表示されています。 アイコンをプレーヤーに非表示にするには、各ラベルの **ForeColor** プロパティをその **BackColor** プロパティと同じ色に設定できます。

6. アイコンを非表示にするには、プログラムを停止し、`For Each` ループ内のコードのコメント行からコメント記号を削除します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial4step2_3_4/cs/form1.cs" id="Snippet15":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial4step2_3_4/vb/form1.vb" id="Snippet15":::

7. メニュー バーで、 **[すべて保存]** をクリックし、プログラムを保存したうえで実行します。 アイコンが非表示になったように見えます。青い背景のみが表示されます。 ただし、アイコンはランダムに割り当てられて、そこに存在しています。 アイコンは、背景と同じ色であるため、プレーヤーには見えなくなっています。 これで、ゲームはやりがいのあるものになりました。プレーヤーはすべてのアイコンをすぐに見ることができなくなったためです。

## <a name="to-continue-or-review"></a>続行または確認するには

- チュートリアルの次の手順に進むには、「 **[手順 4:各ラベルへの Click イベント ハンドラーの追加](../ide/step-4-add-a-click-event-handler-to-each-label.md)** 」をご覧ください。

- チュートリアルの前の手順に戻るには、「[手順 2:Random オブジェクトおよびアイコンのリストの追加](../ide/step-2-add-a-random-object-and-a-list-of-icons.md)」をご覧ください。
