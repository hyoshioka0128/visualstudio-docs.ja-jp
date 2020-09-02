---
title: オプションボタンを使用してワークシートのグラフを更新する
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- worksheets, updating using managed controls
- controls [Office development in Visual Studio], updating worksheets
- worksheets, using radio buttons
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: e63d7d09a09fe4c051d8137428fdae90490cbae5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "88238817"
---
# <a name="walkthrough-updating-a-chart-in-a-worksheet-using-radio-buttons"></a>チュートリアル : オプション ボタンを使用してワークシートのグラフを更新する方法
  このチュートリアルでは、Microsoft Office の Excel ワークシートでオプションボタンを使用して、オプションをすばやく切り替える方法をユーザーに提供する方法の基本について説明します。 この場合、オプションによってグラフのスタイルが変更されます。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

 完成したサンプルとして結果を表示するには、「 [Office 開発のサンプルとチュートリアル](../vsto/office-development-samples-and-walkthroughs.md)」の Excel コントロールのサンプルを参照してください。

 このチュートリアルでは、次の作業について説明します。

- ワークシートにラジオボタンのグループを追加する。

- オプション選択時のグラフ スタイルの変更

> [!NOTE]
> 次の手順で参照している Visual Studio ユーザー インターフェイス要素の一部は、お使いのコンピューターでは名前や場所が異なる場合があります。 これらの要素は、使用している Visual Studio のエディションや独自の設定によって決まります。 詳細については、「[Visual Studio IDE のカスタマイズ](../ide/personalizing-the-visual-studio-ide.md)」を参照してください。

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)] または [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)]。

## <a name="add-a-chart-to-a-worksheet"></a>ワークシートへのグラフの追加
 既存のブックをカスタマイズする Excel ブックプロジェクトを作成できます。 このチュートリアルでは、ブックにグラフを追加し、新しい Excel ソリューションでこのブックを使用します。 このチュートリアルのデータソースは、 **グラフのデータ**という名前のワークシートです。

### <a name="to-add-the-data"></a>データを追加するには

1. Microsoft Excel を開きます。

2. [ **Sheet3** ] タブを右クリックし、ショートカットメニューの [ **名前の変更** ] をクリックします。

3. シートの名前を **グラフのデータ**に変更します。

4. 左上隅にセル A4 がある **グラフのデータ** に次のデータを追加し、右下隅を E8 します。

   |リージョン/四半期|Q1|Q2|Q3|Q4|
   |-|--------|--------|--------|--------|
   |West|500|550|550|600|
   |East|600|625|675|700|
   |North|450|470|490|510|
   |South|800|750|775|790|

   次に、最初のワークシートにグラフを追加して、データを表示します。

### <a name="to-add-a-chart-in-excel"></a>Excel でグラフを追加するには

1. [ **挿入** ] タブの [ **グラフ** ] グループで、[ **列**] をクリックし、[すべての **グラフの種類**] をクリックします。

2. [ **グラフの挿入** ] ダイアログボックスで、[ **OK]** をクリックします。

3. [ **デザイン** ] タブの [ **データ** ] グループで、[ **データの選択**] をクリックします。

4. [ **データソースの選択** ] ダイアログボックスで、[ **chartdata range** ] ボックスをクリックし、既定の選択をすべてオフにします。

5. グラフシート **のデータ** で、数値が格納されているセルのブロックを選択します。これには、左下隅にある A4 が右下隅に表示されます。

6. [ **データソースの選択** ] ダイアログボックスで、[ **OK**] をクリックします。

7. 右上隅がセル **E2**と揃うように、グラフの位置を変更します。

8. ファイルを C ドライブに保存し、 **ExcelChart.xlsx**という名前を付けます。

9. Excel を終了します。

## <a name="create-a-new-project"></a>新しいプロジェクトを作成する
 この手順では、 **Excelchart** ブックに基づいて Excel ブックプロジェクトを作成します。

### <a name="to-create-a-new-project"></a>新しいプロジェクトを作成するには

1. " **My Excel Chart**" という名前の excel ブックプロジェクトを作成します。 ウィザードで、[ **既存のドキュメントをコピーする**] を選択します。

     詳細については、「 [方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)」を参照してください。

2. [ **参照** ] ボタンをクリックし、このチュートリアルの前の手順で作成したブックを参照します。

3. **[OK]** をクリックします。

     新しい Excel ブックがデザイナーで開き、 **[My Excel Chart** ] プロジェクトが **ソリューションエクスプローラー**に追加されます。

## <a name="set-properties-of-the-chart"></a>グラフのプロパティを設定する
 既存のブックを使用する新しい Excel ブックプロジェクトを作成すると、ブック内のすべての名前付き範囲、リストオブジェクト、およびグラフに対してホストコントロールが自動的に作成されます。 コントロールの名前を変更する <xref:Microsoft.Office.Tools.Excel.Chart> には、[ **プロパティ** ] ウィンドウを使用します。

