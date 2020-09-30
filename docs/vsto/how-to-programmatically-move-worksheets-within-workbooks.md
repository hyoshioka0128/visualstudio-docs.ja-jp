---
title: '方法: プログラムによってブック内のワークシートを移動する'
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- worksheets, moving
- workbooks, moving worksheets in
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: fca9d466f3af8a0dd3191f2845613fc9b43ec549
ms.sourcegitcommit: 9d2829dc30b6917e89762d602022915f1ca49089
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2020
ms.locfileid: "91584218"
---
# <a name="how-to-programmatically-move-worksheets-within-workbooks"></a>方法: プログラムによってブック内のワークシートを移動する
  ブック内の他のワークシートを基準として、ワークシートの位置をプログラムで変更することができます。 移動するシートの位置を指定しなかった場合、Excel は、そのシートを含む新しいブックを作成します。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="to-move-a-worksheet-in-a-document-level-customization"></a>ドキュメント レベルのカスタマイズで、ワークシートを移動するには

1. ブック内のシートの合計数を変数に割り当ててから、最初のワークシートが最後のワークシートになるように最初のワークシートを移動します。

     [!code-csharp[Trin_VstcoreExcelAutomation#24](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#24)]
     [!code-vb[Trin_VstcoreExcelAutomation#24](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#24)]

## <a name="to-move-a-worksheet-in-a-vsto-add-in"></a>VSTO アドインでワークシートを移動するには

1. ブック内のシートの合計数を変数に割り当ててから、最初のワークシートが最後のワークシートになるように最初のワークシートを移動します。

     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#16](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#16)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#16](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#16)]

## <a name="see-also"></a>関連項目
- [ワークシートを操作する](../vsto/working-with-worksheets.md)
- [方法: プログラムによってワークシートを非表示にする](../vsto/how-to-programmatically-hide-worksheets.md)
- [方法: プログラムによってブックからワークシートを削除する](../vsto/how-to-programmatically-delete-worksheets-from-workbooks.md)
- [方法: プログラムによってワークシートを保護する](../vsto/how-to-programmatically-protect-worksheets.md)
- [Office プロジェクト内のオブジェクトへのグローバルアクセス](../vsto/global-access-to-objects-in-office-projects.md)
