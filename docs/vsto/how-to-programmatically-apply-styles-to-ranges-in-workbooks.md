---
title: '方法: プログラムによってブック内の範囲にスタイルを適用する'
description: ブック内の領域に名前付きスタイルを適用する方法について説明します。 Excel には、定義済みのスタイルがいくつか用意されています。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ranges, styles
- styles, workbook ranges
- workbooks, styles
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 07372334e9e50275208abd383f73c9d27f8c49d6
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99910074"
---
# <a name="how-to-programmatically-apply-styles-to-ranges-in-workbooks"></a>方法: プログラムによってブック内の範囲にスタイルを適用する
  ブック内の領域に名前付きスタイルを適用できます。 Excel には、定義済みのスタイルがいくつか用意されています。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 **[セルの書式設定]** ダイアログ ボックスには、セルの書式を設定するために使用できるすべてのオプションが表示されます。これらの各オプションはコードから使用できます。 Excel でこのダイアログ ボックスを表示するには、 **[書式]** メニューの **[セル]** をクリックします。

## <a name="to-apply-a-style-to-a-named-range-in-a-document-level-customization"></a>ドキュメント レベルのカスタマイズで名前付き範囲にスタイルを適用するには

1. 新しいスタイルを作成し、その属性を設定します。

     [!code-csharp[Trin_VstcoreExcelAutomation#53](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#53)]
     [!code-vb[Trin_VstcoreExcelAutomation#53](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#53)]

2. <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールを作成し、テキストを割り当て、新しいスタイルを適用します。 このコードは、 `ThisWorkbook` クラスではなく、シート クラスに配置する必要があります。

     [!code-csharp[Trin_VstcoreExcelAutomation#54](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#54)]
     [!code-vb[Trin_VstcoreExcelAutomation#54](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#54)]

## <a name="to-clear-a-style-from-a-named-range-in-a-document-level-customization"></a>ドキュメント レベルのカスタマイズで名前付き範囲からスタイルをクリアするには

1. Normal スタイルを範囲に適用します。 このコードは、 `ThisWorkbook` クラスではなく、シート クラスに配置する必要があります。

     [!code-csharp[Trin_VstcoreExcelAutomation#55](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#55)]
     [!code-vb[Trin_VstcoreExcelAutomation#55](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#55)]

## <a name="to-apply-a-style-to-a-named-range-in-a-vsto-add-in"></a>VSTO アドインで名前付き範囲にスタイルを適用するには

1. 新しいスタイルを作成し、その属性を設定します。

     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#28](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#28)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#28](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#28)]

2. <xref:Microsoft.Office.Interop.Excel.Range> を作成し、テキストを割り当て、新しいスタイルを適用します。

     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#29](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#29)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#29](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#29)]

## <a name="to-clear-a-style-from-a-named-range-in-a-vsto-add-in"></a>VSTO アドインで名前付き範囲からスタイルをクリアするには

1. Normal スタイルを範囲に適用します。

     [!code-csharp[Trin_VstcoreExcelAutomation#56](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#56)]
     [!code-vb[Trin_VstcoreExcelAutomation#56](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#56)]

## <a name="see-also"></a>関連項目
- [範囲の操作](../vsto/working-with-ranges.md)
- [NamedRange コントロール](../vsto/namedrange-control.md)
- [Office プロジェクト内のオブジェクトへのグローバルアクセス](../vsto/global-access-to-objects-in-office-projects.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)
