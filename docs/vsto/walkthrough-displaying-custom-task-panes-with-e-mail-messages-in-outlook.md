---
title: Outlook で電子メールメッセージと共にカスタム作業ウィンドウを表示する
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Outlook [Office development in Visual Studio], custom task panes
- task panes [Office development in Visual Studio], displaying with e-mail messages
- displaying custom task panes in e-mail
- e-mail [Office development in Visual Studio], custom task panes displayed in
- custom task panes [Office development in Visual Studio], displaying with e-mail messages
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 00a8eae3f0beea7482c5fd7a1ac1ebd1994b9c35
ms.sourcegitcommit: 9d2829dc30b6917e89762d602022915f1ca49089
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2020
ms.locfileid: "91584283"
---
# <a name="walkthrough-display-custom-task-panes-with-email-messages-in-outlook"></a>チュートリアル: Outlook で電子メールメッセージと共にカスタム作業ウィンドウを表示する
  このチュートリアルでは、作成または開かれた各電子メールメッセージを使用して、カスタム作業ウィンドウの一意のインスタンスを表示する方法について説明します。 ユーザーは、各電子メール メッセージのリボンにあるボタンを使用して、カスタム作業ウィンドウを表示または非表示にすることができます。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

 複数のエクスプローラーやインスペクターのウィンドウでカスタム作業ウィンドウを表示するには、開いているそれぞれのウィンドウに対してカスタム作業ウィンドウのインスタンスを作成する必要があります。 Outlook ウィンドウのカスタム作業ウィンドウの動作の詳細については、「 [カスタム作業ウィンドウ](../vsto/custom-task-panes.md)」を参照してください。

> [!NOTE]
> このチュートリアルでは、コードのロジックについての説明をわかりやすくするために、VSTO アドイン コードを小さなセクションで提示します。

 このチュートリアルでは、次の作業について説明します。

- カスタム作業ウィンドウのユーザー インターフェイス (UI) の設計。

- カスタム リボン UI の作成。

- 電子メールメッセージと共にカスタムリボン UI を表示する。

- インスペクター ウィンドウとカスタム作業ウィンドウを管理するクラスの作成。

- VSTO アドインで使用されるリソースの初期化とクリーンアップ。

- リボンのトグル ボタンとカスタム作業ウィンドウとの同期。

> [!NOTE]
> 次の手順で参照している Visual Studio ユーザー インターフェイス要素の一部は、お使いのコンピューターでは名前や場所が異なる場合があります。 これらの要素は、使用している Visual Studio のエディションや独自の設定によって決まります。 詳細については、「[Visual Studio IDE のカスタマイズ](../ide/personalizing-the-visual-studio-ide.md)」を参照してください。

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- Microsoft [!INCLUDE[Outlook_15_short](../vsto/includes/outlook-15-short-md.md)] または Microsoft Outlook 2010。

## <a name="create-the-project"></a>プロジェクトの作成
 カスタム作業ウィンドウは、VSTO アドインで実装されます。まず、Outlook 用の VSTO アドインプロジェクトを作成します。

### <a name="to-create-a-new-project"></a>新しいプロジェクトを作成するには

1. **OutlookMailItemTaskPane** という名前の **Outlook アドイン**プロジェクトを作成します。 **Outlook アドイン** プロジェクトのテンプレートを使用します。 詳細については、「 [方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)」を参照してください。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] によって、 *ThisAddIn.cs* コード ファイルまたは *ThisAddIn.vb* コード ファイルが開かれ、 **ソリューション エクスプローラー** に **OutlookMailItemTaskPane**プロジェクトが追加されます。

## <a name="design-the-user-interface-of-the-custom-task-pane"></a>カスタム作業ウィンドウのユーザーインターフェイスの設計
 カスタム作業ウィンドウにはビジュアルなデザイナーはありませんが、お好きな UI を使用してユーザー コントロールを設計できます。 この VSTO アドインのカスタム作業ウィンドウには、 <xref:System.Windows.Forms.TextBox> コントロールを含む単純な UI が装備されています。 この後に説明するチュートリアルでは、ユーザー コントロールをカスタム作業ウィンドウに追加します。

