---
title: '方法: 最近使用したブックファイルをプログラムによって一覧表示する'
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- workbooks, listing recently used
- RecentFiles property
- Excel [Office development in Visual Studio], recently used files listing
- recent file list, Excel
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 5e3d6b57251bb19cfb02849defb157c949f4ce35
ms.sourcegitcommit: 9d2829dc30b6917e89762d602022915f1ca49089
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2020
ms.locfileid: "91585159"
---
# <a name="how-to-programmatically-list-recently-used-workbook-files"></a>方法: 最近使用したブックファイルをプログラムによって一覧表示する
  プロパティは、 <xref:Microsoft.Office.Interop.Excel._Application.RecentFiles%2A> 最近使用したファイルの Microsoft Office Excel リストに表示されるすべてのファイルの名前を含むコレクションを返します。 一覧の長さは、ユーザーが保持するように選択したファイルの数によって異なります。 結果は範囲で表示できます。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="to-list-recently-used-workbooks-in-a-range-object"></a>Range オブジェクトで最近使用したブックを一覧表示するには

1. 最近使用したファイルの一覧をループし、オブジェクトに対して相対的な名前をセルに表示し <xref:Microsoft.Office.Interop.Excel.Range> ます。

     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#9](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#9)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#9](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#9)]

## <a name="see-also"></a>関連項目
- [ブックの操作](../vsto/working-with-workbooks.md)
- [NamedRange コントロール](../vsto/namedrange-control.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)
