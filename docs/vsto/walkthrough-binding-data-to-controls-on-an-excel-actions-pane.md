---
title: 'チュートリアル: Excel の操作ウィンドウでコントロールにデータをバインドする'
description: Microsoft Excel の操作ウィンドウ上のコントロールにデータをバインドします。 このコントロールは、SQL Server データベースのテーブル間のマスター/詳細の関係を示します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- controls [Office development in Visual Studio], data binding
- actions panes [Office development in Visual Studio], data binding
- data binding [Office development in Visual Studio], smart documents
- data binding [Office development in Visual Studio], actions panes
- actions panes [Office development in Visual Studio], binding controls
- smart documents [Office development in Visual Studio], data binding
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 377c3405211c91712f8754131d8379c3dae7e820
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107824550"
---
# <a name="walkthrough-bind-data-to-controls-on-an-excel-actions-pane"></a>チュートリアル: Excel の操作ウィンドウでコントロールにデータをバインドする
  このチュートリアルでは Microsoft Office Excel の操作ウィンドウ上のコントロールへのデータバインドについて説明します。 このコントロールは、SQL Server データベースのテーブル間のマスター/詳細の関係を示します。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

 このチュートリアルでは、次の作業について説明します。

- ワークシートにコントロールを追加する。

- 操作ウィンドウコントロールを作成しています。

- 操作ウィンドウコントロールへのデータバインド Windows フォームコントロールの追加。

- アプリケーションが開いたときに操作ウィンドウを表示します。

> [!NOTE]
> 次の手順で参照している Visual Studio ユーザー インターフェイス要素の一部は、お使いのコンピューターでは名前や場所が異なる場合があります。 これらの要素は、使用している Visual Studio のエディションや独自の設定によって決まります。 詳細については、「[Visual Studio IDE のカスタマイズ](../ide/personalizing-the-visual-studio-ide.md)」を参照してください。

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)] または [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)]。

- Northwind SQL Server サンプルデータベースを使用したサーバーへのアクセス。

- SQL Server データベースに対する読み取りと書き込みの権限。

## <a name="create-the-project"></a>プロジェクトを作成する
 まず、Excel ブック プロジェクトを作成します。

### <a name="to-create-a-new-project"></a>新しいプロジェクトを作成するには

1. " **My Excel Actions Pane**" という名前の excel ブックプロジェクトを作成します。 ウィザードで、[ **新しいドキュメントの作成**] を選択します。 詳細については、「 [方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)」を参照してください。

     新しい Excel ブックがデザイナーで開き、 **[My Excel Actions] ウィンドウ** プロジェクトが **ソリューションエクスプローラー** に追加されます。

## <a name="add-a-new-data-source-to-the-project"></a>新しいデータソースをプロジェクトに追加する

### <a name="to-add-a-new-data-source-to-the-project"></a>新しいデータソースをプロジェクトに追加するには

1. [**データソース**] ウィンドウが表示されていない場合は、メニューバーの [   >  **他の Windows**  >  **データソース** の表示] をクリックして表示します。

2. **[新しいデータ ソースの追加]** をクリックして **データ ソース構成ウィザード** を開始します。

3. [ **データベース** ] を選択し、[ **次へ**] をクリックします。

4. Northwind サンプル SQL Server データベースへのデータ接続を選択するか、[ **新しい接続** ] ボタンを使用して新しい接続を追加します。

5. **[次へ]** をクリックします。

6. 選択されている場合は、接続を保存するオプションをオフにして、[ **次へ**] をクリックします。

7. [**データベースオブジェクト**] ウィンドウで、[**テーブル**] ノードを展開します。

8. [ **仕入先** ] テーブルの横にあるチェックボックスをオンにします。

9. **Products** テーブルを展開し、 **ProductName**、**仕入** 先、 **QuantityPerUnit**、および **UnitPrice** を選択します。

