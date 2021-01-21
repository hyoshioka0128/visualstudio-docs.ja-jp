---
title: チェックボックスコントロールを使用してワークシートの書式を変更する
description: Visual Studio の Office 開発ツールを使用して、プロジェクトにコードを作成して追加する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- worksheets, changing formatting using managed controls
- worksheets, check box controls
- controls [Office development in Visual Studio], adding to worksheets
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 28b9f000c2e8517304387e2b203dfa7888b33d64
ms.sourcegitcommit: 4bd2b770e60965fc0843fc25318a7e1b46137875
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/15/2020
ms.locfileid: "97527226"
---
# <a name="walkthrough-change-worksheet-formatting-using-checkbox-controls"></a>チュートリアル: CheckBox コントロールを使用したワークシートの書式設定の変更
  このチュートリアルでは、Microsoft Office Excel ワークシートでチェックボックスを使用して書式を変更する方法の基本について説明します。 プロジェクトにコードを作成して追加するには、Visual Studio の Office 開発ツールを使用します。 完成したサンプルとして結果を表示するには、「 [Office 開発のサンプルとチュートリアル](../vsto/office-development-samples-and-walkthroughs.md)」の Excel コントロールのサンプルを参照してください。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

 このチュートリアルでは、次の作業を行う方法について説明します。

- ワークシートにテキストとコントロールを追加します。

- オプションを選択したときにテキストの書式を設定します。

- プロジェクトをテストします。

> [!NOTE]
> 次の手順で参照している Visual Studio ユーザー インターフェイス要素の一部は、お使いのコンピューターでは名前や場所が異なる場合があります。 これらの要素は、使用している Visual Studio のエディションや独自の設定によって決まります。 詳細については、「[Visual Studio IDE のカスタマイズ](../ide/personalizing-the-visual-studio-ide.md)」を参照してください。

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)] または [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)]。

## <a name="create-the-project"></a>プロジェクトを作成する
 この手順では、Visual Studio を使用して Excel ブックプロジェクトを作成します。

### <a name="to-create-a-new-project"></a>新しいプロジェクトを作成するには

