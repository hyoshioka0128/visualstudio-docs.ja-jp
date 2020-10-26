---
title: '方法: プログラムによってブックを開く'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- workbooks, opening
- Excel [Office development in Visual Studio], opening workbooks
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 10a849d8545565e450cd099b32a9e3e8f7f11b56
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85537905"
---
# <a name="how-to-programmatically-open-workbooks"></a>方法: プログラムによってブックを開く
  <xref:Microsoft.Office.Interop.Excel.Workbooks>Microsoft Office Excel のコレクションを使用すると、開いているすべてのブックを操作したり、ブックを開いたりすることができます。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="to-open-an-existing-workbook"></a>既存のブックを開くには

1. コレクションのメソッドを使用して <xref:Microsoft.Office.Interop.Excel.Workbooks.Open%2A> <xref:Microsoft.Office.Interop.Excel.Workbooks> 、ブックへのパスを渡します。

     [!code-csharp[Trin_VstcoreExcelAutomation#2](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#2)]
     [!code-vb[Trin_VstcoreExcelAutomation#2](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#2)]

## <a name="compile-the-code"></a>コードのコンパイル
 このコード例で必要な要素は次のとおりです。

- という名前のブックは、 `YourWorkbook.xls` C ドライブ上のという名前のディレクトリに存在する必要があり `Test` ます。

## <a name="see-also"></a>関連項目
- [ブックの操作](../vsto/working-with-workbooks.md)
- [方法: プログラムによってテキストファイルをブックとして開く](../vsto/how-to-programmatically-open-text-files-as-workbooks.md)
- [方法: プログラムによって新しいブックを作成する](../vsto/how-to-programmatically-create-new-workbooks.md)
- [方法: プログラムによってブックを保存する](../vsto/how-to-programmatically-save-workbooks.md)
- [方法: プログラムによってブックを閉じる](../vsto/how-to-programmatically-close-workbooks.md)
- [ホスト項目とホストコントロールのプログラム上の制限事項](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)
- [ホスト項目とホストコントロールの概要](../vsto/host-items-and-host-controls-overview.md)
