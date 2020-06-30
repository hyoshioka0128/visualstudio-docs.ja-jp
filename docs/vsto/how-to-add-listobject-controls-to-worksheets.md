---
title: '方法: ワークシートに ListObject コントロールを追加する'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ListObject control, adding to worksheets
- controls [Office development in Visual Studio], adding to worksheets
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 4c53d820170c359e568b0a7b0ab5711a632d9eba
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85538321"
---
# <a name="how-to-add-listobject-controls-to-worksheets"></a>方法: ワークシートに ListObject コントロールを追加する
  ドキュメント レベルのプロジェクトでは、デザイン時および実行時に、 <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールを Microsoft Office Excel ワークシートに追加できます。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 VSTO アドイン プロジェクトでも、実行時に <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールを追加できます。

 このトピックでは、次のタスクについて説明します。

- [デザイン時に ListObject コントロールを追加する](#designtime)

- [実行時にドキュメントレベルのプロジェクトに ListObject コントロールを追加する](#runtimedoclevel)

- [実行時に VSTO アドインプロジェクトに ListObject コントロールを追加する](#runtimeaddin)

  コントロールの詳細について <xref:Microsoft.Office.Tools.Excel.ListObject> は、「 [ListObject コントロール](../vsto/listobject-control.md)」を参照してください。

## <a name="add-listobject-controls-at-design-time"></a><a name="designtime"></a>デザイン時に ListObject コントロールを追加する
 <xref:Microsoft.Office.Tools.Excel.ListObject>デザイン時にドキュメントレベルのプロジェクトのワークシートにコントロールを追加するには、Excel 内、Visual Studio の**ツールボックス**、および [**データソース**] ウィンドウから、いくつかの方法があります。

 [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

### <a name="to-use-the-ribbon-in-excel"></a>Excel のリボンを使用するには

1. **[挿入]** タブの **[テーブル]** グループで、 **[テーブル]** をクリックします。

2. リストに含める 1 つ以上のセルを選択し、 **[OK]** をクリックします。

#### <a name="to-use-the-toolbox"></a>ツールボックスを使用するには

1. **ツールボックス** の **[Excel コントロール]** タブからワークシートまで <xref:Microsoft.Office.Tools.Excel.ListObject> をドラッグします。

     **[ListObject コントロールの追加]** ダイアログ ボックスが表示されます。

2. リストに含める 1 つ以上のセルを選択し、 **[OK]** をクリックします。

     名前を既定のままにしない場合は、 **[プロパティ]** ウィンドウで変更します。

#### <a name="to-use-the-data-sources-window"></a>[データ ソース] ウィンドウを使用するには

1. **[データ ソース]** ウィンドウを開いて、プロジェクトのデータ ソースを作成します。 詳細については、「[新しい接続の追加](../data-tools/add-new-connections.md)」を参照してください。

2. **[データ ソース]** ウィンドウからワークシートまでテーブルをドラッグします。

     データがバインドされた <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールがワークシートに追加されます。 詳細については、「[データバインディングと Windows フォーム](/dotnet/framework/winforms/data-binding-and-windows-forms)」を参照してください。

## <a name="add-listobject-controls-at-run-time-in-a-document-level-project"></a><a name="runtimedoclevel"></a>実行時にドキュメントレベルのプロジェクトに ListObject コントロールを追加する
 実行時に <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールを動的に追加できます。 この方法を使用すると、イベントに応答してホスト コントロールを作成できます。 動的に作成されたリスト オブジェクトは、ワークシートを閉じる際に、ホスト コントロールとしてワークシートに残りません。 詳細については、「[実行時に Office ドキュメントにコントロールを追加する](../vsto/adding-controls-to-office-documents-at-run-time.md)」を参照してください。

#### <a name="to-add-a-listobject-control-to-a-worksheet-programmatically"></a>プログラムを使用してワークシートに ListObject コントロールを追加するには

1. <xref:Microsoft.Office.Tools.Excel.Worksheet.Startup> の `Sheet1`イベント ハンドラーに以下のコードを挿入して、 <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールをセル **A1** ～ **A4**に追加します。

     [!code-csharp[Trin_VstcoreHostControlsExcel#2](../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs#2)]
     [!code-vb[Trin_VstcoreHostControlsExcel#2](../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet1.vb#2)]

## <a name="add-listobject-controls-at-run-time-in-a-vsto-add-in-project"></a><a name="runtimeaddin"></a>実行時に VSTO アドインプロジェクトに ListObject コントロールを追加する
 プログラムを使用して <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールを VSTO アドイン プロジェクトの任意の開いているワークシートに追加できます。 動的に作成されたリスト オブジェクトは、ワークシートを保存して閉じる際に、ホスト コントロールとしてワークシートに残りません。 詳細については、「 [VSTO アドインでの実行時の Word 文書と Excel ブックの拡張](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)」を参照してください。

#### <a name="to-add-a-listobject-control-to-a-worksheet-programmatically"></a>プログラムを使用してワークシートに ListObject コントロールを追加するには

1. 次のコードでは、開いているワークシートに基づいたワークシート ホスト項目を生成し、 <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールをセル **A1** ～ **A4**に追加します。

     [!code-csharp[Trin_Excel_Dynamic_Controls#8](../vsto/codesnippet/CSharp/Trin_Excel_Dynamic_Controls/ThisAddIn.cs#8)]
     [!code-vb[Trin_Excel_Dynamic_Controls#8](../vsto/codesnippet/VisualBasic/Trin_Excel_Dynamic_Controls/ThisAddIn.vb#8)]

## <a name="see-also"></a>関連項目
- [実行時に VSTO アドインの Word 文書と Excel ブックを拡張する](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)
- [Office ドキュメントのコントロール](../vsto/controls-on-office-documents.md)
- [ListObject コントロール](../vsto/listobject-control.md)
- [拡張オブジェクトを使用して Excel を自動化する](../vsto/automating-excel-by-using-extended-objects.md)
- [ホスト項目とホストコントロールの概要](../vsto/host-items-and-host-controls-overview.md)
- [方法: ListObject コントロールのサイズを変更する](../vsto/how-to-resize-listobject-controls.md)
- [Office ソリューションのコントロールにデータをバインドする](../vsto/binding-data-to-controls-in-office-solutions.md)
- [ホスト項目とホストコントロールのプログラム上の制限事項](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
