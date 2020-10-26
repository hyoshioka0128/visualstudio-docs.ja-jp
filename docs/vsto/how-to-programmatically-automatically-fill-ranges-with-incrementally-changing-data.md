---
title: データ範囲をプログラムによって段階的にオートフィルする
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Autofill method [Excel]
- filling ranges automatically
- ranges, automatically filling
- workbooks, filling ranges
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 076381c93d11c2d13bdd89ea5c36c0039e15ef71
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85547473"
---
# <a name="how-to-programmatically-automatically-fill-ranges-with-incrementally-changing-data"></a>方法: 増分するデータを使用してプログラムによって自動的に範囲を補完する
  <xref:Microsoft.Office.Interop.Excel.Range.AutoFill%2A>オブジェクトのメソッドを使用すると、 <xref:Microsoft.Office.Interop.Excel.Range> ワークシートの範囲に値を自動的に入力できます。 多くの場合、メソッドを使用して、 <xref:Microsoft.Office.Interop.Excel.Range.AutoFill%2A> 範囲内の値を段階的に増加または減少させることができます。 列挙から省略可能な定数を指定することにより、動作を指定でき <xref:Microsoft.Office.Interop.Excel.XlAutoFillType> ます。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 を使用する場合は、2つの範囲を指定する必要があり <xref:Microsoft.Office.Interop.Excel.Range.AutoFill%2A> ます。

- メソッドを呼び出す範囲。このメソッドは、 <xref:Microsoft.Office.Interop.Excel.Range.AutoFill%2A> 塗りつぶしの開始点を指定し、初期値を格納します。

- 入力する範囲。パラメーターとしてメソッドに渡さ <xref:Microsoft.Office.Interop.Excel.Range.AutoFill%2A> れます。 このターゲット範囲には、初期値を含む範囲を含める必要があります。

    > [!NOTE]
    > の代わりにコントロールを渡すことはできません <xref:Microsoft.Office.Tools.Excel.NamedRange> <xref:Microsoft.Office.Interop.Excel.Range> 。 詳細については、「 [ホスト項目とホストコントロールのプログラム上の制限事項](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)」を参照してください。

## <a name="example"></a>例
 [!code-csharp[Trin_VstcoreExcelAutomation#49](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#49)]
 [!code-vb[Trin_VstcoreExcelAutomation#49](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#49)]

## <a name="compile-the-code"></a>コードのコンパイル
 データを格納する範囲の最初のセルには、初期値を含める必要があります。

 この例では、3つのリージョンに入力する必要があります。

- 列 B は、5つの平日を含めることを示します。 初期値には、セル B1 に「 **Monday** 」と入力します。

- 列 C は5か月を含むことになります。 初期値には、セル C1 に「 **January** 」と入力します。

- 列 D には、行ごとに2ずつインクリメントした一連の数値を含めることができます。 初期値については、セル D2 に「 **4** **」と入力** します。

## <a name="see-also"></a>関連項目
- [範囲の操作](../vsto/working-with-ranges.md)
- [方法: プログラムによってコード内でワークシートの範囲を参照する](../vsto/how-to-programmatically-refer-to-worksheet-ranges-in-code.md)
- [方法: プログラムによってブック内の範囲にスタイルを適用する](../vsto/how-to-programmatically-apply-styles-to-ranges-in-workbooks.md)
- [方法: Excel の計算をプログラムで実行する](../vsto/how-to-programmatically-run-excel-calculations-programmatically.md)
- [ホスト項目とホストコントロールの概要](../vsto/host-items-and-host-controls-overview.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)
