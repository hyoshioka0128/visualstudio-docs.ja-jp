---
title: '手順 7: 乗算問題と除算問題の追加 | Microsoft ドキュメント'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
ms.assetid: e638959e-f6a4-4eb4-b2e9-f63b7855cf8f
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: f7f7efb0acf6611346abe67a7a94e5c221919665
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72646970"
---
# <a name="step-7-add-multiplication-and-division-problems"></a>手順 7: 乗算問題と除算問題の追加
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このチュートリアルの第 7 部では、乗算問題と除算問題を追加しますが、まず変更方法について考えてみます。 最初の手順は、値を格納することです。

### <a name="to-add-multiplication-and-division-problems"></a>乗算問題と除算問題を追加するには

1. さらに 4 つの整数変数をフォームに追加します。

     [!code-csharp[VbExpressTutorial3Step7#15](../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial3step7/cs/form1.cs#15)]
     [!code-vb[VbExpressTutorial3Step7#15](../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial3step7/vb/form1.vb#15)]

2. 以前に実行したように、`StartTheQuiz()` メソッドを変更して、乗算問題と除算問題に乱数を入力するようにします。

     [!code-csharp[VbExpressTutorial3Step7#16](../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial3step7/cs/form1.cs#16)]
     [!code-vb[VbExpressTutorial3Step7#16](../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial3step7/vb/form1.vb#16)]

3. 乗算問題と除算問題についても確認するように `CheckTheAnswer()` メソッドを変更します。

     [!code-csharp[VbExpressTutorial3Step7#17](../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial3step7/cs/form1.cs#17)]
     [!code-vb[VbExpressTutorial3Step7#17](../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial3step7/vb/form1.vb#17)]

     乗算記号 (×) と除算記号 (÷) はキーボードから簡単に入力できないため、Visual C# および Visual Basic では、乗算にはアスタリスク (*)、除算にはスラッシュ記号 (/) を使用します。

4. タイマーの Tick イベント ハンドラーの最後の部分を、残り時間がなくなったら正しい解答を表示するように変更します。

     [!code-csharp[VbExpressTutorial3Step7#23](../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial3step7/cs/form1.cs#23)]
     [!code-vb[VbExpressTutorial3Step7#23](../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial3step7/vb/form1.vb#23)]

5. プログラムを保存し、実行します。

     次の図に示すように、クイズの受け手はクイズを完了するためには 4 つの問題に答える必要があります。

     ![4 つの問題がある計算クイズ](../ide/media/express-finishedquiz.png "Express_FinishedQuiz") 4つの問題がある計算クイズ

### <a name="to-continue-or-review"></a>続行または確認するには

- チュートリアルの次の手順に進むには、「 [手順 8: クイズをカスタマイズ](../ide/step-8-customize-the-quiz.md)する」を参照してください。

- チュートリアルの前の手順に戻るには、「 [手順 6: 減算問題の追加](../ide/step-6-add-a-subtraction-problem.md)」を参照してください。
