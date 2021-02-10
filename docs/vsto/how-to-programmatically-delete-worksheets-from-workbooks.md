---
title: '方法: プログラムによってブックからワークシートを削除する'
description: たとえば、ワークシートホスト項目を使用して、Microsoft Excel ブック内の任意のワークシートをプログラムで削除する方法について説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- workbooks, deleting worksheets
- worksheets, deleting
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 2289309932dcd1d946fc775de60a0e07892be222
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99963896"
---
# <a name="how-to-programmatically-delete-worksheets-from-workbooks"></a>方法: プログラムによってブックからワークシートを削除する
  ブック内の任意のワークシートを削除できます。 ワークシートを削除するには、Worksheet ホスト項目を使用するか、ブックの Sheets コレクションを使用してワークシートにアクセスします。

 [!INCLUDE[appliesto_xlalldocapp](includes/appliesto-xlalldocapp-md.md)]

## <a name="use-the-worksheet-host-item"></a>ワークシートのホスト項目を使用する
 デザイン時にドキュメント レベルのカスタマイズでワークシートが追加された場合は、<xref:Microsoft.Office.Tools.Excel.Worksheet.Delete%2A> メソッドを使用して特定のワークシートを削除します。 以下のコードは、Worksheet ホスト項目を直接参照して、ブックからワークシートを削除します。

> [!IMPORTANT]
> このコードは、次のいずれかのプロジェクト テンプレートを使用して作成したプロジェクトでのみ実行されます。
>
> - Excel 2013 ブック
> - Excel 2013 テンプレート
> - Excel 2010 ブック
> - Excel 2010 テンプレート
>
>   このタスクを他の種類のプロジェクトで実行する場合は、そのアセンブリへの参照を追加する必要があり **ます。その** 後、そのアセンブリのクラスを使用してブックを開き、ワークシートを削除する必要があります。 詳細については、「 [方法: プライマリ相互運用機能アセンブリを使用して Office アプリケーションを対象にする](how-to-target-office-applications-through-primary-interop-assemblies.md) 」および「 [Excel 2010 プライマリ相互運用機能アセンブリのリファレンス](office-primary-interop-assemblies.md)」を参照してください。

### <a name="to-delete-a-worksheet-by-using-a-worksheet-host-item"></a>Worksheet ホスト項目を使用してワークシートを削除するには

1. <xref:Microsoft.Office.Tools.Excel.Worksheet.Delete%2A> の `Sheet1`メソッドを呼び出します。

     [!code-csharp[Trin_VstcoreExcelAutomation#17](codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#17)]
     [!code-vb[Trin_VstcoreExcelAutomation#17](codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#17)]

## <a name="use-the-sheets-collection-of-the-excel-workbook"></a>Excel ブックの Sheets コレクションを使用する
 次の場合は、Microsoft Office Excel の <xref:Microsoft.Office.Interop.Excel.Sheets> コレクションを使用してワークシートにアクセスします。

- VSTO アドインでワークシートを削除する場合。

- 削除するワークシートがドキュメント レベルのカスタマイズで実行時に作成された場合。

  次のコードで **は、シートコレクションの** インデックス番号を使用してシートを参照することにより、ブックからワークシートを削除します。 このコードは、新しいワークシートがプログラミングによって作成されたことを前提としています。

> [!IMPORTANT]
> このタスクを他の種類のプロジェクトで実行する場合は、そのアセンブリへの参照を追加する必要があり **ます。その** 後、そのアセンブリのクラスを使用してブックを開き、ワークシートを削除する必要があります。 詳細については、「 [方法: プライマリ相互運用機能アセンブリを使用して Office アプリケーションを対象にする](how-to-target-office-applications-through-primary-interop-assemblies.md) 」および「 [Excel 2010 プライマリ相互運用機能アセンブリのリファレンス](office-primary-interop-assemblies.md)」を参照してください。

### <a name="to-delete-a-worksheet-by-using-the-sheets-collection-of-the-excel-workbook"></a>Excel ブックの Sheets コレクションを使用してワークシートを削除するには

1. <xref:Microsoft.Office.Interop.Excel.Sheets> コレクションの <xref:Microsoft.Office.Interop.Excel._Worksheet.Delete%2A> メソッドを呼び出します。

     [!code-csharp[Trin_VstcoreExcelAutomation#18](codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#18)]
     [!code-vb[Trin_VstcoreExcelAutomation#18](codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#18)]

## <a name="see-also"></a>関連項目
- [ワークシートを操作する](working-with-worksheets.md)
- [方法: プログラムによってワークシートを非表示にする](how-to-programmatically-hide-worksheets.md)
- [方法: プログラムによってブック内のワークシートを移動する](how-to-programmatically-move-worksheets-within-workbooks.md)
- [方法: プログラムによってワークシートを選択する](how-to-programmatically-select-worksheets.md)
- [方法: プログラムによって新しいワークシートをブックに追加する](how-to-programmatically-add-new-worksheets-to-workbooks.md)
- [ワークシートホスト項目](worksheet-host-item.md)
- [Office プロジェクト内のオブジェクトへのグローバルアクセス](global-access-to-objects-in-office-projects.md)
- [ホスト項目とホストコントロールのプログラム上の制限事項](programmatic-limitations-of-host-items-and-host-controls.md)
