---
title: 'チュートリアル: オプションボタンを使用してドキュメントのグラフを更新する'
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], updating using controls
- controls [Office development in Visual Studio], updating documents
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: f4b39949deb3bcbf3d9330ca8d820a5841b0f4c4
ms.sourcegitcommit: 9d2829dc30b6917e89762d602022915f1ca49089
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2020
ms.locfileid: "91584296"
---
# <a name="walkthrough-update-a-chart-in-a-document-using-radio-buttons"></a>チュートリアル: オプションボタンを使用してドキュメントのグラフを更新する
  このチュートリアルでは、Microsoft Office Word のドキュメント レベルのカスタマイズでオプション ボタンを使用して、文書上でグラフのスタイルを選択するオプションをユーザーに提供する方法を示します。

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

 このチュートリアルでは、次の作業について説明します。

- デザイン時におけるドキュメント レベルのプロジェクトの文書へのグラフの追加

- ユーザー コントロールへの追加によるオプション ボタンのグループ化

- オプション選択時のグラフ スタイルの変更

  完成したサンプルとして結果を表示するには、「 [Office 開発のサンプルとチュートリアル](../vsto/office-development-samples-and-walkthroughs.md)」の Word コントロールのサンプルを参照してください。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)] または [!INCLUDE[Word_14_short](../vsto/includes/word-14-short-md.md)]。

## <a name="create-the-project"></a>プロジェクトの作成
 最初に、Word 文書のプロジェクトを作成します。

### <a name="to-create-a-new-project"></a>新しいプロジェクトを作成するには

1. **My Chart Options**という名前の Word 文書プロジェクトを作成します。 ウィザードで、[ **新しいドキュメントの作成**] を選択します。 詳細については、「 [方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)」を参照してください。

     デザイナーで新しい Word 文書が開き、 **[My Chart Options]** プロジェクトが **ソリューションエクスプローラー**に追加されます。

## <a name="add-a-chart-to-the-document"></a>ドキュメントにグラフを追加する

### <a name="to-add-a-chart"></a>グラフを追加するには

1. Visual Studio デザイナーでホストされている Word 文書で、リボンの [ **挿入** ] タブをクリックします。

2. [ **テキスト** ] グループで、[ **オブジェクトの挿入** ] ドロップダウンボタンをクリックし、[ **オブジェクト**] をクリックします。

     [ **オブジェクト** ] ダイアログボックスが表示されます。

3. [**新規作成**] タブの [**オブジェクトの種類**] ボックスの一覧で [ **Microsoft Graph グラフ**] を選択し、[ **OK**] をクリックします。

     挿入ポイントでドキュメントにグラフが追加され、既定のデータと共に [ **データシート** ] ウィンドウが表示されます。

4. グラフの既定値をそのまま使用するには、[ **データシート** ] ウィンドウを閉じ、ドキュメント内をクリックしてグラフからフォーカスを移動します。

5. グラフを右クリックし、[オブジェクトの **書式設定**] をクリックします。

6. [**オブジェクトの書式設定**] ダイアログボックスの [**レイアウト**] タブで、[**四角**] を選択し、[ **OK**] をクリックします。

## <a name="add-a-user-control-to-the-project"></a>プロジェクトにユーザー コントロールを追加する
 文書のオプション ボタンは、既定では 1 つしか指定できないようになっています。 オプション ボタンをユーザー コントロールに追加し、選択を制御するためのコードを記述することによって、オプション ボタンを機能させることができます。

### <a name="to-add-a-user-control"></a>ユーザー コントロールを追加するには

1. **ソリューションエクスプローラー**で **[My Chart Options** ] プロジェクトを選択します。

2. **[プロジェクト]** メニューの **[新しい項目の追加]** をクリックします。

3. [ **新しい項目の追加** ] ダイアログボックスで、[ **ユーザーコントロール**] をクリックし、コントロールに **ChartOptions** という名前を指定して、[ **追加**] をクリックします。

### <a name="to-add-windows-form-controls-to-the-user-control"></a>Windows フォームのコントロールをユーザー コントロールへ追加するには

1. ユーザーコントロールがデザイナーに表示されていない場合は、**ソリューションエクスプローラー**で [ **ChartOptions** ] をダブルクリックします。

