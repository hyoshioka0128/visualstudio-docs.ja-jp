---
title: 'チュートリアル: カスタム作業ウィンドウからのアプリケーションの自動化'
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- task panes [Office development in Visual Studio], PowerPoint
- PowerPoint [Office development in Visual Studio], custom task panes
- automating Office applications
- custom task panes [Office development in Visual Studio], automating applications
- custom task panes [Office development in Visual Studio], PowerPoint
- task panes [Office development in Visual Studio], automating applications
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 52474aeebfbc03fba2a2e119e1b3366c30cf6959
ms.sourcegitcommit: 9d2829dc30b6917e89762d602022915f1ca49089
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2020
ms.locfileid: "91585081"
---
# <a name="walkthrough-automate-an-application-from-a-custom-task-pane"></a>チュートリアル: カスタム作業ウィンドウからのアプリケーションの自動化
  このチュートリアルでは、PowerPoint を自動化するカスタム作業ウィンドウの作成方法を示します。 このカスタム作業ウィンドウでは、カスタム作業ウィンドウに配置された <xref:System.Windows.Forms.MonthCalendar> コントロールをユーザーがクリックしたときに、日付をスライドに挿入します。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

 このチュートリアルでは、具体的に PowerPoint を使用していますが、チュートリアルで示される概念は、上記のすべてのアプリケーションに当てはまります。

 このチュートリアルでは、次の作業について説明します。

- カスタム作業ウィンドウのユーザー インターフェイスの設計。

- カスタム作業ウィンドウによる PowerPoint の自動化。

- PowerPoint でのカスタム作業ウィンドウの表示。

> [!NOTE]
> 次の手順で参照している Visual Studio ユーザー インターフェイス要素の一部は、お使いのコンピューターでは名前や場所が異なる場合があります。 これらの要素は、使用している Visual Studio のエディションや独自の設定によって決まります。 詳細については、「[Visual Studio IDE のカスタマイズ](../ide/personalizing-the-visual-studio-ide.md)」を参照してください。

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- Microsoft PowerPoint 2010 または [!INCLUDE[PowerPoint_15_short](../vsto/includes/powerpoint-15-short-md.md)]。

## <a name="create-the-add-in-project"></a>アドインプロジェクトを作成する
 最初の手順では、PowerPoint 用の VSTO アドインプロジェクトを作成します。

### <a name="to-create-a-new-project"></a>新しいプロジェクトを作成するには

1. PowerPoint アドイン プロジェクト テンプレートを使用して、 **MyAddIn**という名前の PowerPoint VSTO アドイン プロジェクトを作成します。 詳細については、「 [方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)」を参照してください。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]**ThisAddIn.cs**または**ThisAddIn**コードファイルを開き、**ソリューションエクスプローラー**に**MyAddIn**プロジェクトを追加します。

## <a name="design-the-user-interface-of-the-custom-task-pane"></a>カスタム作業ウィンドウのユーザーインターフェイスの設計
 カスタム作業ウィンドウにはビジュアルなデザイナーはありませんが、好みに合わせたレイアウトでユーザー コントロールを設計できます。 この後に説明するチュートリアルでは、ユーザー コントロールをカスタム作業ウィンドウに追加します。

#### <a name="to-design-the-user-interface-of-the-custom-task-pane"></a>カスタム作業ウィンドウのユーザー インターフェイスを設計するには

1. **[プロジェクト]** メニューの **[ユーザー コントロールの追加]** をクリックします。

2. **[新しい項目の追加]** ダイアログ ボックスで、ユーザー コントロールの名前を **MyUserControl**に変更して、 **[追加]** をクリックします。

     ユーザー コントロールがデザイナーで開きます。

3. **ツールボックス** の **[コモン コントロール]** タブから、 **MonthCalendar** コントロールをユーザー コントロールにドラッグします。

     **MonthCalendar** コントロールがユーザー コントロールのデザイン領域よりも大きい場合は、ユーザー コントロールのサイズを変更して、 **MonthCalendar** コントロールが収まるようにします。

