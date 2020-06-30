---
title: プログラムによってドキュメントに画像とワードアートを追加する
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], adding pictures
- Word documents, adding pictures
- Word documents, adding Word Art
- graphics, adding to Word documents
- WordArt, adding to documents
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 621051c827b08e66d68bc348401c2a939e279bcf
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85538087"
---
# <a name="how-to-programmatically-add-pictures-and-word-art-to-documents"></a>方法: プログラムによって文書に画像とワードアートを追加する
  デザイン時または実行時に、画像および描画オブジェクトをドキュメントに追加できます。 ワードアートでは、Microsoft Office Word ドキュメントに装飾的なテキストを追加することができます。 これらの特別なテキスト効果は、ドキュメントに挿入できる、カスタマイズ可能な描画オブジェクトです。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="add-a-picture-at-design-time"></a>デザイン時に画像を追加する
 ドキュメント レベルのカスタマイズを開発している場合は、デザイン時にドキュメントに画像を追加できます。

### <a name="to-add-a-picture-to-a-word-document-at-design-time"></a>デザイン時に Word 文書に画像を追加するには

1. ドキュメント内の画像を挿入する場所にカーソルを置きます。

2. リボンの [**挿入**] タブをクリックします。

3. [図 **] グループの**[**画像**] をクリックします。

4. [**画像の挿入**] ダイアログボックスで、挿入する画像に移動し、[**挿入**] をクリックします。

     画像が、ドキュメントの現在のカーソル位置に追加されます。

## <a name="add-a-picture-at-run-time"></a>実行時に画像を追加する
 現在のカーソル位置でドキュメントに画像を挿入できます。

### <a name="to-add-a-picture-at-the-cursor-location"></a>カーソルの場所に画像を追加するには

1. <xref:Microsoft.Office.Interop.Word.InlineShapes> コレクションの <xref:Microsoft.Office.Interop.Word.InlineShapes.AddPicture%2A> メソッドを呼び出し、ファイル名を渡します。

     [!code-vb[Trin_VstcoreWordAutomation#108](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#108)]
     [!code-csharp[Trin_VstcoreWordAutomation#108](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#108)]

## <a name="add-wordart-at-design-time"></a>デザイン時にワードアートを追加する
 ドキュメント レベルのカスタマイズを開発している場合は、デザイン時にドキュメントにワードアートを追加できます。

### <a name="to-add-wordart-to-a-word-document-at-design-time"></a>デザイン時にワードアートを Word ドキュメントを追加するには

1. ドキュメント内のワードアートを挿入する場所にカーソルを置きます。

2. リボンの [**挿入**] タブをクリックします。

3. [**テキスト**] グループの [**ワードアート**] をクリックし、ワードアートのスタイルを選択します。

4. ドキュメントに表示するテキストを [**ワードアートテキストの編集**] ダイアログボックスに追加し、[ **OK**] をクリックします。

     選択したワードアート スタイルが適用されたテキストが、ドキュメントに追加されます。

## <a name="add-wordart-at-run-time"></a>実行時にワードアートを追加する
 現在のカーソル位置でドキュメントにワードアートを挿入できます。 ドキュメント レベルのカスタマイズと VSTO アドインでは、手順が異なります。

### <a name="to-add-wordart-at-the-cursor-location-in-a-document-level-customization"></a>ドキュメント レベルのカスタマイズで、カーソル位置にワードアートを追加するには

1. 現在のカーソル位置の左と上の位置を取得します。

     [!code-vb[Trin_VstcoreWordAutomation#109](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#109)]
     [!code-csharp[Trin_VstcoreWordAutomation#109](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#109)]

2. ドキュメント内の <xref:Microsoft.Office.Interop.Word.Shapes> オブジェクトの <xref:Microsoft.Office.Interop.Word.Shapes.AddTextEffect%2A> メソッドを呼び出します。

     [!code-vb[Trin_VstcoreWordAutomation#110](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#110)]
     [!code-csharp[Trin_VstcoreWordAutomation#110](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#110)]

### <a name="to-add-wordart-at-the-cursor-location-in-a-vsto-add-in"></a>VSTO アドインでカーソル位置にワードアートを追加するには

1. 現在のカーソル位置の左と上の位置を取得します。

     [!code-vb[Trin_VstcoreWordAutomationAddIn#109](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#109)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#109](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#109)]

2. 作業中のドキュメント (または指定した別のドキュメント) の <xref:Microsoft.Office.Interop.Word.Shapes> オブジェクトの <xref:Microsoft.Office.Interop.Word.Shapes.AddTextEffect%2A> メソッドを呼び出します。

     [!code-vb[Trin_VstcoreWordAutomationAddIn#110](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#110)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#110](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#110)]

## <a name="compile-the-code"></a>コードのコンパイル

- *SamplePicture.jpg*という名前の画像が C ドライブに存在している必要があります。

## <a name="see-also"></a>関連項目
- [方法: プログラムによって既存のドキュメントを開く](../vsto/how-to-programmatically-open-existing-documents.md)
- [方法: プログラムによって Word 文書にテキストを挿入する](../vsto/how-to-programmatically-insert-text-into-word-documents.md)
- [方法: プログラムによって検索後に選択を復元する](../vsto/how-to-programmatically-restore-selections-after-searches.md)
- [方法: プログラムによって文書を保存する](../vsto/how-to-programmatically-save-documents.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)
