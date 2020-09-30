---
title: 'チュートリアル: VSTO アドインプロジェクトでの複合データバインディング'
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data binding [Office development in Visual Studio], Excel
- data [Office development in Visual Studio], binding data
- complex data [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: c0d65bd96a3860070addc6dc05a791d71959f5ea
ms.sourcegitcommit: 9d2829dc30b6917e89762d602022915f1ca49089
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2020
ms.locfileid: "91585042"
---
# <a name="walkthrough-complex-data-binding-in-vsto-add-in-project"></a>チュートリアル: VSTO アドインプロジェクトでの複合データバインディング
  VSTO アドイン プロジェクトでは、ホスト コントロールと Windows フォーム コントロールにデータをバインドできます。 このチュートリアルでは、Microsoft Office Excel ワークシートにコントロールを追加して、そのコントロールを実行時にデータにバインドする方法を示します。

 [!INCLUDE[appliesto_xlallapp](../vsto/includes/appliesto-xlallapp-md.md)]

 このチュートリアルでは、次の作業について説明します。

- 実行時に <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールをワークシートに追加する。

- コントロールをデータセットのインスタンスに接続する <xref:System.Windows.Forms.BindingSource> を作成する。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)] または [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)]。

- `AdventureWorksLT` サンプル データベースがアタッチされた SQL Server 2005 または SQL Server 2005 Express の実行中のインスタンスへのアクセス。 `AdventureWorksLT`データベースは[SQL Server Samples GitHub リポジトリ](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)からダウンロードできます。 データベースをアタッチする方法について詳しくは、次のトピックをご覧ください。

  - SQL Server Management Studio または SQL Server Management Studio Express を使用してデータベースをアタッチする方法については、「 [データベースをアタッチする方法 (SQL Server Management Studio)](/sql/relational-databases/databases/attach-a-database)」を参照してください。

  - コマンドラインを使用してデータベースをアタッチする方法については、「 [方法: SQL Server Express にデータベースファイルをアタッチ](/previous-versions/sql/)する」を参照してください。

## <a name="create-a-new-project"></a>新しいプロジェクトを作成する
 まず、Excel VSTO アドイン プロジェクトを作成します。

### <a name="to-create-a-new-project"></a>新しいプロジェクトを作成するには

1. Visual Basic または C# を使用して、 **Populating Worksheets from a Database**という名前の Excel VSTO アドイン プロジェクトを作成します。

     詳細については、「 [How to: Create Office Projects in Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md)」を参照してください。

     Visual Studio により、 `ThisAddIn.vb` ファイルまたは `ThisAddIn.cs` ファイルが開かれ、 **Populating Worksheets from a Database** プロジェクトが **ソリューション エクスプローラー**に追加されます。

## <a name="create-a-data-source"></a>データ ソースを作成する
 **[データ ソース]** ウィンドウを使用して、型指定されたデータセットをプロジェクトに追加します。

### <a name="to-add-a-typed-dataset-to-the-project"></a>型指定されたデータセットをプロジェクトに追加するには

1. [**データソース**] ウィンドウが表示されていない場合は、メニューバーの [ **View**  >  **他の Windows**  >  **データソース**の表示] をクリックして表示します。

2. **[新しいデータ ソースの追加]** をクリックして **データ ソース構成ウィザード**を開始します。

3. **[データベース]** をクリックして、 **[次へ]** をクリックします。

4. `AdventureWorksLT` データベースへの既存の接続がある場合は、その接続を選んで **[次へ]** をクリックします。

    それ以外の場合は、 **[新しい接続]** をクリックし、 **[接続の追加]** ダイアログ ボックスを使用して新しい接続を作成します。 詳細については、「 [新しい接続の追加](../data-tools/add-new-connections.md)」を参照してください。

5. **[アプリケーション構成ファイルへの接続文字列を保存]** ページで、 **[次へ]** をクリックします。

6. **[データベース オブジェクトの選択]** ページで、 **[テーブル]** を展開し、 **[Address (SalesLT)]** を選びます。

