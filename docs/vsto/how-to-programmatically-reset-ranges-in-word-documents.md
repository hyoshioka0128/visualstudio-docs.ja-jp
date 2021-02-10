---
title: '方法: プログラムによって Word 文書の範囲をリセットする'
description: Visual Studio を使用して、Microsoft Word 文書内の既存の範囲をプログラムによってサイズ変更する方法について説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
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
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 562b4dab6c26af12760190b01ff460c7080a3bb2
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99958779"
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