1. 「 **My excel の書式設定**」という名前の excel ブックプロジェクトを作成します。 [ **新しいドキュメントを作成** する。 詳細については、「 [方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)」を参照してください。

     新しい Excel ブックがデザイナーで開き、 **[My Excel 書式** ] プロジェクトが **ソリューションエクスプローラー** に追加されます。

## <a name="add-text-and-controls-to-the-worksheet"></a>ワークシートにテキストとコントロールを追加する
 このチュートリアルでは、コントロールに3つの <xref:Microsoft.Office.Tools.Excel.Controls.CheckBox> コントロールといくつかのテキストが必要です <xref:Microsoft.Office.Tools.Excel.NamedRange> 。

### <a name="to-add-three-check-boxes"></a>3つのチェックボックスを追加するには

1. ブックが Visual Studio デザイナーで開かれていて、開いていることを確認し `Sheet1` ます。

2. **ツールボックス** の [**コモンコントロール**] タブから、 <xref:Microsoft.Office.Tools.Excel.Controls.CheckBox> コントロールを **Sheet1** 内またはセル **B2** の近くにドラッグします。

3. [ **表示** ] メニューの [ **プロパティ** ウィンドウ] をクリックします。

4. [**プロパティ**] ウィンドウの [オブジェクト名] ボックスの一覧に **Checkbox1** が表示されていることを確認し、次のプロパティを変更します。

    |プロパティ|値|
    |--------------|-----------|
    |**名前**|**Applybold フォント**|
    |**テキスト**|**太字**|

5. セル **B4** の横にある2つ目のチェックボックスをドラッグし、次のプロパティを変更します。

    |プロパティ|値|
    |--------------|-----------|
    |**名前**|**Applybold フォント**|
    |**テキスト**|**斜体**|

6. セル **B6** の横にある3番目のチェックボックスをドラッグし、次のプロパティを変更します。

    |プロパティ|値|
    |--------------|-----------|
    |**名前**|**applyUnderlineFont**|
    |**テキスト**|**Underline**|

7. **Ctrl** キーを押しながら、3つのチェックボックスコントロールをすべて選択します。

8. Excel の [書式] タブの [配置] グループで、[ **配置**] をクリックし、[ **左揃え**] をクリックします。

     3つのチェックボックスコントロールは、選択した最初のコントロールの位置で左側に配置されます。

     次に、 <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールをワークシートにドラッグします。

    > [!NOTE]
    > また、 <xref:Microsoft.Office.Tools.Excel.NamedRange> [**名前**] ボックスに「 **textfont** 」と入力してコントロールを追加することもできます。

#### <a name="to-add-text-to-a-namedrange-control"></a>NamedRange コントロールにテキストを追加するには

1. ツールボックスの [ **Excel コントロール** ] タブから、 <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールをセル **B9** にドラッグします。

2. 編集可能なテキストボックスに **$B $9** が表示され、セル **B9** が選択されていることを確認します。 そうでない場合は、セル **B9** をクリックして選択します。

3. **[OK]** をクリックします。

4. セル **B9** は、という名前の範囲になり `NamedRange1` ます。

    ワークシートには表示されませんが、 `NamedRange1` セル **B9** を選択すると、[**名前] ボックス**(左側のワークシートのすぐ上) に表示されます。

5. [**プロパティ**] ウィンドウの [オブジェクト名] ボックスの一覧に **NamedRange1** が表示されていることを確認し、次のプロパティを変更します。

   |プロパティ|値|
   |--------------|-----------|
   |**名前**|**textFont**|
   |**Value2**|**このテキストの書式を変更するには、チェックボックスをオンにします。**|

   次に、オプションを選択したときにテキストの書式を設定するコードを記述します。

## <a name="format-the-text-when-an-option-is-selected"></a>オプションを選択したときにテキストの書式を設定する
 このセクションでは、ユーザーが書式設定オプションを選択したときに、ワークシート内のテキストの書式が変更されるようにコードを記述します。

### <a name="to-change-formatting-when-a-check-box-is-selected"></a>チェックボックスをオンにしたときに書式を変更するには

1. [ **Sheet1**] を右クリックし、ショートカットメニューの [ **コードの表示** ] をクリックします。

2. <xref:System.Windows.Forms.Control.Click>チェックボックスのイベントハンドラーに次のコードを追加し `applyBoldFont` ます。

     [!code-vb[Trin_VstcoreProgrammingControlsExcel#7](../vsto/codesnippet/VisualBasic/my excel chart/Sheet1.vb#7)]
     [!code-csharp[Trin_VstcoreProgrammingControlsExcel#7](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs#7)]

3. <xref:System.Windows.Forms.Control.Click>チェックボックスのイベントハンドラーに次のコードを追加し `applyItalicFont` ます。

     [!code-vb[Trin_VstcoreProgrammingControlsExcel#8](../vsto/codesnippet/VisualBasic/my excel chart/Sheet1.vb#8)]
     [!code-csharp[Trin_VstcoreProgrammingControlsExcel#8](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs#8)]

4. <xref:System.Windows.Forms.Control.Click>チェックボックスのイベントハンドラーに次のコードを追加し `applyUnderlineFont` ます。

     [!code-vb[Trin_VstcoreProgrammingControlsExcel#9](../vsto/codesnippet/VisualBasic/my excel chart/Sheet1.vb#9)]
     [!code-csharp[Trin_VstcoreProgrammingControlsExcel#9](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs#9)]

5. C# では、次に示すように、チェックボックスのイベントハンドラーをイベントに追加する必要があり <xref:Microsoft.Office.Tools.Excel.Worksheet.Startup> ます。 イベントハンドラーの作成の詳細については、「 [方法: Office プロジェクトでイベントハンドラーを作成](../vsto/how-to-create-event-handlers-in-office-projects.md)する」を参照してください。

     [!code-csharp[Trin_VstcoreProgrammingControlsExcel#10](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs#10)]

## <a name="test-the-application"></a>アプリケーションをテストする
 これで、チェックボックスをオンまたはオフにしたときに、テキストが正しく書式設定されていることを確認するために、ブックをテストできるようになりました。

### <a name="to-test-your-workbook"></a>ブックをテストするには

1. **F5** キーを押して、プロジェクトを実行します。

2. チェック ボックスをオンまたはオフにします。

3. テキストが正しく書式設定されていることを確認します。

## <a name="next-steps"></a>次のステップ
 このチュートリアルでは、Excel ワークシートでチェックボックスを使用してテキストを書式設定する方法の基本について説明します。 ここでは、次の作業を行います。

- プロジェクトを配置しています。 詳細については、「 [ClickOnce を使用した Office ソリューションの配置](../vsto/deploying-an-office-solution-by-using-clickonce.md)」を参照してください。
- ボタンを使用してテキスト ボックスへデータを挿入する。 詳細については、「 [チュートリアル: ボタンを使用してワークシートのテキストボックスにテキストを表示](../vsto/walkthrough-displaying-text-in-a-text-box-in-a-worksheet-using-a-button.md)する」を参照してください。

## <a name="see-also"></a>関連項目
- [Excel を使用したチュートリアル](../vsto/walkthroughs-using-excel.md)
- [NamedRange コントロール](../vsto/namedrange-control.md)
- [Office ドキュメントの Windows フォームコントロールの制限事項](../vsto/limitations-of-windows-forms-controls-on-office-documents.md)
