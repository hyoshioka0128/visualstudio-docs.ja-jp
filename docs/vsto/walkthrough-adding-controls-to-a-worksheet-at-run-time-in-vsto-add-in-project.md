---
title: 実行時に VSTO アドインプロジェクトのワークシートにコントロールを追加する
description: リボンを使用して、ユーザーがボタン、NamedRange、および ListObject をワークシートに追加できるようにする方法について説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- add-ins [Office development in Visual Studio], adding controls
- controls [Office development in Visual Studio], adding to worksheets at run time
- application-level add-ins [Office development in Visual Studio], adding controls
- worksheets, adding controls at run time
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: e9987e9427c0fe982cf3ddcb88ce8071caab04b0
ms.sourcegitcommit: 4bd2b770e60965fc0843fc25318a7e1b46137875
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/15/2020
ms.locfileid: "97522775"
---
# <a name="walkthrough-add-controls-to-a-worksheet-at-run-time-in-vsto-add-in-project"></a>チュートリアル: 実行時における VSTO アドインプロジェクトのワークシートへのコントロールの追加
  Excel VSTO アドインを使用して、任意の開いているワークシートにコントロールを追加できます。 このチュートリアルでは、リボンを使用してユーザーがワークシートに <xref:Microsoft.Office.Tools.Excel.Controls.Button>、<xref:Microsoft.Office.Tools.Excel.NamedRange>、および <xref:Microsoft.Office.Tools.Excel.ListObject> を追加できるようにする方法を説明します。 詳細については、「 [実行時に Office ドキュメントにコントロールを追加する](../vsto/adding-controls-to-office-documents-at-run-time.md)」を参照してください。

 **適用対象:** このトピックの情報は、Excel の VSTO アドインのプロジェクトに適用されます。 詳細については、「[Office アプリケーションおよびプロジェクトの種類別の使用可能な機能](../vsto/features-available-by-office-application-and-project-type.md)」を参照してください。

 このチュートリアルでは、次の作業について説明します。

- ワークシートにコントロールを追加するためのユーザー インターフェイス (UI) を提供する。

- ワークシートにコントロールを追加する。

- ワークシートからコントロールを削除する。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- Excel

## <a name="create-a-new-excel-vsto-add-in-project"></a>新しい Excel VSTO アドインプロジェクトを作成する
 まず、Excel VSTO アドイン プロジェクトを作成します。

### <a name="to-create-a-new-excel-vsto-add-in-project"></a>新しい Excel VSTO アドイン プロジェクトを作成するには

