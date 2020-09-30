---
title: 'チュートリアル: ドキュメントレベルのプロジェクトでの複合データバインディング'
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data [Office development in Visual Studio], binding data
- complex data [Office development in Visual Studio]
- multiple column data binding [Office development in Visual Studio]
- data binding [Office development in Visual Studio], multiple columns
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 7aba307bcd76cc055e42c11418d42f3dd0cfba1f
ms.sourcegitcommit: 9d2829dc30b6917e89762d602022915f1ca49089
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2020
ms.locfileid: "91584322"
---
# <a name="walkthrough-complex-data-binding-in-a-document-level-project"></a>チュートリアル: ドキュメントレベルのプロジェクトでの複合データバインディング
  このチュートリアルでは、ドキュメントレベルのプロジェクトでの複合データバインディングの基本について説明します。 Microsoft Office Excel ワークシートの複数のセルを、Northwind SQL Server データベースのフィールドにバインドできます。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

 このチュートリアルでは、次の作業について説明します。

- ブックプロジェクトにデータソースを追加します。

- ワークシートにデータバインドコントロールを追加する。

- データの変更をデータベースに保存し直しています。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)] または [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)]。

- Northwind SQL Server サンプルデータベースを使用したサーバーへのアクセス。

- SQL Server データベースに対する読み取りと書き込みの権限。

## <a name="create-a-new-project"></a>新しいプロジェクトを作成する
 最初の手順では、Excel ブックプロジェクトを作成します。

### <a name="to-create-a-new-project"></a>新しいプロジェクトを作成するには

1. 「 **My 複合 Data Binding**」という名前の Excel ブックプロジェクトを作成します。 ウィザードで、[ **新しいドキュメントの作成**] を選択します。

     詳細については、「 [How to: Create Office Projects in Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md)」を参照してください。

     新しい Excel ブックがデザイナーで開き、 **[My Complex Data Binding** ] プロジェクトが **ソリューションエクスプローラー**に追加されます。

## <a name="create-the-data-source"></a>データソースを作成する
 **[データ ソース]** ウィンドウを使用して、型指定されたデータセットをプロジェクトに追加します。

### <a name="to-create-the-data-source"></a>データ ソースを作成するには

1. [**データソース**] ウィンドウが表示されていない場合は、メニューバーの [ **View**  >  **他の Windows**  >  **データソース**の表示] をクリックして表示します。

2. **[新しいデータ ソースの追加]** をクリックして **データ ソース構成ウィザード**を開始します。

3. [ **データベース** ] を選択し、[ **次へ**] をクリックします。

4. Northwind サンプル SQL Server データベースへのデータ接続を選択するか、[ **新しい接続** ] ボタンを使用して新しい接続を追加します。

5. 接続を選択または作成したら、[ **次へ**] をクリックします。

6. 選択されている場合は、接続を保存するオプションをオフにして、[ **次へ**] をクリックします。

7. [**データベースオブジェクト**] ウィンドウで、[**テーブル**] ノードを展開します。

8. **Employees**テーブルの横にあるチェックボックスをオンにします。

9. **[完了]** をクリックします。

   [**データソース**] ウィンドウに [ **Employees** ] テーブルが追加されます。 また、 **ソリューションエクスプローラー**に表示される、型指定されたデータセットをプロジェクトに追加します。

## <a name="add-controls-to-the-worksheet"></a>ワークシートにコントロールを追加する
 ブックを開くと、ワークシートに **Employees** テーブルが表示されます。 ユーザーは、データに変更を加えた後、ボタンをクリックすることによって、変更内容をデータベースに保存することができます。

 ワークシートをテーブルに自動的にバインドするには、 <xref:Microsoft.Office.Tools.Excel.ListObject> [ **データソース** ] ウィンドウからワークシートにコントロールを追加します。 変更を保存するためのオプションをユーザーに付与するには、 <xref:System.Windows.Forms.Button> **ツールボックス**からコントロールを追加します。

#### <a name="to-add-a-list-object"></a>リストオブジェクトを追加するには

1. **Sheet1**が表示された状態で、Visual Studio デザイナーで **[My Complex Data Binding.xlsx** ] ブックが開いていることを確認します。

2. [ **データソース** ] ウィンドウを開き、[ **Employees** ] ノードを選択します。

3. 表示されるドロップダウン矢印をクリックします。

4. ドロップダウンリストから [ **ListObject** ] を選択します。

5. **Employees**テーブルをセル**A6**にドラッグします。

     <xref:Microsoft.Office.Tools.Excel.ListObject>という名前のコントロール `EmployeesListObject` がセル**A6**に作成されます。 同時に、と <xref:System.Windows.Forms.BindingSource> いう名前 `EmployeesBindingSource` のテーブルアダプターと <xref:System.Data.DataSet> インスタンスがプロジェクトに追加されます。 コントロールは、にバインドされ <xref:System.Windows.Forms.BindingSource> 、さらにインスタンスにバインドされ <xref:System.Data.DataSet> ます。

### <a name="to-add-a-button"></a>ボタンを追加するには

1. **ツールボックス**の [**コモンコントロール**] タブから、 <xref:System.Windows.Forms.Button> ワークシートのセル**A4**にコントロールを追加します。

   次の手順では、ワークシートが開いたときにボタンにテキストを追加します。

## <a name="initialize-the-control"></a>コントロールを初期化します
 イベントハンドラーのボタンにテキストを追加 <xref:Microsoft.Office.Tools.Excel.Worksheet.Startup> します。

### <a name="to-initialize-the-control"></a>コントロールを初期化するには

1. **ソリューションエクスプローラー**で、[ **Sheet1** ] または [ **Sheet1.cs**] を右クリックし、ショートカットメニューの [**コードの表示**] をクリックします。

