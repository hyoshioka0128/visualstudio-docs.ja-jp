---
title: '方法: ワークシートのコメントをプログラムによって表示する'
description: ドキュメントレベルまたはアプリケーションレベルで Microsoft Excel ワークシートのコメントをプログラムによって表示および非表示にする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- worksheets, comments
- comments, worksheets
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 7de75a1846aa7261a723c87297511b7461c49f47
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99885509"
---
# <a name="how-to-programmatically-display-worksheet-comments"></a>方法: ワークシートのコメントをプログラムによって表示する
  Microsoft Office Excel ワークシート内のコメントは、プログラムを使用して表示、非表示にできます。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="to-display-all-comments-on-a-worksheet-in-a-document-level-customization"></a>ドキュメント レベルのカスタマイズでワークシート内のコメントをすべて表示するには

1. コメントを表示する場合は、 <xref:Microsoft.Office.Interop.Excel.Comment.Visible%2A> プロパティを **true** に設定します。それ以外の場合は **false** に設定します。 このコードは、 `ThisWorkbook` クラスではなく、シート クラスに配置する必要があります。

     [!code-csharp[Trin_VstcoreExcelAutomation#31](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#31)]
     [!code-vb[Trin_VstcoreExcelAutomation#31](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#31)]

## <a name="to-display-all-comments-on-a-worksheet-in-an-application-level-vsto-add-in"></a>VSTO アドインで、ワークシートのすべてのコメントを表示するには

1. コメントを表示する場合は、 <xref:Microsoft.Office.Interop.Excel.Comment.Visible%2A> プロパティを **true** に設定します。それ以外の場合は **false** に設定します。

     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#21](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#21)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#21](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#21)]

## <a name="see-also"></a>関連項目
- [ワークシートを操作する](../vsto/working-with-worksheets.md)
- [方法: ワークシートのコメントをプログラムによって追加および削除する](../vsto/how-to-programmatically-add-and-delete-worksheet-comments.md)
- [ホスト項目とホストコントロールの概要](../vsto/host-items-and-host-controls-overview.md)
