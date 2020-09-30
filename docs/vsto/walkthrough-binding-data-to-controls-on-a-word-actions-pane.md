---
title: 'チュートリアル: Word の操作ウィンドウでコントロールにデータをバインドする'
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
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 05df38bf6056b392c0b991617316ba2c1c657306
ms.sourcegitcommit: 9d2829dc30b6917e89762d602022915f1ca49089
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2020
ms.locfileid: "91585068"
---
# <a name="walkthrough-bind-data-to-controls-on-a-word-actions-pane"></a>チュートリアル: Word の操作ウィンドウでコントロールにデータをバインドする
  このチュートリアルでは、Word の操作ウィンドウ上のコントロールへのデータバインディングについて説明します。 このコントロールは、SQL Server データベースのテーブル間のマスター/詳細の関係を示します。

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

 このチュートリアルでは、次の作業について説明します。

- データにバインドされている Windows フォームコントロールを使用して操作ウィンドウを作成する。

- マスター/詳細関係を使用してコントロールにデータを表示する。

- アプリケーションを開いたときに操作ウィンドウを表示します。

> [!NOTE]
> 次の手順で参照している Visual Studio ユーザー インターフェイス要素の一部は、お使いのコンピューターでは名前や場所が異なる場合があります。 これらの要素は、使用している Visual Studio のエディションや独自の設定によって決まります。 詳細については、「[Visual Studio IDE のカスタマイズ](../ide/personalizing-the-visual-studio-ide.md)」を参照してください。

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)] または [!INCLUDE[Word_14_short](../vsto/includes/word-14-short-md.md)]。

- Northwind SQL Server サンプルデータベースを使用したサーバーへのアクセス。

- SQL Server データベースに対する読み取りと書き込みの権限。

## <a name="create-the-project"></a>プロジェクトの作成
 最初に、Word 文書のプロジェクトを作成します。

### <a name="to-create-a-new-project"></a>新しいプロジェクトを作成するには

1. [Word の **操作] ウィンドウ**という名前の word 文書プロジェクトを作成します。 ウィザードで、[ **新しいドキュメントの作成**] を選択します。

     詳細については、「 [方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)」を参照してください。

     Visual Studio では、デザイナーで新しい Word 文書が開き、 **[マイ Word 操作] ウィンドウ** プロジェクトが **ソリューションエクスプローラー**に追加されます。

## <a name="add-controls-to-the-actions-pane"></a>[操作] ウィンドウにコントロールを追加する
 このチュートリアルでは、データバインド Windows フォームコントロールを含む操作ウィンドウコントロールが必要です。 データソースをプロジェクトに追加し、[ **データソース** ] ウィンドウから [操作] ウィンドウコントロールにコントロールをドラッグします。

### <a name="to-add-an-actions-pane-control"></a>操作ウィンドウコントロールを追加するには

1. **ソリューションエクスプローラー**で **[マイ Word 操作] ウィンドウ**プロジェクトを選択します。

2. **[プロジェクト]** メニューの **[新しい項目の追加]** をクリックします。

3. [ **新しい項目の追加** ] ダイアログボックスで [ **操作ウィンドウコントロール**] を選択し、「 **ActionsControl**」という名前を指定して、[ **追加**] をクリックします。

### <a name="to-add-a-data-source-to-the-project"></a>データソースをプロジェクトに追加するには

1. [**データソース**] ウィンドウが表示されていない場合は、メニューバーの [ **View**  >  **他の Windows**  >  **データソース**の表示] をクリックして表示します。

   > [!NOTE]
   > [ **データソースの表示** ] が使用できない場合は、Word 文書をクリックし、もう一度確認します。

2. [ **新しいデータソースの追加** ] をクリックして、 **データソース構成ウィザード**を開始します。

3. [ **データベース** ] を選択し、[ **次へ**] をクリックします。

4. Northwind サンプル SQL Server データベースへのデータ接続を選択するか、[ **新しい接続** ] ボタンを使用して新しい接続を追加します。

5. **[次へ]** をクリックします。

6. 選択されている場合は、接続を保存するオプションをオフにして、[ **次へ**] をクリックします。

7. [**データベースオブジェクト**] ウィンドウで、[**テーブル**] ノードを展開します。

8. **仕入先**テーブルと**Products**テーブルの横にあるチェックボックスをオンにします。

9. **[完了]** をクリックします。

   ウィザードにより、[**データソース**] ウィンドウに [**仕入先**テーブルと**製品**] テーブルが追加されます。 また、 **ソリューションエクスプローラー**に表示される、型指定されたデータセットをプロジェクトに追加します。

### <a name="to-add-data-bound-windows-forms-controls-to-an-actions-pane-control"></a>データバインド Windows フォームコントロールを操作ウィンドウコントロールに追加するには

1. [ **データソース** ] ウィンドウで、[ **仕入先** ] テーブルを展開します。

