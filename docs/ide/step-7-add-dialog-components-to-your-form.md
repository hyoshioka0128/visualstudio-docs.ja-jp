---
title: '手順 7: フォームへのダイアログ コンポーネントの追加'
description: <xref:System.Windows.Forms.OpenFileDialog> ダイアログ コンポーネントおよび <xref:System.Windows.Forms.ColorDialog> ダイアログ コンポーネントをフォームに追加する方法を説明します。
ms.custom: SEO-VS-2020
ms.date: 08/30/2019
ms.assetid: ea98c55e-6213-4893-ba7b-f19d7f119527
ms.topic: tutorial
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
author: ornellaalt
ms.author: ornella
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: a485433ef73ef853a186a5b441396f6d5a57f679
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99868856"
---
# <a name="step-7-add-dialog-components-to-your-form"></a>手順 7: フォームへのダイアログ コンポーネントの追加

アプリで図ファイルを開き、背景色を選択できるようにするために、この手順では <xref:System.Windows.Forms.OpenFileDialog> コンポーネントと <xref:System.Windows.Forms.ColorDialog> コンポーネントをフォームに追加します。

コンポーネントは、いくつかの点でコントロールに似ています。 コンポーネントは **ツールボックス** を使用してフォームに追加し、そのプロパティの設定には **[プロパティ]** ウィンドウを使用します。 ただし、コントロールとは異なり、コンポーネントをフォームに追加しても、ユーザーに表示される項目がフォームに追加されるわけではありません。 代わりに、コードで発生させることができる特定の動作が提供されます。 ここで追加するのは、**[ファイルを開く]** ダイアログ ボックスを開くコンポーネントです。

## <a name="to-add-dialog-components-to-your-form"></a>フォームにダイアログ コンポーネントを追加するには

1. **Windows フォーム デザイナー** (**Form1.cs [デザイン]**) を選択し、**ツールボックス** の **[ダイアログ]** グループを開きます。

    > [!NOTE]
    > **ツールボックス** の **[ダイアログ]** グループには、多数の便利なダイアログ ボックスを開くコンポーネントが含まれています。これらは、ファイルを開く、ファイルを保存する、フォルダーを参照する、フォントや色を選択するなど、さまざまな用途で使用できます。 このプロジェクトでは、OpenFileDialog と ColorDialog という 2 つのダイアログ コンポーネントを使用します。

1. **openFileDialog1** というコンポーネントをフォームに追加するには、**[OpenFileDialog]** をダブルクリックします。 **colorDialog1** というコンポーネントをフォームに追加するには、**ツールボックス** の **[ColorDialog]** をダブルクリックします  (このコンポーネントはチュートリアルの次の手順で使用します)。**Windows フォーム デザイナー** の下部の領域 (**Picture Viewer** フォームの下) に、次の図に示すように、追加した 2 つのダイアログ コンポーネントのそれぞれに対応するアイコンが表示されます。

     ![ダイアログ コンポーネント](../ide/media/express_dialogsadded.png)<br>***ダイアログ** _ _コンポーネント*

1. **Windows フォーム デザイナー** の下部にある領域で **[openFileDialog1]** アイコンを選択します。 2 つのプロパティを次のように設定します。

    - **Filter** プロパティを次のように設定します (コピーして貼り付けることができます)。

        ```
        JPEG Files (*.jpg)|*.jpg|PNG Files (*.png)|*.png|BMP Files (*.bmp)|*.bmp|All files (*.*)|*.*
        ```

    - **Title** プロパティを **Select a picture file** に設定します。

         **Filter** プロパティの設定は、**[Select a picture]** ファイル ダイアログ ボックスに表示されるファイルの種類を指定します。

    > [!TIP]
    > 他のアプリケーションで **[ファイルを開く]** ダイアログ ボックスの例を確認するには、**メモ帳** または **ペイント** を開き、メニュー バーで、**[ファイル]** > **[開く]** の順に選択します。 ファイル名の横に、ファイルの種類を選択できるドロップダウン リストが表示されていることに注目してください。 <br/><br/>アプリでは、それを設定するために **OpenFileDialog** コンポーネントの **Filter** プロパティを使用しました。 また、**Title** プロパティと **Filter** プロパティが **[プロパティ]** ウィンドウで太字になっていることに注目してください。 IDE では、既定値とは異なる値に変更されたプロパティがわかるように、それらが太字で示されます。

## <a name="next-steps"></a>次のステップ

* チュートリアルの次の手順に進むには、「 **[手順 8:[Show a Picture] ボタンのイベント ハンドラーのコードの記述](../ide/step-8-write-code-for-the-show-a-picture-button-event-handler.md)** 」を参照してください。

* 前のチュートリアルの手順に戻る場合は、「[手順 6: ボタン コントロールの名前の設定](../ide/step-6-name-your-button-controls.md)」をご覧ください。

## <a name="see-also"></a>関連項目

* [チュートリアル 2: 制限時間ありの計算クイズの作成](tutorial-2-create-a-timed-math-quiz.md)
* [チュートリアル 3: 絵合わせゲームの作成](tutorial-3-create-a-matching-game.md)