2. 次のコードをメソッドに追加して `Sheet1_Startup` 、b のテキストを設定し `utton` ます。

    [!code-csharp[Trin_VstcoreDataExcel#8](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet3.cs#8)]
    [!code-vb[Trin_VstcoreDataExcel#8](../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet3.vb#8)]

3. C# の場合のみ、イベントのイベントハンドラーを <xref:System.Windows.Forms.Control.Click> メソッドに追加し `Sheet1_Startup` ます。

    [!code-csharp[Trin_VstcoreDataExcel#9](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet3.cs#9)]

   次に、ボタンのイベントを処理するコードを追加 <xref:System.Windows.Forms.Control.Click> します。

## <a name="save-changes-to-the-database"></a>変更をデータベースに保存する
 データは、明示的にデータベースに保存されるまで、ローカルデータセットにのみ存在します。

### <a name="to-save-changes-to-the-database"></a>変更をデータベースに保存するには

1. のイベントのイベントハンドラーを追加 <xref:System.Windows.Forms.Control.Click> し、 `button` 次のコードを追加して、データセットに加えられたすべての変更をデータベースに戻します。

     [!code-csharp[Trin_VstcoreDataExcel#10](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet3.cs#10)]
     [!code-vb[Trin_VstcoreDataExcel#10](../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet3.vb#10)]

## <a name="test-the-application"></a>アプリケーションをテストする
 ブックをテストして、データが想定どおりに表示されること、およびリストオブジェクト内のデータを操作できることを確認できるようになりました。

### <a name="to-test-the-data-binding"></a>データバインディングをテストするには

- **F5**キーを押します。

     ブックが開いたときに、リストオブジェクトに **Employees** テーブルのデータが格納されていることを確認します。

### <a name="to-modify-data"></a>データを変更するには

1. 「**西脇**」という名前を含むセル**B7**をクリックします。

2. 「 **Anderson**」という名前 **を入力し、enter キーを**押します。

### <a name="to-modify-a-column-header"></a>列ヘッダーを変更するには

1. 列ヘッダー **LastName**を含むセルをクリックします。

2. 2つの単語の間にスペースを含め、**姓**を入力し **、enter キーを押します。**

### <a name="to-save-data"></a>データを保存するには

1. ワークシートの [ **保存** ] をクリックします。

2. Excel を終了します。 行った変更を保存するように求められたら、[ **いいえ** ] をクリックします。

3. **F5**キーを押して、プロジェクトを再度実行します。

     List オブジェクトには、 **Employees** テーブルのデータが格納されます。

4. セル **B7** の名前は引き続き **Anderson**であることに注意してください。これは、これまでに加えたデータ変更であり、データベースに保存されています。 列ヘッダーがデータベースにバインドされておらず、ワークシートに加えた変更が保存されていないため、列ヘッダー **LastName** は空白を使用せずに元のフォームに戻されます。

### <a name="to-add-new-rows"></a>新しい行を追加するには

1. リストオブジェクト内のセルを選択します。

    新しい行が一覧の一番下に表示され、 **\*** 新しい行の最初のセルにアスタリスク () が付きます。

2. 空の行に次の情報を追加します。

   |EmployeeID|LastName|FirstName|タイトル|
   |----------------|--------------|---------------|-----------|
   |10|Ito|Shu|営業マネージャー|

### <a name="to-delete-rows"></a>行を削除するには

- ワークシートの左端にある 16 (行 16) を右クリックし、[ **削除**] をクリックします。

### <a name="to-sort-the-rows-in-the-list"></a>リスト内の行を並べ替えるには

1. リスト内のセルを選択します。

     矢印ボタンは各列ヘッダーに表示されます。

2. [ **Last Name** ] 列ヘッダーの矢印ボタンをクリックします。

3. [ **昇順で並べ替え**] をクリックします。

     行は、姓のアルファベット順に並べ替えられます。

### <a name="to-filter-information"></a>情報をフィルター処理するには

1. リスト内のセルを選択します。

2. [ **タイトル** ] 列のヘッダーにある矢印ボタンをクリックします。

3. [ **営業担当者**] をクリックします。

     一覧には、 **Sales 担当者** が [ **タイトル** ] 列に表示されている行のみが表示されます。

4. **Title**列ヘッダーの矢印ボタンをもう一度クリックします。

5. [ **(すべて)**] をクリックします。

     フィルター処理が削除され、すべての行が表示されます。

## <a name="next-steps"></a>次の手順
 このチュートリアルでは、データベース内のテーブルをリストオブジェクトにバインドする方法の基本について説明します。 ここでは、次の作業を行います。

- データをキャッシュして、オフラインで使用できるようにします。 詳細については、「 [方法: オフラインまたはサーバー上で使用するデータをキャッシュ](../vsto/how-to-cache-data-for-use-offline-or-on-a-server.md)する」を参照してください。

- ソリューションを展開する。 詳細については、「 [Office ソリューションの配置](../vsto/deploying-an-office-solution.md)」を参照してください。

- フィールドとテーブルの間にマスター/詳細関係を作成します。 詳細については、「 [チュートリアル: キャッシュされたデータセットを使用してマスター詳細関係を作成](../vsto/walkthrough-creating-a-master-detail-relation-using-a-cached-dataset.md)する」を参照してください。

## <a name="see-also"></a>関連項目
- [Office ソリューションのコントロールにデータをバインドする](../vsto/binding-data-to-controls-in-office-solutions.md)
- [Office ソリューションのデータ](../vsto/data-in-office-solutions.md)
- [チュートリアル: ドキュメントレベルのプロジェクトでの単純データバインディング](../vsto/walkthrough-simple-data-binding-in-a-document-level-project.md)
