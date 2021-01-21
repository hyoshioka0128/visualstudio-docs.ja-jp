---
title: '方法: パスワードで保護されたドキュメントでデータをキャッシュする'
description: パスワードで保護されているドキュメントまたはブックのデータキャッシュにデータを追加する場合、プロジェクトの2つのメソッドをオーバーライドすることによって、キャッシュされたデータへの変更を保存できます。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data caching [Office development in Visual Studio], protected documents
- datasets [Office development in Visual Studio], caching
- data [Office development in Visual Studio], caching
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 2a11b70da4bdd2500f70d2b45f025340af21ea94
ms.sourcegitcommit: ce85cff795df29e2bd773b4346cd718dccda5337
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/08/2020
ms.locfileid: "96846000"
---
# <a name="how-to-cache-data-in-a-password-protected-document"></a>方法: パスワードで保護されたドキュメントでデータをキャッシュする
  パスワードで保護されているドキュメントまたはブックのデータキャッシュにデータを追加した場合、キャッシュされたデータへの変更は自動的には保存されません。 キャッシュされたデータへの変更を保存するには、プロジェクト内の2つのメソッドをオーバーライドします。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

## <a name="caching-in-word-documents"></a>Word 文書でのキャッシュ

### <a name="to-cache-data-in-a-word-document-that-is-protected-with-a-password"></a>パスワードで保護されている Word 文書にデータをキャッシュするには

1. クラスで `ThisDocument` 、パブリックフィールドまたはキャッシュされるプロパティをマークします。 詳細については、「 [データのキャッシュ](../vsto/caching-data.md)」を参照してください。

2. クラスの <xref:Microsoft.Office.Tools.Word.DocumentBase.UnprotectDocument%2A> メソッドをオーバーライド `ThisDocument` し、ドキュメントから保護を削除します。

     ドキュメントが保存されると、は [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] このメソッドを呼び出してドキュメントの保護を解除できるようにします。 これにより、キャッシュされたデータへの変更を保存できます。

3. クラスの <xref:Microsoft.Office.Tools.Word.DocumentBase.ProtectDocument%2A> メソッドをオーバーライド `ThisDocument` し、文書に保護を適用し直します。

     ドキュメントが保存されると、は [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] このメソッドを呼び出して、文書に保護を再適用する機会を与えます。

### <a name="example"></a>例
 次のコード例は、パスワードで保護されている Word 文書にデータをキャッシュする方法を示しています。 メソッドで保護を削除する前に、メソッドで <xref:Microsoft.Office.Tools.Word.DocumentBase.UnprotectDocument%2A> <xref:Microsoft.Office.Tools.Word.Document.ProtectionType%2A> 同じ種類の保護を再適用できるように、現在の値が保存され <xref:Microsoft.Office.Tools.Word.DocumentBase.ProtectDocument%2A> ます。

 [!code-csharp[Trin_CachedDataProtectedDocument#1](../vsto/codesnippet/CSharp/Trin_CachedDataProtectedDocument/ThisDocument.cs#1)]
 [!code-vb[Trin_CachedDataProtectedDocument#1](../vsto/codesnippet/VisualBasic/Trin_CachedDataProtectedDocument/ThisDocument.vb#1)]

### <a name="compile-the-code"></a>コードのコンパイル
 プロジェクトのクラスに次のコードを追加 `ThisDocument` します。 このコードでは、パスワードがという名前のフィールドに格納されていることを前提としてい `securelyStoredPassword` ます。

## <a name="cache-in-excel-workbooks"></a>Excel ブック内のキャッシュ
 Excel プロジェクトでは、メソッドを使用してブック全体をパスワードで保護する場合にのみ、この手順が必要になり <xref:Microsoft.Office.Tools.Excel.Workbook.Protect%2A> ます。 メソッドを使用して特定のワークシートだけをパスワードで保護する場合、この手順は必要ありません <xref:Microsoft.Office.Tools.Excel.Worksheet.Protect%2A> 。

### <a name="to-cache-data-in-an-excel-workbook-that-is-protected-with-a-password"></a>パスワードで保護されている Excel ブックにデータをキャッシュするには

1. `ThisWorkbook`クラスまたは n クラスのいずれかで `Sheet` *n* 、パブリックフィールドまたはキャッシュされるプロパティをマークします。 詳細については、「 [データのキャッシュ](../vsto/caching-data.md)」を参照してください。

2. クラスの <xref:Microsoft.Office.Tools.Excel.WorkbookBase.UnprotectDocument%2A> メソッドをオーバーライド `ThisWorkbook` し、ブックから保護を削除します。

     ブックが保存されると、は [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] このメソッドを呼び出して、ブックの保護を解除する機会を与えます。 これにより、キャッシュされたデータへの変更を保存できます。

3. クラスの <xref:Microsoft.Office.Tools.Excel.WorkbookBase.ProtectDocument%2A> メソッドをオーバーライド `ThisWorkbook` し、文書に保護を適用し直します。

     ブックが保存されると、は [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] このメソッドを呼び出して、ブックに保護を再適用する機会を与えます。

### <a name="example"></a>例
 次のコード例は、パスワードで保護されている Excel ブックにデータをキャッシュする方法を示しています。 メソッドで保護を削除する前に、メソッドで <xref:Microsoft.Office.Tools.Excel.WorkbookBase.UnprotectDocument%2A> <xref:Microsoft.Office.Tools.Excel.Workbook.ProtectStructure%2A> 同じ種類の保護を再適用できるように、現在のとの値が保存 <xref:Microsoft.Office.Tools.Excel.Workbook.ProtectWindows%2A> され <xref:Microsoft.Office.Tools.Excel.WorkbookBase.ProtectDocument%2A> ます。

 [!code-vb[Trin_CachedDataProtectedWorkbook#1](../vsto/codesnippet/VisualBasic/Trin_CachedDataProtectedWorkbook/ThisWorkbook.vb#1)]
 [!code-csharp[Trin_CachedDataProtectedWorkbook#1](../vsto/codesnippet/CSharp/Trin_CachedDataProtectedWorkbook/ThisWorkbook.cs#1)]

### <a name="compile-the-code"></a>コードのコンパイル
 プロジェクトのクラスに次のコードを追加 `ThisWorkbook` します。 このコードでは、パスワードがという名前のフィールドに格納されていることを前提としてい `securelyStoredPassword` ます。

## <a name="see-also"></a>関連項目
- [キャッシュ データ](../vsto/caching-data.md)
- [方法: オフラインまたはサーバーで使用するデータをキャッシュする](../vsto/how-to-cache-data-for-use-offline-or-on-a-server.md)
- [方法: Office ドキュメント内のデータソースをプログラムによってキャッシュする](../vsto/how-to-programmatically-cache-a-data-source-in-an-office-document.md)
