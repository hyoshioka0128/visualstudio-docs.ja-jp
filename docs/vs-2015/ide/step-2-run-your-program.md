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
ms.openlocfilehash: 2ddec4c7327aa9799ae8a12a04b3940d690205cb
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "75851573"
---
# <a name="step-2-run-your-program"></a>手順 2: プログラムの実行
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

新しいソリューションを作成すると、実際には実行するプログラムが作成されます。 まだ実行される処理は少なく、タイトル バーに **Form1** と表示された空のウィンドウを表示するだけのプログラムですが、 もうおわかりのように実行することはできます。

 ![ビデオへのリンク](../data-tools/media/playvideo.gif "PlayVideo")このトピックのビデオ版については、「 [チュートリアル 1: Visual Basic でのピクチャビューアーの作成](https://msdn.microsoft.com/vbasic/gg315352.aspx) -ビデオ1」または「 [チュートリアル 1: C# でのピクチャビューアーの作成-ビデオ 1](https://msdn.microsoft.com/vcsharp/gg278409.aspx)」を参照してください。 これらのビデオでは、旧バージョンの Visual Studio を使用しているため、一部のメニュー コマンドやその他のユーザー インターフェイス要素が若干異なります。 ただし、概念および手順は、現在のバージョンの Visual Studio でも同様です。

### <a name="to-run-your-program"></a>プログラムを実行するには

1. プログラムを実行するには、次のいずれかの方法を使用します。

    - **F5** キーを押します。

    - メニュー バーで、 **[デバッグ]** 、 **[デバッグ開始]** の順に選択します。

    - ツールバーで、[ **デバッグの開始** ] ボタンをクリックします。このボタンは次のように表示されます。

         ![[デバッグの開始] ツールバーボタン](../ide/media/express-icondebug.png "Express_IconDebug") [デバッグの開始] ツールバーボタン

2. Visual Studio でプログラムが実行され、**Form1** というウィンドウが表示されます。 次の図は、作成したプログラムを示しています。 この実行中のプログラムに対し、これから機能を追加していきます。

     ![Windows フォームアプリケーションプログラムを実行して](../ide/media/express-firstrun.png "Express_FirstRun") いますWindows フォームアプリケーションプログラムを実行しています

3. Visual Studio 統合開発環境 (IDE) に戻り、新しいツール バーを参照します。 プログラムを実行すると、追加ボタンがツール バーに表示されます。 これらのボタンを使用するとプログラムの停止や開始などの操作ができ、発生する可能性のあるエラー (バグ) の追跡に役立ちます。 この例では、単にプログラムを開始および停止するために使用します。

     ![デバッグツールバー](../ide/media/express-debugtoolbar.png "Express_DebugToolbar") デバッグツールバー

4. プログラムを停止するには、次のいずれかの方法を使用します。

    - ツール バーで、 **[デバッグの停止]** ボタンを選択します。

    - メニュー バーで、**[デバッグ]**、**[デバッグの停止]** の順に選択します。

    - **[Form1]** ウィンドウの上隅にある X ボタンを選択します。

    > [!NOTE]
    > IDE 内からプログラムを実行する場合は、通常、プログラムでバグ (エラー) を見つけて修正するために、 *デバッグ* と呼ばれます。 このプログラムは小さくて、実際には何も実行しませんが、それでも実際のプログラムです。 同じ手順で他のプログラムを実行し、デバッグします。 デバッグの詳細については、「 [デバッガーの基本](../debugger/debugger-basics.md)」を参照してください。

### <a name="to-continue-or-review"></a>続行または確認するには

- チュートリアルの次の手順に進むには、「 [手順 3: フォームのプロパティを設定](../ide/step-3-set-your-form-properties.md)する」を参照してください。

- チュートリアルの前の手順に戻るには、「 [手順 1: Windows フォームアプリケーションプロジェクトを作成](../ide/step-1-create-a-windows-forms-application-project.md)する」を参照してください。
