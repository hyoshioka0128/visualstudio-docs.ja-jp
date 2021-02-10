---
title: プログラムによってドキュメント内の範囲または選択項目を折りたたむ
description: 範囲または選択オブジェクトを操作している場合は、テキストを挿入する前に、選択範囲を挿入ポイントに変更することをお勧めします。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- selections, collapsing
- documents [Office development in Visual Studio], collapsing ranges
- collapsing selections
- ranges, collapsing
- collapsing ranges
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 9b063244c8ac611d3a864b9cc3753b5cd8460474
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99964291"
---
# <a name="how-to-programmatically-collapse-ranges-or-selections-in-documents"></a>方法: プログラムによって文書内の範囲または選択項目を折りたたむ
  <xref:Microsoft.Office.Interop.Word.Range> または <xref:Microsoft.Office.Interop.Word.Selection> オブジェクトを使用する場合、既存のテキストが上書きされないように、テキストを挿入する前に、選択範囲を挿入ポイントに変更できます。 <xref:Microsoft.Office.Interop.Word.Range>オブジェクトとオブジェクトの両方に <xref:Microsoft.Office.Interop.Word.Selection> Collapse メソッドがあり、列挙値を使用し <xref:Microsoft.Office.Interop.Word.WdCollapseDirection> ます。

- <xref:Microsoft.Office.Interop.Word.WdCollapseDirection.wdCollapseStart> は、選択範囲を選択範囲の先頭に向かって縮小します。 列挙値を指定しない場合は、これが既定の動作です。

- <xref:Microsoft.Office.Interop.Word.WdCollapseDirection.wdCollapseEnd> は、選択範囲を選択範囲の末尾に向かって縮小します。

  [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="to-collapse-a-range-and-insert-new-text"></a>範囲を縮小して新しいテキストを挿入するには

1. ドキュメントの最初の段落で構成される <xref:Microsoft.Office.Interop.Word.Range> オブジェクトを作成します。

    次のコード例はドキュメント レベルのカスタマイズで使用できます。

    [!code-vb[Trin_VstcoreWordAutomation#46](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#46)]
    [!code-csharp[Trin_VstcoreWordAutomation#46](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#46)]

    次のコード例は VSTO アドインで使用できます。 このコードでは作業中のドキュメントを使用します。

    [!code-vb[Trin_VstcoreWordAutomationAddIn#46](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#46)]
    [!code-csharp[Trin_VstcoreWordAutomationAddIn#46](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#46)]

2. <xref:Microsoft.Office.Interop.Word.WdCollapseDirection.wdCollapseStart> 列挙値を使用して、範囲を縮小します。

    [!code-vb[Trin_VstcoreWordAutomation#47](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#47)]
    [!code-csharp[Trin_VstcoreWordAutomation#47](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#47)]

3. 新しいテキストを挿入します。

    [!code-vb[Trin_VstcoreWordAutomation#48](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#48)]
    [!code-csharp[Trin_VstcoreWordAutomation#48](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#48)]

4. <xref:Microsoft.Office.Interop.Word.Range>を選択します。

    [!code-vb[Trin_VstcoreWordAutomation#49](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#49)]
    [!code-csharp[Trin_VstcoreWordAutomation#49](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#49)]

   <xref:Microsoft.Office.Interop.Word.WdCollapseDirection.wdCollapseEnd> 列挙値を使用すると、テキストは次の段落の先頭に挿入されます。

   [!code-vb[Trin_VstcoreWordAutomation#50](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#50)]
   [!code-csharp[Trin_VstcoreWordAutomation#50](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#50)]

   新しい文を挿入すると、段落記号の前に挿入されると期待するかもしれませんが、それは当てはまりません。元の範囲に段落記号が含まれているためです。 詳細については、「 [方法: 範囲を作成するときにプログラムによって段落記号を除外](../vsto/how-to-programmatically-exclude-paragraph-marks-when-creating-ranges.md)する」を参照してください。

## <a name="document-level-customization-example"></a>ドキュメントレベルのカスタマイズの例

### <a name="to-collapse-a-range-in-a-document-level-customization"></a>ドキュメント レベルのカスタマイズで範囲を縮小するには

1. 次の例は、ドキュメント レベルのカスタマイズのメソッド全体を示しています。 このコードを使用するには、プロジェクトの `ThisDocument` クラスから実行します。

     [!code-vb[Trin_VstcoreWordAutomation#45](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#45)]
     [!code-csharp[Trin_VstcoreWordAutomation#45](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#45)]

## <a name="vsto-add-in-example"></a>VSTO アドインの例

### <a name="to-collapse-a-range-in-a-vsto-add-in"></a>VSTO アドインで範囲を折りたたむには

1. 次の例は、VSTO アドインの完全なメソッドを示しています。 このコードを使用するには、プロジェクトの `ThisAddIn` クラスから実行します。

     [!code-vb[Trin_VstcoreWordAutomationAddIn#45](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#45)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#45](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#45)]

## <a name="see-also"></a>関連項目
- [方法: プログラムによって Word 文書にテキストを挿入する](../vsto/how-to-programmatically-insert-text-into-word-documents.md)
- [方法: プログラムによって文書内の範囲を定義および選択する](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)
- [方法: プログラムによって範囲内の開始文字と終了文字を取得する](../vsto/how-to-programmatically-retrieve-start-and-end-characters-in-ranges.md)
- [方法: 範囲を作成するときにプログラムによって段落記号を除外する](../vsto/how-to-programmatically-exclude-paragraph-marks-when-creating-ranges.md)
- [方法: プログラムによって文書内の範囲を拡張する](../vsto/how-to-programmatically-extend-ranges-in-documents.md)
- [方法: プログラムによって Word 文書の範囲をリセットする](../vsto/how-to-programmatically-reset-ranges-in-word-documents.md)
