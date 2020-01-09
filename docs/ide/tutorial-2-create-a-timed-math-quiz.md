---
title: 'チュートリアル 2: 制限時間ありの計算クイズの作成'
ms.date: 10/16/2019
ms.assetid: d7165d08-ace3-457d-b57d-fb8f80760a6f
ms.topic: tutorial
ms.technology: vs-ide-general
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 884047237652f6b69bd437b5faf47d820903b824
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75588669"
---
# <a name="tutorial-2-create-a-timed-math-quiz"></a>チュートリアル 2: 制限時間ありの計算クイズの作成

このチュートリアルでは、クイズの受け手が制限時間内にランダムに表示される 4 つの計算問題に答えるクイズを作成します。

> [!NOTE]
> このチュートリアルでは、C# と Visual Basic の両方が取り上げられているため、使用しているプログラミング言語固有の情報に注意してください。

このチュートリアルでは、次のタスクについて説明します。

- <xref:System.Random> クラスを使用して乱数を生成します。

- <xref:System.Windows.Forms.Timer> コントロールを使用して特定の時点で発生するようにイベントをトリガーします。

- `if else` ステートメントを使用してプログラム フローを制御します。

- コードで基本的な算術演算を実行します。

完了すると、クイズは数値が異なることを除いて次のスクリーンショットのようになります。

![4 つの問題がある計算クイズ](../ide/media/express_finishedquiz.png)

## <a name="tutorial-links"></a>チュートリアルのリンク

|Title|説明|
|-----------|-----------------|
|[手順 1:プロジェクトの作成とフォームへのラベルの追加](../ide/step-1-create-a-project-and-add-labels-to-your-form.md)|最初にプロジェクトを作成し、プロパティを変更し、`Label` コントロールを追加します。|
|[手順 2:ランダムな加算問題の作成](../ide/step-2-create-a-random-addition-problem.md)|加算問題を作成し、`Random` クラスを使用して乱数を生成します。|
|[手順 3:カウントダウン タイマーを追加する](../ide/step-3-add-a-countdown-timer.md)|クイズに制限時間を設定できるようにカウントダウン タイマーを追加します。|
|[手順 4:CheckTheAnswer() メソッドの追加](../ide/step-4-add-the-checktheanswer-parens-method.md)|クイズの受け手が問題の正しい解答を入力したかどうかを確認するメソッドを追加します。|
|[手順 5:NumericUpDown コントロールの Enter イベント ハンドラーの追加](../ide/step-5-add-enter-event-handlers-for-the-numericupdown-controls.md)|クイズを受けやすくするイベント ハンドラーを追加します。|
|[手順 6:減算問題を追加する](../ide/step-6-add-a-subtraction-problem.md)|乱数を生成し、タイマーを使用し、正しい解答を確認する減算問題を追加します。|
|[手順 7:乗算問題と除算問題の追加](../ide/step-7-add-multiplication-and-division-problems.md)|乱数を生成し、タイマーを使用し、正しい解答を確認する乗算問題および除算問題を追加します。|
|[手順 8:クイズのカスタマイズ](../ide/step-8-customize-the-quiz.md)|色の変更、ヒントの追加など、その他の機能を試します。|

無料で利用できる便利なビデオ学習リソースもあります。 C# でのプログラミングの詳細については、「[C# の基礎: 入門者向けの開発](https://channel9.msdn.com/Series/C-Sharp-Fundamentals-Development-for-Absolute-Beginners)」を参照してください。 Visual Basic でのプログラミングの詳細については、「[Visual Basic の基礎:入門者向けの開発](https://channel9.msdn.com/Series/Visual-Basic-Development-for-Absolute-Beginners)」を参照してください。

## <a name="next-steps"></a>次の手順

チュートリアルを開始するには、「 **[手順 1:プロジェクトの作成とフォームへのラベルの追加](../ide/step-1-create-a-project-and-add-labels-to-your-form.md)** 」を参照してください。

## <a name="see-also"></a>関連項目

* [その他の C# のチュートリアル](/visualstudio/get-started/csharp/)
* [Visual Basic のチュートリアル](/visualstudio/get-started/visual-basic/)
* [C++ のチュートリアル](/cpp/get-started/tutorial-console-cpp)
