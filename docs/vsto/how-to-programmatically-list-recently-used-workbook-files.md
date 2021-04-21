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
ms.openlocfilehash: ba7ca717af4330e8fb3c102b3a5fe5bf7d9162b6
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107825330"
---
# <a name="how-to-programmatically-list-recently-used-workbook-files"></a>方法: 最近使用したブックファイルをプログラムによって一覧表示する
  プロパティは、 <xref:Microsoft.Office.Interop.Excel._Application.RecentFiles%2A> 最近使用したファイルの Microsoft Office Excel リストに表示されるすべてのファイルの名前を含むコレクションを返します。 一覧の長さは、ユーザーが保持するように選択したファイルの数によって異なります。 結果は範囲で表示できます。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="to-list-recently-used-workbooks-in-a-range-object"></a>Range オブジェクトで最近使用したブックを一覧表示するには

1. 最近使用したファイルの一覧をループし、オブジェクトに対して相対的な名前をセルに表示し <xref:Microsoft.Office.Interop.Excel.Range> ます。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet9":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet9":::

## <a name="see-also"></a>関連項目
- [ブックの操作](../vsto/working-with-workbooks.md)
- [NamedRange コントロール](../vsto/namedrange-control.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)
