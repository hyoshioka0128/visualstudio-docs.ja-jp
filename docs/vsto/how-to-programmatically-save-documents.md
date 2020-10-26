---
title: '方法: プログラムによって文書を保存する'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], saving
- Word [Office development in Visual Studio], saving documents
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 464d131261ecfb0a64a3ca279007ff9332cdb2e4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85537593"
---
# <a name="how-to-programmatically-save-documents"></a>方法: プログラムによって文書を保存する

Word 文書 Microsoft Office 保存するには、いくつかの方法があります。 ドキュメントの名前を変更せずにドキュメントを保存することも、新しい名前でドキュメントを保存することもできます。

[!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="save-a-document-without-changing-the-name"></a>名前を変更せずにドキュメントを保存する

### <a name="to-save-the-document-associated-with-a-document-level-customization"></a>ドキュメントレベルのカスタマイズに関連付けられているドキュメントを保存するには

1. <xref:Microsoft.Office.Tools.Word.Document.Save%2A> クラスの <xref:Microsoft.Office.Tools.Word.Document> メソッドを呼び出します。 このコード例を使用するには、プロジェクトの `ThisDocument` クラスからコードを実行します。

     [!code-vb[Trin_VstcoreWordAutomation#7](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#7)]
     [!code-csharp[Trin_VstcoreWordAutomation#7](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#7)]

### <a name="to-save-the-active-document"></a>アクティブ文書を保存するには

1. <xref:Microsoft.Office.Interop.Word._Document.Save%2A>アクティブなドキュメントに対してメソッドを呼び出します。 このコード例を使用するには、プロジェクトの `ThisDocument` クラスまたは `ThisAddIn` クラスからコードを実行します。

    [!code-vb[Trin_VstcoreWordAutomation#8](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#8)]
    [!code-csharp[Trin_VstcoreWordAutomation#8](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#8)]

   保存するドキュメントがアクティブなドキュメントであるかどうかわからない場合は、そのドキュメントを名前で参照できます。

### <a name="to-save-a-document-specified-by-name"></a>名前で指定したドキュメントを保存するには

1. コレクションの引数としてドキュメント名を使用し <xref:Microsoft.Office.Interop.Word.Documents> ます。 このコード例を使用するには、プロジェクトの `ThisDocument` クラスまたは `ThisAddIn` クラスからコードを実行します。

     [!code-vb[Trin_VstcoreWordAutomation#9](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#9)]
     [!code-csharp[Trin_VstcoreWordAutomation#9](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#9)]

## <a name="save-a-document-with-a-new-name"></a>新しい名前でドキュメントを保存する

`SaveAs`新しい名前でドキュメントを保存するには、メソッドを使用します。 このホスト項目のメソッドは、ドキュメントレベルの Word プロジェクトで使用することも <xref:Microsoft.Office.Tools.Word.Document> 、任意の word プロジェクトのネイティブオブジェクトで使用することもでき <xref:Microsoft.Office.Interop.Word.Document> ます。 このメソッドでは、新しいファイル名を指定する必要がありますが、他の引数は省略可能です。

> [!NOTE]
> のイベントハンドラー内に [ **SaveAs** ] ダイアログボックスを表示 <xref:Microsoft.Office.Interop.Word.ApplicationEvents4_Event.DocumentBeforeSave> し、 `ThisDocument` *Cancel* パラメーターを **false**に設定すると、アプリケーションが予期せず終了する可能性があります。 *Cancel*パラメーターを**true**に設定すると、自動保存が無効になっていることを示すエラーメッセージが表示されます。

### <a name="to-save-the-document-associated-with-a-document-level-customization-with-a-new-name"></a>ドキュメントレベルのカスタマイズに関連付けられているドキュメントを新しい名前で保存するには

1. `SaveAs` `ThisDocument` 完全修飾パスとファイル名を使用して、プロジェクトのクラスのメソッドを呼び出します。 指定した名前のファイルが既に対象のフォルダー内に存在する場合、そのファイルは警告なしで上書きされます。 このコード例を使用するには、 `ThisDocument` クラスからコードを実行します。

    > [!NOTE]
    > `SaveAs`ターゲットディレクトリが存在しない場合、またはファイルの保存に関する他の問題がある場合、メソッドは例外をスローします。 `try...catch`メソッドの周囲、 `SaveAs` または呼び出し元のメソッド内でブロックを使用することをお勧めします。

     [!code-vb[Trin_VstcoreWordAutomation#10](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#10)]
     [!code-csharp[Trin_VstcoreWordAutomation#10](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#10)]

### <a name="to-save-a-native-document-with-a-new-name"></a>ネイティブドキュメントを新しい名前で保存するには

1. <xref:Microsoft.Office.Interop.Word._Document.SaveAs%2A> <xref:Microsoft.Office.Interop.Word.Document> 完全修飾パスとファイル名を使用して、保存するのメソッドを呼び出します。 指定した名前のファイルが既に対象のフォルダー内に存在する場合、そのファイルは警告なしで上書きされます。

     次のコード例では、作業中のドキュメントを新しい名前で保存します。 このコード例を使用するには、プロジェクトの `ThisDocument` クラスまたは `ThisAddIn` クラスからコードを実行します。

    > [!NOTE]
    > <xref:Microsoft.Office.Interop.Word._Document.SaveAs%2A>ターゲットディレクトリが存在しない場合、またはファイルの保存に関する他の問題がある場合、メソッドは例外をスローします。 試すことをお勧めします。 **try...catch**メソッドの周囲、 <xref:Microsoft.Office.Interop.Word._Document.SaveAs%2A> または呼び出し元のメソッド内の catch ブロック。

     [!code-vb[Trin_VstcoreWordAutomationAddIn#10](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#10)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#10](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#10)]

## <a name="compile-the-code"></a>コードのコンパイル

このコード例で必要な要素は次のとおりです。

- ドキュメントを名前で保存するには、 *NewDocument.doc* という名前のドキュメントが C ドライブの *Test* という名前のディレクトリに存在する必要があります。

- 新しい名前でドキュメントを保存するには、 *Test* という名前のディレクトリが C ドライブに存在している必要があります。

## <a name="see-also"></a>関連項目

- [方法: プログラムによって文書を閉じる](../vsto/how-to-programmatically-close-documents.md)
- [方法: プログラムによって既存のドキュメントを開く](../vsto/how-to-programmatically-open-existing-documents.md)
- [ドキュメントホスト項目](../vsto/document-host-item.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)
