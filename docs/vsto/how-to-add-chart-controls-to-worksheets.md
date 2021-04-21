---
title: '方法: ワークシートにグラフコントロールを追加する'
description: ドキュメントレベルのカスタマイズでデザイン時および実行時にグラフコントロールを Microsoft Office Excel ワークシートに追加する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Chart control [Office development in Visual Studio], adding to worksheets
- controls [Office development in Visual Studio], adding to worksheets
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 88ebe38a881e148f10149189a2d27ac81bd0ddc2
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107827033"
---
# <a name="how-to-add-chart-controls-to-worksheets"></a>方法: ワークシートにグラフコントロールを追加する
  <xref:Microsoft.Office.Tools.Excel.Chart>ドキュメントレベルのカスタマイズでは、デザイン時および実行時にコントロールを Microsoft Office Excel ワークシートに追加できます。 VSTO アドインでは、実行時にコントロールを追加することもでき <xref:Microsoft.Office.Tools.Excel.Chart> ます。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 このトピックでは、次のタスクについて説明します。

- [デザイン時にグラフコントロールを追加する](#designtime)

- [実行時にドキュメントレベルのプロジェクトにグラフコントロールを追加する](#runtimedoclevel)

- [実行時に VSTO アドインプロジェクトにグラフコントロールを追加する](#runtimeaddin)

  コントロールの詳細について <xref:Microsoft.Office.Tools.Excel.Chart> は、「 [Chart コントロール](../vsto/chart-control.md)」を参照してください。

## <a name="add-chart-controls-at-design-time"></a><a name="designtime"></a> デザイン時にグラフコントロールを追加する
 アプリケーションの中からグラフを追加するのと同じ方法で、ワークシートに <xref:Microsoft.Office.Tools.Excel.Chart> コントロールを追加できます。

> [!NOTE]
> コントロールは、 <xref:Microsoft.Office.Tools.Excel.Chart> **ツールボックス** または [ **データソース** ] ウィンドウからは使用できません。

### <a name="to-add-a-chart-host-control-to-a-worksheet-in-excel"></a>Excel のワークシートに Chart ホスト コントロールを追加するには

1. [ **挿入** ] タブの [ **グラフ** ] グループで、[ **列**] をクリックし、グラフのカテゴリをクリックして、目的のグラフの種類をクリックします。

2. [ **グラフの挿入** ] ダイアログボックスで、[ **OK]** をクリックします。

3. [ **デザイン** ] タブの [ **データ** ] グループで、[ **データの選択**] をクリックします。

4. [**データソースの選択**] ダイアログボックスで、[**グラフ****データの範囲**] ボックスをクリックし、既定の選択をオフにします。

5. グラフシート **のデータ** で、グラフのデータを含むセルの範囲を選択します (セル **A5** ~ **D8**)。

6. [ **データソースの選択** ] ダイアログボックスで、[ **OK**] をクリックします。

## <a name="add-chart-controls-at-run-time-in-a-document-level-project"></a><a name="runtimedoclevel"></a> 実行時にドキュメントレベルのプロジェクトにグラフコントロールを追加する
 実行時に <xref:Microsoft.Office.Tools.Excel.Chart> コントロールを動的に追加できます。 動的に作成したグラフは、ドキュメントを閉じるとホスト コントロールとしてドキュメントに保持されません。 詳細については、「 [実行時に Office ドキュメントにコントロールを追加する](../vsto/adding-controls-to-office-documents-at-run-time.md)」を参照してください。

#### <a name="to-add-a-chart-control-to-a-worksheet-programmatically"></a>プログラムを使用してワークシートに Chart コントロールを追加するには

1. `Sheet1` の <xref:Microsoft.Office.Tools.Excel.Worksheet.Startup> イベント ハンドラーに以下のコードを挿入して、<xref:Microsoft.Office.Tools.Excel.Chart> コントロールを追加します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs" id="Snippet1":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet1.vb" id="Snippet1":::

## <a name="add-chart-controls-at-run-time-in-a-vsto-add-in-project"></a><a name="runtimeaddin"></a> 実行時に VSTO アドインプロジェクトにグラフコントロールを追加する
 プログラムを使用して <xref:Microsoft.Office.Tools.Excel.Chart> コントロールを VSTO アドイン プロジェクトの任意の開いているワークシートに追加できます。 詳細については、「 [VSTO アドインでの実行時の Word 文書と Excel ブックの拡張](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)」を参照してください。

 動的に作成されたグラフ コントロールは、ワークシートを閉じるとホスト コントロールとしてワークシートに保持されません。 詳細については、「 [実行時に Office ドキュメントにコントロールを追加する](../vsto/adding-controls-to-office-documents-at-run-time.md)」を参照してください。

#### <a name="to-add-a-chart-control-to-a-worksheet-programmatically"></a>プログラムを使用してワークシートに Chart コントロールを追加するには

1. 次のコードでは、開いているワークシートに基づいたワークシート ホスト項目を生成し、<xref:Microsoft.Office.Tools.Excel.Chart> コントロールを追加します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Excel_Dynamic_Controls/ThisAddIn.cs" id="Snippet9":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Excel_Dynamic_Controls/ThisAddIn.vb" id="Snippet9":::

## <a name="compile-the-code"></a>コードのコンパイル
 この例の要件は以下のとおりです。

- グラフ化するデータが、ワークシートの A5 ～ D8 の範囲に格納されていること。

## <a name="see-also"></a>関連項目
- [実行時に VSTO アドインの Word 文書と Excel ブックを拡張する](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)
- [Office ドキュメントのコントロール](../vsto/controls-on-office-documents.md)
- [グラフコントロール](../vsto/chart-control.md)
- [拡張オブジェクトを使用して Excel を自動化する](../vsto/automating-excel-by-using-extended-objects.md)
- [ホスト項目とホストコントロールの概要](../vsto/host-items-and-host-controls-overview.md)
- [Office ソリューションのコントロールにデータをバインドする](../vsto/binding-data-to-controls-in-office-solutions.md)
- [ホスト項目とホストコントロールのプログラム上の制限事項](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
