---
title: '方法: プログラムによって Word の組み込みダイアログボックスを使用する'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Word [Office development in Visual Studio], dialog boxes
- dialog boxes, Word
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 2c3273b22d98be1c22cf0c8cea2cb57e277b9b48
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85537619"
---
# <a name="how-to-programmatically-use-built-in-dialog-boxes-in-word"></a>方法: プログラムによって Word の組み込みダイアログボックスを使用する
  Microsoft Office Word を使用する場合、ユーザー入力のダイアログボックスを表示する必要がある場合があります。 独自のものを作成することもできますが、Word の組み込みダイアログボックスを使用する方法をお勧めします。この方法は、 <xref:Microsoft.Office.Interop.Word.Dialogs> オブジェクトのコレクションで公開され <xref:Microsoft.Office.Interop.Word.Application> ます。 これにより、列挙として表現される、200の組み込みダイアログボックスにアクセスできます。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="display-dialog-boxes"></a>ダイアログボックスの表示
 ダイアログボックスを表示するには、列挙のいずれかの値を使用して、 <xref:Microsoft.Office.Interop.Word.WdWordDialog> <xref:Microsoft.Office.Interop.Word.Dialog> 表示するダイアログボックスを表すオブジェクトを作成します。 次に、 <xref:Microsoft.Office.Interop.Word.Dialog.Show%2A> オブジェクトのメソッドを呼び出し <xref:Microsoft.Office.Interop.Word.Dialog> ます。

 次のコード例は、[ファイルを**開く**] ダイアログボックスを表示する方法を示しています。 この例を使用するに `ThisDocument` は、プロジェクトのクラスまたはクラスから実行し `ThisAddIn` ます。

 [!code-vb[Trin_VstcoreWordAutomation#100](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#100)]
 [!code-csharp[Trin_VstcoreWordAutomation#100](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#100)]

### <a name="access-dialog-box-members-that-are-available-through-late-binding"></a>遅延バインディングによって使用できるダイアログボックスのメンバーにアクセスする
 Word のダイアログボックスのプロパティとメソッドの一部は、遅延バインディングを通じてのみ使用できます。 **Option Strict**がオンになっている Visual Basic プロジェクトでは、これらのメンバーにアクセスするためにリフレクションを使用する必要があります。 詳細については、「 [Office ソリューションの遅延バインディング](../vsto/late-binding-in-office-solutions.md)」を参照してください。

 次のコード例では、 **Option Strict**がオフになっている Visual Basic プロジェクトの [**ファイルを開く**] ダイアログボックスの [**名前**] プロパティを使用する方法と、またはを対象とする Visual C# プロジェクトを使用する方法を示し [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] ます。 この例を使用するに `ThisDocument` は、プロジェクトのクラスまたはクラスから実行し `ThisAddIn` ます。

 [!code-vb[Trin_VstcoreWordAutomation#122](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#122)]
 [!code-csharp[Trin_VstcoreWordAutomation#122](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#122)]

 次のコード例は、 **Option Strict**がオンになっている Visual Basic プロジェクトの [**ファイルを開く**] ダイアログボックスの [**名前**] プロパティに、リフレクションを使用してアクセスする方法を示しています。 この例を使用するに `ThisDocument` は、プロジェクトのクラスまたはクラスから実行し `ThisAddIn` ます。

 [!code-vb[Trin_VstcoreWordAutomation#102](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#102)]

## <a name="see-also"></a>関連項目
- [方法: プログラムによって Word のダイアログボックスを非表示モードで使用する](../vsto/how-to-programmatically-use-word-dialog-boxes-in-hidden-mode.md)
- [Word オブジェクトモデルの概要](../vsto/word-object-model-overview.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)
- [Option strict ステートメント](/dotnet/visual-basic/language-reference/statements/option-strict-statement)
- [リフレクション (C#)](/dotnet/csharp/programming-guide/concepts/reflection)
- [リフレクション (Visual Basic)](/dotnet/visual-basic/programming-guide/concepts/reflection)
