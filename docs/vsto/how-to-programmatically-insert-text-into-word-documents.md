---
title: '方法: プログラムによって Word 文書にテキストを挿入する'
description: Visual Studio を使用して Microsoft Word 文書にテキストをプログラムで挿入する方法について説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 08/14/2019
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ranges, inserting text in documents
- text [Office development in Visual Studio], inserting in documents
- ranges, replacing text in documents
- documents [Office development in Visual Studio], inserting text
- text [Office development in Visual Studio], replacing
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: e82aef0fc473b0ed11bcc9fce15b6426d5b91b4b
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99885392"
---
# <a name="how-to-programmatically-insert-text-into-word-documents"></a>方法: プログラムによって Word 文書にテキストを挿入する
  Microsoft Office Word の文書にテキストを挿入するには、主に次の 3 つの方法があります。

- 範囲内にテキストを挿入する。

- 範囲内のテキストを新しいテキストに置換する。

- <xref:Microsoft.Office.Interop.Word.Selection.TypeText%2A> オブジェクトの <xref:Microsoft.Office.Interop.Word.Selection> メソッドを使用して、カーソルの位置または選択範囲にテキストを挿入する。

> [!NOTE]
> テキストをコンテンツ コントロールやブックマークに挿入することもできます。 詳細については、「 [コンテンツコントロール](../vsto/content-controls.md) と [ブックマークコントロール](../vsto/bookmark-control.md)」を参照してください。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

[!include[Add-ins note](includes/addinsnote.md)]

## <a name="insert-text-in-a-range"></a>範囲内にテキストを挿入する
 <xref:Microsoft.Office.Interop.Word.Range.Text%2A> オブジェクトの <xref:Microsoft.Office.Interop.Word.Range> プロパティを使用して、文書にテキストを挿入します。

### <a name="to-insert-text-in-a-range"></a>範囲内にテキストを挿入するには