2. [ **会社名** ] ノードのドロップダウン矢印をクリックし、[ **ComboBox**] を選択します。

3. [**データソース**] ウィンドウから [ **CompanyName** ] を操作ウィンドウコントロールにドラッグします。

     <xref:System.Windows.Forms.ComboBox>操作ウィンドウコントロールにコントロールが作成されます。 同時に、と <xref:System.Windows.Forms.BindingSource> いう名前 `SuppliersBindingSource` の、テーブルアダプター、およびが <xref:System.Data.DataSet> コンポーネントトレイのプロジェクトに追加されます。

4. `SuppliersBindingNavigator`**コンポーネント**トレイでを選択し、 **del**キーを押します。 このチュートリアルでは、を使用しません `SuppliersBindingNavigator` 。

    > [!NOTE]
    > を削除しても、 `SuppliersBindingNavigator` 生成されたコードはすべて削除されません。 このコードは削除できます。

5. コンボボックスをラベルの下に移動し、 **Size** プロパティを **171, 21**に変更します。

6. [**データソース**] ウィンドウで、[**仕入先**] テーブルの子である**Products**テーブルを展開します。

7. [ **ProductName** ] ノードのドロップダウン矢印をクリックし、[ **ListBox**] を選択します。

8. **ProductName**を [操作] ウィンドウコントロールにドラッグします。

     <xref:System.Windows.Forms.ListBox>操作ウィンドウコントロールにコントロールが作成されます。 同時に、 <xref:System.Windows.Forms.BindingSource> という名前の `ProductBindingSource` テーブルアダプターがコンポーネントトレイのプロジェクトに追加されます。

9. リストボックスをラベルの下に移動し、 **Size** プロパティを **171, 95**に変更します。

10. <xref:System.Windows.Forms.Button>**ツールボックス**から [操作] ウィンドウコントロールにをドラッグし、リストボックスの下に配置します。

11. を右クリックし、 <xref:System.Windows.Forms.Button> ショートカットメニューの [ **プロパティ** ] をクリックして、次のプロパティを変更します。

    |プロパティ|値|
    |--------------|-----------|
    |**名前**|**挿入**|
    |**Text**|**挿入**|

12. コントロールに合わせてユーザーコントロールのサイズを変更します。

## <a name="set-up-the-data-source"></a>データ ソースを設定する
 データソースを設定するには、[操作] ウィンドウコントロールのイベントにコードを追加して、 <xref:System.Windows.Forms.UserControl.Load> コントロールにのデータを入力 <xref:System.Data.DataTable> し、 <xref:System.Windows.Forms.Binding.DataSource%2A> <xref:System.Windows.Forms.BindingSource.DataMember%2A> 各コントロールのプロパティとプロパティを設定します。

### <a name="to-load-the-control-with-data"></a>データを使用してコントロールを読み込むには