10. **[完了]** をクリックします。

    ウィザードにより、[**データソース**] ウィンドウに [**仕入先** テーブルと **製品**] テーブルが追加されます。 また、 **ソリューションエクスプローラー** に表示される、型指定されたデータセットをプロジェクトに追加します。

## <a name="add-controls-to-the-worksheet"></a>ワークシートにコントロールを追加する
 次に、 <xref:Microsoft.Office.Tools.Excel.NamedRange> 最初のワークシートにコントロールとコントロールを追加し <xref:Microsoft.Office.Tools.Excel.ListObject> ます。

### <a name="to-add-a-namedrange-control-and-a-listobject-control"></a>NamedRange コントロールと ListObject コントロールを追加するには

1. **[My Excel Actions Pane.xlsx** ] ブックが Visual Studio デザイナーで開かれていることを確認 `Sheet1` します。

2. [ **データソース** ] ウィンドウで、[ **仕入先** ] テーブルを展開します。

3. [ **会社名** ] ノードのドロップダウン矢印をクリックし、[ **NamedRange**] をクリックします。

4. [**データソース**] ウィンドウから [**会社名**] をセル **A2** にドラッグ `Sheet1` します。

     と <xref:Microsoft.Office.Tools.Excel.NamedRange> いう名前のコントロール `CompanyNameNamedRange` が作成され、テキストが \<CompanyName> セル **A2** に表示されます。 同時に、と <xref:System.Windows.Forms.BindingSource> いう名前の、 `suppliersBindingSource` テーブルアダプター、および <xref:System.Data.DataSet> がプロジェクトに追加されます。 コントロールは、にバインドされ <xref:System.Windows.Forms.BindingSource> 、さらにインスタンスにバインドされ <xref:System.Data.DataSet> ます。

5. [ **データソース** ] ウィンドウで、[ **仕入先** ] テーブルの下にある列を下にスクロールします。 一覧の一番下には **Products** テーブルがあります。これは、 **仕入先** テーブルの子であるためです。 [**仕入先**] テーブルと同じレベルにある [この **製品**] テーブルを選択し、表示されるドロップダウン矢印をクリックします。

6. ドロップダウンリストで [ **ListObject** ] をクリックし、 **Products** テーブルをのセル **A6** にドラッグし `Sheet1` ます。

     <xref:Microsoft.Office.Tools.Excel.ListObject>という名前のコントロール `ProductNameListObject` がセル **A6** に作成されます。 同時に、 <xref:System.Windows.Forms.BindingSource> という名前の `productsBindingSource` テーブルアダプターがプロジェクトに追加されます。 コントロールは、にバインドされ <xref:System.Windows.Forms.BindingSource> 、さらにインスタンスにバインドされ <xref:System.Data.DataSet> ます。

7. C# の場合のみ、コンポーネントトレイの [ **suppliersBindingSource** ] を選択し、[**プロパティ**] ウィンドウで [**修飾子**] プロパティを [**内部**] に変更します。

## <a name="add-controls-to-the-actions-pane"></a>[操作] ウィンドウにコントロールを追加する
 次に、コンボボックスを持つ操作ウィンドウコントロールが必要です。

### <a name="to-add-an-actions-pane-control"></a>操作ウィンドウコントロールを追加するには

1. **ソリューションエクスプローラー** で **[My Excel Actions] ウィンドウ** プロジェクトを選択します。

2. **[プロジェクト]** メニューの **[新しい項目の追加]** をクリックします。

3. [ **新しい項目の追加** ] ダイアログボックスで [ **操作ウィンドウコントロール**] を選択し、「 **ActionsControl**」という名前を指定して、[ **追加**] をクリックします。

### <a name="to-add-data-bound-windows-forms-controls-to-an-actions-pane-control"></a>データバインド Windows フォームコントロールを操作ウィンドウコントロールに追加するには

1. [**ツールボックス**] の [**コモンコントロール**] タブから、[ <xref:System.Windows.Forms.ComboBox> 操作] ウィンドウコントロールにコントロールをドラッグします。

2. **Size** プロパティを **171, 21** に変更します。