1. 文書の先頭に範囲を指定し、 **New Text** というテキストを挿入します。

     次のコード例はドキュメント レベルのカスタマイズで使用できます。

     [!code-vb[Trin_VstcoreWordAutomation#51](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#51)]
     [!code-csharp[Trin_VstcoreWordAutomation#51](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#51)]

     次のコード例は VSTO アドインで使用できます。 このコードでは作業中のドキュメントを使用します。

     [!code-vb[Trin_VstcoreWordAutomationAddIn#51](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#51)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#51](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#51)]

2. 1 文字から挿入したテキストの長さまで拡張された <xref:Microsoft.Office.Interop.Word.Range> オブジェクトを選択します。

     [!code-vb[Trin_VstcoreWordAutomation#52](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#52)]
     [!code-csharp[Trin_VstcoreWordAutomation#52](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#52)]

## <a name="replace-text-in-a-range"></a>範囲内のテキストの置換
 指定した範囲にテキストが含まれている場合は、範囲内のすべてのテキストが挿入したテキストで置換されます。

### <a name="to-replace-text-in-a-range"></a>範囲内のテキストを置換するには

1. 文書の先頭の 12 文字から成る <xref:Microsoft.Office.Interop.Word.Range> オブジェクトを作成します。

     次のコード例はドキュメント レベルのカスタマイズで使用できます。

     [!code-vb[Trin_VstcoreWordAutomation#53](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#53)]
     [!code-csharp[Trin_VstcoreWordAutomation#53](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#53)]

     次のコード例は VSTO アドインで使用できます。 このコードでは作業中のドキュメントを使用します。

     [!code-vb[Trin_VstcoreWordAutomationAddIn#53](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#53)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#53](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#53)]

2. これらの文字を **New Text** という文字列で置換します。

     [!code-vb[Trin_VstcoreWordAutomation#54](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#54)]
     [!code-csharp[Trin_VstcoreWordAutomation#54](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#54)]

3. 範囲を選択します。

     [!code-vb[Trin_VstcoreWordAutomation#55](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#55)]
     [!code-csharp[Trin_VstcoreWordAutomation#55](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#55)]

## <a name="insert-text-using-typetext"></a>TypeText を使用してテキストを挿入する
 <xref:Microsoft.Office.Interop.Word.Selection.TypeText%2A> メソッドは、選択範囲にテキストを挿入します。 <xref:Microsoft.Office.Interop.Word.Selection.TypeText%2A> の動作は、ユーザーのコンピューターで設定されているオプションによって異なります。 次のプロシージャのコードは、 <xref:Microsoft.Office.Interop.Word.Selection> オブジェクト変数を宣言し、 **Overtype** オプションがオンになっている場合はオフにします。 **Overtype** オプションが有効になっていると、カーソル位置の隣にあるテキストが上書きされます。

### <a name="to-insert-text-using-the-typetext-method"></a>TypeText メソッドを使用してテキストを挿入するには

1. まず、<xref:Microsoft.Office.Interop.Word.Selection> オブジェクト変数を宣言します。

    [!code-vb[Trin_VstcoreWordAutomation#57](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#57)]
    [!code-csharp[Trin_VstcoreWordAutomation#57](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#57)]

2. **Overtype** オプションがオンの場合はオフにします。

    [!code-vb[Trin_VstcoreWordAutomation#58](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#58)]
    [!code-csharp[Trin_VstcoreWordAutomation#58](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#58)]

3. 現在の選択範囲が挿入ポイントであるかどうかを確認します。

    選択範囲が挿入位置である場合は、 <xref:Microsoft.Office.Interop.Word.Selection.TypeText%2A>を使用して文を挿入し、 <xref:Microsoft.Office.Interop.Word.Selection.TypeParagraph%2A> メソッドを使用して段落記号を挿入します。

    [!code-vb[Trin_VstcoreWordAutomation#59](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#59)]
    [!code-csharp[Trin_VstcoreWordAutomation#59](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#59)]

4. **ElseIf** ブロック内のコードで、選択範囲が通常の選択範囲であるかどうかを確認します。 通常の選択範囲である場合は、次の **If** ブロックで、 **ReplaceSelection** オプションがオンになっているかどうかを確認します。 オンである場合は、選択範囲の <xref:Microsoft.Office.Interop.Word.Selection.Collapse%2A> メソッドを使用して、選択範囲を選択されているテキスト ブロックの先頭の挿入ポイントに折りたたみます。 テキストと段落記号を挿入します。

    [!code-vb[Trin_VstcoreWordAutomation#60](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#60)]
    [!code-csharp[Trin_VstcoreWordAutomation#60](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#60)]

5. 選択範囲が挿入ポイントでも選択テキストのブロックではない場合、 **Else** ブロックのコードは何も実行しません。

    [!code-vb[Trin_VstcoreWordAutomation#61](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#61)]
    [!code-csharp[Trin_VstcoreWordAutomation#61](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#61)]

   また、オブジェクトのメソッドを使用することもできます。このメソッドは、 <xref:Microsoft.Office.Interop.Word.Selection.TypeBackspace%2A> <xref:Microsoft.Office.Interop.Word.Selection> キーボードの **Backspace** キーの機能を模倣しています。 ただし、テキストの挿入および操作については、<xref:Microsoft.Office.Interop.Word.Range> オブジェクトの方がより細かく制御できます。

   完全なコード例を次に示します。 この例を使用するには、プロジェクトの `ThisDocument` クラスか `ThisAddIn` クラスからコードを実行します。

   [!code-vb[Trin_VstcoreWordAutomation#56](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#56)]
   [!code-csharp[Trin_VstcoreWordAutomation#56](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#56)]

## <a name="see-also"></a>関連項目
- [方法: プログラムによって文書内のテキストを書式設定する](../vsto/how-to-programmatically-format-text-in-documents.md)
- [方法: プログラムによって文書内の範囲を定義および選択する](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)
- [方法: プログラムによって文書内の範囲を拡張する](../vsto/how-to-programmatically-extend-ranges-in-documents.md)
