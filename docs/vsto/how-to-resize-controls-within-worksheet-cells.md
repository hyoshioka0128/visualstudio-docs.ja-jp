---
title: '方法: ワークシートのセル内のコントロールのサイズを変更する'
description: Visual Studio を使用して、デザイン時と実行時の両方で、Microsoft Excel ワークシートのセル内のコントロールのサイズを変更する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- controls [Office development in Visual Studio], resizing
- managed controls, resizing
- worksheets, resizing
- Windows Forms controls [Office development in Visual Studio], resizing
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 7b62d3fed62b4d17b9f1918b76760593b38d83a9
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99927822"
---
# <a name="how-to-resize-controls-within-worksheet-cells"></a>方法: ワークシートのセル内のコントロールのサイズを変更する
  ワークシート上の列または行のサイズを変更すると、セル内のホストコントロールは、サイズ変更されたセルの高さまたは幅に自動的にサイズ変更されます。 Windows フォームコントロールは、既定では自動的にサイズ変更されません。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

 デザイン時にコントロールを追加する場合は、各コントロールの配置オプションを設定する必要があります。

 プログラムを使用して Windows フォームコントロールを追加し、範囲引数を指定すると、範囲内のセルのサイズが変更されたときにコントロールのサイズが自動的に変更されます。 詳細については、「 [実行時に Office ドキュメントにコントロールを追加する](../vsto/adding-controls-to-office-documents-at-run-time.md)」を参照してください。

## <a name="resize-controls-at-design-time"></a>デザイン時にコントロールのサイズを変更する

### <a name="to-make-controls-resize-with-cells-at-design-time"></a>デザイン時にコントロールのサイズをセルに合わせて変更するには

1. [ **ツールボックス**] から Windows フォームコントロールをワークシートにドラッグします。

2. コントロールを右クリックし、[コントロールの **書式設定**] をクリックします。

3. [ **コントロールの書式設定** ] ダイアログボックスで、[ **プロパティ** ] タブをクリックします。

4. [ **オブジェクトの配置**] で、[ **セルの移動とサイズ** 変更] オプションを選択し、[ **OK**] をクリックします。

     コントロールを含むセルのサイズを変更すると、セルに合わせてコントロールのサイズが変更されます。

## <a name="resize-controls-at-run-time"></a>実行時にコントロールのサイズを変更する
 実行時に Windows フォームコントロールを追加し、 <xref:Microsoft.Office.Interop.Excel.Range> コントロールの場所としてを渡すと、その範囲を含むワークシートセルのサイズが変更されると、コントロールのサイズが自動的に変更されます。

### <a name="to-make-controls-resize-with-cells-at-run-time"></a>実行時にコントロールのサイズをセルに合わせて変更するには

1. 範囲 A1 にコントロールを追加します。

     [!code-vb[Trin_VstcoreProgrammingControlsExcel#5](../vsto/codesnippet/VisualBasic/my excel chart/Sheet1.vb#5)]
     [!code-csharp[Trin_VstcoreProgrammingControlsExcel#5](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs#5)]

     コントロールを含むセルのサイズを変更すると、セルに合わせてコントロールのサイズが変更されます。

## <a name="reset-control-placement"></a>制御位置のリセット
 `Placement`プロパティを次のいずれかの値に設定することによって、コントロールの配置とサイズ変更をリセットでき <xref:Microsoft.Office.Interop.Excel.XlPlacement> ます。

- <xref:Microsoft.Office.Interop.Excel.XlPlacement.xlFreeFloating>

- <xref:Microsoft.Office.Interop.Excel.XlPlacement.xlMove>

- <xref:Microsoft.Office.Interop.Excel.XlPlacement.xlMoveAndSize>

### <a name="to-change-the-behavior-of-a-control-so-that-it-does-not-resize-or-move-with-the-cell"></a>コントロールの動作を変更して、セルのサイズ変更や移動が行われないようにするには

1. コントロールの placement プロパティを呼び出し、値をに設定し <xref:Microsoft.Office.Interop.Excel.XlPlacement.xlFreeFloating> ます。

     [!code-vb[Trin_VstcoreProgrammingControlsExcel#6](../vsto/codesnippet/VisualBasic/my excel chart/Sheet1.vb#6)]
     [!code-csharp[Trin_VstcoreProgrammingControlsExcel#6](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs#6)]

## <a name="see-also"></a>関連項目
- [Office ドキュメントのコントロール](../vsto/controls-on-office-documents.md)
- [方法: Office ドキュメントに Windows フォームコントロールを追加する](../vsto/how-to-add-windows-forms-controls-to-office-documents.md)
- [方法: 印刷時にワークシートのコントロールを非表示にする](../vsto/how-to-hide-controls-on-worksheets-when-printing.md)
- [実行時に Office ドキュメントにコントロールを追加する](../vsto/adding-controls-to-office-documents-at-run-time.md)
- [Office ドキュメントの Windows フォームコントロールの制限事項](../vsto/limitations-of-windows-forms-controls-on-office-documents.md)
