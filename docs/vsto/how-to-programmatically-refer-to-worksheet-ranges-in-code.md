---
title: '方法: プログラムによってコード内でワークシートの範囲を参照する'
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ranges, referring to
- worksheets, referring to ranges
- referring to worksheet ranges
- Excel [Office development in Visual Studio], referring to worksheet ranges
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 319be5ad6c878e08a862d1e20e826c2800c33512
ms.sourcegitcommit: 9d2829dc30b6917e89762d602022915f1ca49089
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2020
ms.locfileid: "91584834"
---
# <a name="how-to-programmatically-refer-to-worksheet-ranges-in-code"></a>方法: プログラムによってコード内でワークシートの範囲を参照する
  同様のプロセスを使用して、 <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールまたはネイティブの Excel 範囲オブジェクトの内容を参照します。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="use-a-namedrange-control"></a>NamedRange コントロールを使用する
 次の例では、ワークシートにを追加し、その <xref:Microsoft.Office.Tools.Excel.NamedRange> 範囲内のセルにテキストを追加します。

### <a name="to-refer-to-a-namedrange-control"></a>NamedRange コントロールを参照するには

1. コントロールのプロパティに文字列を割り当て <xref:Microsoft.Office.Tools.Excel.NamedRange.Value2%2A> <xref:Microsoft.Office.Tools.Excel.NamedRange> ます。 このコードは、 `ThisWorkbook` クラスではなく、シート クラスに配置する必要があります。

     [!code-csharp[Trin_VstcoreExcelAutomation#46](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#46)]
     [!code-vb[Trin_VstcoreExcelAutomation#46](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#46)]

## <a name="use-native-excel-ranges"></a>ネイティブの Excel の範囲を使用する
 次の例では、ネイティブの Excel 範囲をワークシートに追加し、その範囲内のセルにテキストを追加します。

### <a name="to-refer-to-a-native-range-object"></a>ネイティブ範囲オブジェクトを参照するには

1. 範囲のプロパティに文字列を割り当て <xref:Microsoft.Office.Interop.Excel.Range.Value2%2A> ます。

     [!code-csharp[Trin_VstcoreExcelAutomation#47](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#47)]
     [!code-vb[Trin_VstcoreExcelAutomation#47](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#47)]

## <a name="see-also"></a>関連項目
- [範囲の操作](../vsto/working-with-ranges.md)
- [方法: プログラムによってワークシートでスペルチェックを行う](../vsto/how-to-programmatically-check-spelling-in-worksheets.md)
- [方法: プログラムによってブック内の範囲にスタイルを適用する](../vsto/how-to-programmatically-apply-styles-to-ranges-in-workbooks.md)
- [方法: 増分するデータを使用してプログラムによって自動的に範囲を補完する](../vsto/how-to-programmatically-automatically-fill-ranges-with-incrementally-changing-data.md)
- [方法: プログラムによってワークシートの範囲内のテキストを検索する](../vsto/how-to-programmatically-search-for-text-in-worksheet-ranges.md)
- [NamedRange コントロール](../vsto/namedrange-control.md)
- [ホスト項目とホストコントロールの概要](../vsto/host-items-and-host-controls-overview.md)
- [ホスト項目とホストコントロールのプログラム上の制限事項](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)
