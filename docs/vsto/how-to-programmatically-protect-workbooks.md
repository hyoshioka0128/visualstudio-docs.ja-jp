---
title: '方法: プログラムによってブックを保護する'
description: ユーザーがワークシートを追加または削除できないように Microsoft Excel ブックを保護する方法、およびプログラムによってブックの保護を解除する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- workbooks, passwords
- documents [Office development in Visual Studio], document protection
- workbooks, unprotecting
- document protection, removing from workbooks
- document protection, adding to workbooks
- workbooks, protecting
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 05587b067fb5e8365433049c7da7fd3d5949a831
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99963849"
---
# <a name="how-to-programmatically-protect-workbooks"></a>方法: プログラムによってブックを保護する
  ユーザーがワークシートを追加または削除したり、プログラムでブックの保護を解除したりできないように、Microsoft Office Excel ブックを保護することができます。 必要に応じて、パスワードを指定したり、構造を保護するかどうか (ユーザーがシートを移動できないようにする) を指定したり、ブックの windows を保護するかどうかを指定したりすることができます。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 ブックを保護しても、ユーザーがセルを編集できなくなることはありません。 データを保護するには、ワークシートを保護する必要があります。 詳細については、「 [方法: ワークシートをプログラムによって保護する](../vsto/how-to-programmatically-protect-worksheets.md)」を参照してください。

 次のコード例では、変数を使用して、ユーザーから取得したパスワードを格納します。

## <a name="protect-a-workbook-that-is-part-of-a-document-level-customization"></a>ドキュメントレベルのカスタマイズの一部であるブックを保護する

### <a name="to-protect-a-workbook"></a>ブックを保護するには

1. <xref:Microsoft.Office.Tools.Excel.Workbook.Protect%2A>ブックのメソッドを呼び出し、パスワードを含めます。 次のコード例を使用するには、 `ThisWorkbook` シートクラスではなく、クラスで実行します。

     [!code-csharp[Trin_VstcoreExcelAutomation#10](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/ThisWorkbook.cs#10)]
     [!code-vb[Trin_VstcoreExcelAutomation#10](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/ThisWorkbook.vb#10)]

### <a name="to-unprotect-a-workbook"></a>ブックの保護を解除するには

1. 必要に <xref:Microsoft.Office.Tools.Excel.Workbook.Unprotect%2A> 応じて、メソッドを呼び出し、パスワードを渡します。 次のコード例を使用するには、 `ThisWorkbook` シートクラスではなく、クラスで実行します。

     [!code-csharp[Trin_VstcoreExcelAutomation#11](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/ThisWorkbook.cs#11)]
     [!code-vb[Trin_VstcoreExcelAutomation#11](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/ThisWorkbook.vb#11)]

## <a name="protect-a-workbook-by-using-an-application-level-add-in"></a>アプリケーションレベルのアドインを使用してブックを保護する

### <a name="to-protect-a-workbook"></a>ブックを保護するには

1. <xref:Microsoft.Office.Interop.Excel._Workbook.Protect%2A>ブックのメソッドを呼び出し、パスワードを含めます。 このコード例では、アクティブなブックを使用します。 この例を使用するには、プロジェクトの `ThisAddIn` クラスからコードを実行します。

     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#6](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#6)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#6](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#6)]

### <a name="to-unprotect-a-workbook"></a>ブックの保護を解除するには

1. <xref:Microsoft.Office.Interop.Excel._Workbook.Unprotect%2A>必要に応じて、アクティブなブックのメソッドを呼び出し、パスワードを渡します。 この例を使用するには、プロジェクトの `ThisAddIn` クラスからコードを実行します。

     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#7](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#7)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#7](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#7)]

## <a name="see-also"></a>関連項目
- [ブックの操作](../vsto/working-with-workbooks.md)
- [方法: プログラムによってワークシートを保護する](../vsto/how-to-programmatically-protect-worksheets.md)
- [方法: プログラムによってワークシートを非表示にする](../vsto/how-to-programmatically-hide-worksheets.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)