2. **ツールボックス**の [**コモンコントロール**] タブから、最初の**オプションボタン**コントロールをユーザーコントロールにドラッグし、次のプロパティを変更します。

    |プロパティ|値|
    |--------------|-----------|
    |**名前**|**columnChart**|
    |**Text**|**縦棒グラフ**|

3. 2番目の **オプションボタン** をユーザーコントロールに追加し、次のプロパティを変更します。

    |プロパティ|値|
    |--------------|-----------|
    |**名前**|**barChart**|
    |**Text**|**横棒グラフ**|

4. 3番目の **オプションボタン** をユーザーコントロールに追加し、次のプロパティを変更します。

    |プロパティ|値|
    |--------------|-----------|
    |**名前**|**lineChart**|
    |**Text**|**折れ線グラフ**|

5. 4番目の **オプションボタン** をユーザーコントロールに追加し、次のプロパティを変更します。

    |プロパティ|値|
    |--------------|-----------|
    |**名前**|**areaBlockChart**|
    |**Text**|**Area Block Chart**|

## <a name="add-references"></a>参照の追加
 ドキュメントのユーザーコントロールからグラフにアクセスするには、プロジェクト内のアセンブリへの参照が必要 `Microsoft.Office.Interop.Graph` です。

### <a name="to-add-a-reference-to-the-microsoftofficeinteropgraph-assembly"></a>Microsoft.Office.Interop.Graph アセンブリへの参照を追加するには

1. **[プロジェクト]** メニューの **[参照の追加]** をクリックします。

     **[参照の追加]** ダイアログ ボックスが表示されます。

2. [ **.Net** ] タブで、[ **Microsoft.** ..] を選択し、[ **OK**] をクリックします。 アセンブリの 14.0.0.0 バージョンを選択します。

## <a name="change-the-chart-style-when-a-radio-button-is-selected"></a>オプションボタンが選択されているときにグラフのスタイルを変更する
 ボタンを正しく動作させるために、ユーザー コントロールにパブリック イベントを作成し、選択の種類を設定するプロパティを追加して、各オプション ボタンの `CheckedChanged` イベントにプロシージャを作成します。

### <a name="to-create-an-event-and-property-on-a-user-control"></a>ユーザー コントロールにイベントおよびプロパティを作成するには

1. **ソリューションエクスプローラー**で、ユーザーコントロールを右クリックし、[コードの**表示**] をクリックします。

