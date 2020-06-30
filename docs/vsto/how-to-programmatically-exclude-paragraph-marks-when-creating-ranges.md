---
title: プログラムによって範囲を作成するときに段落記号を除外する
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], excluding paragraphs
- ranges, excluding paragraph marks in Word
- documents [Office development in Visual Studio], paragraph marks
- paragraphs, controlling structure
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 20d91aff6b09e659375494c387eea94ef05cc682
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547434"
---
# <a name="how-to-programmatically-exclude-paragraph-marks-when-creating-ranges"></a>方法: 範囲を作成するときにプログラムによって段落記号を除外する
  段落に基づいて <xref:Microsoft.Office.Interop.Word.Range> オブジェクトを作成する場合、段落記号などの印刷されない文字はすべて範囲に含まれています。 出力先の段落に、元の段落からテキストを挿入したい場合があります。 出力先の段落を複数の段落に分割したくない場合、元の段落から段落記号を最初に削除する必要があります。 また、段落の書式設定情報は段落記号に格納されるので、範囲を既存の段落に挿入するとき、この情報を含めないようにすることもできます。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

 次の手順の例では、2 つの文字列変数を宣言し、アクティブなドキュメント内の最初と 2 番目の段落の内容を取得し、その内容を入れ替えます。 その後、 <xref:Microsoft.Office.Interop.Word.Range.MoveEnd%2A> メソッドを使用して範囲から段落記号を削除し、段落内にテキストを挿入しています。

## <a name="to-control-paragraph-structure-when-inserting-text"></a>テキストを挿入するときに、段落の構造を制御するには

1. 最初と 2 番目の段落の 2 つの範囲変数を作成して、 <xref:Microsoft.Office.Interop.Word.Range.Text%2A> プロパティを使用してその内容を取得します。

     次のコード例はドキュメント レベルのカスタマイズで使用できます。

     [!code-vb[Trin_VstcoreWordAutomation#27](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#27)]
     [!code-csharp[Trin_VstcoreWordAutomation#27](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#27)]

     次のコード例はアプリケーション レベルの VSTO アドインで使用できます。 このコードでは作業中のドキュメントを使用します。

     [!code-vb[Trin_VstcoreWordAutomationAddIn#27](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#27)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#27](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#27)]

2. 2 つの段落の間のテキストを入れ替え、 <xref:Microsoft.Office.Interop.Word.Range.Text%2A> プロパティを割り当てます。

     [!code-vb[Trin_VstcoreWordAutomation#28](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#28)]
     [!code-csharp[Trin_VstcoreWordAutomation#28](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#28)]

3. 範囲を順に選択し、一時停止してメッセージ ボックスに結果を表示します。

     [!code-vb[Trin_VstcoreWordAutomation#29](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#29)]
     [!code-csharp[Trin_VstcoreWordAutomation#29](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#29)]

4. `firstRange` メソッドを使用して <xref:Microsoft.Office.Interop.Word.Range.MoveEnd%2A> を調整し、段落記号が `firstRange`に含まれないようにします。

     [!code-vb[Trin_VstcoreWordAutomation#30](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#30)]
     [!code-csharp[Trin_VstcoreWordAutomation#30](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#30)]

5. 最初の段落の残りのテキストを置換して、新しい文字列を範囲の <xref:Microsoft.Office.Interop.Word.Range.Text%2A> プロパティに割り当てます。

     [!code-vb[Trin_VstcoreWordAutomation#31](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#31)]
     [!code-csharp[Trin_VstcoreWordAutomation#31](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#31)]

6. `secondRange`のテキストを置換して、段落記号を含めます。

     [!code-vb[Trin_VstcoreWordAutomation#32](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#32)]
     [!code-csharp[Trin_VstcoreWordAutomation#32](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#32)]

7. `firstRange` を選択し、一時停止してメッセージ ボックスに結果を表示して、 `secondRange`と同じ操作を行います。

     `firstRange` が再定義され、段落記号が除外されると段落の元の書式が保持されます。 ただし、文が `secondRange`の段落記号の上に挿入されると、別の段落が削除されます。

     [!code-vb[Trin_VstcoreWordAutomation#33](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#33)]
     [!code-csharp[Trin_VstcoreWordAutomation#33](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#33)]

     2 つの範囲の元の内容は文字列として保存されているため、ドキュメントを元の状態に復元することができます。

8. `firstRange` <xref:Microsoft.Office.Interop.Word.Range.MoveEnd%2A> 1 文字の位置に対してメソッドを使用して、段落記号を含めるように再調整します。

     [!code-vb[Trin_VstcoreWordAutomation#34](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#34)]
     [!code-csharp[Trin_VstcoreWordAutomation#34](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#34)]

9. `secondRange`を削除します。 これにより、3 段落目が元の位置に戻ります。

     [!code-vb[Trin_VstcoreWordAutomation#35](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#35)]
     [!code-csharp[Trin_VstcoreWordAutomation#35](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#35)]

10. `firstRange`に元の段落テキストを復元します。

     [!code-vb[Trin_VstcoreWordAutomation#36](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#36)]
     [!code-csharp[Trin_VstcoreWordAutomation#36](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#36)]

11. <xref:Microsoft.Office.Interop.Word.Range.InsertAfter%2A> オブジェクトの <xref:Microsoft.Office.Interop.Word.Range> メソッドを使用して元の 2 段落目の内容を `firstRange`の後に挿入し、 `firstRange`を選択します。

     [!code-vb[Trin_VstcoreWordAutomation#37](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#37)]
     [!code-csharp[Trin_VstcoreWordAutomation#37](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#37)]

## <a name="document-level-customization-example"></a>ドキュメントレベルのカスタマイズの例

### <a name="to-control-paragraph-structure-when-inserting-text-in-document-level-customizations"></a>ドキュメント レベルのカスタマイズでテキストを挿入するときに段落の構造を制御するには

1. 次の例は、ドキュメント レベルのカスタマイズのメソッド全体を示しています。 このコードを使用するには、プロジェクトの `ThisDocument` クラスから実行します。

     [!code-vb[Trin_VstcoreWordAutomation#26](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#26)]
     [!code-csharp[Trin_VstcoreWordAutomation#26](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#26)]

## <a name="vsto-add-in-example"></a>VSTO アドインの例

### <a name="to-control-paragraph-structure-when-inserting-text-in-a-vsto-add-in"></a>VSTO アドインにテキストを挿入するときに段落の構造を制御するには

1. 次の例は、VSTO アドインの完全なメソッドを示しています。 このコードを使用するには、プロジェクトの `ThisAddIn` クラスから実行します。

     [!code-vb[Trin_VstcoreWordAutomationAddIn#26](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#26)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#26](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#26)]

## <a name="see-also"></a>関連項目
- [方法: プログラムによって文書内の範囲を拡張する](../vsto/how-to-programmatically-extend-ranges-in-documents.md)
- [方法: プログラムによって文書内の範囲または選択項目を折りたたむ](../vsto/how-to-programmatically-collapse-ranges-or-selections-in-documents.md)
- [方法: プログラムによって Word 文書にテキストを挿入する](../vsto/how-to-programmatically-insert-text-into-word-documents.md)
- [方法: プログラムによって Word 文書の範囲をリセットする](../vsto/how-to-programmatically-reset-ranges-in-word-documents.md)
- [方法: プログラムによって文書内の範囲を定義および選択する](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)
