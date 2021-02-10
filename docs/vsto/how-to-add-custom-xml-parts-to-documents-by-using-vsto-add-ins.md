---
title: VSTO アドインを使用してドキュメントにカスタム XML 部分を追加する
description: VSTO アドインでカスタム XML 部分を作成することにより、次の種類のドキュメントに XML データを格納する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- add-ins [Office development in Visual Studio], custom XML parts
- Office documents [Office development in Visual Studio, custom XML parts
- Word [Office development in Visual Studio], custom XML parts
- PowerPoint [Office development in Visual Studio], custom XML parts
- Excel [Office development in Visual Studio], custom XML parts
- custom XML parts [Office development in Visual Studio], adding
- documents [Office development in Visual Studio], custom XML parts
- application-level add-ins [Office development in Visual Studio], custom XML parts
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: fbba5c629807815a306221368d00b7d759dcc294
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99954229"
---
# <a name="how-to-add-custom-xml-parts-to-documents-by-using-vsto-add-ins"></a>方法: VSTO アドインを使用してドキュメントにカスタム XML 部分を追加する
  VSTO アドインでカスタム XML 部分を作成することにより、次のタイプのドキュメントに XML データを格納できます。

- Microsoft Office Excel ブック。

- Microsoft Office Word ドキュメント。

- Microsoft Office PowerPoint プレゼンテーション。

  詳細については、「 [カスタム XML 部分の概要](../vsto/custom-xml-parts-overview.md)」を参照してください。

  **対象:** このトピックの情報は、Excel、PowerPoint、および Word のアプリケーション レベルのプロジェクトに適用されます。 詳細については、「 [Office アプリケーションおよびプロジェクトの種類別の使用可能な機能](../vsto/features-available-by-office-application-and-project-type.md)」を参照してください。

## <a name="to-add-a-custom-xml-part-to-an-excel-workbook"></a>カスタム XML 部分を Excel ブックに追加するには

1. ブックの <xref:Microsoft.Office.Core.CustomXMLPart> コレクションに、新しい <xref:Microsoft.Office.Interop.Excel._Workbook.CustomXMLParts%2A> オブジェクトを追加します。 <xref:Microsoft.Office.Core.CustomXMLPart> にはブックに格納する XML 文字列が含まれています。

     次のコード例は、指定したブックにカスタム XML 部分を追加します。

     [!code-vb[Trin_AddCustomXmlPartExcelAppLevel#1](../vsto/codesnippet/VisualBasic/trin_addcustomxmlpartexcelapplevel/ThisAddIn.vb#1)]
     [!code-csharp[Trin_AddCustomXmlPartExcelAppLevel#1](../vsto/codesnippet/CSharp/Trin_AddCustomXmlPartExcelAppLevel/ThisAddIn.cs#1)]

2. `AddCustomXmlPartToWorkbook` `ThisAddIn` Excel 用の VSTO アドインプロジェクトのクラスにメソッドを追加します。

3. プロジェクトの他のコードからメソッドを呼び出します。 たとえば、ユーザーがブックを開いたときにカスタム XML 部分を作成するには、 <xref:Microsoft.Office.Interop.Excel.AppEvents_Event.WorkbookOpen> イベントのイベント ハンドラーからメソッドを呼び出します。

## <a name="to-add-a-custom-xml-part-to-a-word-document"></a>カスタム XML 部分を Word ドキュメントに追加するには

1. ドキュメントの <xref:Microsoft.Office.Core.CustomXMLPart> コレクションに、新しい <xref:Microsoft.Office.Interop.Word._Document.CustomXMLParts%2A> オブジェクトを追加します。 <xref:Microsoft.Office.Core.CustomXMLPart> にはドキュメントに格納する XML 文字列が含まれています。

     次のコード例は、指定したドキュメントにカスタム XML 部分を追加します。

     [!code-vb[Trin_AddCustomXmlPartWordAppLevel#1](../vsto/codesnippet/VisualBasic/Trin_AddCustomXmlPartWordAppLevel/ThisAddIn.vb#1)]
     [!code-csharp[Trin_AddCustomXmlPartWordAppLevel#1](../vsto/codesnippet/CSharp/Trin_AddCustomXmlPartWordAppLevel/ThisAddIn.cs#1)]

2. `AddCustomXmlPartToDocument` `ThisAddIn` WORD の VSTO アドインプロジェクトのクラスにメソッドを追加します。

3. プロジェクトの他のコードからメソッドを呼び出します。 たとえば、ユーザーがドキュメントを開いたときにカスタム XML 部分を作成するには、 <xref:Microsoft.Office.Interop.Word.ApplicationEvents4_Event.DocumentOpen> イベントのイベント ハンドラーからメソッドを呼び出します。

## <a name="to-add-a-custom-xml-part-to-a-powerpoint-presentation"></a>PowerPoint プレゼンテーションにカスタム XML 部分を追加するには

1. 新しいオブジェクトを <xref:Microsoft.Office.Core.CustomXMLPart> プレゼンテーションの [Microsoft.Office.Interop.PowerPoint._Presentation CustomXMLParts](/previous-versions/office/developer/office-2010/ff760806%28v%3doffice.14%29) コレクションに追加します。 <xref:Microsoft.Office.Core.CustomXMLPart> にはプレゼンテーションに格納する XML 文字列が含まれています。

     次のコード例は、指定したプレゼンテーションにカスタム XML 部分を追加します。

     [!code-csharp[Trin_AddCustomXmlPartPowerPointAppLevel#1](../vsto/codesnippet/CSharp/Trin_AddCustomXmlPartPowerPointAppLevel/ThisAddIn.cs#1)]
     [!code-vb[Trin_AddCustomXmlPartPowerPointAppLevel#1](../vsto/codesnippet/VisualBasic/Trin_AddCustomXmlPartPowerPointAppLevel/ThisAddIn.vb#1)]

2. `AddCustomXmlPartToPresentation` `ThisAddIn` POWERPOINT の VSTO アドインプロジェクトのクラスにメソッドを追加します。

3. プロジェクトの他のコードからメソッドを呼び出します。 たとえば、ユーザーがプレゼンテーションを開いたときにカスタム XML 部分を作成するには、 [Microsoft.Office.Interop.PowerPoint.EApplication_Event afterpresentation open](/previous-versions/office/developer/office-2010/ff762843(v=office.14)) イベントのイベントハンドラーからメソッドを呼び出します。

## <a name="robust-programming"></a>信頼性の高いプログラミング
 わかりやすくするために、この例では、メソッドでローカル変数として定義されている XML 文字列を使用しています。 通常は、ファイルやデータベースなどの外部ソースから XML を取得する必要があります。

## <a name="see-also"></a>関連項目
- [カスタム XML 部分の概要](../vsto/custom-xml-parts-overview.md)
- [方法: ドキュメントレベルのカスタマイズにカスタム XML 部分を追加する](../vsto/how-to-add-custom-xml-parts-to-document-level-customizations.md)
