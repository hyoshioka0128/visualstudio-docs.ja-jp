---
title: '方法: プログラムによってワークシート内のデータを並べ替える'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data sorting, worksheets
- data [Office development in Visual Studio], sorting in worksheets
- worksheets, sorting data
- sorting data, in worksheets
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 08fa461dc55bf42857e21a5419cab6a0ff147173
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85546979"
---
# <a name="how-to-programmatically-sort-data-in-worksheets"></a>方法: プログラムによってワークシート内のデータを並べ替える
  実行時にワークシートの範囲およびリストに含まれているデータを並べ替えることができます。 次のコードは、複数の列で構成される `Fruits` という名前の範囲を、最初の列のデータを基に並べ替え、次に 2 番目の列のデータを基に並べ替えます。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="sort-data-in-a-document-level-customization"></a>ドキュメントレベルのカスタマイズでデータを並べ替える

### <a name="to-sort-data-in-a-namedrange-control"></a>NamedRange コントロール内のデータを並べ替えるには

1. <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールの <xref:Microsoft.Office.Tools.Excel.NamedRange.Sort%2A> メソッドを呼び出します。 次のコード例では、ワークシートに `Fruits` という名前の <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールが必要です。 このコードは、 `ThisWorkbook` クラスではなく、シート クラスに配置する必要があります。

    [!code-csharp[Trin_VstcoreExcelAutomation#78](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#78)]
    [!code-vb[Trin_VstcoreExcelAutomation#78](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#78)]

   コントロール内のデータを並べ替えるには、 *Sheet1* または *Sheet1.cs* に次のコードを配置し <xref:Microsoft.Office.Tools.Excel.ListObject> ます。 このコードでは、`Sheet1` という名前のワークシートに、`fruitList` という名前の <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールがあることを前提としています。

### <a name="to-sort-data-in-a-listobject-control"></a>ListObject コントロール内のデータを並べ替えるには

1. <xref:Microsoft.Office.Tools.Excel.ListObject> ホスト コントロールの <xref:Microsoft.Office.Tools.Excel.ListObject.Range%2A> プロパティの <xref:Microsoft.Office.Interop.Excel.Range.Sort%2A> メソッドを呼び出します。

     [!code-csharp[Trin_VstcoreExcelAutomation#79](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#79)]
     [!code-vb[Trin_VstcoreExcelAutomation#79](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#79)]

## <a name="sort-data-in-a-vsto-add-in"></a>VSTO アドインでのデータの並べ替え

### <a name="to-sort-data-in-a-native-range"></a>ネイティブな範囲でデータを並べ替えるには

1. ネイティブな Excel <xref:Microsoft.Office.Interop.Excel.Range> コントロールの <xref:Microsoft.Office.Interop.Excel.Range.Sort%2A> メソッドを呼び出します。 次のコード例では、ワークシートに `Fruits` という名前のネイティブな Excel コントロールが必要です。

     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#23](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#23)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#23](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#23)]

### <a name="to-sort-data-in-a-listobject-control"></a>ListObject コントロール内のデータを並べ替えるには

1. ネイティブな Excel <xref:Microsoft.Office.Interop.Excel.ListObject> コントロールの <xref:Microsoft.Office.Tools.Excel.ListObject.Range%2A> プロパティの <xref:Microsoft.Office.Interop.Excel.Range.Sort%2A> メソッドを呼び出します。 次の例は、作業中のワークシートに `fruitList` という名前のネイティブな Excel <xref:Microsoft.Office.Interop.Excel.ListObject> コントロールがあることを前提としています。

     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#24](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#24)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#24](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#24)]

## <a name="see-also"></a>関連項目
- [ワークシートを操作する](../vsto/working-with-worksheets.md)
- [方法: 増分するデータを使用してプログラムによって自動的に範囲を補完する](../vsto/how-to-programmatically-automatically-fill-ranges-with-incrementally-changing-data.md)
- [方法: プログラムによってコード内でワークシートの範囲を参照する](../vsto/how-to-programmatically-refer-to-worksheet-ranges-in-code.md)
- [方法: プログラムによってブック内の範囲にスタイルを適用する](../vsto/how-to-programmatically-apply-styles-to-ranges-in-workbooks.md)
- [NamedRange コントロール](../vsto/namedrange-control.md)
- [ListObject コントロール](../vsto/listobject-control.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)
