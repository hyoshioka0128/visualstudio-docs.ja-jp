---
title: CheckBox コントロールを使用してドキュメントの書式を変更する
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Word documents, changing formatting using controls
- documents [Office development in Visual Studio], formatting
- check boxes, Word documents
- documents [Office development in Visual Studio], check box controls
- controls [Office development in Visual Studio], adding to documents
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 24c3cb8d76551bb477f9c13cc56c313519f3b617
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "67328725"
---
# <a name="walkthrough-change-document-formatting-using-checkbox-controls"></a>チュートリアル: CheckBox コントロールを使用したドキュメント書式の変更
  このチュートリアルでは、Microsoft Office Word のドキュメントレベルのカスタマイズで Windows フォームコントロールを使用して、テキストの書式設定を変更する方法について説明します。

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

 このチュートリアルでは、次の作業について説明します。

- デザイン時にドキュメントレベルのプロジェクトの文書にテキストとコントロールを追加する。

- オプションを選択したときのテキストの書式設定。

  完成したサンプルとして結果を表示するには、「 [Office 開発のサンプルとチュートリアル](../vsto/office-development-samples-and-walkthroughs.md)」の Word コントロールのサンプルを参照してください。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)] または [!INCLUDE[Word_14_short](../vsto/includes/word-14-short-md.md)]。

## <a name="create-the-project"></a>プロジェクトの作成
 最初に、Word 文書のプロジェクトを作成します。

### <a name="create-a-new-project"></a>新しいプロジェクトを作成する

1. Word 文書プロジェクトを作成し、word の **書式を設定**します。 ウィザードで、[ **新しいドキュメントの作成**] を選択します。

     詳細については、「 [方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)」を参照してください。

     Visual Studio により、デザイナーで新しい Word 文書が開き、**ソリューションエクスプローラー**に**My Word の書式設定**プロジェクトが追加されます。

## <a name="add-text-and-controls-to-the-word-document"></a>Word 文書にテキストとコントロールを追加する
 このチュートリアルでは、3つのチェックボックスと、コントロール内のテキスト <xref:Microsoft.Office.Tools.Word.Bookmark> を Word 文書に追加します。 チェックボックスをオンにすると、テキストを書式設定するためのオプションがユーザーに表示されます。

### <a name="add-three-check-boxes"></a>3つのチェックボックスを追加する

1. Visual Studio デザイナーで文書が開いていることを確認します。

2. **ツールボックス**の [**コモンコントロール**] タブから、最初の <xref:Microsoft.Office.Tools.Word.Controls.CheckBox> コントロールを文書にドラッグします。

3. **[プロパティ]** ウィンドウで、次のプロパティを変更します。

    |プロパティ|値|
    |--------------|-----------|
    |**名前**|**Applybold フォント**|
    |**Text**|**太字**|

4. **Enter**キーを押して、最初のチェックボックスの下に挿入ポイントを移動します。

5. チェックボックスの下にあるドキュメントに2つ目のチェックボックスを追加 `ApplyBoldFont` し、次のプロパティを変更します。

    |プロパティ|値|
    |--------------|-----------|
    |**名前**|**Applybold フォント**|
    |**Text**|**斜体**|

6. **Enter**キーを押して、2番目のチェックボックスの下に挿入ポイントを移動します。

7. チェックボックスの下にあるドキュメントに3つ目のチェックボックスを追加 `ApplyItalicFont` し、次のプロパティを変更します。

    |プロパティ|値|
    |--------------|-----------|
    |**名前**|**applyUnderlineFont**|
    |**Text**|**強調**|

### <a name="add-text-and-a-bookmark-control"></a>テキストとブックマークコントロールを追加する

1. カーソル位置をチェックボックスコントロールの下に移動し、次のテキストを入力します。

    **このテキストの書式を変更するには、チェックボックスをオンにします。**

2. **ツールボックス**の [ **Word コントロール**] タブから、 <xref:Microsoft.Office.Tools.Word.Bookmark> コントロールを文書にドラッグします。

    [ **ブックマークコントロールの追加** ] ダイアログボックスが表示されます。

3. ドキュメントに追加したテキストを選択し、[ **OK]** をクリックします。

    <xref:Microsoft.Office.Tools.Word.Bookmark> **Bookmark1**という名前のコントロールが、ドキュメント内の選択したテキストに追加されます。

