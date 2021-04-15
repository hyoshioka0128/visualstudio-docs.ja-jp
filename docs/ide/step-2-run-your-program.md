---
title: '手順 2: Picture Viewer アプリを実行する'
description: 画像ビューアー アプリの実行方法を説明します。
ms.custom: SEO-VS-2020
ms.date: 09/06/2019
ms.assetid: 9a8fe90e-c97b-4e98-b6c8-0c6b3962c49d
ms.topic: tutorial
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 7113c308416a5ddcd9bf2bb989cf17d31c4fffa6
ms.sourcegitcommit: 6d88913a8b5a9e5eda01d3f95205b4d138f440f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/13/2021
ms.locfileid: "107296496"
---
# <a name="step-2-run-your-picture-viewer-app"></a>手順 2: Picture Viewer アプリを実行する

Windows フォーム アプリ プロジェクトを作成するとき、実際には実行されるプログラムをビルドします。 このチュートリアルでは、まだ Picture Viewer アプリの機能をあまり利用しません。&mdash; 後で利用します。 この段階では、タイトル バーに **Form1** と表示された空のウィンドウが開きます。

アプリを実行する方法を次に示します。 

1. 以下のいずれかの方法を選択します。

    - **F5** キーを押します。

    - メニュー バーで、 **[デバッグ]**  >  **[デバッグ開始]** の順に選択します。

    - ツールバーで、**[デバッグ開始]** ボタンを選択します (次の図を参照)。

      ![[デバッグの開始] ツール バー ボタン](../ide/media/express_icondebug.png)<br>
      ***[デバッグの開始]** _ _ツール バー ボタン*

1. Visual Studio でアプリが実行され、**Form1** というウィンドウが表示されます。 次のスクリーンショットは、先ほど作成したアプリを示しています。 アプリが実行されているので、すぐにそれに追加します。

     ![実行中の Windows フォーム アプリ](../ide/media/express_firstrun.png)<br>
***Windows フォーム アプリ** _、_実行中*

1. Visual Studio 統合開発環境 (IDE) に戻り、新しいツール バーを参照します。 アプリケーションを実行すると、追加ボタンがツール バーに表示されます。 これらのボタンを使用するとアプリの停止や開始などの操作ができ、発生する可能性のあるエラー (バグ) の追跡に役立ちます。 この例では、アプリを開始および停止するために使用しています。

     ![デバッグ ツール バー](../ide/media/express_debugtoolbar.png)<br>
* **[デバッグ]** _ _ツール バー*

1. アプリを停止するには、次のいずれかの方法を使用します。

    - ツール バーで、**[デバッグの停止]** ボタンを選択します。

    - メニュー バーで、 **[デバッグ]**  >  **[デバッグの停止]** の順に選択します。

    - キーボードを使用して、**Shift**+**F5** キーを押します。

    - **[Form1]** ウィンドウの上隅にある **X** ボタンを選択します。

    > [!NOTE]
    > IDE 内からアプリを実行する作業は、通常はアプリケーションでバグ (エラー) を特定して修正することが目的であるためデバッグと呼ばれます。 このアプリは小さくて、まだあまり機能しませんが、それでも本物のプログラムです。 同じ手順で他のプログラムを実行し、デバッグします。 デバッグの詳細については、「[デバッガーでのはじめに](../debugger/debugger-feature-tour.md)」をご覧ください。

## <a name="next-steps"></a>次のステップ

* チュートリアルの次の手順に進むには、「 **[手順 3:フォームのプロパティの設定](../ide/step-3-set-your-form-properties.md)** 」を参照してください。

* チュートリアルの前の手順に戻るには、「[手順 1: Windows フォーム アプリケーション プロジェクトの作成](../ide/step-1-create-a-windows-forms-application-project.md)」を参照してください。

## <a name="see-also"></a>関連項目

* [チュートリアル 2: 制限時間ありの計算クイズの作成](tutorial-2-create-a-timed-math-quiz.md)
* [チュートリアル 3: 絵合わせゲームの作成](tutorial-3-create-a-matching-game.md)
