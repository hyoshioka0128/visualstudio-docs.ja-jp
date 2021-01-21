---
title: '方法: カスタムドキュメントプロパティを作成および変更する'
description: ドキュメントに格納する追加情報がある場合に、カスタムドキュメントプロパティを作成および変更する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom document properties
- documents [Office development in Visual Studio], properties
- document properties [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 4897008f102600bd222a21761237acc4bcb62a30
ms.sourcegitcommit: ce85cff795df29e2bd773b4346cd718dccda5337
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/08/2020
ms.locfileid: "96844297"
---
# <a name="how-to-create-and-modify-custom-document-properties"></a>方法: カスタムドキュメントプロパティを作成および変更する
  上記の Microsoft Office アプリケーションは、ドキュメントで保存される組み込みのプロパティを提供します。 さらに、ドキュメントで保存する追加情報がある場合は、カスタム ドキュメント プロパティを作成し、変更することができます。

 [!INCLUDE[appliesto_docprops](../vsto/includes/appliesto-docprops-md.md)]

 カスタムプロパティを操作するには、ドキュメントの CustomDocumentProperties プロパティを使用します。 たとえば、Microsoft Office Excel のドキュメント レベルのプロジェクトでは、 <xref:Microsoft.Office.Tools.Excel.Workbook.CustomDocumentProperties%2A> クラスの `ThisWorkbook` プロパティを使用します。 Excel の VSTO アドイン プロジェクトでは、 <xref:Microsoft.Office.Interop.Excel._Workbook.CustomDocumentProperties%2A> オブジェクトの <xref:Microsoft.Office.Interop.Excel.Workbook> プロパティを使用します。 これらのプロパティは、 <xref:Microsoft.Office.Core.DocumentProperties> オブジェクトのコレクションである <xref:Microsoft.Office.Core.DocumentProperty> オブジェクトを返します。 このコレクションの `Item` プロパティを使用すると、名前またはコレクション内のインデックスに基づいて特定のプロパティを取得できます。

 次の例は、Excel のドキュメント レベルのカスタマイズでカスタム プロパティを追加し、値を割り当てる方法を示します。

## <a name="example"></a>例
 [!code-vb[Trin_VstcoreProgramming#6](../vsto/codesnippet/VisualBasic/Trin_VstcoreProgrammingExcelVB/ThisWorkbook.vb#6)]
 [!code-csharp[Trin_VstcoreProgramming#6](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingExcelCS/ThisWorkbook.cs#6)]

## <a name="robust-programming"></a>信頼性の高いプログラミング
 未定義の `Value` プロパティにアクセスしようとすると、例外が発生します。

## <a name="see-also"></a>関連項目
- [プログラム VSTO アドイン](../vsto/programming-vsto-add-ins.md)
- [プログラムドキュメントレベルのカスタマイズ](../vsto/programming-document-level-customizations.md)
- [方法: ドキュメントプロパティの読み取りと書き込みを行う](../vsto/how-to-read-from-and-write-to-document-properties.md)