### <a name="to-design-the-user-interface-of-the-custom-task-pane"></a>カスタム作業ウィンドウのユーザー インターフェイスを設計するには

1. **ソリューション エクスプローラー**で、 **OutlookMailItemTaskPane** プロジェクトをクリックします。

2. **[プロジェクト]** メニューの **[ユーザー コントロールの追加]** をクリックします。

3. **[新しい項目の追加]** ダイアログ ボックスでユーザー コントロールの名前を **TaskPaneControl**に変更し、 **[追加]** をクリックします。

     ユーザー コントロールがデザイナーで開きます。

4. **[ツールボックス]** の **[コモン コントロール]** タブから **TextBox** コントロールをユーザー コントロールにドラッグします。

## <a name="design-the-user-interface-of-the-ribbon"></a>リボンのユーザーインターフェイスをデザインする
 この VSTO アドインの目標の1つは、各電子メールメッセージのリボンからカスタム作業ウィンドウを表示または非表示にする方法をユーザーに提供することです。 ユーザー インターフェイスを提供するには、カスタム リボン UI を作成して、カスタム作業ウィンドウを表示または非表示にするためにクリックするトグル ボタンを表示します。

### <a name="to-create-a-custom-ribbon-ui"></a>カスタム リボン UI を作成するには

1. **[プロジェクト]** メニューの **[新しい項目の追加]** をクリックします。

2. **[新しい項目の追加]** ダイアログ ボックスで、 **[リボン (ビジュアル デザイナー)]** をクリックします。

3. 新しいリボンの名前を **ManageTaskPaneRibbon**に変更し、 **[追加]** をクリックします。

     リボン デザイナーで *ManageTaskPaneRibbon.cs* ファイルまたは *ManageTaskPaneRibbon.vb* ファイルが開き、既定のタブとグループが表示されます。

4. リボン デザイナーで、 **group1**をクリックします。

5. **[プロパティ]** ウィンドウで、 **[ラベル]** プロパティを **作業ウィンドウ マネージャー**に設定します。

6. **[ツールボックス]** の **[Office リボン コントロール]** タブから、[ToggleButton] コントロールを **[作業ウィンドウ マネージャー]** グループにドラッグします。

7. **toggleButton1**をクリックします。

8. **[プロパティ]** ウィンドウで、 **[ラベル]** プロパティを **[作業ウィンドウの表示]** に設定します。

## <a name="display-the-custom-ribbon-user-interface-with-email-messages"></a>電子メールメッセージと共にカスタムリボンユーザーインターフェイスを表示する
 このチュートリアルで作成したカスタム作業ウィンドウは、電子メール メッセージを含むインスペクター ウィンドウでのみ表示されるよう設計されています。 そのため、これらのウィンドウでのみ、カスタム リボン UI を表示するようプロパティを設定します。

### <a name="to-display-the-custom-ribbon-ui-with-email-messages"></a>電子メールメッセージと共にカスタムリボン UI を表示するには

1. リボン デザイナーで、 **[ManageTaskPaneRibbon]** リボンをクリックします。

2. **[プロパティ]** ウィンドウで、 **[RibbonType]** の隣にあるドロップダウン リストをクリックして、 **Microsoft.Outlook.Mail.Compose** と **Microsoft.Outlook.Mail.Read**を選択します。

## <a name="create-a-class-to-manage-inspector-windows-and-custom-task-panes"></a>インスペクターウィンドウとカスタム作業ウィンドウを管理するクラスを作成する
 特定の電子メールメッセージに関連付けられているカスタム作業ウィンドウを VSTO アドインが識別する必要がある場合があります。 たとえば、次のようなケースがあります。

- ユーザーが電子メールメッセージを閉じるとき。 この場合、VSTO アドインで、対応するカスタム作業ウィンドウを削除して、VSTO アドインで使用されるリソースが適切にクリーンアップされるようにする必要があります。

- ユーザーがカスタム作業ウィンドウを閉じるとき。 この場合、VSTO アドインは、電子メールメッセージのリボンのトグルボタンの状態を更新する必要があります。

