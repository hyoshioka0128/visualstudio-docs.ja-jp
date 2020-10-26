---
title: '方法: プログラムによってワークシートを印刷する'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- printing [Office development in Visual Studio], worksheets
- worksheets, printing
- print preview, worksheets
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: b0affdd34ad1cb302beacdc1abc9d02275878afd
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85537892"
---
# <a name="how-to-programmatically-print-worksheets"></a>方法: プログラムによってワークシートを印刷する

ブック内のワークシートはすべて印刷できます。

[!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="print-a-worksheet-in-a-document-level-customization"></a>ドキュメントレベルのカスタマイズでワークシートを印刷する

### <a name="to-print-a-worksheet"></a>ワークシートを印刷するには

1. `Sheet1` の `PrintOut` メソッドを呼び出します。印刷部数は 2 部で、印刷前に文書をプレビューします。

    [!code-csharp[Trin_VstcoreExcelAutomation#22](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#22)]
    [!code-vb[Trin_VstcoreExcelAutomation#22](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#22)]

   <xref:Microsoft.Office.Tools.Excel.Worksheet.PrintPreview%2A>メソッドを使用すると、指定したオブジェクトを [**印刷プレビュー** ] ウィンドウに表示できます。 次のコードでは、`Sheet1` という名前の <xref:Microsoft.Office.Tools.Excel.Worksheet> ホスト項目があることを前提としています。

### <a name="to-preview-a-page-before-printing"></a>印刷する前にページをプレビューするには

1. ワークシートの <xref:Microsoft.Office.Tools.Excel.Worksheet.PrintPreview%2A> メソッドを呼び出します。

     [!code-csharp[Trin_VstcoreExcelAutomation#23](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#23)]
     [!code-vb[Trin_VstcoreExcelAutomation#23](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#23)]

## <a name="print-a-worksheet-in-a-vsto-add-in"></a>VSTO アドインでワークシートを印刷する

### <a name="to-print-a-worksheet"></a>ワークシートを印刷するには

1. 作業中のワークシートの <xref:Microsoft.Office.Interop.Excel._Worksheet.PrintOut%2A> メソッドを呼び出します。印刷部数は 2 部で、印刷前に文書をプレビューします。

    [!code-csharp[Trin_VstcoreExcelAutomationAddIn#14](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#14)]
    [!code-vb[Trin_VstcoreExcelAutomationAddIn#14](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#14)]

   <xref:Microsoft.Office.Interop.Excel._Worksheet.PrintPreview%2A>メソッドを使用すると、指定したオブジェクトを [**印刷プレビュー** ] ウィンドウに表示できます。

### <a name="to-preview-a-page-before-printing"></a>印刷する前にページをプレビューするには

1. 作業中のワークシートの <xref:Microsoft.Office.Interop.Excel._Worksheet.PrintPreview%2A> メソッドを呼び出します。

     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#15](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#15)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#15](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#15)]

## <a name="see-also"></a>関連項目

- [ワークシートを操作する](../vsto/working-with-worksheets.md)
- [方法: プログラムによってワークシートでスペルチェックを行う](../vsto/how-to-programmatically-check-spelling-in-worksheets.md)
- [ワークシートホスト項目](../vsto/worksheet-host-item.md)
- [Office プロジェクト内のオブジェクトへのグローバルアクセス](../vsto/global-access-to-objects-in-office-projects.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)
