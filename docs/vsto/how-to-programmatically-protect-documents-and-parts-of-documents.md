---
title: '方法: プログラムによって文書および文書の一部を保護'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- document protection
- documents [Office development in Visual Studio], document protection
- Word documents, protection
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 9acef141944b106a9bace38fef8ede7041bfecc5
ms.sourcegitcommit: 6944ceb7193d410a2a913ecee6f40c6e87e8a54b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/06/2018
ms.locfileid: "35671837"
---
# <a name="how-to-programmatically-protect-documents-and-parts-of-documents"></a>方法: プログラムによって文書および文書の一部を保護
  Microsoft Office Word 文書に保護を追加して、ユーザーによるドキュメントの編集を防止できます。  
  
 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]  
  
 ドキュメントの特定の領域を例外としてマークし、指定したユーザーに対し、ドキュメントのその領域の編集のみを許可することもできます。 たとえば、特定のブックマークを除くドキュメント全体を保護できます。 必要に応じてパスワードを追加し、パスワードを知らないユーザーに対し、ドキュメント保護の解除を禁止できます。  
  
> [!NOTE]  
>  次の例では、パスワード保護を使用しません。ただし、ドキュメント保護を追加するときに、パスワードの使用を検討することもできます。 詳細については、あるドキュメント保護のサンプルを参照してください。 [Office 開発のサンプルとチュートリアル](../vsto/office-development-samples-and-walkthroughs.md)します。  
  
 コンテンツ コントロールを使用してドキュメントの一部を保護することもできます。 詳細については、次を参照してください。[方法: コンテンツ コントロールを使用してドキュメントの一部を保護](../vsto/how-to-protect-parts-of-documents-by-using-content-controls.md)します。  
  
## <a name="protect-a-document-that-is-part-of-a-document-level-customization"></a>ドキュメント レベルのカスタマイズの一部であるドキュメントを保護します。  
  
### <a name="to-protect-a-document-that-is-part-of-a-document-level-customization"></a>ドキュメント レベルのカスタマイズの一部であるドキュメントを保護するには  
  
1.  プロジェクトの <xref:Microsoft.Office.Tools.Word.Document.Protect%2A> クラスの `ThisDocument` メソッドを呼び出します。  
  
     [!code-vb[Trin_VstcoreWordAutomation#111](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#111)]
     [!code-csharp[Trin_VstcoreWordAutomation#111](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#111)]  
  
### <a name="to-exclude-a-bookmark-control-from-document-protection"></a>ブックマーク コントロールをドキュメント保護から除外するには  
  
1.  <xref:Microsoft.Office.Tools.Word.Document.Protect%2A> メソッドを使用してドキュメント全体を保護します。  
  
     [!code-vb[Trin_VstcoreWordAutomation#111](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#111)]
     [!code-csharp[Trin_VstcoreWordAutomation#111](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#111)]  
  
2.  ドキュメント保護から `Bookmark1` を除外します。  
  
     [!code-vb[Trin_VstcoreWordAutomation#112](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#112)]
     [!code-csharp[Trin_VstcoreWordAutomation#112](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#112)]  
  
### <a name="compile-the-code"></a>コードのコンパイル  
 これらのコード例を使用するには、プロジェクトの `ThisDocument` クラスからコードを実行します。 これらのコード例は、コードが表示されるドキュメントに <xref:Microsoft.Office.Tools.Word.Bookmark> という名前の既存の `Bookmark1` コントロールが存在していることを前提としています。  
  
## <a name="protect-a-document-by-using-a-vsto-add-in"></a>VSTO アドインを使用してドキュメントを保護します。  
  
### <a name="to-protect-a-document-by-using-an-application-level-vsto-add-in"></a>アプリケーション レベルの VSTO アドインを使用してドキュメントを保護するには  
  
1.  保護する <xref:Microsoft.Office.Interop.Word._Document.Protect%2A> の <xref:Microsoft.Office.Interop.Word.Document> メソッドを呼び出します。  
  
     アクティブなドキュメントを保護するコード例を次に示します。 このコード例を使用するには、プロジェクトの `ThisAddIn` クラスからコードを実行します。  
  
     [!code-vb[Trin_VstcoreWordAutomationAddIn#111](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#111)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#111](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#111)]  
  
## <a name="see-also"></a>関連項目  
 [ドキュメント レベルのソリューションでドキュメントの保護](../vsto/document-protection-in-document-level-solutions.md)   
 [Office ドキュメントのパスワード保護](../vsto/password-protection-on-office-documents.md)   
 [方法: コードの制限されたアクセス許可を持つドキュメントの背後で実行を許可](../vsto/how-to-permit-code-to-run-behind-documents-with-restricted-permissions.md)   
 [方法: Word 文書に Bookmark コントロールを追加](../vsto/how-to-add-bookmark-controls-to-word-documents.md)   
 [設計および Office ソリューションの作成](../vsto/designing-and-creating-office-solutions.md)  
  
  