## <a name="automate-powerpoint-from-the-custom-task-pane"></a>カスタム作業ウィンドウから PowerPoint を自動化する
 VSTO アドインの目的は、アクティブなプレゼンテーションの最初のスライドに、選択した日付を記入することです。 コントロールの <xref:System.Windows.Forms.MonthCalendar.DateChanged> イベントを使用すると、日付の選択を変更するたびに、その日付が追加されるようになります。

### <a name="to-automate-powerpoint-from-the-custom-task-pane"></a>カスタム作業ウィンドウから PowerPoint を自動化するには

1. デザイナーで、 <xref:System.Windows.Forms.MonthCalendar> コントロールをダブルクリックします。

     **MyUserControl.cs** ファイルまたは **MyUserControl.vb** ファイルが開き、 <xref:System.Windows.Forms.MonthCalendar.DateChanged> イベントのイベント ハンドラーが作成されます。

2. 次のコードをファイルの先頭に追加します。 このコードでは、 <xref:Microsoft.Office.Core> 名前空間と [PowerPoint](/previous-versions/office/developer/office-2010/ff763170%28v%3doffice.14%29) 名前空間のエイリアスを作成します。

     [!code-csharp[Trin_TaskPaneMonthCalendar#1](../vsto/codesnippet/CSharp/Trin_TaskPaneMonthCalendar/MyUserControl.cs#1)]
     [!code-vb[Trin_TaskPaneMonthCalendar#1](../vsto/codesnippet/VisualBasic/Trin_TaskPaneMonthCalendar/MyUserControl.vb#1)]

3. 次のコードを `MyUserControl` クラスに追加します。 このコードは、 [図形](/previous-versions/office/developer/office-2010/ff760244(v=office.14)) オブジェクトをのメンバーとして宣言 `MyUserControl` します。 次の手順では、この [図形](/previous-versions/office/developer/office-2010/ff760244(v=office.14)) を使用して、アクティブなプレゼンテーションのスライドにテキストボックスを追加します。

     [!code-csharp[Trin_TaskPaneMonthCalendar#2](../vsto/codesnippet/CSharp/Trin_TaskPaneMonthCalendar/MyUserControl.cs#2)]
     [!code-vb[Trin_TaskPaneMonthCalendar#2](../vsto/codesnippet/VisualBasic/Trin_TaskPaneMonthCalendar/MyUserControl.vb#2)]

4. `monthCalendar1_DateChanged` イベント ハンドラーを次のコードで置き換えます。 このコードでは、アクティブなプレゼンテーションの最初のスライドにテキスト ボックスを追加して、現在選択されている日付をそのテキスト ボックスに追加します。 また、このコードでは `Globals.ThisAddIn` オブジェクトを使用して PowerPoint のオブジェクト モデルにアクセスします。

     [!code-csharp[Trin_TaskPaneMonthCalendar#3](../vsto/codesnippet/CSharp/Trin_TaskPaneMonthCalendar/MyUserControl.cs#3)]
     [!code-vb[Trin_TaskPaneMonthCalendar#3](../vsto/codesnippet/VisualBasic/Trin_TaskPaneMonthCalendar/MyUserControl.vb#3)]

5. **ソリューション エクスプローラー**で、 **MyAddIn** プロジェクトを右クリックして、 **[ビルド]** をクリックします。 プロジェクトのビルドでエラーが発生しないことを確認します。

## <a name="display-the-custom-task-pane"></a>カスタム作業ウィンドウを表示する
 VSTO アドインの起動時にカスタム作業ウィンドウを表示するには、VSTO アドインの <xref:Microsoft.Office.Tools.AddIn.Startup> イベント ハンドラーで、ユーザー コントロールを作業ウィンドウに追加します。

### <a name="to-display-the-custom-task-pane"></a>カスタム作業ウィンドウを表示するには

1. **ソリューション エクスプローラー**で、 **[PowerPoint]** を展開します。

2. **ThisAddIn.cs** または **ThisAddIn.vb** を右クリックして、 **[コードの表示]** をクリックします。

3. 次のコードを `ThisAddIn` クラスに追加します。 このコードは `MyUserControl` と <xref:Microsoft.Office.Tools.CustomTaskPane> のインスタンスを `ThisAddIn` クラスのメンバーとして宣言します。

     [!code-vb[Trin_TaskPaneMonthCalendar#4](../vsto/codesnippet/VisualBasic/Trin_TaskPaneMonthCalendar/ThisAddIn.vb#4)]
     [!code-csharp[Trin_TaskPaneMonthCalendar#4](../vsto/codesnippet/CSharp/Trin_TaskPaneMonthCalendar/ThisAddIn.cs#4)]

4. `ThisAddIn_Startup` イベント ハンドラーを次のコードで置き換えます。 このコードは <xref:Microsoft.Office.Tools.CustomTaskPane> オブジェクトを `MyUserControl` コレクションに追加することにより、新しい `CustomTaskPanes` を作成します。 コードでは、作業ウィンドウも表示されます。

     [!code-vb[Trin_TaskPaneMonthCalendar#5](../vsto/codesnippet/VisualBasic/Trin_TaskPaneMonthCalendar/ThisAddIn.vb#5)]
     [!code-csharp[Trin_TaskPaneMonthCalendar#5](../vsto/codesnippet/CSharp/Trin_TaskPaneMonthCalendar/ThisAddIn.cs#5)]

## <a name="test-the-add-in"></a>アドインのテスト
 プロジェクトを実行すると、PowerPoint が開き、VSTO アドインによりカスタム作業ウィンドウが表示されます。 <xref:System.Windows.Forms.MonthCalendar> コントロールをクリックし、コードをテストします。

### <a name="to-test-your-vsto-add-in"></a>VSTO アドインをテストするには

1. **F5**キーを押して、プロジェクトを実行します。

2. カスタム作業ウィンドウが表示されていることを確認します。

3. 作業ウィンドウの <xref:System.Windows.Forms.MonthCalendar> コントロールで日付をクリックします。

     アクティブなプレゼンテーションの最初のスライドに日付が挿入されます。

## <a name="next-steps"></a>次の手順
 カスタム作業ウィンドウの作成方法の詳細については、次のトピックを参照してください。

- 別のアプリケーション用の VSTO アドインにカスタム作業ウィンドウを作成します。 カスタム作業ウィンドウをサポートするアプリケーションの詳細については、「 [カスタム作業ウィンドウ](../vsto/custom-task-panes.md)」を参照してください。

- カスタム作業ウィンドウの表示/非表示の切り替えに使用できるリボン ボタンを作成する。 詳細については、「 [チュートリアル: カスタム作業ウィンドウとリボンボタンの同期](../vsto/walkthrough-synchronizing-a-custom-task-pane-with-a-ribbon-button.md)」を参照してください。

- Outlook で開いたそれぞれの電子メール メッセージ用に、カスタム作業ウィンドウを作成する。 詳細については、「 [チュートリアル: Outlook で電子メールメッセージと共にカスタム作業ウィンドウを表示](../vsto/walkthrough-displaying-custom-task-panes-with-e-mail-messages-in-outlook.md)する」を参照してください。

## <a name="see-also"></a>関連項目
- [カスタム作業ウィンドウ](../vsto/custom-task-panes.md)
- [方法: カスタム作業ウィンドウをアプリケーションに追加する](../vsto/how-to-add-a-custom-task-pane-to-an-application.md)
- [チュートリアル: カスタム作業ウィンドウとリボンボタンの同期](../vsto/walkthrough-synchronizing-a-custom-task-pane-with-a-ribbon-button.md)
- [チュートリアル: Outlook で電子メールメッセージと共にカスタム作業ウィンドウを表示する](../vsto/walkthrough-displaying-custom-task-panes-with-e-mail-messages-in-outlook.md)
