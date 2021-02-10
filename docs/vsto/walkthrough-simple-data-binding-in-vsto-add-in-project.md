---
title: 'チュートリアル: VSTO アドインプロジェクトでの単純データバインディング'
description: Microsoft Word 文書にコントロールを追加し、実行時にコントロールをデータにバインドする方法について説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data [Office development in Visual Studio], binding data
- data binding [Office development in Visual Studio], Word
- data [Office development in Visual Studio], simple binding data
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: e6162c8cc508c1eaada6c2be90bd28d430779cb0
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99937369"
---
# <a name="walkthrough-simple-data-binding-in-vsto-add-in-project"></a>チュートリアル: VSTO アドインプロジェクトでの単純データバインディング

VSTO アドイン プロジェクトでは、ホスト コントロールと Windows フォーム コントロールにデータをバインドできます。 このチュートリアルでは、実行時に Microsoft Office Word 文書にコントロールを追加して、そのコントロールをデータにバインドする方法を示します。

[!INCLUDE[appliesto_wdallapp](../vsto/includes/appliesto-wdallapp-md.md)]

このチュートリアルでは、次の作業について説明します。

- 実行時にドキュメントに <xref:Microsoft.Office.Tools.Word.ContentControl> を追加する。

- コントロールをデータセットのインスタンスに接続する <xref:System.Windows.Forms.BindingSource> を作成する。

- ユーザーがレコードをスクロールしてレコードをコントロールに表示できるようにする。

[!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>必須コンポーネント

このチュートリアルを実行するには、次のコンポーネントが必要です。

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)] または [!INCLUDE[Word_14_short](../vsto/includes/word-14-short-md.md)]。

- `AdventureWorksLT` サンプル データベースがアタッチされた SQL Server 2005 または SQL Server 2005 Express の実行中のインスタンスへのアクセス。 `AdventureWorksLT`データベースは[SQL Server Samples GitHub リポジトリ](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)からダウンロードできます。 データベースをアタッチする方法について詳しくは、次のトピックをご覧ください。

  - SQL Server Management Studio または SQL Server Management Studio Express を使用してデータベースをアタッチする方法については、「 [データベースをアタッチする方法 (SQL Server Management Studio)](/sql/relational-databases/databases/attach-a-database)」を参照してください。

  - コマンドラインを使用してデータベースをアタッチする方法については、「 [方法: SQL Server Express にデータベースファイルをアタッチ](/previous-versions/sql/)する」を参照してください。

## <a name="create-a-new-project"></a>新しいプロジェクトを作成する

まず、Word VSTO アドイン プロジェクトを作成します。

### <a name="to-create-a-new-project"></a>新しいプロジェクトを作成するには

1. Visual Basic または C# を使用して、 **Populating Documents from a Database** という名前の Word VSTO アドイン プロジェクトを作成します。

     詳細については、「 [方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)」を参照してください。

     Visual Studio によって、 *ThisAddIn* ファイルまたは *ThisAddIn.cs* ファイルが開かれ、データベースプロジェクトの **ドキュメント** が **ソリューションエクスプローラー** に追加されます。

2. プロジェクトがまたはを対象としている場合は、 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] *Microsoft.Office.Tools.Word.v4.0.Utilities.dll* アセンブリへの参照を追加します。 この参照は、このチュートリアルの後半でプログラムを使用して Windows フォーム コントロールをドキュメントに追加するのに必要です。

## <a name="create-a-data-source"></a>データ ソースを作成する

**[データ ソース]** ウィンドウを使用して、型指定されたデータセットをプロジェクトに追加します。

### <a name="to-add-a-typed-dataset-to-the-project"></a>型指定されたデータセットをプロジェクトに追加するには

1. [**データソース**] ウィンドウが表示されていない場合は、メニューバーの [   >  **他の Windows**  >  **データソース** の表示] をクリックして表示します。

