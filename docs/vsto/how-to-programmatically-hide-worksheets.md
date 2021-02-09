---
title: '方法: プログラムによってワークシートを非表示にする'
description: ワークシートホスト項目を使用して Microsoft Excel ブックのワークシートをプログラムで表示または非表示にする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- hidden worksheets
- worksheets, hiding
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 5763e040e0206272b6b50b039f1260bcbc99db49
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99908590"
---
# <a name="how-to-programmatically-hide-worksheets"></a>方法: プログラムによってワークシートを非表示にする
  ブック内の任意のワークシートの表示と非表示を切り替えることができます。 ワークシートを非表示にするには、Worksheet ホスト項目を使用するか、ブックの Sheets コレクションを使用してワークシートにアクセスします。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="use-the-worksheet-host-item"></a>ワークシートのホスト項目を使用する
 デザイン時にドキュメント レベルのカスタマイズでワークシートが追加された場合は、 <xref:Microsoft.Office.Tools.Excel.Worksheet.Visible%2A> プロパティを使用して特定のワークシートを非表示にします。

### <a name="to-hide-a-worksheet-using-a-worksheet-host-item"></a>Worksheet ホスト項目を使用してワークシートを非表示にするには

1. <xref:Microsoft.Office.Tools.Excel.Worksheet.Visible%2A> ホスト項目の `Sheet1` プロパティを列挙値 <xref:Microsoft.Office.Interop.Excel.XlSheetVisibility.xlSheetHidden> に設定します。

     [!code-csharp[Trin_VstcoreExcelAutomation#25](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#25)]
     [!code-vb[Trin_VstcoreExcelAutomation#25](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#25)]

## <a name="use-the-sheets-collection-of-the-excel-workbook"></a>Excel ブックの Sheets コレクションを使用する
 次の場合は、Microsoft Office Excel の <xref:Microsoft.Office.Interop.Excel.Sheets> コレクションを使用してワークシートにアクセスします。

- VSTO アドインでワークシートを非表示にする場合。

- 非表示にするワークシートがドキュメント レベルのカスタマイズで実行時に作成された場合。

### <a name="to-hide-a-worksheet-using-the-sheets-collection-of-the-excel-workbook"></a>Excel ブックの Sheets コレクションを使用してワークシートを非表示にするには

1. ワークシートの <xref:Microsoft.Office.Interop.Excel.Worksheets.Visible%2A> プロパティを列挙値 <xref:Microsoft.Office.Interop.Excel.XlSheetVisibility.xlSheetHidden> に設定します。

     [!code-csharp[Trin_VstcoreExcelAutomation#26](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#26)]
     [!code-vb[Trin_VstcoreExcelAutomation#26](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#26)]

## <a name="see-also"></a>関連項目
- [ワークシートを操作する](../vsto/working-with-worksheets.md)
- [方法: プログラムによってブックからワークシートを削除する](../vsto/how-to-programmatically-delete-worksheets-from-workbooks.md)
- [方法: プログラムによってブック内のワークシートを移動する](../vsto/how-to-programmatically-move-worksheets-within-workbooks.md)
- [方法: プログラムによってワークシートを保護する](../vsto/how-to-programmatically-protect-worksheets.md)
- [ホスト項目とホストコントロールの概要](../vsto/host-items-and-host-controls-overview.md)
- [Office プロジェクト内のオブジェクトへのグローバルアクセス](../vsto/global-access-to-objects-in-office-projects.md)
