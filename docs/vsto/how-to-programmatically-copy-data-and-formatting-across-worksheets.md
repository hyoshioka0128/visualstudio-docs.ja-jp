---
title: プログラムによってワークシート間でデータと書式設定をコピーする
description: FillAcrossSheets メソッドを使用して、あるシートの範囲からブック内の他のすべてのシートにデータをコピーする方法について説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- worksheets, copying data
- formatting [Office development in Visual Studio]
- data [Office development in Visual Studio], copying across worksheets
- copying data, Office development in Visual Studio
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: d768eb086707af2eeddeb18a77bad1ef1f101839
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99964239"
---
# <a name="how-to-programmatically-copy-data-and-formatting-across-worksheets"></a>方法: プログラムによってワークシート間でデータと書式設定をコピーする
  メソッドを使用して、あるシートの範囲のデータをブック内の他のすべてのシートにコピーでき <xref:Microsoft.Office.Interop.Excel.Worksheets.FillAcrossSheets%2A> ます。 範囲を指定し、データ、書式設定、またはその両方をコピーするかどうかを指定します。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="example"></a>例
 [!code-csharp[Trin_VstcoreExcelAutomation#44](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#44)]
 [!code-vb[Trin_VstcoreExcelAutomation#44](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#44)]

## <a name="compile-the-code"></a>コードのコンパイル
 この例では、ワークシートにという名前の範囲が必要です `rangeData` 。

## <a name="see-also"></a>関連項目
- [ワークシートを操作する](../vsto/working-with-worksheets.md)
- [方法: プログラムによって新しいワークシートをブックに追加する](../vsto/how-to-programmatically-add-new-worksheets-to-workbooks.md)
- [方法: 選択したセルを含むワークシートの行の書式をプログラムによって変更する](../vsto/how-to-programmatically-change-formatting-in-worksheet-rows-containing-selected-cells.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)
