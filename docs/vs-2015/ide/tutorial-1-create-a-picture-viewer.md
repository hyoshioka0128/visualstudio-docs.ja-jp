---
title: 'チュートリアル 1: ピクチャ ビューアーの作成 | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
ms.assetid: 3071d6df-2b2f-4e95-ab68-bef727323136
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 66988fa88ae347a2db08bf2f6d1b79ba3bcd80b8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "75851317"
---
# <a name="tutorial-1-create-a-picture-viewer"></a>チュートリアル 1: ピクチャ ビューアーの作成
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このチュートリアルでは、ピクチャをファイルから読み込んでウィンドウに表示するプログラムを作成します。 ボタンやピクチャ ボックスなどのコントロールをフォームにドラッグする方法、それらのプロパティを設定する方法、およびコンテナーを使用してフォームのサイズを滑らかに変更する方法を習得できます。 また、コードの記述の基本事項についても学習します。 以下の方法について説明します。

- 新しいプロジェクトを作成します。

- アプリケーションをテスト (デバッグ) します。

- チェック ボックスやボタンなどの基本的なコントロールをフォームに追加します。

- レイアウトを使用してフォーム上のコントロールの位置を設定します。

- **[ファイルを開く]** ダイアログ ボックスと **[色]** ダイアログ ボックスをフォームに追加します。

- IntelliSense とコード スニペットを使用してコードを記述します。

- イベント ハンドラー メソッドを記述します。

  完成すると、プログラムは次の図のようになります。

  ![このチュートリアルで作成する画像](../ide/media/express-pictureviewerdone.png "Express_PictureViewerDone")このチュートリアルで作成する画像

  ![ビデオへのリンク](../data-tools/media/playvideo.gif "PlayVideo")このトピックのビデオ版については、「 [操作方法: Visual Basic でのピクチャビューアーの作成](https://msdn.microsoft.com/vstudio/gg315352) 」または「 [操作方法: C# でのピクチャビューアーの作成](https://msdn.microsoft.com/vcsharp/gg278960.aspx)」を参照してください。

> [!NOTE]
> これらのビデオでは、旧バージョンの Visual Studio を使用しているため、一部のメニュー コマンドやその他のユーザー インターフェイス要素が若干異なります。 ただし、概念および手順は、現在のバージョンの Visual Studio でも同様です。 このチュートリアルでは、Visual C# と Visual Basic の両方が取り上げられているため、使用しているプログラミング言語固有の情報に注意してください。
>
> Visual Basic のコードを表示するには、コードブロックの上部にある [ **VB** ] タブをクリックし、Visual c# のコードを表示するには、[ **c#** ] タブを選択します。Visual C++ の詳細については、「 [はじめに](../misc/getting-started-with-visual-cpp-in-visual-studio-2015.md) および [C++ 言語のチュートリアル](http://www.cplusplus.com/doc/tutorial/)」を参照してください。
>
> Windows ストア用の Visual C# アプリまたは Visual Basic アプリの記述方法の学習に関心がある場合は、「[C# または Visual Basic を使った初めての Windows ランタイム アプリの作成](https://msdn.microsoft.com/library/windows/apps/hh974581.aspx)」を参照してください。 Windows ストア用の JavaScript アプリの作成の詳細については、「[JavaScript を使った初めての Windows ランタイム アプリの作成](https://msdn.microsoft.com/library/windows/apps/br211385.aspx)」を参照してください。

## <a name="related-topics"></a>関連トピック

|Title|説明|
|-----------|-----------------|
|[手順 1: Windows フォーム アプリケーション プロジェクトの作成](../ide/step-1-create-a-windows-forms-application-project.md)|最初に Windows フォーム アプリケーション プロジェクトを作成します。|
|[手順 2: プログラムの実行](../ide/step-2-run-your-program.md)|前の手順で作成した Windows フォーム アプリケーション プログラムを実行します。|
|[手順 3: フォームのプロパティを設定する](../ide/step-3-set-your-form-properties.md)|**[プロパティ]** ウィンドウを使用してフォームの外観を変更します。|
|[手順 4: TableLayoutPanel コントロールを使用してフォームをレイアウトする](../ide/step-4-lay-out-your-form-with-a-tablelayoutpanel-control.md)|フォームに `TableLayoutPanel` コントロールを追加します。|
|[手順 5: フォームへのコントロールの追加](../ide/step-5-add-controls-to-your-form.md)|`PictureBox` コントロールや `CheckBox` コントロールなどのコントロールをフォームに追加します。 また、ボタンも追加します。|
|[手順 6: ボタンコントロールの名前を設定する](../ide/step-6-name-your-button-controls.md)|ボタンの名前をわかりやすい名前に変更します。|
|[手順 7: フォームへのダイアログコンポーネントの追加](../ide/step-7-add-dialog-components-to-your-form.md)|**OpenFileDialog** コンポーネントと **ColorDialog** コンポーネントをフォームに追加します。|
|[手順 8: [Show a Picture] ボタンのイベントハンドラーのコードを記述する](../ide/step-8-write-code-for-the-show-a-picture-button-event-handler.md)|IntelliSense ツールを使用してコードを記述します。|
|[手順 9: コードの確認、コメントの作成、およびテスト](../ide/step-9-review-comment-and-test-your-code.md)|コードのレビューとテストを行います。 必要に応じてコメントを追加します。|
|[手順 10: 追加のボタンとチェックボックスのコードを記述する](../ide/step-10-write-code-for-additional-buttons-and-a-check-box.md)|他のボタンやチェック ボックスを使用できるようにするために、IntelliSense を使用してコードを記述します。|
|[手順 11: プログラムを実行し、その他の機能を試す](../ide/step-11-run-your-program-and-try-other-features.md)|プログラムを実行して背景色を設定します。 色、フォント、および境界線の変更など、その他の機能を試します。|
