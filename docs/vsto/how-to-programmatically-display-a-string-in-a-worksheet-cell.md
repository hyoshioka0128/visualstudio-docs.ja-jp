---
title: '方法: プログラムによってワークシートのセルに文字列を表示する'
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- text [Office development in Visual Studio], adding to worksheets
- worksheets, displaying text in cells
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: eb3dbaec2efd95f63428e8494598720953f791e7
ms.sourcegitcommit: 9d2829dc30b6917e89762d602022915f1ca49089
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2020
ms.locfileid: "91585224"
---
# <a name="how-to-programmatically-display-a-string-in-a-worksheet-cell"></a>方法: プログラムによってワークシートのセルに文字列を表示する
  この例では、テキストをプログラムによってセルに表示する方法を示します。 セルにテキストを表示するには、 <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールまたはネイティブの Excel 範囲オブジェクトを使用します。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="use-a-namedrange-control"></a>NamedRange コントロールを使用する
 この例では、 <xref:Microsoft.Office.Tools.Excel.NamedRange> という名前のコントロールを使用 `message` します。 コントロールは、デザイン時にドキュメントレベルのカスタマイズに追加する必要があります。 次のコードは、クラスではなく、シートクラスに配置する必要があり `ThisWorkbook` ます。

### <a name="to-display-text-in-a-namedrange-control"></a>NamedRange コントロールにテキストを表示するには

1. コントロールの値 <xref:Microsoft.Office.Tools.Excel.NamedRange> を **Hello World**に設定します。

     [!code-csharp[Trin_VstcoreExcelAutomation#68](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#68)]
     [!code-vb[Trin_VstcoreExcelAutomation#68](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#68)]

## <a name="use-a-native-excel-range"></a>ネイティブの Excel 範囲を使用する
 次のコードでは、プログラムによって新しい範囲を作成し、値を代入します。

### <a name="to-display-text-in-an-excel-range"></a>Excel 範囲にテキストを表示するには

1. のセル **A1** で範囲を取得 `Sheet1` し、値を **Hello World**に設定します。

     [!code-csharp[Trin_VstcoreExcelAutomation#69](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#69)]
     [!code-vb[Trin_VstcoreExcelAutomation#69](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#69)]

## <a name="see-also"></a>関連項目
- [チュートリアル: Windows フォームを使用したデータの収集](../vsto/walkthrough-collecting-data-using-a-windows-form.md)
- [Office ソリューションのトラブルシューティング](../vsto/troubleshooting-office-solutions.md)
- [NamedRange コントロール](../vsto/namedrange-control.md)
- [Office プロジェクト内のオブジェクトへのグローバルアクセス](../vsto/global-access-to-objects-in-office-projects.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)