- ユーザーがリボンのトグルボタンをクリックしたとき。 この場合、VSTO アドインで、対応する作業ウィンドウを非表示にしたり、表示したりする必要があります。

  VSTO アドインで、各電子メールメッセージに関連付けられているカスタム作業ウィンドウを追跡できるようにするには、オブジェクトとオブジェクトのペアをラップするカスタムクラスを作成し <xref:Microsoft.Office.Interop.Outlook.Inspector> <xref:Microsoft.Office.Tools.CustomTaskPane> ます。 このクラスは、電子メールメッセージごとに新しいカスタム作業ウィンドウオブジェクトを作成し、対応する電子メールメッセージが閉じられたときに、カスタム作業ウィンドウを削除します。

### <a name="to-create-a-class-to-manage-inspector-windows-and-custom-task-panes"></a>インスペクターウィンドウとカスタム作業ウィンドウを管理するクラスを作成するには

1. **ソリューション エクスプローラー**で、 *ThisAddIn.cs* または *ThisAddIn.vb* ファイルを右クリックし、 **[コードの表示]** をクリックします。

2. ファイルの先頭に次のステートメントを追加します。

     [!code-csharp[Trin_OutlookMailItemTaskPane#2](../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ThisAddIn.cs#2)]
     [!code-vb[Trin_OutlookMailItemTaskPane#2](../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ThisAddIn.vb#2)]

3. 次のコードを *クラスの外側で* ThisAddIn.cs *または* ThisAddIn.vb `ThisAddIn` ファイルに追加します (Visual C# の場合はこのコードを `OutlookMailItemTaskPane` 名前空間内部に追加します)。 `InspectorWrapper` クラスは <xref:Microsoft.Office.Interop.Outlook.Inspector> と <xref:Microsoft.Office.Tools.CustomTaskPane> オブジェクトのペアを管理します。 次の手順で、このクラスの定義が完了します。

     [!code-csharp[Trin_OutlookMailItemTaskPane#3](../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ThisAddIn.cs#3)]
     [!code-vb[Trin_OutlookMailItemTaskPane#3](../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ThisAddIn.vb#3)]

4. 前の手順で追加したコードの後に、次のコンストラクターを追加します。 このコンストラクターは、渡される <xref:Microsoft.Office.Interop.Outlook.Inspector> オブジェクトに関連付けられている新しいカスタム作業ウィンドウの作成と初期化を行います。 C# の場合は、コンストラクターはイベント ハンドラーを <xref:Microsoft.Office.Interop.Outlook.InspectorEvents_Event.Close> オブジェクトの <xref:Microsoft.Office.Interop.Outlook.Inspector> イベントと <xref:Microsoft.Office.Tools.CustomTaskPane.VisibleChanged> オブジェクトの <xref:Microsoft.Office.Tools.CustomTaskPane> イベントにもアタッチします。

     [!code-csharp[Trin_OutlookMailItemTaskPane#4](../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ThisAddIn.cs#4)]
     [!code-vb[Trin_OutlookMailItemTaskPane#4](../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ThisAddIn.vb#4)]

5. 前の手順で追加したコードの後に、次のメソッドを追加します。 このメソッドは、 <xref:Microsoft.Office.Tools.CustomTaskPane.VisibleChanged> クラスに含まれている <xref:Microsoft.Office.Tools.CustomTaskPane> オブジェクトの `InspectorWrapper` イベント用のイベント ハンドラーです。 このコードは、カスタム作業ウィンドウを開いたり閉じたりするたびに、トグル ボタンの状態を更新します。

     [!code-csharp[Trin_OutlookMailItemTaskPane#5](../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ThisAddIn.cs#5)]
     [!code-vb[Trin_OutlookMailItemTaskPane#5](../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ThisAddIn.vb#5)]

6. 前の手順で追加したコードの後に、次のメソッドを追加します。 このメソッドは、 <xref:Microsoft.Office.Interop.Outlook.InspectorEvents_Event.Close> <xref:Microsoft.Office.Interop.Outlook.Inspector> 現在の電子メールメッセージを含むオブジェクトのイベントのイベントハンドラーです。 イベントハンドラーは、電子メールメッセージが閉じられたときにリソースを解放します。 またイベント ハンドラーは、 `CustomTaskPanes` コレクションから現在のカスタム作業ウィンドウを削除します。 これにより、次の電子メールメッセージを開いたときに、カスタム作業ウィンドウの複数のインスタンスを防ぐことができます。

     [!code-csharp[Trin_OutlookMailItemTaskPane#6](../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ThisAddIn.cs#6)]
     [!code-vb[Trin_OutlookMailItemTaskPane#6](../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ThisAddIn.vb#6)]

7. 前の手順で追加したコードの後に、次のコードを追加します。 このチュートリアルの後の部分で、このプロパティをカスタム リボン UI 内のメソッドから呼び出して、カスタム作業ウィンドウの表示と非表示を行います。

     [!code-csharp[Trin_OutlookMailItemTaskPane#7](../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ThisAddIn.cs#7)]
     [!code-vb[Trin_OutlookMailItemTaskPane#7](../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ThisAddIn.vb#7)]

## <a name="initialize-and-clean-up-resources-used-by-the-add-in"></a>アドインによって使用されるリソースを初期化してクリーンアップする
 コードを `ThisAddIn` クラスに追加して、VSTO アドインを読み込む際に初期化し、また VSTO アドインをアンロードする際には使用したリソースをクリーンアップします。 VSTO アドインを初期化するには、イベントのイベントハンドラーを設定 <xref:Microsoft.Office.Interop.Outlook.InspectorsEvents_Event.NewInspector> し、すべての既存の電子メールメッセージをこのイベントハンドラーに渡します。 VSTO アドインを読み込む際に、イベント ハンドラーをデタッチして、VSTO アドインで使用されたオブジェクトをクリーンアップします。

### <a name="to-initialize-and-clean-up-resources-used-by-the-vsto-add-in"></a>VSTO アドインで使用されるリソースの初期化とクリーンアップをするには

1. *ThisAddIn.cs* または *ThisAddIn.vb* ファイルで、 `ThisAddIn` クラスの定義を検索します。

2. `ThisAddIn` クラスに次の宣言を追加します。

   - `inspectorWrappersValue` フィールドには、VSTO アドインによって管理される <xref:Microsoft.Office.Interop.Outlook.Inspector> と `InspectorWrapper` のオブジェクトすべてが格納されます。

   - `inspectors` フィールドは、Outlook の現在のインスタンスに含まれるインスペクター ウィンドウのコレクションへの参照を保持します。 この参照によって、次の手順で宣言する、 <xref:Microsoft.Office.Interop.Outlook.InspectorsEvents_Event.NewInspector> イベントのイベント ハンドラーが格納されたメモリをガベージ コレクターが解放することを防止できます。

     [!code-csharp[Trin_OutlookMailItemTaskPane#8](../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ThisAddIn.cs#8)]
     [!code-vb[Trin_OutlookMailItemTaskPane#8](../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ThisAddIn.vb#8)]

3. `ThisAddIn_Startup` メソッドを次のコードに置き換えます。 このコードは、イベント ハンドラーを <xref:Microsoft.Office.Interop.Outlook.InspectorsEvents_Event.NewInspector> イベントにアタッチし、すべての既存の <xref:Microsoft.Office.Interop.Outlook.Inspector> オブジェクトをそのイベント ハンドラーに渡します。 Outlook が既に実行されている場合にユーザーが VSTO アドインを読み込むと、VSTO アドインはこの情報を使用して、既に開いているすべての電子メールメッセージに対してカスタム作業ウィンドウを作成します。

    [!code-csharp[Trin_OutlookMailItemTaskPane#9](../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ThisAddIn.cs#9)]
    [!code-vb[Trin_OutlookMailItemTaskPane#9](../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ThisAddIn.vb#9)]

4. `ThisAddIn_ShutDown` メソッドを次のコードに置き換えます。 このコードは、 <xref:Microsoft.Office.Interop.Outlook.InspectorsEvents_Event.NewInspector> イベント ハンドラーをデタッチして、VSTO アドインで使用されたオブジェクトをクリーンアップします。

    [!code-csharp[Trin_OutlookMailItemTaskPane#10](../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ThisAddIn.cs#10)]
    [!code-vb[Trin_OutlookMailItemTaskPane#10](../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ThisAddIn.vb#10)]

5. 次の <xref:Microsoft.Office.Interop.Outlook.InspectorsEvents_Event.NewInspector> イベント ハンドラーを `ThisAddIn` クラスに追加します。 新しいに <xref:Microsoft.Office.Interop.Outlook.Inspector> 電子メールメッセージが含まれている場合、メソッドは、 `InspectorWrapper` 電子メールメッセージと対応する作業ウィンドウの間の関係を管理するために、新しいオブジェクトのインスタンスを作成します。

    [!code-csharp[Trin_OutlookMailItemTaskPane#11](../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ThisAddIn.cs#11)]
    [!code-vb[Trin_OutlookMailItemTaskPane#11](../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ThisAddIn.vb#11)]

6. `ThisAddIn` クラスに次のプロパティを追加します。 このプロパティは、プライベート `inspectorWrappersValue` フィールドを `ThisAddIn` クラスの外部のコードに公開します。

    [!code-csharp[Trin_OutlookMailItemTaskPane#12](../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ThisAddIn.cs#12)]
    [!code-vb[Trin_OutlookMailItemTaskPane#12](../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ThisAddIn.vb#12)]

## <a name="checkpoint"></a>Checkpoint
 エラーが発生することなくプロジェクトをコンパイルできるように、必ずプロジェクトをビルドします。

### <a name="to-build-your-project"></a>プロジェクトをビルドするには

1. **ソリューション エクスプローラー**で、 **OutlookMailItemTaskPane** プロジェクトを右クリックし、 **[ビルド]** をクリックします。 プロジェクトのコンパイルでエラーが発生しないことを確認します。

## <a name="synchronize-the-ribbon-toggle-button-with-the-custom-task-pane"></a>リボンのトグルボタンとカスタム作業ウィンドウの同期
 作業ウィンドウが表示されている場合、トグル ボタンは押されているように見え、作業ウィンドウが非表示になっている場合は、押されていないように見えます。 ボタンの状態をカスタム作業ウィンドウと同期させるには、トグル ボタンの <xref:Microsoft.Office.Tools.Ribbon.RibbonToggleButton.Click> イベント ハンドラーを変更します。

### <a name="to-synchronize-the-custom-task-pane-with-the-toggle-button"></a>カスタム作業ウィンドウをトグル ボタンと同期させるには

1. リボン デザイナーで、 **[作業ウィンドウの表示]** トグル ボタンをダブルクリックします。

     Visual Studio によって、 `toggleButton1_Click`という名前のイベント ハンドラーが自動的に生成されます。トグル ボタンの <xref:Microsoft.Office.Tools.Ribbon.RibbonToggleButton.Click> イベントは、このハンドラーが処理します。 また Visual Studio により、コード エディターに *ManageTaskPaneRibbon.cs* または *ManageTaskPaneRibbon.vb* ファイルも開かれます。

2. *ManageTaskPaneRibbon.cs* または *ManageTaskPaneRibbon.vb* ファイルの先頭に次のステートメントを追加します。

     [!code-csharp[Trin_OutlookMailItemTaskPane#14](../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ManageTaskPaneRibbon.cs#14)]
     [!code-vb[Trin_OutlookMailItemTaskPane#14](../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ManageTaskPaneRibbon.vb#14)]

3. `toggleButton1_Click` イベント ハンドラーを次のコードで置き換えます。 トグル ボタンをクリックすると、このメソッドによって、現在のインスペクター ウィンドウに関連付けられているカスタム作業ウィンドウが非表示または表示にされます。

     [!code-csharp[Trin_OutlookMailItemTaskPane#15](../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ManageTaskPaneRibbon.cs#15)]
     [!code-vb[Trin_OutlookMailItemTaskPane#15](../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ManageTaskPaneRibbon.vb#15)]

## <a name="test-the-project"></a>プロジェクトをテストする
 プロジェクトのデバッグを開始すると、Outlook が開き、VSTO アドインが読み込まれます。 VSTO アドインでは、開いている各電子メールメッセージと共に、カスタム作業ウィンドウの一意のインスタンスが表示されます。 コードをテストする新しい電子メールメッセージをいくつか作成します。

### <a name="to-test-the-vsto-add-in"></a>VSTO アドインをテストするには

1. **F5**キーを押します。

2. Outlook で、[ **新規** ] をクリックして新しい電子メールメッセージを作成します。

3. 電子メールメッセージのリボンで、[ **アドイン** ] タブをクリックし、[ **作業ウィンドウの表示** ] ボタンをクリックします。

    **[個人用作業ウィンドウ]** というタイトルの作業ウィンドウが電子メールメッセージと共に表示されていることを確認します。

4. 作業ウィンドウで、テキスト ボックスに「 **最初の作業ウィンドウ** 」と入力します。

5. 作業ウィンドウを閉じます。

    **[作業ウィンドウの表示]** ボタンの状態が変更され、ボタンが押されていない状態になっていることを確認します。

6. **[作業ウィンドウの表示]** ボタンをもう一度クリックします。

    作業ウィンドウが開き、テキスト ボックスにも、「 **最初の作業ウィンドウ**」という文字列が含まれていることを確認します。

7. Outlook で、[ **新規** ] をクリックして、2番目の電子メールメッセージを作成します。

8. 電子メールメッセージのリボンで、[ **アドイン** ] タブをクリックし、[ **作業ウィンドウの表示** ] ボタンをクリックします。

    **[個人用作業ウィンドウ]** というタイトルの作業ウィンドウが電子メールメッセージと共に表示され、この作業ウィンドウのテキストボックスが空であることを確認します。

9. 作業ウィンドウで、テキスト ボックスに「 **2 番目の作業ウィンドウ** 」と入力します。

10. 最初の電子メールメッセージにフォーカスを移動します。

     この電子メールメッセージに関連付けられている作業ウィンドウに、テキストボックスに **最初の作業ウィンドウ** が表示されていることを確認します。

    また、この VSTO アドインでは、より高度なシナリオも試すことができます。 たとえば、 **[次の項目** ] ボタンと [ **前の項目** ] ボタンを使用して、電子メールを表示するときの動作をテストできます。 VSTO アドインをアンロードしたときの動作をテストし、いくつかの電子メールメッセージを開いて、VSTO アドインを再度読み込むこともできます。

## <a name="next-steps"></a>次の手順
 カスタム作業ウィンドウの作成方法の詳細については、次のトピックを参照してください。

- 別のアプリケーション用の VSTO アドインにカスタム作業ウィンドウを作成します。 カスタム作業ウィンドウをサポートするアプリケーションの詳細については、「 [カスタム作業ウィンドウ](../vsto/custom-task-panes.md)」を参照してください。

- カスタム作業ウィンドウを使用して、Microsoft Office アプリケーションを自動化します。 詳細については、「 [チュートリアル: カスタム作業ウィンドウからのアプリケーションの自動化](../vsto/walkthrough-automating-an-application-from-a-custom-task-pane.md)」を参照してください。

- Excel にリボン ボタンを作成して、カスタム作業ウィンドウの非表示または表示に使用できるようにします。 詳細については、「 [チュートリアル: カスタム作業ウィンドウとリボンボタンの同期](../vsto/walkthrough-synchronizing-a-custom-task-pane-with-a-ribbon-button.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [カスタム作業ウィンドウ](../vsto/custom-task-panes.md)
- [方法: カスタム作業ウィンドウをアプリケーションに追加する](../vsto/how-to-add-a-custom-task-pane-to-an-application.md)
- [チュートリアル: カスタム作業ウィンドウからのアプリケーションの自動化](../vsto/walkthrough-automating-an-application-from-a-custom-task-pane.md)
- [チュートリアル: カスタム作業ウィンドウとリボンボタンの同期](../vsto/walkthrough-synchronizing-a-custom-task-pane-with-a-ribbon-button.md)
- [リボンの概要](../vsto/ribbon-overview.md)
- [Outlook オブジェクトモデルの概要](../vsto/outlook-object-model-overview.md)
- [実行時のリボンへのアクセス](../vsto/accessing-the-ribbon-at-run-time.md)