2. `SelectionChanged` イベントと `Selection` プロパティを作成するコードを `ChartOptions` クラスに追加します。

     [!code-csharp[Trin_VstcoreProgrammingControlsWord#9](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ChartOptions.cs#9)]
     [!code-vb[Trin_VstcoreProgrammingControlsWord#9](../vsto/codesnippet/VisualBasic/my chart options/ChartOptions.vb#9)]

### <a name="to-handle-the-checkedchange-event-of-the-radio-buttons"></a>オプション ボタンの CheckedChange イベントを処理するには

1. `CheckedChanged` オプション ボタンの `areaBlockChart` イベント ハンドラーでグラフの種類を設定し、イベントを発生させます。

     [!code-csharp[Trin_VstcoreProgrammingControlsWord#10](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ChartOptions.cs#10)]
     [!code-vb[Trin_VstcoreProgrammingControlsWord#10](../vsto/codesnippet/VisualBasic/my chart options/ChartOptions.vb#10)]

2. `CheckedChanged` オプション ボタンの `barChart` イベント ハンドラーでグラフの種類を設定します。

     [!code-csharp[Trin_VstcoreProgrammingControlsWord#11](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ChartOptions.cs#11)]
     [!code-vb[Trin_VstcoreProgrammingControlsWord#11](../vsto/codesnippet/VisualBasic/my chart options/ChartOptions.vb#11)]

3. `CheckedChanged` オプション ボタンの `columnChart` イベント ハンドラーでグラフの種類を設定します。

     [!code-csharp[Trin_VstcoreProgrammingControlsWord#12](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ChartOptions.cs#12)]
     [!code-vb[Trin_VstcoreProgrammingControlsWord#12](../vsto/codesnippet/VisualBasic/my chart options/ChartOptions.vb#12)]

4. `CheckedChanged` オプション ボタンの `lineChart` イベント ハンドラーでグラフの種類を設定します。

     [!code-csharp[Trin_VstcoreProgrammingControlsWord#13](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ChartOptions.cs#13)]
     [!code-vb[Trin_VstcoreProgrammingControlsWord#13](../vsto/codesnippet/VisualBasic/my chart options/ChartOptions.vb#13)]

5. C# では、オプション ボタンに対してイベント ハンドラーを追加する必要があります。 このコードを、`ChartOptions` への呼び出しの後で `InitializeComponent` コンストラクターに追加できます。 イベントハンドラーの作成の詳細については、「 [方法: Office プロジェクトでイベントハンドラーを作成](../vsto/how-to-create-event-handlers-in-office-projects.md)する」を参照してください。

     [!code-csharp[Trin_VstcoreProgrammingControlsWord#14](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ChartOptions.cs#14)]

## <a name="add-the-user-control-to-the-document"></a>ドキュメントにユーザーコントロールを追加する
 ソリューションをビルドすると、新しいユーザーコントロールが [ **ツールボックス**] に自動的に追加されます。 その後、 **ツールボックス** からドキュメントにコントロールをドラッグできます。

### <a name="to-add-the-user-control-your-document"></a>文書にユーザー コントロールを追加するには

1. **[ビルド]** メニューの **[ソリューションのビルド]** をクリックします。

     **ChartOptions**ユーザーコントロールが**ツールボックス**に追加されます。

2. **ソリューションエクスプローラー**で、[ **ThisDocument** ] または [ **ThisDocument.cs**] を右クリックし、[**デザイナーの表示**] をクリックします。

3. コントロールを [ `ChartOptions` **ツールボックス** ] から文書にドラッグします。

     [ **プロパティ** ] ウィンドウで、ドキュメントに追加したコントロールに名前を指定し  `ChartOptions1` ます。

## <a name="change-the-chart-type"></a>グラフの種類を変更する
 ユーザー コントロールで選択したオプションに基づいてグラフの種類を変更するイベント ハンドラーを作成します。

### <a name="to-change-the-type-of-chart-that-is-displayed-in-the-document"></a>文書に表示されるグラフの種類を変更するには

1. 次のイベント ハンドラーを `ThisDocument` クラスに追加します。

     [!code-vb[Trin_VstcoreProgrammingControlsWord#15](../vsto/codesnippet/VisualBasic/my chart options/ThisDocument.vb#15)]
     [!code-csharp[Trin_VstcoreProgrammingControlsWord#15](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ThisDocument.cs#15)]

2. C# では、ユーザー コントロールのイベント ハンドラーを <xref:Microsoft.Office.Tools.Word.Document.Startup> イベントに追加する必要があります。

     [!code-csharp[Trin_VstcoreProgrammingControlsWord#16](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ThisDocument.cs#16)]

## <a name="test-the-application"></a>アプリケーションをテストする
 文書をテストして、オプション ボタンを選択したときにグラフのスタイルが正しく更新されることを確認できます。

### <a name="to-test-your-document"></a>文書をテストするには

1. **F5**キーを押して、プロジェクトを実行します。

2. オプション ボタンを選択するには

3. 選択した内容に合わせてグラフのスタイルが変わることを確認します。

## <a name="next-steps"></a>次の手順
 ここでは、次の作業を行います。

- ボタンを使用してテキスト ボックスへデータを挿入する。 詳細については、「 [チュートリアル: ボタンを使用してドキュメント内のテキストボックスにテキストを表示](../vsto/walkthrough-displaying-text-in-a-text-box-in-a-document-using-a-button.md)する」を参照してください。

- コンボ ボックスからスタイルを選択して書式を変更する。 詳細については、「 [チュートリアル: CheckBox コントロールを使用してドキュメントの書式を変更する](../vsto/walkthrough-changing-document-formatting-using-checkbox-controls.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [Word を使用したチュートリアル](../vsto/walkthroughs-using-word.md)
- [Office 開発のサンプルとチュートリアル](../vsto/office-development-samples-and-walkthroughs.md)
- [Office ドキュメントの Windows フォームコントロールの制限事項](../vsto/limitations-of-windows-forms-controls-on-office-documents.md)
