---
title: '方法: プログラムによって Word 文書の範囲をリセットする'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], resetting ranges
- ranges, resetting in documents
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 8f1978a280a26af3b2a21e0bc5a4c9a238a723a9
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547122"
---
# <a name="how-to-programmatically-reset-ranges-in-word-documents"></a>方法: プログラムによって Word 文書の範囲をリセットする
  <xref:Microsoft.Office.Interop.Word.Range.SetRange%2A> メソッドを使用して、Microsoft Office の Word 文書で既存の範囲のサイズを変更します。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="to-reset-an-existing-range"></a>既存の範囲をリセットするには

1. ドキュメント内の最初の 7 つの文字で始まる最初の範囲を設定します。

     次のコード例はドキュメント レベルのカスタマイズで使用できます。

     [!code-vb[Trin_VstcoreWordAutomation#43](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#43)]
     [!code-csharp[Trin_VstcoreWordAutomation#43](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#43)]

     次のコード例は VSTO アドインで使用できます。 このコードでは作業中のドキュメントを使用します。

     [!code-vb[Trin_VstcoreWordAutomationAddIn#43](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#43)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#43](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#43)]

2. <xref:Microsoft.Office.Interop.Word.Range.SetRange%2A> を使用して、2 番目の文から範囲を開始し、5 番目の文の末尾までで範囲を終了します。

     [!code-vb[Trin_VstcoreWordAutomation#44](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#44)]
     [!code-csharp[Trin_VstcoreWordAutomation#44](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#44)]

## <a name="document-level-customization-example"></a>ドキュメント レベルのカスタマイズの例

### <a name="to-reset-an-existing-range-in-a-document-level-customization"></a>ドキュメント レベルのカスタマイズで既存の範囲をリセットするには

1. 次の例は、ドキュメント レベルのカスタマイズの例全体を示しています。 このコードを使用するには、プロジェクトの `ThisDocument` クラスから実行します。

     [!code-vb[Trin_VstcoreWordAutomation#42](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#42)]
     [!code-csharp[Trin_VstcoreWordAutomation#42](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#42)]

## <a name="vsto-add-in-example"></a>VSTO アドインの例

### <a name="to-reset-an-existing-range-in-a-vsto-add-in"></a>VSTO アドインで既存の範囲をリセットするには

1. 次の例は、VSTO アドインの完全な例を示しています。 このコードを使用するには、プロジェクトの `ThisAddIn` クラスから実行します。

     [!code-vb[Trin_VstcoreWordAutomationAddIn#42](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#42)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#42](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#42)]

## <a name="see-also"></a>関連項目
- [方法: プログラムによって文書内の範囲を拡張する](../vsto/how-to-programmatically-extend-ranges-in-documents.md)
- [方法: プログラムによって文書内の範囲を定義および選択する](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)
- [方法: プログラムによって範囲内の開始文字と終了文字を取得する](../vsto/how-to-programmatically-retrieve-start-and-end-characters-in-ranges.md)
- [方法: プログラムによって文書内の範囲または選択項目を折りたたむ](../vsto/how-to-programmatically-collapse-ranges-or-selections-in-documents.md)
