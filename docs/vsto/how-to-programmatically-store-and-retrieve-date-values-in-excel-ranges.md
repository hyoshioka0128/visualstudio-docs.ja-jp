---
title: Excel の範囲内で日付の値をプログラムによって取得 & 格納する
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Excel [Office development in Visual Studio], retrieving date values from ranges
- ranges, retrieving data values
- dates, retrieving from Excel ranges
- Excel [Office development in Visual Studio], storing date values in ranges
- date values, storing in Excel ranges
- dates, storing in Excel ranges
- ranges, storing date values
- date values
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: c2bd76d37a9c9b6e51de7bbe01b54d1be6c93128
ms.sourcegitcommit: 9d2829dc30b6917e89762d602022915f1ca49089
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2020
ms.locfileid: "91583776"
---
# <a name="how-to-programmatically-store-and-retrieve-date-values-in-excel-ranges"></a>方法: プログラムによって Excel の範囲内の日付値を格納および取得する
  値を格納および取得するには、 <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールまたはネイティブの Excel 範囲オブジェクトを使用します。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 Visual Studio の Office 開発ツールを使用して、範囲内で1/1/1900 以降の日付値を格納すると、その値は OLE オートメーション (OA) 形式で格納されます。 <xref:System.DateTime.FromOADate%2A>OLE オートメーション (OA) の日付の値を取得するには、メソッドを使用する必要があります。 日付が1/1/1900 より前の場合は、文字列として格納されます。

> [!NOTE]
> Excel の日付は、1900の最初の2か月の OLE オートメーション日付とは異なります。 また、1904の [ **日付システム** ] オプションがオンになっている場合にも違いがあります。 以下のコード例では、これらの違いについては説明しません。

## <a name="use-a-namedrange-control"></a>NamedRange コントロールを使用する

- この例は、ドキュメントレベルのカスタマイズ用です。 次のコードは、クラスではなく、シートクラスに配置する必要があり `ThisWorkbook` ます。

### <a name="to-store-a-date-value-in-a-named-range"></a>名前付き範囲に日付値を格納するには

1. <xref:Microsoft.Office.Tools.Excel.NamedRange>セル**A1**にコントロールを作成します。

     [!code-csharp[Trin_VstcoreExcelAutomation#50](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#50)]
     [!code-vb[Trin_VstcoreExcelAutomation#50](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#50)]

2. 今日の日付をの値として設定 `NamedRange1` します。

     [!code-csharp[Trin_VstcoreExcelAutomation#51](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#51)]
     [!code-vb[Trin_VstcoreExcelAutomation#51](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#51)]

### <a name="to-retrieve-a-date-value-from-a-named-range"></a>名前付き範囲から日付値を取得するには

1. から日付値を取得 `NamedRange1` します。

     [!code-csharp[Trin_VstcoreExcelAutomation#52](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#52)]
     [!code-vb[Trin_VstcoreExcelAutomation#52](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#52)]

## <a name="use-native-excel-ranges"></a>ネイティブの Excel の範囲を使用する

### <a name="to-store-a-date-value-in-a-native-excel-range-object"></a>ネイティブの Excel 範囲オブジェクトに日付値を格納するには

1. <xref:Microsoft.Office.Interop.Excel.Range>セル**A1**を表すを作成します。

     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#25](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#25)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#25](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#25)]

2. 今日の日付をの値として設定 `rng` します。

     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#26](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#26)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#26](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#26)]

### <a name="to-retrieve-a-date-value-from-a-native-excel-range-object"></a>ネイティブの Excel 範囲オブジェクトから日付値を取得するには

1. から日付値を取得 `rng` します。

     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#27](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#27)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#27](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#27)]

## <a name="see-also"></a>関連項目
- [範囲の操作](../vsto/working-with-ranges.md)
- [Excel オブジェクトモデルの概要](../vsto/excel-object-model-overview.md)
- [NamedRange コントロール](../vsto/namedrange-control.md)
- [方法: プログラムによってコード内でワークシートの範囲を参照する](../vsto/how-to-programmatically-refer-to-worksheet-ranges-in-code.md)
- [方法: ワークシートに NamedRange コントロールを追加する](../vsto/how-to-add-namedrange-controls-to-worksheets.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)