3. コンボボックスに合わせてユーザーコントロールのサイズを変更します。

## <a name="bind-the-control-on-the-actions-pane-to-data"></a>操作ウィンドウのコントロールをデータにバインドする
 このセクションでは、のデータソース <xref:System.Windows.Forms.ComboBox> を、 <xref:Microsoft.Office.Tools.Excel.NamedRange> ワークシート上のコントロールと同じデータソースに設定します。

### <a name="to-set-data-binding-properties-of-the-control"></a>コントロールのデータバインディングプロパティを設定するには

1. [操作] ウィンドウコントロールを右クリックし、[ **コードの表示**] をクリックします。

2. <xref:System.Windows.Forms.UserControl.Load>[操作] ウィンドウコントロールのイベントに次のコードを追加します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneExcelVB/ActionsControl.vb" id="Snippet1":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneExcelCS/ActionsControl.cs" id="Snippet1":::

3. C# では、のイベントハンドラーを作成する必要があり `ActionsControl` ます。 このコードは、コンストラクターに配置でき `ActionsControl` ます。 イベントハンドラーの作成の詳細については、「 [方法: Office プロジェクトでイベントハンドラーを作成](../vsto/how-to-create-event-handlers-in-office-projects.md)する」を参照してください。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneExcelCS/ActionsControl.cs" id="Snippet2":::

## <a name="show-the-actions-pane"></a>操作ウィンドウを表示する
 実行時にコントロールを追加するまで、[操作] ウィンドウは表示されません。

#### <a name="to-show-the-actions-pane"></a>操作ウィンドウを表示するには

1. **ソリューションエクスプローラー** で、[ *thisworkbook* ] または [ *thisworkbook*] を右クリックし、[**コードの表示**] をクリックします。

2. クラスにユーザーコントロールの新しいインスタンスを作成 `ThisWorkbook` します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneExcelCS/ThisWorkbook.cs" id="Snippet3":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneExcelVB/ThisWorkbook.vb" id="Snippet3":::

3. <xref:Microsoft.Office.Tools.Excel.Workbook.Startup>のイベントハンドラーで `ThisWorkbook` 、[操作] ウィンドウにコントロールを追加します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneExcelCS/ThisWorkbook.cs" id="Snippet4":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneExcelVB/ThisWorkbook.vb" id="Snippet4":::

## <a name="test-the-application"></a>アプリケーションをテストする
 ドキュメントをテストして、ドキュメントを開いたときに操作ウィンドウが開いていること、およびコントロールにマスター/詳細関係があることを確認できるようになりました。

### <a name="to-test-your-document"></a>文書をテストするには

1. **F5** キーを押して、プロジェクトを実行します。

2. 操作ウィンドウが表示されていることを確認します。

3. リストボックスで会社を選択します。 コントロールに会社名が表示されていること、 <xref:Microsoft.Office.Tools.Excel.NamedRange> および製品の詳細がコントロールに表示されていることを確認し <xref:Microsoft.Office.Tools.Excel.ListObject> ます。

4. 会社名と製品詳細が必要に応じて変更されていることを確認するには、さまざまな企業を選択します。

## <a name="next-steps"></a>次のステップ
 ここでは、次の作業を行います。

- Word のコントロールへのデータのバインド 詳細については、「 [チュートリアル: Word の操作ウィンドウでコントロールにデータをバインドする](../vsto/walkthrough-binding-data-to-controls-on-a-word-actions-pane.md)」を参照してください。

- プロジェクトを配置しています。 詳細については、「 [ClickOnce を使用した Office ソリューションの配置](../vsto/deploying-an-office-solution-by-using-clickonce.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [操作ウィンドウの概要](../vsto/actions-pane-overview.md)
- [方法: 操作ウィンドウのコントロールのレイアウトを管理する](../vsto/how-to-manage-control-layout-on-actions-panes.md)
- [Office ソリューションのコントロールにデータをバインドする](../vsto/binding-data-to-controls-in-office-solutions.md)
