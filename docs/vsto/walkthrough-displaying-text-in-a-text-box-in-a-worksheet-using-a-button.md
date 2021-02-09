---
title: ボタンを使用してワークシートのテキストボックスにテキストを表示する
description: Microsoft Excel ワークシートでボタンとテキストボックスを使用する方法の基本について説明します。 また、Visual Studio の Office 開発ツールを使用して Excel プロジェクトを作成します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- text [Office development in Visual Studio], displaying worksheets
- worksheets, displaying text
- text boxes, displaying text in worksheets
- text [Office development in Visual Studio], text boxes
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 270754005704d91569f014ed2e0be382bc2dd707
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99906472"
---
# <a name="walkthrough-display-text-in-a-text-box-in-a-worksheet-using-a-button"></a>チュートリアル: ボタンを使用してワークシートのテキストボックスにテキストを表示する
  このチュートリアルでは Microsoft Office Excel ワークシートでボタンとテキストボックスを使用する方法、および Visual Studio の Office 開発ツールを使用して Excel プロジェクトを作成する方法の基本について説明します。 完成したサンプルとして結果を表示するには、「 [Office 開発のサンプルとチュートリアル](../vsto/office-development-samples-and-walkthroughs.md)」の Excel コントロールのサンプルを参照してください。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

 このチュートリアルでは、次の作業を行う方法について説明します。

- ワークシートにコントロールを追加します。

- ボタンがクリックされたときにテキストボックスに入力します。

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

1. [Excel の名前を付けてください **] ボタン** を使用して excel ブックプロジェクトを作成します。 [ **新しいドキュメントを作成** する。 詳細については、「 [方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)」を参照してください。

     新しい Excel ブックがデザイナーで開き、 **[My Excel Button]** プロジェクトが **ソリューションエクスプローラー** に追加されます。

## <a name="add-controls-to-the-worksheet"></a>ワークシートにコントロールを追加する
 このチュートリアルでは、最初のワークシートにボタンとテキストボックスが必要です。

### <a name="to-add-a-button-and-a-text-box"></a>ボタンとテキスト ボックスを追加するには

1. Visual Studio デザイナーで **[My Excel Button.xlsx** ] ブックが開き、表示されていることを確認し `Sheet1` ます。

2. ツールボックスの [ **コモンコントロール** ] タブから、 <xref:Microsoft.Office.Tools.Excel.Controls.TextBox> をにドラッグし `Sheet1` ます。

3. [ **表示** ] メニューの [ **プロパティウィンドウ**] をクリックします。

4. [**プロパティ**] ウィンドウのドロップダウンボックスに [ **TextBox1** ] が表示されていることを確認し、テキストボックスの [**名前**] プロパティを [表示可能 **] に変更** します。

5. **Button** コントロールをにドラッグ `Sheet1` し、次のプロパティを変更します。

   |プロパティ|値|
   |--------------|-----------|
   |**名前**|**insertText**|
   |**Text**|**テキストの挿入**|

   ここで、ボタンがクリックされたときに実行するコードを記述します。

## <a name="populate-the-text-box-when-the-button-is-clicked"></a>ボタンがクリックされたときにテキストボックスにデータを設定する
 ユーザーがボタンをクリックするたびに、 **Hello World ます。** がテキストボックスに追加されます。

### <a name="to-write-to-the-text-box-when-the-button-is-clicked"></a>ボタンがクリックされたときにテキスト ボックスに書き込むには

1. **ソリューションエクスプローラー** で、[ **Sheet1**] を右クリックし、ショートカットメニューの [**コードの表示**] をクリックします。

2. ボタンのイベントハンドラーに次のコードを追加し <xref:System.Windows.Forms.Control.Click> ます。

     [!code-vb[Trin_VstcoreProgrammingControlsExcel#11](../vsto/codesnippet/VisualBasic/my excel chart/Sheet1.vb#11)]
     [!code-csharp[Trin_VstcoreProgrammingControlsExcel#11](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs#11)]

3. C# では、次のようにイベントハンドラーをイベントに追加する必要があり <xref:Microsoft.Office.Tools.Excel.Worksheet.Startup> ます。 イベントハンドラーの作成の詳細については、「 [方法: Office プロジェクトでイベントハンドラーを作成](../vsto/how-to-create-event-handlers-in-office-projects.md)する」を参照してください。

     [!code-csharp[Trin_VstcoreProgrammingControlsExcel#12](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs#12)]

## <a name="test-the-application"></a>アプリケーションをテストする
 これで、ブックをテストして、メッセージが Hello World ことを確認できるようになりました **。** ボタンをクリックすると、テキストボックスに表示されます。

### <a name="to-test-your-workbook"></a>ブックをテストするには

1. **F5** キーを押して、プロジェクトを実行します。

2. ボタンをクリックします。

3. Hello World していることを確認し **ます。** がテキストボックスに表示されます。

## <a name="next-steps"></a>次の手順
 このチュートリアルでは、Excel ワークシートでボタンとテキストボックスを使用する方法の基本について説明します。 ここでは、次の作業を行います。

- プロジェクトを配置しています。 詳細については、「 [Office ソリューションの配置](../vsto/deploying-an-office-solution.md)」を参照してください。

- チェックボックスを使用して書式を変更します。 詳細については、「 [チュートリアル: CheckBox コントロールを使用してワークシートの書式を変更する](../vsto/walkthrough-changing-worksheet-formatting-using-checkbox-controls.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [方法: Office ドキュメントに Windows フォームコントロールを追加する](../vsto/how-to-add-windows-forms-controls-to-office-documents.md)
- [Excel を使用したチュートリアル](../vsto/walkthroughs-using-excel.md)
- [Office ドキュメントの Windows フォームコントロールの制限事項](../vsto/limitations-of-windows-forms-controls-on-office-documents.md)