### <a name="to-change-the-name-of-the-chart-control"></a>グラフコントロールの名前を変更するには

1. <xref:Microsoft.Office.Tools.Excel.Chart>デザイナーでコントロールを選択し、[**プロパティ**] ウィンドウで次のプロパティを変更します。

    |プロパティ|値|
    |--------------|-----------|
    |**名前**|**dataChart**|
    |**HasLegend**|**false**|

## <a name="add-controls"></a>コントロールの追加
 このワークシートは、オプションボタンを使用して、グラフのスタイルをすばやく変更する方法をユーザーに提供します。 ただし、ラジオボタンは排他的にする必要があります。1つのボタンが選択されている場合、グループ内の他のボタンを同時に選択することはできません。 ワークシートに複数のオプションボタンを追加した場合、この動作は既定では発生しません。

 この動作を追加する方法の1つは、ユーザーコントロールのオプションボタンをグループ化し、ユーザーコントロールの背後にコードを記述してから、ユーザーコントロールをワークシートに追加することです。

### <a name="to-add-a-user-control"></a>ユーザー コントロールを追加するには

1. **ソリューションエクスプローラー**で **[My Excel Chart** ] プロジェクトを選択します。

2. **[プロジェクト]** メニューの **[新しい項目の追加]** をクリックします。

3. [ **新しい項目の追加** ] ダイアログボックスで、[ **ユーザーコントロール**] をクリックし、コントロールに **ChartOptions** という名前を指定して、[ **追加**] をクリックします。

### <a name="to-add-radio-buttons-to-the-user-control"></a>ユーザーコントロールにオプションボタンを追加するには

1. ユーザーコントロールがデザイナーに表示されていない場合は、**ソリューションエクスプローラー**で [ **ChartOptions** ] をダブルクリックします。

2. **ツールボックス**の [**コモンコントロール**] タブから、**ラジオボタン**コントロールをユーザーコントロールにドラッグし、次のプロパティを変更します。

   | プロパティ | 値 |
   |----------|------------------|
   | **名前** | **columnChart** |
   | **Text** | **縦棒グラフ** |

3. 2番目のオプションボタンをユーザーコントロールに追加し、次のプロパティを変更します。

   | プロパティ | 値 |
   |----------|---------------|
   | **名前** | **barChart** |
   | **Text** | **横棒グラフ** |

4. 3番目のオプションボタンをユーザーコントロールに追加し、次のプロパティを変更します。

   | プロパティ | 値 |
   |----------|----------------|
   | **名前** | **lineChart** |
   | **Text** | **折れ線グラフ** |

5. 4番目のオプションボタンをユーザーコントロールに追加し、次のプロパティを変更します。

   |プロパティ|値|
   |--------------|-----------|
   |**名前**|**areaBlockChart**|
   |**Text**|**Area Block Chart**|

   次に、オプションボタンがクリックされたときにグラフを更新するコードを記述します。

## <a name="change-the-chart-style-when-a-radio-button-is-selected"></a>オプションボタンが選択されているときにグラフのスタイルを変更する
 これで、コードを追加してグラフのスタイルを変更できます。 これを行うには、ユーザーコントロールでパブリックイベントを作成し、プロパティを追加して選択の種類を設定し、 `CheckedChanged` 各オプションボタンのイベントのイベントハンドラーを作成します。

### <a name="to-create-an-event-and-property-on-a-user-control"></a>ユーザー コントロールにイベントおよびプロパティを作成するには

1. **ソリューションエクスプローラー**で、ユーザーコントロールを右クリックし、[コードの**表示**] をクリックします。

