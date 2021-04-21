---
title: 'チュートリアル: NamedRange コントロールのイベントに対するプログラミング'
description: Visual Studio の Office 開発ツールを使用して、Microsoft Excel ワークシートに NamedRange コントロールを追加し、そのイベントに対してプログラムを作成する方法について説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ranges, programming against events
- worksheets, changing cell values
- NamedRange control, events
- worksheets, events
- worksheets, automating
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: ec1c670867fae277a3c3c8290cd34d0d4be7ddf3
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107824966"
---
# <a name="walkthrough-program-against-events-of-a-namedrange-control"></a>チュートリアル: NamedRange コントロールのイベントに対するプログラミング
  このチュートリアルでは、 <xref:Microsoft.Office.Tools.Excel.NamedRange> Visual Studio の Office 開発ツールを使用して、Microsoft Office Excel ワークシートにコントロールを追加し、そのイベントに対してプログラムを作成する方法について説明します。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

 このチュートリアルでは、次の作業を行う方法について説明します。

- <xref:Microsoft.Office.Tools.Excel.NamedRange>ワークシートにコントロールを追加します。

- コントロールイベントに対してプログラム <xref:Microsoft.Office.Tools.Excel.NamedRange> を実行します。

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

1. **"My 名前付き範囲イベント" という** 名前の Excel ブックプロジェクトを作成します。 [ **新しいドキュメントを作成** する。 詳細については、「 [方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)」を参照してください。

     デザイナーで新しい Excel ブックが開き、**ソリューションエクスプローラー** に **My 名前付き範囲のイベント** プロジェクトが追加されます。

## <a name="add-text-and-named-ranges-to-the-worksheet"></a>ワークシートにテキストと名前付き範囲を追加する
 ホストコントロールは Office の拡張オブジェクトであるため、ネイティブオブジェクトを追加するのと同じ方法でドキュメントに追加することができます。 たとえば、ワークシートに Excel コントロールを追加するには、[ <xref:Microsoft.Office.Tools.Excel.NamedRange> **挿入** ] メニューを開き、[ **名前**] をポイントし、[ **定義**] をクリックします。 また、 <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールを [ **ツールボックス** ] からワークシートにドラッグして追加することもできます。

 この手順では、 **ツールボックス** を使用して2つの名前付き範囲コントロールをワークシートに追加し、ワークシートにテキストを追加します。

### <a name="to-add-a-range-to-your-worksheet"></a>ワークシートに範囲を追加するには

1. Visual Studio デザイナーで *[名前付き範囲 Events.xlsx* ブック] が開き、表示されていることを確認 `Sheet1` します。

2. ツールボックスの [ **Excel コントロール** ] タブから、 <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールをセル **A1** にドラッグし `Sheet1` ます。

     [ **NamedRange コントロールの追加** ] ダイアログボックスが表示されます。

3. 編集可能なテキストボックスに **$A $1** が表示され、セル **A1** が選択されていることを確認します。 そうでない場合は、セル **A1** をクリックして選択します。

4. **[OK]** をクリックします。

     セル **A1** は、という名前の範囲になり `namedRange1` ます。 ワークシートには表示されませんが、 `namedRange1` セル **A1** が選択されている場合は、(左側のワークシートのすぐ上にある) [**名前**] ボックスに表示されます。

5. <xref:Microsoft.Office.Tools.Excel.NamedRange>セル **B3** に別のコントロールを追加します。

6. 編集可能なテキストボックスに **$B $3** が表示され、そのセル **B3** が選択されていることを確認します。 そうでない場合は、セル **B3** をクリックして選択します。

7. **[OK]** をクリックします。

     セル **B3** は、という名前の範囲になり `namedRange2` ます。

### <a name="to-add-text-to-your-worksheet"></a>ワークシートにテキストを追加するには

1. セル **A1** で、次のテキストを入力します。

    **これは、NamedRange コントロールの例です。**

2. セル **A3** (の左側 `namedRange2` ) に、次のテキストを入力します。

    **記録**

   次のセクションでは `namedRange2` `namedRange2` <xref:Microsoft.Office.Tools.Excel.NamedRange.BeforeDoubleClick> 、の、、およびイベントに応答して、テキストを挿入し、コントロールのプロパティを変更するコードを記述し <xref:Microsoft.Office.Tools.Excel.NamedRange.Change> <xref:Microsoft.Office.Tools.Excel.NamedRange.SelectionChange> `namedRange1` ます。

## <a name="add-code-to-respond-to-the-beforedoubleclick-event"></a>BeforeDoubleClick イベントに応答するコードを追加します

### <a name="to-insert-text-into-namedrange2-based-on-the-beforedoubleclick-event"></a>BeforeDoubleClick イベントに基づいて NamedRange2 にテキストを挿入するには

1. **ソリューションエクスプローラー** で、 **Sheet1** または **sheet1** を右クリックして [コードの **表示**] を選択します。

2. イベントハンドラーが次のようになるように、コードを追加し `namedRange1_BeforeDoubleClick` ます。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs" id="Snippet24":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet1.vb" id="Snippet24":::

3. C# では、次のイベントに示すように、名前付き範囲のイベントハンドラーを追加する必要があり <xref:Microsoft.Office.Tools.Excel.Worksheet.Startup> ます。 イベントハンドラーの作成の詳細については、「 [方法: Office プロジェクトでイベントハンドラーを作成](../vsto/how-to-create-event-handlers-in-office-projects.md)する」を参照してください。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs" id="Snippet25":::

## <a name="add-code-to-respond-to-the-change-event"></a>変更イベントに応答するコードを追加します

### <a name="to-insert-text-into-namedrange2-based-on-the-change-event"></a>Change イベントに基づいて namedRange2 にテキストを挿入するには

1. イベントハンドラーが次のようになるように、コードを追加し `NamedRange1_Change` ます。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs" id="Snippet26":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet1.vb" id="Snippet26":::

    > [!NOTE]
    > Excel 範囲内のセルをダブルクリックすると編集モードに切り替わるため、 <xref:Microsoft.Office.Tools.Excel.NamedRange.Change> テキストが変更されていない場合でも、選択が範囲外に移動するときにイベントが発生します。

## <a name="add-code-to-respond-to-the-selectionchange-event"></a>SelectionChange イベントに応答するコードを追加します。

### <a name="to-insert-text-into-namedrange2-based-on-the-selectionchange-event"></a>SelectionChange イベントに基づいて namedRange2 にテキストを挿入するには

1. **NamedRange1_SelectionChange** イベントハンドラーが次のようになるようにコードを追加します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs" id="Snippet27":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet1.vb" id="Snippet27":::

    > [!NOTE]
    > Excel 範囲内のセルをダブルクリックすると選択範囲が範囲内に移動するため、イベントが <xref:Microsoft.Office.Tools.Excel.NamedRange.SelectionChange> 発生する前にイベントが発生し <xref:Microsoft.Office.Tools.Excel.NamedRange.BeforeDoubleClick> ます。

## <a name="test-the-application"></a>アプリケーションをテストする
 次に、ブックをテストして、イベントが発生したときに、コントロールのイベントを説明するテキストが <xref:Microsoft.Office.Tools.Excel.NamedRange> 別の名前付き範囲に挿入されていることを確認します。

### <a name="to-test-your-document"></a>文書をテストするには

1. **F5** キーを押して、プロジェクトを実行します。

2. にカーソルを置き、 `namedRange1` イベントに関するテキストが <xref:Microsoft.Office.Tools.Excel.NamedRange.SelectionChange> 挿入され、ワークシートにコメントが挿入されていることを確認します。

3. [内側] `namedRange1` をダブルクリックすると、イベントに関するテキスト <xref:Microsoft.Office.Tools.Excel.NamedRange.BeforeDoubleClick> がに赤い斜体のテキストで挿入されていることを確認し `namedRange2` ます。

4. の外側をクリックする `namedRange1` と、テキストに変更が加えられていなくても編集モードを終了したときに変更イベントが発生することに注意してください。

5. 内のテキストを変更 `namedRange1` します。

6. の外側をクリックし、 `namedRange1` テキストに関する [関連 <xref:Microsoft.Office.Tools.Excel.NamedRange.Change> イベント] が青色のテキストと共に挿入されていることを確認し `namedRange2` ます。

## <a name="next-steps"></a>次のステップ
 このチュートリアルでは、コントロールのイベントに対するプログラミングの基本について説明し <xref:Microsoft.Office.Tools.Excel.NamedRange> ます。 次のようなタスクがあります。

- プロジェクトを配置しています。 詳細については、「 [Office ソリューションの配置](../vsto/deploying-an-office-solution.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [ホスト項目とホストコントロールの概要](../vsto/host-items-and-host-controls-overview.md)
- [拡張オブジェクトを使用して Excel を自動化する](../vsto/automating-excel-by-using-extended-objects.md)
- [NamedRange コントロール](../vsto/namedrange-control.md)
- [方法: NamedRange コントロールのサイズを変更する](../vsto/how-to-resize-namedrange-controls.md)
- [方法: ワークシートに NamedRange コントロールを追加する](../vsto/how-to-add-namedrange-controls-to-worksheets.md)
- [ホスト項目とホストコントロールのプログラム上の制限事項](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [方法: Office プロジェクトでイベントハンドラーを作成する](../vsto/how-to-create-event-handlers-in-office-projects.md)