1. で [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 、 **Exceldynamiccontrols** という名前の Excel VSTO アドインプロジェクトを作成します。 詳細については、「 [How to: Create Office Projects in Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md)」を参照してください。

2. **Microsoft.Office.Tools.Excel.v4.0.Utilities.dll** アセンブリへの参照を追加します。 この参照は、このチュートリアルの後半で Windows フォーム コントロールをワークシートにプログラムを使用して追加するのに必要です。

## <a name="provide-a-ui-to-add-controls-to-a-worksheet"></a>ワークシートにコントロールを追加するための UI を提供する
 Excel のリボンにカスタム タブを追加します。 ユーザーはタブにあるチェック ボックスをオンにして、ワークシートにコントロールを追加できます。

#### <a name="to-provide-a-ui-to-add-controls-to-a-worksheet"></a>ワークシートにコントロールを追加するための UI を提供するには

1. **[プロジェクト]** メニューの **[新しい項目の追加]** をクリックします。

2. [ **新しい項目の追加** ] ダイアログボックスで、[ **リボン (ビジュアルデザイナー)**] を選択し、[ **追加**] をクリックします。

     リボンデザイナーで **Ribbon1.cs** または **ribbon1.vb** という名前のファイルが開き、既定のタブとグループが表示されます。

3. **ツールボックス** の **[Office リボン コントロール]** タブから、 CheckBox コントロールを **group1** にドラッグします。

4. **[CheckBox1]** をクリックしてオンにします。

5. **[プロパティ]** ウィンドウで、次のプロパティを変更します。

    |プロパティ|値|
    |--------------|-----------|
    |**名前**|**Button**|
    |**Label**|**Button**|

6. **group1** に 2 つ目のチェック ボックスを追加し、次のプロパティを変更します。

    |プロパティ|値|
    |--------------|-----------|
    |**名前**|**NamedRange**|
    |**Label**|**NamedRange**|

7. [ **Group1**] に3番目のチェックボックスを追加し、次のプロパティを変更します。

    |プロパティ|値|
    |--------------|-----------|
    |**名前**|**ListObject**|
    |**Label**|**ListObject**|

## <a name="add-controls-to-the-worksheet"></a>ワークシートにコントロールを追加する
 マネージド コントロールは、ホスト項目に対してのみ追加できます。これは、コンテナーとして機能します。 VSTO アドイン プロジェクトは任意の開いているブックを操作するため、VSTO アドインはワークシートをホスト項目に変換するか、または既存のホスト項目を取得してから、コントロールを追加します。 開いているワークシートに基づく <xref:Microsoft.Office.Tools.Excel.Worksheet> ホスト項目を生成するように、各コントロールのクリック イベント ハンドラーにコードを追加します。 次に、ワークシートの現在選択されている位置に <xref:Microsoft.Office.Tools.Excel.Controls.Button>、<xref:Microsoft.Office.Tools.Excel.NamedRange>、および <xref:Microsoft.Office.Tools.Excel.ListObject> を追加します。

### <a name="to-add-controls-to-a-worksheet"></a>ワークシートにコントロールを追加するには

1. リボンデザイナーで、[ **] ボタン** をダブルクリックします。

     <xref:Microsoft.Office.Tools.Ribbon.RibbonCheckBox.Click>コードエディターで、**ボタン** のチェックボックスのイベントハンドラーが開きます。

2. `Button_Click` イベント ハンドラーを次のコードで置き換えます。

     このコードでは、`GetVstoObject` メソッドを使用してブックの最初のワークシートを表すホスト項目を取得し、現在選択されているセルに <xref:Microsoft.Office.Tools.Excel.Controls.Button> コントロールを追加します。

     [!code-csharp[Trin_Excel_Dynamic_Controls#2](../vsto/codesnippet/CSharp/Trin_Excel_Dynamic_Controls/Ribbon1.cs#2)]
     [!code-vb[Trin_Excel_Dynamic_Controls#2](../vsto/codesnippet/VisualBasic/Trin_Excel_Dynamic_Controls/Ribbon1.vb#2)]

3. **ソリューションエクスプローラー** で、 *Ribbon1.cs* または *ribbon1.vb* を選択します。

4. [ **表示** ] メニューの [ **デザイナー**] をクリックします。

5. リボンデザイナーで、[ **NamedRange**] をダブルクリックします。

6. `NamedRange_Click` イベント ハンドラーを次のコードで置き換えます。

     このコードでは、`GetVstoObject` メソッドを使用してブックの最初のワークシートを表すホスト項目を取得し、現在選択されている (1 つまたは複数の) セルの <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールを定義します。

     [!code-csharp[Trin_Excel_Dynamic_Controls#3](../vsto/codesnippet/CSharp/Trin_Excel_Dynamic_Controls/Ribbon1.cs#3)]
     [!code-vb[Trin_Excel_Dynamic_Controls#3](../vsto/codesnippet/VisualBasic/Trin_Excel_Dynamic_Controls/Ribbon1.vb#3)]

7. リボンデザイナーで、[ **ListObject**] をダブルクリックします。

8. `ListObject_Click` イベント ハンドラーを次のコードで置き換えます。

     このコードでは、`GetVstoObject` メソッドを使用してブックの最初のワークシートを表すホスト項目を取得し、現在選択されている (1 つまたは複数の) セルの <xref:Microsoft.Office.Tools.Excel.ListObject> を定義します。

     [!code-csharp[Trin_Excel_Dynamic_Controls#4](../vsto/codesnippet/CSharp/Trin_Excel_Dynamic_Controls/Ribbon1.cs#4)]
     [!code-vb[Trin_Excel_Dynamic_Controls#4](../vsto/codesnippet/VisualBasic/Trin_Excel_Dynamic_Controls/Ribbon1.vb#4)]

9. リボン コード ファイルの先頭に次のステートメントを追加します。

     [!code-csharp[Trin_Excel_Dynamic_Controls#1](../vsto/codesnippet/CSharp/Trin_Excel_Dynamic_Controls/Ribbon1.cs#1)]
     [!code-vb[Trin_Excel_Dynamic_Controls#1](../vsto/codesnippet/VisualBasic/Trin_Excel_Dynamic_Controls/Ribbon1.vb#1)]

## <a name="remove-controls-from-the-worksheet"></a>ワークシートからコントロールを削除する
 ワークシートが保存されて閉じられるとき、コントロールは保持されません。 ワークシートを保存する前に、生成されたすべての Windows フォーム コントロールをプログラムを使用して削除する必要があります。そうしないと、ワークシートを再び開いたときに、コントロールのアウトラインのみが表示されます。 生成されたホスト項目のコントロール コレクションから Windows フォーム コントロールを削除するコードを <xref:Microsoft.Office.Interop.Excel.AppEvents_Event.WorkbookBeforeSave> イベントに追加します。 詳細については、「 [Office ドキュメントに動的コントロールを保存](../vsto/persisting-dynamic-controls-in-office-documents.md)する」を参照してください。

### <a name="to-remove-controls-from-the-worksheet"></a>ワークシートからコントロールを削除するには

1. **ソリューションエクスプローラー** で、 *ThisAddIn.cs* または *ThisAddIn* を選択します。

2. **[表示]** メニューの **[コード]** をクリックします。

3. 次のメソッドを `ThisAddIn` クラスに追加します。 このコードはブックの最初のワークシートを取得し、`HasVstoObject` メソッドを使用して、ワークシートにワークシート オブジェクトが生成されているかどうかを確認します。 生成されたワークシート オブジェクトにコントロールがある場合、コードはそのワークシート オブジェクトを取得し、コントロール コレクションを反復処理してコントロールを削除します。

     [!code-csharp[Trin_Excel_Dynamic_Controls#6](../vsto/codesnippet/CSharp/Trin_Excel_Dynamic_Controls/ThisAddIn.cs#6)]
     [!code-vb[Trin_Excel_Dynamic_Controls#6](../vsto/codesnippet/VisualBasic/Trin_Excel_Dynamic_Controls/ThisAddIn.vb#6)]

4. C# では、<xref:Microsoft.Office.Interop.Excel.AppEvents_Event.WorkbookBeforeSave> イベントのイベント ハンドラーを作成する必要があります。 このコードを `ThisAddIn_Startup` メソッドに配置できます。 イベントハンドラーの作成の詳細については、「 [方法: Office プロジェクトでイベントハンドラーを作成](../vsto/how-to-create-event-handlers-in-office-projects.md)する」を参照してください。 `ThisAddIn_Startup` メソッドを次のコードに置き換えます。

     [!code-csharp[Trin_Excel_Dynamic_Controls#5](../vsto/codesnippet/CSharp/Trin_Excel_Dynamic_Controls/ThisAddIn.cs#5)]

## <a name="test-the-solution"></a>ソリューションをテストする
 リボンのカスタムタブからコントロールを選択して、ワークシートにコントロールを追加します。 ワークシートを保存すると、これらのコントロールは削除されます。

### <a name="to-test-the-solution"></a>ソリューションをテストするには

1. **F5** キーを押して、プロジェクトを実行します。

2. Sheet1 で任意のセルを選択します。

3. **[アドイン]** タブをクリックします。

4. [ **Group1** ] グループで、[ **] ボタン** をクリックします。

     選択したセルにボタンが表示されます。

5. Sheet1 で別のセルを選択します。

6. [ **Group1** ] グループで、[ **NamedRange**] をクリックします。

     選択したセルに名前付き範囲が定義されます。

7. Sheet1 で一連のセルを選択します。

8. [ **Group1** ] グループで、[ **ListObject**] をクリックします。

     選択したセルにリスト オブジェクトが追加されます。

9. ワークシートを保存します。

     Sheet1 に追加したコントロールは表示されなくなります。

## <a name="next-steps"></a>次のステップ
 Excel VSTO アドイン プロジェクトのコントロールの詳細については、以下のトピックをご覧ください。

- コントロールをワークシートに保存する方法の詳細については、「 [Office 開発のサンプルとチュートリアル](../vsto/office-development-samples-and-walkthroughs.md)」の「Excel VSTO アドイン動的コントロールのサンプル」を参照してください。

## <a name="see-also"></a>関連項目
- [Excel ソリューション](../vsto/excel-solutions.md)
- [Office ドキュメントでの Windows フォームコントロールの概要](../vsto/windows-forms-controls-on-office-documents-overview.md)
- [Office ドキュメントのコントロール](../vsto/controls-on-office-documents.md)
- [NamedRange コントロール](../vsto/namedrange-control.md)
- [ListObject コントロール](../vsto/listobject-control.md)
