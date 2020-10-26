---
title: グラフコントロール
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VST.ProjectItem.ExcelChart
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Chart control [Office development in Visual Studio], events
- Chart control [Office development in Visual Studio]
- Chart control [Office development in Visual Studio], data binding
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 864422aac695fbf474e6ed6b8cf6d765247eabf9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "71255302"
---
# <a name="chart-control"></a>グラフコントロール
  <xref:Microsoft.Office.Tools.Excel.Chart> コントロールはイベントを公開するグラフ オブジェクトです。 ワークシートにグラフを追加すると、ユーザーが Microsoft Office Excel オブジェクト モデルを走査する必要なく、直接、プログラムできる <xref:Microsoft.Office.Tools.Excel.Chart> オブジェクトが Visual Studio により作成されます。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="create-the-control"></a>コントロールを作成する
 <xref:Microsoft.Office.Tools.Excel.Chart>ドキュメントレベルのプロジェクトでは、デザイン時または実行時にコントロールを Microsoft Office Excel ワークシートに追加できます。

 VSTO アドインでは実行時に <xref:Microsoft.Office.Tools.Excel.Chart> コントロールをワークシートに追加できます。 詳細については、「 [方法: ワークシートにグラフコントロールを追加](../vsto/how-to-add-chart-controls-to-worksheets.md)する」を参照してください。

> [!NOTE]
> 動的に作成されたグラフ オブジェクトは、ワークシートを閉じる際に、ホスト コントロールとしてワークシートに残りません。 詳細については、「 [実行時に Office ドキュメントにコントロールを追加する](../vsto/adding-controls-to-office-documents-at-run-time.md)」を参照してください。

## <a name="formatting"></a>書式設定
 <xref:Microsoft.Office.Interop.Excel.Chart> に適用できるすべての書式設定は、<xref:Microsoft.Office.Tools.Excel.Chart> コントロールにも適用できます。 これには、罫線、フォント、グラフの種類、グリッド線、凡例、およびデータ ラベルが含まれます。

## <a name="events"></a>イベント
 次のイベントは <xref:Microsoft.Office.Tools.Excel.Chart> コントロールに対して利用できます。

- <xref:Microsoft.Office.Tools.Excel.Chart.ActivateEvent>

- <xref:Microsoft.Office.Tools.Excel.Chart.BeforeDoubleClick>

- <xref:Microsoft.Office.Tools.Excel.Chart.BeforeRightClick>

- <xref:Microsoft.Office.Tools.Excel.Chart.BindingContextChanged>

- <xref:Microsoft.Office.Tools.Excel.Chart.Calculate>

- <xref:Microsoft.Office.Tools.Excel.Chart.Deactivate>

- <xref:System.ComponentModel.Component.Disposed>

- <xref:Microsoft.Office.Tools.Excel.Chart.DragOver>

- <xref:Microsoft.Office.Tools.Excel.Chart.DragPlot>

- <xref:Microsoft.Office.Tools.Excel.Chart.MouseDown>

- <xref:Microsoft.Office.Tools.Excel.Chart.MouseMove>

- <xref:Microsoft.Office.Tools.Excel.Chart.MouseUp>

- <xref:Microsoft.Office.Tools.Excel.Chart.Resize>

- <xref:Microsoft.Office.Tools.Excel.Chart.SelectEvent>

- <xref:Microsoft.Office.Tools.Excel.Chart.SeriesChange>

## <a name="see-also"></a>関連項目
- [Office 開発のサンプルとチュートリアル](../vsto/office-development-samples-and-walkthroughs.md)
- [実行時に VSTO アドインの Word 文書と Excel ブックを拡張する](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)
- [Office ドキュメントのコントロール](../vsto/controls-on-office-documents.md)
- [実行時に Office ドキュメントにコントロールを追加する](../vsto/adding-controls-to-office-documents-at-run-time.md)
- [拡張オブジェクトを使用して Excel を自動化する](../vsto/automating-excel-by-using-extended-objects.md)
- [方法: ワークシートにグラフコントロールを追加する](../vsto/how-to-add-chart-controls-to-worksheets.md)
- [Office ソリューションのコントロールにデータをバインドする](../vsto/binding-data-to-controls-in-office-solutions.md)
- [ホスト項目とホストコントロールのプログラム上の制限事項](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
