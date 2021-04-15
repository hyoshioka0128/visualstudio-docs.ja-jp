---
title: '手順 7: 乗算問題と除算問題の追加'
description: 乗算と除算の問題を追加する方法を説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: tutorial
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
dev_langs:
- CSharp
- VB
ms.assetid: e638959e-f6a4-4eb4-b2e9-f63b7855cf8f
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 6443d80b2dba347691dd6721da19518dc86c71bf
ms.sourcegitcommit: 6d88913a8b5a9e5eda01d3f95205b4d138f440f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/13/2021
ms.locfileid: "107297029"
---
# <a name="step-7-add-multiplication-and-division-problems"></a>手順 7: 乗算問題と除算問題の追加

このチュートリアルの第 7 部では、乗算問題と除算問題を追加しますが、まず変更方法について考えてみます。 最初の手順は、値を格納することです。

> [!NOTE]
> このトピックは、コーディングの基本概念に関するチュートリアル シリーズの一部です。 チュートリアルの概要については、「[チュートリアル 2:制限時間ありの計算クイズの作成](../ide/tutorial-2-create-a-timed-math-quiz.md)」を参照してください。

## <a name="to-add-multiplication-and-division-problems"></a>乗算問題と除算問題を追加するには

1. さらに 4 つの整数変数をフォームに追加します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial3step7/vb/form1.vb" id="Snippet15":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial3step7/cs/form1.cs" id="Snippet15":::

     [!INCLUDE [devlang-control-csharp-vb](./includes/devlang-control-csharp-vb.md)]

2. 以前に実行したように、`StartTheQuiz()` メソッドを変更して、乗算問題と除算問題に乱数を入力するようにします。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial3step7/vb/form1.vb" id="Snippet16":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial3step7/cs/form1.cs" id="Snippet16":::

3. 乗算問題と除算問題についても確認するように `CheckTheAnswer()` メソッドを変更します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial3step7/vb/form1.vb" id="Snippet17":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial3step7/cs/form1.cs" id="Snippet17":::

     乗算記号 (×) と除算記号 (÷) はキーボードから簡単に入力できないため、C# および Visual Basic では、乗算にはアスタリスク (*)、除算にはスラッシュ記号 (/) を使用します。

4. タイマーの <xref:System.Windows.Forms.Timer.Tick> イベント ハンドラーの最後の部分を、残り時間がなくなったら正しい解答を表示するように変更します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial3step7/vb/form1.vb" id="Snippet23":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial3step7/cs/form1.cs" id="Snippet23":::

5. プログラムを保存し、実行します。

     次の図に示すように、クイズの受け手はクイズを完了するためには 4 つの問題に答える必要があります。

     ![4 つの問題がある計算クイズ](../ide/media/express_finishedquiz.png)<br/>
*4 つの問題がある **計算クイズ** _ _*

## <a name="to-continue-or-review"></a>続行または確認するには

- チュートリアルの次の手順に進むには、「 **[手順 8:クイズのカスタマイズ](../ide/step-8-customize-the-quiz.md)** 」をご覧ください。

- チュートリアルの前の手順に戻るには、「[手順 6: 減算問題の追加](../ide/step-6-add-a-subtraction-problem.md)」を参照してください。
