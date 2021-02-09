---
title: '方法: プログラムによって Word の表に行と列を追加する'
description: Rows オブジェクトの Add メソッドを使用して、テーブルに行を追加する方法について説明します。 Columns オブジェクトの Add メソッドを使用して、列を追加することもできます。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- rows [Office development in Visual Studio], adding to Word tables
- tables [Office development in Visual Studio], adding rows and columns
- columns [Office development in Visual Studio], adding to Word tables
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: a4077e78da512ef7b49546ae9b5271b5dfd8ff15
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99910160"
---
# <a name="how-to-programmatically-add-rows-and-columns-to-word-tables"></a>方法: プログラムによって Word の表に行と列を追加する
  Microsoft Office Word の表では、セルが行と列に編成されます。 表に行を追加するには、<xref:Microsoft.Office.Interop.Word.Rows> オブジェクトの <xref:Microsoft.Office.Interop.Word.Rows.Add%2A> メソッドを使用し、列を追加するには <xref:Microsoft.Office.Interop.Word.Columns> オブジェクトの <xref:Microsoft.Office.Interop.Word.Columns.Add%2A> メソッドを使用します。

 [!INCLUDE[appliesto_wdalldocapp](includes/appliesto-wdalldocapp-md.md)]

## <a name="document-level-customization-examples"></a>ドキュメントレベルのカスタマイズの例
 次のコード例はドキュメント レベルのカスタマイズで使用できます。 これらの例を使用するには、プロジェクトの `ThisDocument` クラスからコードを実行します。 これらの例は、カスタマイズに関連するドキュメントに、少なくとも 1 つの表が既にあることを前提としています。

> [!IMPORTANT]
> このコードは、次のいずれかのプロジェクト テンプレートを使用して作成したプロジェクトでのみ実行されます。
>
> - Word 2013 ドキュメント
> - Word 2013 テンプレート
> - Word 2010 ドキュメント
> - Word 2010 テンプレート
>
>   このタスクを他の種類のプロジェクトで実行する場合は、 **そのアセンブリへ** の参照を追加する必要があります。その後、そのアセンブリのクラスを使用して、行と列をテーブルに追加する必要があります。 詳細については、「 [方法: プライマリ相互運用機能アセンブリを使用して Office アプリケーションを対象にする](how-to-target-office-applications-through-primary-interop-assemblies.md) 」および「 [Word 2010 プライマリ相互運用機能アセンブリリファレンス](office-primary-interop-assemblies.md)」を参照してください。

### <a name="to-add-a-row-to-a-table"></a>表に行を追加するには

1. <xref:Microsoft.Office.Interop.Word.Rows.Add%2A> メソッドを使用して表に行を追加します。

     [!code-vb[Trin_VstcoreWordAutomation#95](codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#95)]
     [!code-csharp[Trin_VstcoreWordAutomation#95](codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#95)]

### <a name="to-add-a-column-to-a-table"></a>表に列を追加するには

1. <xref:Microsoft.Office.Interop.Word.Columns.Add%2A> メソッドを使用し、次に <xref:Microsoft.Office.Interop.Word.Columns.DistributeWidth%2A> メソッドを使用してすべての列を同じ幅にします。

     [!code-vb[Trin_VstcoreWordAutomation#96](codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#96)]
     [!code-csharp[Trin_VstcoreWordAutomation#96](codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#96)]

## <a name="vsto-add-in-examples"></a>VSTO アドインの例
 次のコード例は VSTO アドインで使用できます。 これらの例を使用するには、プロジェクトの `ThisAddIn` クラスからコードを実行します。 これらの例は、作業中のドキュメントに少なくとも 1 つの表が既にあることを想定しています。

> [!IMPORTANT]
> このコードは、Word VSTO アドイン テンプレートを使用して作成したプロジェクトでのみ実行されます。
>
> このタスクを他の種類のプロジェクトで実行する場合は、 **そのアセンブリへ** の参照を追加する必要があります。その後、そのアセンブリのクラスを使用して、行と列をテーブルに追加する必要があります。 詳細については、「 [方法: プライマリ相互運用機能アセンブリを使用して Office アプリケーションを対象にする](how-to-target-office-applications-through-primary-interop-assemblies.md) 」および「 [Word 2010 プライマリ相互運用機能アセンブリリファレンス](office-primary-interop-assemblies.md)」を参照してください。

### <a name="to-add-a-row-to-a-table"></a>表に行を追加するには

1. <xref:Microsoft.Office.Interop.Word.Rows.Add%2A> メソッドを使用して表に行を追加します。

     [!code-vb[Trin_VstcoreWordAutomationAddIn#95](codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#95)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#95](codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#95)]

### <a name="to-add-a-column-to-a-table"></a>表に列を追加するには

1. <xref:Microsoft.Office.Interop.Word.Columns.Add%2A> メソッドを使用し、次に <xref:Microsoft.Office.Interop.Word.Columns.DistributeWidth%2A> メソッドを使用してすべての列を同じ幅にします。

     [!code-vb[Trin_VstcoreWordAutomationAddIn#96](codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#96)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#96](codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#96)]

## <a name="see-also"></a>関連項目
- [方法: プログラムによって Word の表を作成する](how-to-programmatically-create-word-tables.md)
- [方法: プログラムによって Word の表のセルにテキストと書式設定を追加する](how-to-programmatically-add-text-and-formatting-to-cells-in-word-tables.md)
- [方法: プログラムによって document プロパティを Word の表に読み込む](how-to-programmatically-populate-word-tables-with-document-properties.md)
