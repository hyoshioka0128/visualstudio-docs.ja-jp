---
title: '方法: ワークシート内の行をプログラムによってグループ化する'
description: NamedRange コントロールまたはネイティブの Excel 範囲オブジェクトを使用して、Microsoft Excel で1つ以上の行をプログラムによってグループ化する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- worksheets, creating groups
- groups, creating in worksheets
- ranges, creating groups
- worksheets, clearing groups
- groups
- groups [Office development in Visual Studio], clearing in worksheets
- worksheets, ungrouping rows and columns
- rows [Office development in Visual Studio], ungrouping
- columns [Office development in Visual Studio], ungrouping
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 203ea7d17a02a224c290e5dd3c6070c06a1d26e4
ms.sourcegitcommit: 4bd2b770e60965fc0843fc25318a7e1b46137875
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/15/2020
ms.locfileid: "97525715"
---
# <a name="how-to-programmatically-group-rows-in-a-worksheet"></a>方法: ワークシート内の行をプログラムによってグループ化する
  1つ以上の行をグループ化できます。 ワークシートにグループを作成するには、 <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールまたはネイティブの Excel 範囲オブジェクトを使用します。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="use-a-namedrange-control"></a>NamedRange コントロールを使用する
 デザイン時にドキュメントレベルのプロジェクトにコントロールを追加する場合は、 <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールを使用してプログラムでグループを作成できます。 次の例では <xref:Microsoft.Office.Tools.Excel.NamedRange> 、同じワークシートに、、およびの3つのコントロールがあることを前提としています `data2001` `data2002` `dataAll` 。 各名前付き範囲は、ワークシート内の行全体を参照します。

### <a name="to-create-a-group-of-namedrange-controls-on-a-worksheet"></a>ワークシートに NamedRange コントロールのグループを作成するには

1. 各範囲のメソッドを呼び出すことによって、3つの名前付き範囲をグループ化 <xref:Microsoft.Office.Tools.Excel.NamedRange.Group%2A> します。 このコードは、 `ThisWorkbook` クラスではなく、シート クラスに配置する必要があります。

     [!code-csharp[Trin_VstcoreExcelAutomation#32](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#32)]
     [!code-vb[Trin_VstcoreExcelAutomation#32](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#32)]

    > [!NOTE]
    > 行のグループ化を解除するには、メソッドを呼び出し <xref:Microsoft.Office.Tools.Excel.NamedRange.Ungroup%2A> ます。

## <a name="use-native-excel-ranges"></a>ネイティブの Excel の範囲を使用する
 このコードでは `data2001` 、 `data2002` ワークシートに、、およびという3つの Excel 範囲があることを前提としてい `dataAll` ます。

### <a name="to-create-a-group-of-excel-ranges-in-a-worksheet"></a>ワークシートに Excel の範囲のグループを作成するには

1. 各範囲のメソッドを呼び出すことによって、3つの名前付き範囲をグループ化 <xref:Microsoft.Office.Interop.Excel.Range.Group%2A> します。 次の例では <xref:Microsoft.Office.Interop.Excel.Range> `data2001` 、 `data2002` 同じワークシートに、、およびという名前のコントロールが3つあることを前提としてい `dataAll` ます。 各名前付き範囲は、ワークシート内の行全体を参照します。

     [!code-csharp[Trin_VstcoreExcelAutomation#33](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#33)]
     [!code-vb[Trin_VstcoreExcelAutomation#33](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#33)]

    > [!NOTE]
    > 行のグループ化を解除するには、メソッドを呼び出し <xref:Microsoft.Office.Interop.Excel.Range.Ungroup%2A> ます。

## <a name="see-also"></a>関連項目
- [ワークシートを操作する](../vsto/working-with-worksheets.md)
- [NamedRange コントロール](../vsto/namedrange-control.md)
- [方法: ワークシートに NamedRange コントロールを追加する](../vsto/how-to-add-namedrange-controls-to-worksheets.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)