2. **[新しいデータ ソースの追加]** をクリックして **データ ソース構成ウィザード** を開始します。

3. **[データベース]** をクリックして、 **[次へ]** をクリックします。

4. `AdventureWorksLT` データベースへの既存の接続がある場合は、その接続を選んで **[次へ]** をクリックします。

    それ以外の場合は、 **[新しい接続]** をクリックし、 **[接続の追加]** ダイアログ ボックスを使用して新しい接続を作成します。 詳細については、「 [新しい接続の追加](../data-tools/add-new-connections.md)」を参照してください。

5. **[アプリケーション構成ファイルへの接続文字列を保存]** ページで、 **[次へ]** をクリックします。

6. **[データベース オブジェクトの選択]** ページで、 **[テーブル]** を展開し、 **[Customer (SalesLT)]** を選びます。

7. **[Finish]** をクリックします。

    *Adventureworksltdataset.xsd* ファイルが **ソリューションエクスプローラー** に追加されます。 このファイルでは、次の項目を定義します。

   - `AdventureWorksLTDataSet`という名前の型指定されたデータセット。 このデータセットは、AdventureWorksLT データベースの **Customer (SalesLT)** テーブルの内容を表します。

   - という名前の TableAdapter `CustomerTableAdapter` 。 この TableAdapter を使用して、のデータの読み取りと書き込みを行うことができ `AdventureWorksLTDataSet` ます。 詳細については、「 [TableAdapter の概要](../data-tools/fill-datasets-by-using-tableadapters.md#tableadapter-overview)」を参照してください。

     これらのオブジェクトは、どちらもこのチュートリアルの後半で使用します。

## <a name="create-controls-and-binding-controls-to-data"></a>コントロールを作成し、データにコントロールをバインドする

このチュートリアルでは、データベースレコードを表示するためのインターフェイスは基本的なものであり、ドキュメント内に作成されます。 1 つの <xref:Microsoft.Office.Tools.Word.ContentControl> には一度に 1 つのデータベース レコードが表示されます。2 つの <xref:Microsoft.Office.Tools.Word.Controls.Button> コントロールを使用してレコードを前後にスクロールできます。 コンテンツ コントロールは <xref:System.Windows.Forms.BindingSource> を使用して、データベースに接続します。

コントロールをデータにバインドする方法の詳細については、「 [データを Office ソリューションのコントロールにバインドする](../vsto/binding-data-to-controls-in-office-solutions.md)」を参照してください。

### <a name="to-create-the-interface-in-the-document"></a>ドキュメントでインターフェイスを作成するには

1. `ThisAddIn` クラスで、次のコントロールを宣言し、 `Customer` データベースの `AdventureWorksLTDataSet` テーブルをスクロールして表示できるようにします。

     [!code-vb[Trin_WordAddInDatabase#1](../vsto/codesnippet/VisualBasic/trin_wordaddindatabase/ThisAddIn.vb#1)]
     [!code-csharp[Trin_WordAddInDatabase#1](../vsto/codesnippet/CSharp/trin_wordaddindatabase/ThisAddIn.cs#1)]

2. `ThisAddIn_Startup` メソッドに次のコードを追加し、データセットを初期化して、そのデータセットに `AdventureWorksLTDataSet` データベースから得た情報を設定します。

     [!code-vb[Trin_WordAddInDatabase#2](../vsto/codesnippet/VisualBasic/trin_wordaddindatabase/ThisAddIn.vb#2)]
     [!code-csharp[Trin_WordAddInDatabase#2](../vsto/codesnippet/CSharp/trin_wordaddindatabase/ThisAddIn.cs#2)]

3. `ThisAddIn_Startup` メソッドに次のコードを追加します。 これによりホスト項目が生成され、ドキュメントの機能が拡張されます。 詳細については、「 [VSTO アドインでの実行時の Word 文書と Excel ブックの拡張](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)」を参照してください。

     [!code-vb[Trin_WordAddInDatabase#3](../vsto/codesnippet/VisualBasic/trin_wordaddindatabase/ThisAddIn.vb#3)]
     [!code-csharp[Trin_WordAddInDatabase#3](../vsto/codesnippet/CSharp/trin_wordaddindatabase/ThisAddIn.cs#3)]

4. ドキュメントの先頭でいくつかの範囲を定義します。 これらの範囲は、テキストを挿入し、コントロールを配置する場所を指定します。

     [!code-vb[Trin_WordAddInDatabase#4](../vsto/codesnippet/VisualBasic/trin_wordaddindatabase/ThisAddIn.vb#4)]
     [!code-csharp[Trin_WordAddInDatabase#4](../vsto/codesnippet/CSharp/trin_wordaddindatabase/ThisAddIn.cs#4)]

5. 以前に定義された範囲にインターフェイス コントロールを追加します。

     [!code-vb[Trin_WordAddInDatabase#5](../vsto/codesnippet/VisualBasic/trin_wordaddindatabase/ThisAddIn.vb#5)]
     [!code-csharp[Trin_WordAddInDatabase#5](../vsto/codesnippet/CSharp/trin_wordaddindatabase/ThisAddIn.cs#5)]

6. `AdventureWorksLTDataSet` を使用してコンテンツ コントロールを <xref:System.Windows.Forms.BindingSource>にバインドします。 C# 開発者の場合、2 つのイベント ハンドラーを <xref:Microsoft.Office.Tools.Word.Controls.Button> コントロールに追加します。

     [!code-vb[Trin_WordAddInDatabase#6](../vsto/codesnippet/VisualBasic/trin_wordaddindatabase/ThisAddIn.vb#6)]
     [!code-csharp[Trin_WordAddInDatabase#6](../vsto/codesnippet/CSharp/trin_wordaddindatabase/ThisAddIn.cs#6)]

7. データベース レコード間を移動するには、次のコードを追加します。

     [!code-vb[Trin_WordAddInDatabase#7](../vsto/codesnippet/VisualBasic/trin_wordaddindatabase/ThisAddIn.vb#7)]
     [!code-csharp[Trin_WordAddInDatabase#7](../vsto/codesnippet/CSharp/trin_wordaddindatabase/ThisAddIn.cs#7)]

## <a name="test-the-add-in"></a>アドインのテスト

Word を開くと、コンテンツ コントロールに `AdventureWorksLTDataSet` データセットからのデータが表示されます。 **[次へ]** と **[前へ]** ボタンをクリックして、データベース レコードをスクロールします。

### <a name="to-test-the-vsto-add-in"></a>VSTO アドインをテストするには

1. **F5** キーを押します。

     `customerContentControl` という名前のコンテンツ コントロールが作成され、データが読み込まれます。 同時に、 `adventureWorksLTDataSet` という名前のデータセット オブジェクトと、 <xref:System.Windows.Forms.BindingSource> という名前の `customerBindingSource` がプロジェクトに追加されます。 <xref:Microsoft.Office.Tools.Word.ContentControl> が <xref:System.Windows.Forms.BindingSource>にバインドされ、さらにこれがデータセット オブジェクトにバインドされます。

2. **[次へ]** ボタンと **[前へ]** ボタンをクリックして、データベース レコードをスクロールします。

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
- [方法: オブジェクトのデータをドキュメントに読み込む](../vsto/how-to-populate-documents-with-data-from-objects.md)
- [方法: ホストコントロールのデータを使用してデータソースを更新する](../vsto/how-to-update-a-data-source-with-data-from-a-host-control.md)
- [Office ソリューションのローカルデータベースファイルの使用の概要](../vsto/using-local-database-files-in-office-solutions-overview.md)
- [BindingSource コンポーネントの概要](/dotnet/framework/winforms/controls/bindingsource-component-overview)
