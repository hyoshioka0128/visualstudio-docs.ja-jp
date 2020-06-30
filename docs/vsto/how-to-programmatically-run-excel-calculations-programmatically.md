---
title: '方法: Excel の計算をプログラムで実行する'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ranges, running calculations
- calculations, running in Excel
- Excel [Office development in Visual Studio], running calculations programmatically
- workbooks, running calculations
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: a02e86864065d2c626de2f6e7fea7528554f1391
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547382"
---
# <a name="how-to-programmatically-run-excel-calculations"></a>方法: Excel の計算をプログラムで実行する
  同様のプロセスを使用して、 <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールまたはネイティブの Excel 範囲オブジェクトで計算を実行します。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="run-calculations-in-a-namedrange-control"></a>NamedRange コントロールでの計算の実行
 次の例では、を <xref:Microsoft.Office.Tools.Excel.NamedRange> セル A1 に作成し、セルを計算します。 このコードは、 `ThisWorkbook` クラスではなく、シート クラスに配置する必要があります。

### <a name="to-run-calculations-in-a-namedrange-control"></a>NamedRange コントロールで計算を実行するには

1. 名前付き範囲を作成します。

     [!code-csharp[Trin_VstcoreExcelAutomation#75](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#75)]
     [!code-vb[Trin_VstcoreExcelAutomation#75](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#75)]

2. <xref:Microsoft.Office.Tools.Excel.NamedRange.Calculate%2A>指定された範囲のメソッドを呼び出します。

     [!code-csharp[Trin_VstcoreExcelAutomation#76](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#76)]
     [!code-vb[Trin_VstcoreExcelAutomation#76](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#76)]

## <a name="run-calculations-in-a-native-excel-range"></a>ネイティブの Excel 範囲で計算を実行する

### <a name="to-run-calculations-in-a-native-excel-range"></a>ネイティブの Excel 範囲で計算を実行するには

1. 名前付き範囲を作成します。

     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#30](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#30)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#30](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#30)]

2. <xref:Microsoft.Office.Interop.Excel.Range.Calculate%2A>指定された範囲のメソッドを呼び出します。

     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#31](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#31)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#31](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#31)]

## <a name="see-also"></a>関連項目
- [範囲の操作](../vsto/working-with-ranges.md)
- [NamedRange コントロール](../vsto/namedrange-control.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)