1. <xref:System.Windows.Forms.UserControl.Load>クラスのイベントハンドラーに `ActionsControl` 次のコードを追加します。

     [!code-vb[Trin_VstcoreActionsPaneWord#1](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ActionsControl.vb#1)]
     [!code-csharp[Trin_VstcoreActionsPaneWord#1](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ActionsControl.cs#1)]

2. C# では、イベントハンドラーをイベントにアタッチする必要があり <xref:System.Windows.Forms.UserControl.Load> ます。 このコードは `ActionsControl` 、の呼び出しの後、コンストラクターに配置でき `InitializeComponent` ます。 イベントハンドラーを作成する方法の詳細については、「 [方法: Office プロジェクトでイベントハンドラーを作成](../vsto/how-to-create-event-handlers-in-office-projects.md)する」を参照してください。

     [!code-csharp[Trin_VstcoreActionsPaneWord#33](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ActionsControl.cs#33)]

### <a name="to-set-data-binding-properties-of-the-controls"></a>コントロールのデータバインディングプロパティを設定するには

1. `CompanyNameComboBox` コントロールを選択します。

2. [ **プロパティ** ] ウィンドウで、 **DataSource** プロパティの右側にあるボタンをクリックし、[ **suppliersBindingSource**] を選択します。

3. **Displaymember**プロパティの右側にあるボタンをクリックし、[ **CompanyName**] を選択します。

4. [ **連結** ] プロパティを展開し、 **Text** プロパティの右側にあるボタンをクリックして、[ **なし**] を選択します。

5. `ProductNameListBox` コントロールを選択します。

6. [ **プロパティ** ] ウィンドウで、 **DataSource** プロパティの右側にあるボタンをクリックし、[製品 **bindingsource**] を選択します。

7. **Displaymember**プロパティの右側にあるボタンをクリックし、[ **ProductName**] を選択します。

8. [ **連結** ] プロパティを展開し、 **SelectedValue** プロパティの右側にあるボタンをクリックして、[ **なし**] を選択します。

## <a name="add-a-method-to-insert-data-into-a-table"></a>テーブルにデータを挿入するメソッドを追加する
 次のタスクでは、バインドされたコントロールからデータを読み取り、Word 文書にテーブルを設定します。 まず、テーブルの見出しを書式設定するためのプロシージャを作成し、 `AddData` Word の表を作成および書式設定するメソッドを追加します。

### <a name="to-format-the-table-headings"></a>テーブルの見出しの書式を設定するには

1. クラスで、 `ActionsControl` テーブルの見出しの書式を設定するメソッドを作成します。

     [!code-vb[Trin_VstcoreActionsPaneWord#2](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ActionsControl.vb#2)]
     [!code-csharp[Trin_VstcoreActionsPaneWord#2](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ActionsControl.cs#2)]

### <a name="to-create-the-table"></a>テーブルを作成するには

1. クラスで、 `ActionsControl` テーブルがまだ存在しない場合にテーブルを作成するメソッドを記述し、操作ウィンドウからテーブルにデータを追加します。

     [!code-vb[Trin_VstcoreActionsPaneWord#3](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ActionsControl.vb#3)]
     [!code-csharp[Trin_VstcoreActionsPaneWord#3](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ActionsControl.cs#3)]

### <a name="to-insert-text-into-a-word-table"></a>Word の表にテキストを挿入するには

1. <xref:System.Windows.Forms.Control.Click>[**挿入**] ボタンのイベントハンドラーに次のコードを追加します。

     [!code-vb[Trin_VstcoreActionsPaneWord#4](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ActionsControl.vb#4)]
     [!code-csharp[Trin_VstcoreActionsPaneWord#4](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ActionsControl.cs#4)]

2. C# では、ボタンのイベントのイベントハンドラーを作成する必要があり <xref:System.Windows.Forms.Control.Click> ます。  このコードは <xref:System.Windows.Forms.UserControl.Load> 、クラスのイベントハンドラーに配置でき `ActionsControl` ます。

     [!code-csharp[Trin_VstcoreActionsPaneWord#5](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ActionsControl.cs#5)]

## <a name="show-the-actions-pane"></a>操作ウィンドウを表示する
 コントロールが追加された後、操作ウィンドウが表示されます。

### <a name="to-show-the-actions-pane"></a>操作ウィンドウを表示するには

1. **ソリューションエクスプローラー**で、[ **ThisDocument** ] または [ **ThisDocument.cs**] を右クリックし、ショートカットメニューの [**コードの表示**] をクリックします。

2. 次の例のように、クラスの上部にコントロールの新しいインスタンスを作成 `ThisDocument` します。

     [!code-csharp[Trin_VstcoreActionsPaneWord#6](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs#6)]
     [!code-vb[Trin_VstcoreActionsPaneWord#6](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb#6)]

3. <xref:Microsoft.Office.Tools.Word.Document.Startup>次の例のように、のイベントハンドラーにコードを追加 `ThisDocument` します。

     [!code-csharp[Trin_VstcoreActionsPaneWord#7](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs#7)]
     [!code-vb[Trin_VstcoreActionsPaneWord#7](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb#7)]

## <a name="test-the-application"></a>アプリケーションをテストする
 ドキュメントをテストして、ドキュメントを開いたときに操作ウィンドウが表示されることを確認できるようになりました。 操作ウィンドウのコントロールでマスター/詳細リレーションシップをテストし、[ **挿入** ] ボタンがクリックされたときに、Word テーブルにデータが入力されていることを確認します。

### <a name="to-test-your-document"></a>文書をテストするには

1. **F5**キーを押して、プロジェクトを実行します。

2. 操作ウィンドウが表示されていることを確認します。

3. コンボボックスで会社を選択し、[ **Products** ] リストボックス内の項目が変更されていることを確認します。

4. 製品を選択し、[操作] ウィンドウで [ **挿入** ] をクリックして、製品の詳細が Word のテーブルに追加されていることを確認します。

5. さまざまな企業から追加の製品を挿入します。

## <a name="next-steps"></a>次の手順
 このチュートリアルでは、Word の操作ウィンドウ上のコントロールにデータをバインドする方法の基本について説明します。 ここでは、次の作業を行います。

- Excel のコントロールにデータをバインドする。 詳細については、「 [チュートリアル: Excel の操作ウィンドウでコントロールにデータをバインドする](../vsto/walkthrough-binding-data-to-controls-on-an-excel-actions-pane.md)」を参照してください。

- プロジェクトを配置しています。 詳細については、「 [ClickOnce を使用した Office ソリューションの配置](../vsto/deploying-an-office-solution-by-using-clickonce.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [操作ウィンドウの概要](../vsto/actions-pane-overview.md)
- [方法: Word 文書または Excel ブックに操作ウィンドウを追加する](../vsto/how-to-add-an-actions-pane-to-word-documents-or-excel-workbooks.md)
- [Office ソリューションのコントロールにデータをバインドする](../vsto/binding-data-to-controls-in-office-solutions.md)
