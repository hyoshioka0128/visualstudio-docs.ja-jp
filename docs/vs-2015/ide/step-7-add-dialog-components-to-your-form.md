---
title: '手順 7: フォームへのダイアログ コンポーネントの追加 | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
ms.assetid: ea98c55e-6213-4893-ba7b-f19d7f119527
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: f734c818265d32f6895c09ab01fd2468e0f5a247
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74295681"
---
# <a name="step-7-add-dialog-components-to-your-form"></a>手順 7: フォームへのダイアログ コンポーネントの追加
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

この手順で、図ファイルを開き、背景色を選択するためにプログラムを有効にするには、**OpenFileDialog** コンポーネントと **ColorDialog** コンポーネントをフォームに追加します。

 コンポーネントは、いくつかの点でコントロールに似ています。 コンポーネントはツールボックスを使用してフォームに追加し、そのプロパティの設定には **[プロパティ]** ウィンドウを使用します。 ただし、コントロールとは異なり、コンポーネントをフォームに追加しても、ユーザーに表示される項目がフォームに追加されるわけではありません。 代わりに、コードで発生させることができる特定の動作が提供されます。 ここで追加するのは、 **[ファイルを開く]** ダイアログ ボックスを開くコンポーネントです。

 ![ビデオへのリンク](../data-tools/media/playvideo.gif "PlayVideo")このトピックのビデオ版については、「[チュートリアル 1: Visual Basic でのピクチャビューアーの作成-](https://go.microsoft.com/fwlink/?LinkId=205213)ビデオ3」または「[チュートリアル 1 C# : ピクチャビューアーの作成-ビデオ 3](https://go.microsoft.com/fwlink/?LinkId=205202)」を参照してください。 これらのビデオでは、旧バージョンの Visual Studio を使用しているため、一部のメニュー コマンドやその他のユーザー インターフェイス要素が若干異なります。 ただし、概念および手順は、現在のバージョンの Visual Studio でも同様です。

### <a name="to-add-dialog-components-to-your-form"></a>フォームにダイアログ コンポーネントを追加するには

1. Windows フォーム デザイナー (Form1.cs [デザイン] または Form1.vb [デザイン]) を選択し、ツールボックスの **[ダイアログ]** グループを開きます。

    > [!NOTE]
    > ツールボックスの **[ダイアログ]** グループには、多数の便利なダイアログ ボックスを開くコンポーネントが含まれています。これらは、ファイルを開く、ファイルを保存する、フォルダーを参照する、フォントや色を選択するなど、さまざまな用途で使用できます。 このプロジェクトでは、**OpenFileDialog** と **ColorDialog** という 2 つのダイアログ コンポーネントを使用します。

2. **openFileDialog1** というコンポーネントをフォームに追加するには、 **[OpenFileDialog]** をダブルクリックします。 **colorDialog1** というコンポーネントを追加するには、ツールボックスの **[ColorDialog]** をダブルクリックします (次のチュートリアルの手順で使用します)。次の図に示すように、追加した2つのダイアログコンポーネントのそれぞれに対応するアイコンが表示された Windows フォームデザイナーの下部 (Picture Viewer フォームの下) に領域が表示されます。

     ![ダイアログコンポーネント](../ide/media/express-dialogsadded.png "Express_DialogsAdded")ダイアログコンポーネント

3. Windows フォーム デザイナーの下部にある領域で **[openFileDialog1]** アイコンを選択します。 2 つのプロパティを次のように設定します。

    - **Filter** プロパティを次のように設定します (コピーして貼り付けることができます)。

        ```
        JPEG Files (*.jpg)|*.jpg|PNG Files (*.png)|*.png|BMP Files (*.bmp)|*.bmp|All files (*.*)|*.*
        ```

    - **Title** プロパティを **Select a picture file** に設定します。

         **Filter** プロパティの設定は、 **[Select a picture]** ファイル ダイアログ ボックスに表示されるファイルの種類を指定します。

    > [!NOTE]
    > 他のアプリケーションで **[ファイルを開く]** ダイアログ ボックスの例を確認するには、メモ帳またはウィンドウトを開き、メニュー バーで、 **[ファイル]** 、 **[開く]** の順に選択します。 下部にある **[ファイルの種類]** ドロップダウン リストに注目してください。 ここではそのボックスの内容を、**OpenFileDialog** コンポーネントの **Filter** プロパティを使用して設定しました。 また、**Title** プロパティと **Filter** プロパティが **[プロパティ]** ウィンドウで太字になっていることに注目してください。 IDE では、既定値とは異なる値に変更されたプロパティがわかるように、それらが太字で示されます。

### <a name="to-continue-or-review"></a>続行または確認するには

- 次のチュートリアルの手順に進む場合は、「[手順 8: [Show a Picture] ボタンのイベント ハンドラーのコードの記述](../ide/step-8-write-code-for-the-show-a-picture-button-event-handler.md)」を参照してください。

- 前のチュートリアルの手順に戻る場合は、「[手順 6: ボタン コントロールの名前の設定](../ide/step-6-name-your-button-controls.md)」を参照してください。
