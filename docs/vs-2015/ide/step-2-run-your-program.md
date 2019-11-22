---
title: '手順 2: プログラムの実行 | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
ms.assetid: 9a8fe90e-c97b-4e98-b6c8-0c6b3962c49d
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: ef28781252181dbf765db52dbe6fed1b286516b2
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74295774"
---
# <a name="step-2-run-your-program"></a>手順 2: プログラムの実行
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

新しいソリューションを作成すると、実際には実行するプログラムが作成されます。 まだ実行される処理は少なく、タイトル バーに **Form1** と表示された空のウィンドウを表示するだけのプログラムですが、 もうおわかりのように実行することはできます。

 ![link to video](../data-tools/media/playvideo.gif "PlayVideo")For a video version of this topic, see [Tutorial 1: Create a Picture Viewer in Visual Basic - Video 1](https://go.microsoft.com/fwlink/?LinkId=205209) or [Tutorial 1: Create a Picture Viewer in C# - Video 1](https://go.microsoft.com/fwlink/?LinkId=205199). これらのビデオでは、旧バージョンの Visual Studio を使用しているため、一部のメニュー コマンドやその他のユーザー インターフェイス要素が若干異なります。 ただし、概念および手順は、現在のバージョンの Visual Studio でも同様です。

### <a name="to-run-your-program"></a>プログラムを実行するには

1. プログラムを実行するには、次のいずれかの方法を使用します。

    - **F5** キーを押します。

    - メニュー バーで、 **[デバッグ]** 、 **[デバッグ開始]** の順に選択します。

    - ツール バーで、 **[デバッグ開始]** ボタンを選択します (次の図を参照)。

         ![Start Debugging toolbar button](../ide/media/express-icondebug.png "Express_IconDebug") Start Debugging toolbar button

2. Visual Studio でプログラムが実行され、**Form1** というウィンドウが表示されます。 次の図は、作成したプログラムを示しています。 この実行中のプログラムに対し、これから機能を追加していきます。

     ![Windows Form application program running](../ide/media/express-firstrun.png "Express_FirstRun") Windows Form Application program running

3. Visual Studio 統合開発環境 (IDE) に戻り、新しいツール バーを参照します。 プログラムを実行すると、追加ボタンがツール バーに表示されます。 これらのボタンを使用するとプログラムの停止や開始などの操作ができ、発生する可能性のあるエラー (バグ) の追跡に役立ちます。 この例では、単にプログラムを開始および停止するために使用します。

     ![Debugging toolbar](../ide/media/express-debugtoolbar.png "Express_DebugToolbar") Debugging toolbar

4. プログラムを停止するには、次のいずれかの方法を使用します。

    - ツール バーで、 **[デバッグの停止]** ボタンを選択します。

    - メニュー バーで、 **[デバッグ]** 、 **[デバッグの停止]** の順に選択します。

    - **[Form1]** ウィンドウの上隅にある X ボタンを選択します。

    > [!NOTE]
    > IDE 内からプログラムを実行する作業は、通常はプログラムでバグ (エラー) を特定して修正することが目的であるため*デバッグ*と呼ばれます。 このプログラムは小さくて、実際には何も実行しませんが、それでも実際のプログラムです。 同じ手順で他のプログラムを実行し、デバッグします。 デバッグの詳細については、「[デバッガーの基本事項](../debugger/debugger-basics.md)」を参照してください。

### <a name="to-continue-or-review"></a>続行または確認するには

- チュートリアルの次の手順に進む場合は、「[手順 3: フォームのプロパティの設定](../ide/step-3-set-your-form-properties.md)」を参照してください。

- チュートリアルの前の手順に戻る場合は、「[手順 1: Windows フォーム アプリケーション プロジェクトの作成](../ide/step-1-create-a-windows-forms-application-project.md)」を参照してください。