4. [ **プロパティ** ] ウィンドウで、 **(Name)** プロパティの値を fonttext に変更し **ます。**

   次に、チェックボックスがオンまたはオフになったときにテキストの書式を設定するコードを記述します。

## <a name="format-the-text-when-a-check-box-is-checked-or-cleared"></a>チェックボックスをオンまたはオフにしたときにテキストの書式を設定する
 ユーザーが書式設定オプションを選択した場合は、ドキュメント内のテキストの書式を変更します。

### <a name="change-formatting-when-a-check-box-is-selected"></a>チェックボックスをオンにしたときの書式設定の変更

1. `ThisDocument`**ソリューションエクスプローラー**を右クリックし、ショートカットメニューの [**コードの表示**] をクリックします。

2. C# の場合のみ、次の定数を **ThisDocument** クラスに追加します。

     [!code-csharp[Trin_VstcoreProgrammingControlsWord#2](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ThisDocument.cs#2)]

3. <xref:System.Windows.Forms.Control.Click>チェックボックスのイベントハンドラーに次のコードを追加し `applyBoldFont` ます。

     [!code-vb[Trin_VstcoreProgrammingControlsWord#3](../vsto/codesnippet/VisualBasic/my chart options/ThisDocument.vb#3)]
     [!code-csharp[Trin_VstcoreProgrammingControlsWord#3](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ThisDocument.cs#3)]

4. <xref:System.Windows.Forms.Control.Click>チェックボックスのイベントハンドラーに次のコードを追加し `applyItalicFont` ます。

     [!code-vb[Trin_VstcoreProgrammingControlsWord#4](../vsto/codesnippet/VisualBasic/my chart options/ThisDocument.vb#4)]
     [!code-csharp[Trin_VstcoreProgrammingControlsWord#4](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ThisDocument.cs#4)]

5. <xref:System.Windows.Forms.Control.Click>チェックボックスのイベントハンドラーに次のコードを追加し `applyUnderlineFont` ます。

     [!code-vb[Trin_VstcoreProgrammingControlsWord#5](../vsto/codesnippet/VisualBasic/my chart options/ThisDocument.vb#5)]
     [!code-csharp[Trin_VstcoreProgrammingControlsWord#5](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ThisDocument.cs#5)]

6. C# では、テキストボックスのイベントハンドラーをイベントに追加する必要があり <xref:Microsoft.Office.Tools.Word.Document.Startup> ます。 イベントハンドラーの作成方法の詳細については、「 [方法: Office プロジェクトでイベントハンドラーを作成](../vsto/how-to-create-event-handlers-in-office-projects.md)する」を参照してください。

     [!code-csharp[Trin_VstcoreProgrammingControlsWord#6](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ThisDocument.cs#6)]

## <a name="test-the-application"></a>アプリケーションをテストする
 ドキュメントをテストして、チェックボックスをオンまたはオフにしたときにテキストが正しく書式設定されていることを確認できるようになりました。

### <a name="test-your-document"></a>ドキュメントをテストする

1. **F5**キーを押して、プロジェクトを実行します。

2. チェック ボックスをオンまたはオフにします。

3. テキストが正しく書式設定されていることを確認します。

## <a name="next-steps"></a>次のステップ
 このチュートリアルでは、Word 文書でチェックボックスを使用し、プログラムによってテキストの書式を変更する方法の基本について説明します。 ここでは、次の作業を行います。

- ボタンを使用して、テキストボックスにデータを入力します。 詳細については、「 [チュートリアル: ボタンを使用してドキュメント内のテキストボックスにテキストを表示](../vsto/walkthrough-displaying-text-in-a-text-box-in-a-document-using-a-button.md)する」を参照してください。

- オプション ボタンを使用してグラフのスタイルを選択する。 詳細については、「 [チュートリアル: オプションボタンを使用してドキュメントのグラフを更新](../vsto/walkthrough-updating-a-chart-in-a-document-using-radio-buttons.md)する」を参照してください。

## <a name="see-also"></a>関連項目
- [Word を使用したチュートリアル](../vsto/walkthroughs-using-word.md)
- [Office 開発のサンプルとチュートリアル](../vsto/office-development-samples-and-walkthroughs.md)
- [NamedRange コントロール](../vsto/namedrange-control.md)
- [Office ドキュメントの Windows フォームコントロールの制限事項](../vsto/limitations-of-windows-forms-controls-on-office-documents.md)