2. `ChartOptions`イベントとプロパティを作成するコードをクラスに追加し `SelectionChanged` `Selection` ます。

     [!code-vb[Trin_VstcoreProgrammingControlsExcel#13](../vsto/codesnippet/VisualBasic/my excel chart/ChartOptions.vb#13)]
     [!code-cs[Trin_VstcoreProgrammingControlsExcel#13](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/ChartOptions.cs#13)]

### <a name="to-handle-the-checkedchanged-event-of-the-radio-buttons"></a>オプションボタンの CheckedChanged イベントを処理するには

1. `CheckedChanged` オプション ボタンの `areaBlockChart` イベント ハンドラーでグラフの種類を設定し、イベントを発生させます。

     [!code-vb[Trin_VstcoreProgrammingControlsExcel#14](../vsto/codesnippet/VisualBasic/my excel chart/ChartOptions.vb#14)]
     [!code-cs[Trin_VstcoreProgrammingControlsExcel#14](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/ChartOptions.cs#14)]

2. `CheckedChanged` オプション ボタンの `barChart` イベント ハンドラーでグラフの種類を設定します。

     [!code-vb[Trin_VstcoreProgrammingControlsExcel#15](../vsto/codesnippet/VisualBasic/my excel chart/ChartOptions.vb#15)]
     [!code-cs[Trin_VstcoreProgrammingControlsExcel#15](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/ChartOptions.cs#15)]

3. `CheckedChanged` オプション ボタンの `columnChart` イベント ハンドラーでグラフの種類を設定します。

     [!code-vb[Trin_VstcoreProgrammingControlsExcel#16](../vsto/codesnippet/VisualBasic/my excel chart/ChartOptions.vb#16)]
     [!code-cs[Trin_VstcoreProgrammingControlsExcel#16](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/ChartOptions.cs#16)]

4. `CheckedChanged` オプション ボタンの `lineChart` イベント ハンドラーでグラフの種類を設定します。

     [!code-vb[Trin_VstcoreProgrammingControlsExcel#17](../vsto/codesnippet/VisualBasic/my excel chart/ChartOptions.vb#17)]
     [!code-cs[Trin_VstcoreProgrammingControlsExcel#17](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/ChartOptions.cs#17)]

5. C# では、オプション ボタンに対してイベント ハンドラーを追加する必要があります。 このコードを、`ChartOptions` への呼び出しの後で `InitializeComponent` コンストラクターに追加できます。 イベントハンドラーの作成方法の詳細については、「 [方法: Office プロジェクトでイベントハンドラーを作成](../vsto/how-to-create-event-handlers-in-office-projects.md)する」を参照してください。

     [!code-cs[Trin_VstcoreProgrammingControlsExcel#18](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/ChartOptions.cs#18)]

## <a name="add-the-user-control-to-the-worksheet"></a>ワークシートにユーザーコントロールを追加する
 ソリューションをビルドすると、新しいユーザーコントロールが [ **ツールボックス**] に自動的に追加されます。 **ツールボックス**からワークシートにコントロールをドラッグできます。

### <a name="to-add-the-user-control-your-worksheet"></a>ワークシートにユーザーコントロールを追加するには

1. **[ビルド]** メニューの **[ソリューションのビルド]** をクリックします。

     **ChartOptions**ユーザーコントロールが**ツールボックス**に追加されます。

2. **ソリューションエクスプローラー**で、 **Sheet1**または**Sheet1.cs**を右クリックし、[デザイナーの**表示**] をクリックします。

3. [**ツールボックス**] から [ **ChartOptions** ] コントロールをワークシートにドラッグします。

     という名前の新しいコントロール `my_Excel_Chart_ChartOptions1` がプロジェクトに追加されます。

4. コントロールの名前を **ChartOptions1**に変更します。

## <a name="change-the-chart-type"></a>グラフの種類を変更する
 グラフの種類を変更するには、ユーザーコントロールで選択したオプションに従ってスタイルを設定するイベントハンドラーを作成します。

### <a name="to-change-the-type-of-chart-that-is-displayed-in-the-worksheet"></a>ワークシートに表示されるグラフの種類を変更するには

1. 次のイベント ハンドラーを `Sheet1` クラスに追加します。

     [!code-vb[Trin_VstcoreProgrammingControlsExcel#19](../vsto/codesnippet/VisualBasic/my excel chart/Sheet1.vb#19)]
     [!code-cs[Trin_VstcoreProgrammingControlsExcel#19](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs#19)]

2. C# では、次に示すように、ユーザーコントロールのイベントハンドラーをイベントに追加する必要があり <xref:Microsoft.Office.Tools.Excel.Worksheet.Startup> ます。 イベントハンドラーの作成方法の詳細については、「 [方法: Office プロジェクトでイベントハンドラーを作成](../vsto/how-to-create-event-handlers-in-office-projects.md)する」を参照してください。

     [!code-cs[Trin_VstcoreProgrammingControlsExcel#20](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs#20)]

## <a name="test-the-application"></a>アプリケーションをテストする
 これで、オプションボタンを選択したときに、グラフのスタイルが正しく表示されているかどうかを確認するために、ブックをテストできるようになりました。

### <a name="to-test-your-workbook"></a>ブックをテストするには

1. **F5**キーを押して、プロジェクトを実行します。

2. オプション ボタンを選択するには

3. 選択した内容に合わせてグラフのスタイルが変わることを確認します。

## <a name="next-steps"></a>次のステップ
 このチュートリアルでは、ワークシートでオプションボタンとグラフスタイルを使用する方法の基本について説明します。 ここでは、次の作業を行います。

- プロジェクトを配置しています。 詳細については、「 [Office ソリューションの配置](../vsto/deploying-an-office-solution.md)」を参照してください。

- ボタンを使用してテキスト ボックスへデータを挿入する。 詳細については、「 [チュートリアル: ボタンを使用してワークシートのテキストボックスにテキストを表示](../vsto/walkthrough-displaying-text-in-a-text-box-in-a-worksheet-using-a-button.md)する」を参照してください。

- チェックボックスを使用して、ワークシートの書式設定を変更します。 詳細については、「 [チュートリアル: CheckBox コントロールを使用してワークシートの書式を変更する](../vsto/walkthrough-changing-worksheet-formatting-using-checkbox-controls.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [Excel を使用したチュートリアル](../vsto/walkthroughs-using-excel.md)
