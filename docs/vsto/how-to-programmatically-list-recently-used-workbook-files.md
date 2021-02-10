---
title: '方法: 最近使用したブックファイルをプログラムによって一覧表示する'
description: Visual Studio を使用して、最近使用した Microsoft Excel ブックファイルをプログラムで一覧表示する方法について説明します。
ms.custom: SEO-VS-2020
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
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 75405c7a2e02189e205edf6615c5d95a8f1d023c
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99963147"
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