7. **[完了]** をクリックします。

    *Adventureworksltdataset.xsd*ファイルが**ソリューションエクスプローラー**に追加されます。 このファイルでは、次の項目を定義します。

   - `AdventureWorksLTDataSet`という名前の型指定されたデータセット。 このデータセットは、AdventureWorksLT データベースの **Address (SalesLT)** テーブルの内容を表します。

   - という名前の TableAdapter `AddressTableAdapter` 。 この TableAdapter を使用して、のデータの読み取りと書き込みを行うことができ `AdventureWorksLTDataSet` ます。 詳細については、「 [TableAdapter の概要](../data-tools/fill-datasets-by-using-tableadapters.md#tableadapter-overview)」を参照してください。

     これらのオブジェクトは、どちらもこのチュートリアルの後半で使用します。

## <a name="create-controls-and-bind-controls-to-data"></a>コントロールを作成し、データにコントロールをバインドする
 このチュートリアルでは、ユーザーがブックを開くとすぐに、事前に選んでおいたテーブル内のすべてのデータが <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールによって表示されます。 リスト オブジェクトは <xref:System.Windows.Forms.BindingSource> を使用してコントロールをデータベースに接続します。

 コントロールをデータにバインドする方法の詳細については、「 [データを Office ソリューションのコントロールにバインドする](../vsto/binding-data-to-controls-in-office-solutions.md)」を参照してください。

### <a name="to-add-the-list-object-dataset-and-table-adapter"></a>リスト オブジェクト、データセット、テーブル アダプターを追加するには

1. `ThisAddIn` クラスで、次のコントロールを宣言し、 `Address` データセットの `AdventureWorksLTDataSet` テーブルを表示するようにします。

     [!code-csharp[Trin_ExcelAddInDatabase#1](../vsto/codesnippet/CSharp/Trin_ExcelAddInDatabase_O12/ThisAddIn.cs#1)]
     [!code-vb[Trin_ExcelAddInDatabase#1](../vsto/codesnippet/VisualBasic/Trin_ExcelAddInDatabase_O12/ThisAddIn.vb#1)]

2. `ThisAddIn_Startup` メソッドに次のコードを追加し、データセットを初期化して、そのデータセットに `AdventureWorksLTDataSet` データセットから得た情報を設定します。

     [!code-csharp[Trin_ExcelAddInDatabase#2](../vsto/codesnippet/CSharp/Trin_ExcelAddInDatabase_O12/ThisAddIn.cs#2)]
     [!code-vb[Trin_ExcelAddInDatabase#2](../vsto/codesnippet/VisualBasic/Trin_ExcelAddInDatabase_O12/ThisAddIn.vb#2)]

3. `ThisAddIn_Startup` メソッドに次のコードを追加します。 これによりホスト項目が生成され、ワークシートの機能が拡張されます。 詳細については、「 [VSTO アドインでの実行時の Word 文書と Excel ブックの拡張](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)」を参照してください。

     [!code-csharp[Trin_ExcelAddInDatabase#3](../vsto/codesnippet/CSharp/Trin_ExcelAddInDatabase_O12/ThisAddIn.cs#3)]
     [!code-vb[Trin_ExcelAddInDatabase#3](../vsto/codesnippet/VisualBasic/Trin_ExcelAddInDatabase_O12/ThisAddIn.vb#3)]

4. 範囲を作成して <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールを追加します。

     [!code-csharp[Trin_ExcelAddInDatabase#4](../vsto/codesnippet/CSharp/Trin_ExcelAddInDatabase_O12/ThisAddIn.cs#4)]
     [!code-vb[Trin_ExcelAddInDatabase#4](../vsto/codesnippet/VisualBasic/Trin_ExcelAddInDatabase_O12/ThisAddIn.vb#4)]

5. `AdventureWorksLTDataSet` を使用して、リスト オブジェクトを <xref:System.Windows.Forms.BindingSource>にバインドします。 リスト オブジェクトにバインドする列の名前を渡します。

     [!code-csharp[Trin_ExcelAddInDatabase#5](../vsto/codesnippet/CSharp/Trin_ExcelAddInDatabase_O12/ThisAddIn.cs#5)]
     [!code-vb[Trin_ExcelAddInDatabase#5](../vsto/codesnippet/VisualBasic/Trin_ExcelAddInDatabase_O12/ThisAddIn.vb#5)]

## <a name="test-the-add-in"></a>アドインのテスト
 Excel を開くと、 <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールにより `Address` データセットの `AdventureWorksLTDataSet` テーブルから得られるデータが表示されます。

### <a name="to-test-the-vsto-add-in"></a>VSTO アドインをテストするには

- **F5**キーを押します。

     <xref:Microsoft.Office.Tools.Excel.ListObject> という名前の `addressListObject` コントロールがワークシートに作成されます。 同時に、 `adventureWorksLTDataSet` という名前のデータセット オブジェクトと、 <xref:System.Windows.Forms.BindingSource> という名前の `addressBindingSource` がプロジェクトに追加されます。 <xref:Microsoft.Office.Tools.Excel.ListObject> が <xref:System.Windows.Forms.BindingSource>にバインドされ、さらにこれがデータセット オブジェクトにバインドされます。

## <a name="see-also"></a>関連項目

- [Office ソリューションのデータ](../vsto/data-in-office-solutions.md)
- [Office ソリューションのコントロールにデータをバインドする](../vsto/binding-data-to-controls-in-office-solutions.md)
- [方法: データベースのデータをワークシートに読み込む](../vsto/how-to-populate-worksheets-with-data-from-a-database.md)
- [方法: データベースのデータをドキュメントに読み込む](../vsto/how-to-populate-documents-with-data-from-a-database.md)
- [方法: サービスのデータをドキュメントに読み込む](../vsto/how-to-populate-documents-with-data-from-services.md)
- [方法: オブジェクトのデータをドキュメントに読み込む](../vsto/how-to-populate-documents-with-data-from-objects.md)
- [方法: ワークシート内のデータベースレコードをスクロールする](../vsto/how-to-scroll-through-database-records-in-a-worksheet.md)
- [方法: ホストコントロールのデータを使用してデータソースを更新する](../vsto/how-to-update-a-data-source-with-data-from-a-host-control.md)
- [チュートリアル: ドキュメントレベルのプロジェクトでの単純データバインディング](../vsto/walkthrough-simple-data-binding-in-a-document-level-project.md)
- [チュートリアル: ドキュメントレベルのプロジェクトでの複合データバインディング](../vsto/walkthrough-complex-data-binding-in-a-document-level-project.md)
- [Office ソリューションのローカルデータベースファイルの使用の概要](../vsto/using-local-database-files-in-office-solutions-overview.md)
- [新しいデータ ソースの追加](../data-tools/add-new-data-sources.md)
- [Visual Studio でのデータへの Windows フォーム コントロールのバインド](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
- [Office ソリューションのローカルデータベースファイルの使用の概要](../vsto/using-local-database-files-in-office-solutions-overview.md)
- [BindingSource コンポーネントの概要](/dotnet/framework/winforms/controls/bindingsource-component-overview)
