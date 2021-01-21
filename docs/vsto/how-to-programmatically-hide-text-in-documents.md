---
title: '方法: プログラムによって文書内のテキストを非表示にする'
description: 特定のテキスト範囲のフォントの Hidden プロパティを設定して、Microsoft Word 文書内のテキストを非表示にする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], hiding text
- text [Office development in Visual Studio], hiding in documents
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: a375e8b844f82b5d310841d7b4cdc092b18ff6c3
ms.sourcegitcommit: 4bd2b770e60965fc0843fc25318a7e1b46137875
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/15/2020
ms.locfileid: "97525706"
---
# <a name="how-to-programmatically-hide-text-in-documents"></a>方法: プログラムによって文書内のテキストを非表示にする
  特定範囲のテキストに対応する <xref:Microsoft.Office.Interop.Word._Font.Hidden%2A> の <xref:Microsoft.Office.Interop.Word.Range.Font%2A> プロパティを設定して、文書内のテキストを非表示にできます。

 たとえば、ドキュメントを <xref:Microsoft.Office.Tools.Word.Bookmark> プリンターに送信する前に、内 (ドキュメントレベルのカスタマイズの場合) または (VSTO アドインの場合) 内のテキストを一時的に非表示にすることができ <xref:Microsoft.Office.Interop.Word.Bookmark> ます。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="to-hide-text-in-a-bookmark-control-while-printing-the-document"></a>文書の印刷時に Bookmark コントロール内のテキストを非表示にするには

1. 指定した範囲内にあるテキストをすべて非表示にするプロシージャを作成します。

     [!code-vb[Trin_VstcoreWordAutomation#105](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#105)]
     [!code-csharp[Trin_VstcoreWordAutomation#105](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#105)]

2. 指定した範囲内にあるテキストをすべて再表示するプロシージャを作成します。

     [!code-vb[Trin_VstcoreWordAutomation#106](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#106)]
     [!code-csharp[Trin_VstcoreWordAutomation#106](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#106)]

3. `HideText` メソッドにブックマークの範囲を渡し、文書を印刷して、 `UnhideText` メソッドに同じ範囲を渡します。

     次のコード例はドキュメント レベルのカスタマイズで使用できます。 このコード例を使用するには、プロジェクトの `ThisDocument` クラスから実行します。

     [!code-vb[Trin_VstcoreWordAutomation#107](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#107)]
     [!code-csharp[Trin_VstcoreWordAutomation#107](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#107)]

     次のコード例は VSTO アドインで使用できます。 この例ではアクティブ ドキュメントを使用します。 この例を使用するには、プロジェクトの `ThisAddIn` クラスから実行します。

     [!code-vb[Trin_VstcoreWordAutomationAddIn#107](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#107)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#107](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#107)]

## <a name="compile-the-code"></a>コードのコンパイル
 このコード例では、 <xref:Microsoft.Office.Tools.Word.Bookmark> という名前のコントロール (ドキュメントレベルのカスタマイズの場合) または <xref:Microsoft.Office.Interop.Word.Bookmark> コントロール (VSTO アドインの場合) がドキュメントに含まれていることを前提としてい `bookmark1` ます。

## <a name="see-also"></a>関連項目
- [方法: プログラムによって文書を印刷する](../vsto/how-to-programmatically-print-documents.md)
- [方法: プログラムによって文書内の範囲を定義および選択する](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)
- [方法: プログラムによって Word 文書の範囲をリセットする](../vsto/how-to-programmatically-reset-ranges-in-word-documents.md)
- [方法: プログラムによってブックマークテキストを更新する](../vsto/how-to-programmatically-update-bookmark-text.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)
