---
title: '手順 8: クイズのカスタマイズ'
description: timeLabel コントロールの色を変更する方法、およびクイズの受け手にヒントを与える方法を説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: tutorial
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
dev_langs:
- CSharp
- VB
ms.assetid: dc8edb13-1b23-47d7-b859-8c6f7888c1a9
author: ornellaalt
ms.author: ornella
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 727d880caf912441009bda66bf516d501bd7303f
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99969647"
---
# <a name="step-8-customize-the-quiz"></a>手順 8: クイズのカスタマイズ

チュートリアルの最後の部分では、クイズをカスタマイズする方法を説明して、既に学習した内容を掘り下げます。 たとえば、プログラムで解答が決して分数にはならないランダムな除算問題を作成する方法を考えてみます。 さらに詳しく学習するには、`timeLabel` コントロールの色を変更したり、クイズの受け手にヒントを示したりしてみてください。

> [!NOTE]
> このトピックは、コーディングの基本概念に関するチュートリアル シリーズの一部です。 チュートリアルの概要については、「[チュートリアル 2:制限時間ありの計算クイズの作成](../ide/tutorial-2-create-a-timed-math-quiz.md)」を参照してください。

## <a name="to-customize-the-quiz"></a>クイズをカスタマイズするには

- クイズの残り時間が 5 秒になったら、**BackColor** プロパティを設定して、**timeLabel** コントロールの色を赤に変更します。

  ```csharp
  timeLabel.BackColor = Color.Red;
  ```

  ```vb
  timeLabel.BackColor = Color.Red
  ```

  [!INCLUDE [devlang-control-csharp-vb](./includes/devlang-control-csharp-vb.md)]

  クイズが終了したら元の色に戻します。

- <xref:System.Windows.Forms.NumericUpDown> コントロールに正しい解答が入力されたら、サウンドを再生してクイズの受け手にヒントを示します  (クイズの受け手がコントロールの値を変更するたびに実行される、各コントロールの <xref:System.Windows.Forms.NumericUpDown.ValueChanged> イベントのイベント ハンドラーを記述する必要があります)。

## <a name="to-continue-or-review"></a>続行または確認するには

- 次のチュートリアルに進むには、「 **[チュートリアル 3: 絵合わせゲームの作成](../ide/tutorial-3-create-a-matching-game.md)** 」参照してください。

- チュートリアルの前の手順に戻るには、「[手順 7:乗算問題と除算問題の追加](../ide/step-7-add-multiplication-and-division-problems.md)」を参照してください。
