---
title: '手順 8: プレーヤーが勝利したかどうかを確認するメソッドの追加'
ms.date: 11/04/2016
ms.topic: tutorial
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
dev_langs:
- CSharp
- VB
ms.assetid: 6e317f6e-ba4c-4306-8924-300b0c2f65c6
author: ornellaalt
ms.author: ornella
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 881fa0d90390a059bea28cb19584381f814396d3
ms.sourcegitcommit: 2ae2436dc3484b9dfa10e0483afba1e5a02a52eb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/25/2020
ms.locfileid: "77579766"
---
# <a name="step-8-add-a-method-to-verify-whether-the-player-won"></a>手順 8: プレーヤーが勝利したかどうかを確認するメソッドの追加
楽しいゲームが作成されましたが、完成させるには追加の項目が必要です。 ゲームは、プレーヤーが勝利した時点で終了する必要があるため、プレーヤーが勝利したかどうかを確認する `CheckForWinner()` メソッドを追加する必要があります。

## <a name="to-add-a-method-to-verify-whether-the-player-won"></a>プレーヤーが勝利したかどうかを確認するメソッドを追加するには

1. `CheckForWinner()` メソッドを、コードの下部にある `timer1_Tick()` イベント ハンドラーの下に追加します。次のコードのようになります。

     [!code-csharp[VbExpressTutorial4Step8#10](../ide/codesnippet/CSharp/step-8-add-a-method-to-verify-whether-the-player-won_1.cs)]
     [!code-vb[VbExpressTutorial4Step8#10](../ide/codesnippet/VisualBasic/step-8-add-a-method-to-verify-whether-the-player-won_1.vb)]

      > [!IMPORTANT]
      > このページの右上にあるプログラミング言語のコントロールを使用して、C# コード スニペットまたは Visual Basic コード スニペットのいずれかを表示します。<br><br>![Docs.Microsoft.com のプログラミング言語コントロール](../ide/media/docs-programming-language-control.png)     

     このメソッドでは、別の `foreach` ループ (C# の場合) または `For Each` ループ (Visual Basic の場合) を使用して、<xref:System.Windows.Forms.TableLayoutPanel> 内の各ラベルを処理します。 このメソッドでは、等値演算子 (C# の場合は `==`、Visual Basic の場合は `=`) を使用して、各ラベルのアイコンの色をチェックし、それらが背景と一致しているかどうかを確認します。 色が一致する場合は、アイコンが非表示のままになっており、プレーヤーはまだすべてのアイコンを一致させていないことになります。 この場合、プログラムでは `return` ステートメントを使用して、メソッドの残りの処理がスキップされます。 ループが、`return` ステートメントを実行することなくすべてのラベルの処理を終了した場合は、フォーム上のすべてのアイコンが一致していることを意味します。 プログラムでは、MessageBox を表示してプレーヤーの勝利を通知した後に、フォームの `Close()` メソッドを呼び出してゲームを終了します。

2. 次に、ラベルの <xref:System.Windows.Forms.Control.Click> イベント ハンドラーに新しい `CheckForWinner()` メソッドを呼び出させます。 必ず、プログラムでは、プレーヤーがクリックした 2 つ目のアイコンを表示したらすぐに、勝者をチェックするようにしてください。 クリックされた 2 つ目のアイコンの色を設定している行を探して、次のコードに示すように、そのすぐ後で、`CheckForWinner()` メソッドを呼び出します。

     [!code-csharp[VbExpressTutorial4Step8#11](../ide/codesnippet/CSharp/step-8-add-a-method-to-verify-whether-the-player-won_2.cs)]
     [!code-vb[VbExpressTutorial4Step8#11](../ide/codesnippet/VisualBasic/step-8-add-a-method-to-verify-whether-the-player-won_2.vb)]

3. プログラムを保存し、実行します。 ゲームを実行し、すべてのアイコンを一致させます。 勝利すると、プログラムでは、次の図に示すように **MessageBox** が表示され、その後にボックスが閉じられます。

     ![MessageBox が表示された絵合わせゲーム](../ide/media/express_tut4step8.png)<br/>
***MessageBox*** *が表示された* ***絵合わせゲーム***

## <a name="to-continue-or-review"></a>続行または確認するには

- チュートリアルの次の手順に進むには、「**[手順 9: その他の機能を試す](../ide/step-9-try-other-features.md)**」をご覧ください。

- チュートリアルの前の手順に戻るには、「[手順 7:ペアの表示の維持](../ide/step-7-keep-pairs-visible.md)」をご覧ください。
