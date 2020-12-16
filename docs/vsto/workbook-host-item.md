---
title: ブックホスト項目
description: Workbook ホスト項目は、Microsoft Excel のプライマリ相互運用機能アセンブリからブックの種類を拡張する型であることについて説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Excel workbooks
- Workbook host items
- host items [Office development in Visual Studio], Workbook
- workbooks, Excel
- Workbook host items, events
- workbooks
- Excel [Office development in Visual Studio], workbooks
- workbooks, events
- events [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 8d3d5b7efadefd77be7ce25026c8f485ee0ef133
ms.sourcegitcommit: 4bd2b770e60965fc0843fc25318a7e1b46137875
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/15/2020
ms.locfileid: "97528350"
---
# <a name="workbook-host-item"></a>ブックホスト項目
  <xref:Microsoft.Office.Tools.Excel.Workbook> ホスト項目は、Excel のプライマリ相互運用機能アセンブリの <xref:Microsoft.Office.Interop.Excel.Workbook> 型を拡張する型です。 <xref:Microsoft.Office.Tools.Excel.Workbook> ホスト項目は <xref:Microsoft.Office.Interop.Excel.Workbook> オブジェクトと同じプロパティ、メソッド、イベントがすべて用意されているだけなく、追加の機能も用意されています。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 ドキュメント レベルのプロジェクトには、プロジェクト内のブックを表す既定の <xref:Microsoft.Office.Tools.Excel.Workbook> ホスト項目があります。 VSTO アドイン プロジェクトでは、実行時に <xref:Microsoft.Office.Tools.Excel.Workbook> ホスト項目を生成できます。

## <a name="understand-the-workbook-host-item-in-document-level-projects"></a>ドキュメントレベルのプロジェクトのブックホスト項目について
 プロジェクトのブックにアクセスするには、 `ThisWorkbook` クラスを使用します。 `ThisWorkbook` クラスによって、 <xref:Microsoft.Office.Tools.Excel.Workbook> ホスト項目のメンバーにアクセスし、ブックが開かれたり閉じられたりしたときにコードを実行するなど、カスタマイズの基本的なタスクを実行できます。 詳細については、「 [プログラムによるドキュメントレベルのカスタマイズ](../vsto/programming-document-level-customizations.md)」を参照してください。

 `ThisWorkbook` クラスには、プロジェクトでコードの記述を開始できる場所が用意されています。 このクラスには、Excel のプライマリ相互運用機能アセンブリの <xref:Microsoft.Office.Interop.Excel.Workbook> オブジェクトと同じプロパティ、メソッド、イベントがすべて用意されているため、 `ThisWorkbook` を使用して Excel のオブジェクト モデルにアクセスすることもできます。 詳細については、「 [Excel オブジェクトモデルの概要](../vsto/excel-object-model-overview.md)」を参照してください。

 **[ソリューション エクスプローラー]** で **ThisWorkbook** プロジェクト項目をダブルクリックすると、ブックのデザイナーが表示され、 **[プロパティ]** ウィンドウにブックのプロパティとイベントが表示されます。

### <a name="limitations-of-the-workbook-host-item-in-document-level-projects"></a>ドキュメントレベルのプロジェクトでのブックホスト項目の制限事項
 ドキュメント レベルのプロジェクトには、1 つの <xref:Microsoft.Office.Tools.Excel.Workbook> ホスト項目のみ (つまり `ThisWorkbook` クラス) を含めることができます。 デザイン時に新しい <xref:Microsoft.Office.Tools.Excel.Workbook> ホスト項目をプロジェクトに追加することはできません。また、実行時にドキュメント レベルのカスタマイズから新しい <xref:Microsoft.Office.Tools.Excel.Workbook> ホスト項目を作成することもできません。

 実行時に新しい Excel ブックを作成すると、そのワークシートは <xref:Microsoft.Office.Interop.Excel.Workbook>型になります。 これはホスト項目ではないため、ホスト コントロールや Windows フォーム コントロールを含めることはできません。 実行時にブックを作成する方法の詳細については、「 [方法: プログラムによって新しいブックを作成する](../vsto/how-to-programmatically-create-new-workbooks.md)」を参照してください。

 <xref:Microsoft.Office.Tools.Excel.Workbook> ホスト項目は、ホスト コントロールのコンテナーとしては機能しません。 そのため、表示されるコントロールをブックに追加することはできませんが、 <xref:System.Data.DataSet>などのコンポーネントを追加すると、すべてのワークシートでそのコンポーネントを共有できます。 ドキュメント レベルのプロジェクトでは、ブックで使用できるコンポーネントは、 **[ツールボックス]** の **[コンポーネント]** タブ、 **[データ]** タブ、 **[すべての Windows フォーム]** タブに表示されます。

> [!NOTE]
> Visual Studio の Office 開発ツールでは、共有ブックはサポートされません。

## <a name="understand-workbook-host-items-in-vsto-add-in-projects"></a>VSTO アドインプロジェクトでのブックホスト項目について
 VSTO アドイン プロジェクトでは、Excel で開いている任意のブックの <xref:Microsoft.Office.Tools.Excel.Workbook> ホスト項目を実行時に生成できます。 <xref:Microsoft.Office.Tools.Excel.Workbook> ホスト項目を生成するには、`GetVstoObject` メソッドを使用します。 詳細については、「 [VSTO アドインでの実行時の Word 文書と Excel ブックの拡張](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [Office 開発のサンプルとチュートリアル](../vsto/office-development-samples-and-walkthroughs.md)
- [実行時に VSTO アドインの Word 文書と Excel ブックを拡張する](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)
- [ホスト項目とホストコントロールの概要](../vsto/host-items-and-host-controls-overview.md)
- [ワークシートホスト項目](../vsto/worksheet-host-item.md)
- [拡張オブジェクトを使用して Excel を自動化する](../vsto/automating-excel-by-using-extended-objects.md)
- [ホスト項目とホストコントロールのプログラム上の制限事項](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
