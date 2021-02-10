---
title: '手順 5: ラベルの参照の追加'
description: ラベルの参照をフォームに追加する方法を説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: tutorial
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
dev_langs:
- CSharp
- VB
ms.assetid: d418350c-0396-494e-8149-71fa61b395c5
author: ornellaalt
ms.author: ornella
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: a009f5667f2eb01b22c45c9439a582d2319e6df9
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99868973"
---
# <a name="step-5-add-label-references"></a>手順 5: ラベルの参照の追加
プログラムでは、プレーヤーがどのラベル コントロールをクリックしたかを追跡する必要があります。 現在のところ、プレーヤーが選択したすべてのラベルが表示されます。 しかし、次のように変更します。 1 つ目のラベルがクリックされると、プログラムではラベルのアイコンを表示します。 2 つ目のラベルがクリックされると、一時的に両方のアイコンを表示した後に、再びアイコンを非表示にします。 *参照変数* を使用して、1 回目および 2 回目にどのラベル コントロールがクリックされたかを追跡します。

## <a name="to-add-label-references"></a>ラベルの参照を追加するには

1. 次のコードを使用して、フォームにラベルの参照を追加します。

     [!code-vb[VbExpressTutorial4Step5#5](../ide/codesnippet/VisualBasic/step-5-add-label-references_1.vb)]
     [!code-csharp[VbExpressTutorial4Step5#5](../ide/codesnippet/CSharp/step-5-add-label-references_1.cs)]

     > [!IMPORTANT]
     > このページの右上にあるプログラミング言語のコントロールを使用して、C# コード スニペットまたは Visual Basic コード スニペットのいずれかを表示します。<br><br>![Docs.Microsoft.com のプログラミング言語コントロール](../ide/media/docs-programming-language-control.png)

     これらの参照変数は、フォームにオブジェクト (<xref:System.Windows.Forms.Timer> オブジェクト、<xref:System.Collections.Generic.List%601> オブジェクト、<xref:System.Random> オブジェクトなど) を追加するために前に使用したステートメントに似ているように見えます。 ただし、これらのステートメントでは、フォームに追加の 2 つのラベル コントロールは表示されません。これは、2 つのステートメントのいずれにも `new` を使用していないためです。 `new` キーワードを使用しないと、オブジェクトは作成されません。 `firstClicked` および `secondClicked` が参照変数と呼ばれるのはこのためです。これらは、単に Label オブジェクトを追跡 (参照) するだけです。

     変数は、オブジェクトを追跡していない間は、特殊な予約値 `null` (C# の場合) および `Nothing` (Visual Basic の場合) に設定されます。 そのため、プログラムが起動されると、`firstClicked` および `secondClicked` の両方が `null` または `Nothing` に設定されます。これは、変数が何も追跡していないことを意味しています。

2. 新しい `firstClicked` 参照変数を使用するように <xref:System.Windows.Forms.Control.Click> イベント ハンドラーを変更します。 `label_Click()` イベント ハンドラー メソッドの最後のステートメント (`clickedLabel.ForeColor = Color.Black;`) を削除し、次に示す `if` ステートメントに置き換えます  (必ずコメントと `if` ステートメント全体を含めてください)。

     [!code-vb[VbExpressTutorial4Step5#6](../ide/codesnippet/VisualBasic/step-5-add-label-references_2.vb)]
     [!code-csharp[VbExpressTutorial4Step5#6](../ide/codesnippet/CSharp/step-5-add-label-references_2.cs)]

3. プログラムを保存し、実行します。 いずれかのラベル コントロールをクリックすると、そのアイコンが表示されます。

4. 次のラベル コントロールをクリックすると、何も起こらないことに気付きます。 プログラムでは、プレーヤーがクリックした 1 つ目のラベルが既に追跡されているため、`firstClicked` は `null` (C# の場合) または `Nothing` (Visual Basic の場合) ではありません。 `if` ステートメントは、`firstClicked` が `null` または `Nothing` かどうかをチェックし、そうでないことがわかった場合は、`if` ステートメント内のステートメントを実行しません。 そのため、次の図に示すように、クリックされた 1 つ目のアイコンのみが黒になり、他のアイコンは非表示になります。

     ![1 つのアイコンが表示された絵合わせゲーム](../ide/media/express_tut4step5.png)<br/>
*1 つのアイコンが表示された **絵合わせゲーム** _ _*

     この状況は、チュートリアルの次のステップで **Timer** コントロールを追加することで修正します。

## <a name="to-continue-or-review"></a>続行または確認するには

- チュートリアルの次の手順に進むには、「 **[手順 6: タイマーの追加](../ide/step-6-add-a-timer.md)** 」をご覧ください。

- チュートリアルの前の手順に戻るには、「[手順 4: 各ラベルへの Click イベント ハンドラーの追加](../ide/step-4-add-a-click-event-handler-to-each-label.md)」を参照してください。
