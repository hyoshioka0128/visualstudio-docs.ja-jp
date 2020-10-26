---
title: '方法: プログラムによってブックマークテキストを更新する'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- bookmarks, updating text
- text [Office development in Visual Studio], updating in bookmarks
- Bookmark control, updating contents
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 9b76c239606a4bf0d6da203bd4eea45a11162706
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85546953"
---
# <a name="how-to-programmatically-update-bookmark-text"></a>方法: プログラムによってブックマークテキストを更新する
  Microsoft Office Word 文書のプレースホルダー ブックマークにテキストを挿入することにより、そのテキストを後で取得したり、ブックマーク内のテキストを置き換えたりすることができます。 ドキュメント レベルのカスタマイズを開発している場合は、データにバインドされた <xref:Microsoft.Office.Tools.Word.Bookmark> コントロール内のテキストを更新することもできます。 詳細については、「 [データを Office ソリューションのコントロールにバインドする](../vsto/binding-data-to-controls-in-office-solutions.md)」を参照してください。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

 ブックマーク オブジェクトには次の 2 種類があります。

- <xref:Microsoft.Office.Tools.Word.Bookmark> ホスト コントロール。

   <xref:Microsoft.Office.Tools.Word.Bookmark> コントロールは、ネイティブ <xref:Microsoft.Office.Interop.Word.Bookmark> オブジェクトを拡張したもので、データのバインドとイベントの公開が可能になります。 ホストコントロールの詳細については、「 [ホスト項目とホストコントロールの概要](../vsto/host-items-and-host-controls-overview.md)」を参照してください。

- <xref:Microsoft.Office.Interop.Word.Bookmark> ネイティブ オブジェクトです。

   <xref:Microsoft.Office.Interop.Word.Bookmark> オブジェクトには、イベントや、データのバインド機能はありません。

  ブックマークにテキストを割り当てる場合、<xref:Microsoft.Office.Interop.Word.Bookmark> と <xref:Microsoft.Office.Tools.Word.Bookmark> の動作は異なります。 詳細については、「 [Bookmark コントロール](../vsto/bookmark-control.md)」を参照してください。

## <a name="use-host-controls"></a>ホストコントロールを使用する

### <a name="to-update-bookmark-contents-using-a-bookmark-control"></a>Bookmark コントロールを使用してブックマークの内容を更新するには

1. ブックマークの名前を指定する引数 `bookmark` と <xref:Microsoft.Office.Tools.Word.Bookmark.Text%2A> プロパティに割り当てる文字列を指定する引数 `newText` を受け取るプロシージャを作成します。

    > [!NOTE]
    > <xref:Microsoft.Office.Tools.Word.Bookmark> コントロールの <xref:Microsoft.Office.Tools.Word.Bookmark.Text%2A> または <xref:Microsoft.Office.Tools.Word.Bookmark.FormattedText%2A> プロパティにテキストを割り当てても、ブックマークは削除されません。

     [!code-vb[Trin_VstcoreWordAutomation#63](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#63)]
     [!code-csharp[Trin_VstcoreWordAutomation#63](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#63)]

2. *NewText*文字列を <xref:Microsoft.Office.Tools.Word.Bookmark.Text%2A> のプロパティに割り当て <xref:Microsoft.Office.Tools.Word.Bookmark> ます。

     [!code-vb[Trin_VstcoreWordAutomation#64](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#64)]
     [!code-csharp[Trin_VstcoreWordAutomation#64](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#64)]

## <a name="use-word-objects"></a>Word オブジェクトを使用する

### <a name="to-update-bookmark-contents-using-a-word-bookmark-object"></a>Word の Bookmark オブジェクトを使用してブックマークの内容を更新するには

1. <xref:Microsoft.Office.Interop.Word.Bookmark> の名前を指定する引数 `bookmark` とブックマークの <xref:Microsoft.Office.Interop.Word.Range.Text%2A> プロパティに割り当てる文字列を指定する引数 `newText` を受け取るプロシージャを作成します。

    > [!NOTE]
    > Word のネイティブ <xref:Microsoft.Office.Interop.Word.Bookmark> オブジェクトにテキストを割り当てると、ブックマークは削除されます。

     [!code-vb[Trin_VstcoreWordAutomation#65](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#65)]
     [!code-csharp[Trin_VstcoreWordAutomation#65](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#65)]

2. ブックマークのプロパティに *newText* 文字列を割り当てます。これにより、 <xref:Microsoft.Office.Interop.Word.Range.Text%2A> ブックマークが自動的に削除されます。 その後、<xref:Microsoft.Office.Interop.Word.Bookmarks> コレクションにブックマークを再び追加します。

     次のコード例はドキュメント レベルのカスタマイズで使用できます。

     [!code-vb[Trin_VstcoreWordAutomation#66](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#66)]
     [!code-csharp[Trin_VstcoreWordAutomation#66](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#66)]

     次のコード例は VSTO アドインで使用できます。 この例ではアクティブ ドキュメントを使用します。

     [!code-vb[Trin_VstcoreWordAutomationAddIn#66](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#66)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#66](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#66)]

## <a name="see-also"></a>関連項目
- [方法: プログラムによって Word 文書にテキストを挿入する](../vsto/how-to-programmatically-insert-text-into-word-documents.md)
- [Word オブジェクトモデルの概要](../vsto/word-object-model-overview.md)
- [Bookmark コントロール](../vsto/bookmark-control.md)
