---
title: '方法: ホストコントロールのデータを使用してデータソースを更新する'
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], data source updates
- data [Office development in Visual Studio], updating a data source from a document
- host controls [Office development in Visual Studio], data source updates
- Office documents [Office development in Visual Studio, data sources
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 52540f0cf94a12efda891657ec4aae9452ad6f86
ms.sourcegitcommit: 9d2829dc30b6917e89762d602022915f1ca49089
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2020
ms.locfileid: "91585120"
---
# <a name="how-to-update-a-data-source-with-data-from-a-host-control"></a>方法: ホストコントロールのデータを使用してデータソースを更新する
  ホスト コントロールをデータ ソースにバインドし、コントロール内のデータに加えられた変更でデータ ソースを更新することができます。 この処理には主に 2 つの手順があります。

1. コントロールで変更されたデータを使用して、メモリ内データ ソースを更新します。 一般に、メモリ内データ ソースは <xref:System.Data.DataSet>、 <xref:System.Data.DataTable>、またはその他のデータ オブジェクトです。

2. メモリ内データ ソースで変更されたデータを使用して、データベースを更新します。 これは、データ ソースが SQL Server や Microsoft Office Access データベースなどのバックエンド データベースに接続されている場合にのみ有効です。

   ホストコントロールとデータバインディングの詳細については、「 [ホスト項目とホストコントロールの概要](../vsto/host-items-and-host-controls-overview.md) 」および「 [Office ソリューションのコントロールへのデータのバインド](../vsto/binding-data-to-controls-in-office-solutions.md)」を参照してください。

   [!INCLUDE[appliesto_controls](../vsto/includes/appliesto-controls-md.md)]

## <a name="update-the-in-memory-data-source"></a>メモリ内データソースの更新
 既定では、単純データ バインディングを有効にしているホスト コントロール (Word 文書のコンテンツ コントロールや Excel ワークシートの名前付き範囲コントロールなど) は、データの変更内容をメモリ内データ ソースに保存しません。 つまり、エンド ユーザーがホスト コントロールの値に変更を加えてからコントロールの外に移動すると、コントロールの新しい値は自動的にはデータ ソースに保存されません。

 データ ソースにデータを保存するには、実行時に特定のイベントに応答してデータ ソースを更新するコードを記述します。または、コントロールの値が変更されたときに自動的にデータ ソースを更新するようにコントロールを構成することもできます。

 メモリ内データ ソースに <xref:Microsoft.Office.Tools.Excel.ListObject> の変更を保存する必要はありません。 <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールをデータにバインドすると、 <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールは追加のコードなしで変更内容を自動的にメモリ内データ ソースに保存します。

### <a name="to-update-the-in-memory-data-source-at-run-time"></a>実行時にメモリ内データ ソースを更新するには

- コントロールをデータ ソースにバインドする <xref:System.Windows.Forms.Binding.WriteValue%2A> オブジェクトの <xref:System.Windows.Forms.Binding> メソッドを呼び出します。

     Excel ワークシートの <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールに加えられた変更をデータ ソースに保存する例を次に示します。 この例は、 <xref:Microsoft.Office.Tools.Excel.NamedRange> という名前の `namedRange1` コントロールで <xref:Microsoft.Office.Tools.Excel.NamedRange.Value2%2A> プロパティがデータ ソースのフィールドにバインドされていることを前提としています。

     [!code-csharp[Trin_VstcoreDataExcel#1](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs#1)]
     [!code-vb[Trin_VstcoreDataExcel#1](../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb#1)]

### <a name="automatically-update-the-in-memory-data-source"></a>メモリ内データソースを自動的に更新する
 メモリ内データ ソースを自動的に更新するように、コントロールを構成することもできます。 ドキュメント レベルのプロジェクトでこれを行うには、コードまたはデザイナーを使用します。 VSTO アドインプロジェクトでは、コードを使用する必要があります。

#### <a name="to-set-a-control-to-automatically-update-the-in-memory-data-source-by-using-code"></a>コードを使用してメモリ内データ ソースを自動的に更新するようにコントロールを設定するには

1. <xref:System.Windows.Forms.Binding>コントロールをデータソースにバインドするオブジェクトの OnPropertyChanged モードを使用します。このモードには、コントロールがバインドされています。 データ ソースの更新には 2 つのオプションがあります。

   - コントロールの検証時にデータソースを更新するには、このプロパティを「system.string」に設定します。

   - コントロールのデータバインドプロパティの値が変更されたときにデータソースを更新するには、このプロパティを OnPropertyChanged に設定します。

     > [!NOTE]
     > Word ではドキュメント変更通知またはコントロール変更通知が提供されないため、OnPropertyChanged オプションは Word ホストコントロールには適用されません。 ただし、Word 文書上の Windows フォーム コントロールには、このオプションを使用できます。

     コントロールの値が変わると自動的にデータ ソースを更新するように <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールを構成する例を次に示します。 この例は、 <xref:Microsoft.Office.Tools.Excel.NamedRange> という名前の `namedRange1` コントロールで <xref:Microsoft.Office.Tools.Excel.NamedRange.Value2%2A> プロパティがデータ ソースのフィールドにバインドされていることを前提としています。

     [!code-csharp[Trin_VstcoreDataExcel#19](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs#19)]
     [!code-vb[Trin_VstcoreDataExcel#19](../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb#19)]

#### <a name="to-set-a-control-to-automatically-update-the-in-memory-data-source-by-using-the-designer"></a>デザイナーを使用してメモリ内データ ソースを自動的に更新するようにコントロールを設定するには

1. Visual Studio のデザイナーで、Word 文書または Excel ブックを開きます。

2. データ ソースの自動更新を行うコントロールをクリックします。

3. **[プロパティ]** ウィンドウで **(DataBindings)** プロパティを展開します。

4. [ **(詳細)** ] プロパティの横にある省略記号ボタン (![VisualStudioEllipsesButton スクリーンショット](../vsto/media/vbellipsesbutton.png "VisualStudioEllipsesButton スクリーンショット")) をクリックします。

5. **[フォーマットと詳細バインド]** ダイアログ ボックスで、 **[データ ソース更新モード]** ドロップダウン リストをクリックし、次の値のいずれかを選びます。

    - コントロールの検証時にデータ ソースを更新するには、 **[OnValidation]** を選びます。

    - コントロールのデータ バインド プロパティの値が変更されたときにデータ ソースを更新するには、 **[OnPropertyChanged]** を選びます。

        > [!NOTE]
        > **[OnPropertyChanged]** オプションは、Word ホスト コントロールには適用されません。Word では文書変更やコントロール変更の通知は提供されないためです。 ただし、Word 文書上の Windows フォーム コントロールには、このオプションを使用できます。

6. **[フォーマットと詳細バインド]** ダイアログ ボックスを閉じます。

## <a name="update-the-database"></a>データベースを更新する
 メモリ内データ ソースがデータベースに関連付けられている場合、データ ソースへの変更内容を使用して、データベースを更新する必要があります。 データベースの更新の詳細については、「 [データをデータベースに保存](../data-tools/save-data-back-to-the-database.md)  し、TableAdapter を使用して [データを更新](../data-tools/update-data-by-using-a-tableadapter.md) する」を参照してください。

### <a name="to-update-the-database"></a>データベースを更新するには

1. コントロールの <xref:System.Windows.Forms.BindingSource.EndEdit%2A> の <xref:System.Windows.Forms.BindingSource> メソッドを呼び出します。

     デザイン時に文書またはブックにデータ バインド コントロールを追加すると、 <xref:System.Windows.Forms.BindingSource> が自動的に生成されます。 <xref:System.Windows.Forms.BindingSource> によって、コントロールはプロジェクト内の型指定されたデータセットに接続されます。 詳細については、「 [BindingSource コンポーネントの概要](/dotnet/framework/winforms/controls/bindingsource-component-overview)」を参照してください。

     次のコード例は、プロジェクトに <xref:System.Windows.Forms.BindingSource> という名前の `customersBindingSource`が含まれていることを前提としています。

     [!code-csharp[Trin_VstcoreDataExcel#20](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs#20)]
     [!code-vb[Trin_VstcoreDataExcel#20](../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb#20)]

2. `Update`プロジェクトで生成された TableAdapter のメソッドを呼び出します。

     デザイン時に文書またはブックにデータバインドコントロールを追加すると、TableAdapter が自動的に生成されます。 TableAdapter は、プロジェクト内の型指定されたデータセットをデータベースに接続します。 詳細については、「 [TableAdapter の概要](../data-tools/fill-datasets-by-using-tableadapters.md#tableadapter-overview)」を参照してください。

     次のコード例では、Northwind データベースの Customers テーブルへの接続があり、プロジェクトにという名前の TableAdapter とと `customersTableAdapter` いう名前の型指定されたデータセットが含まれていることを前提としてい `northwindDataSet` ます。

     [!code-csharp[Trin_VstcoreDataExcel#21](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs#21)]
     [!code-vb[Trin_VstcoreDataExcel#21](../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb#21)]

## <a name="see-also"></a>関連項目
- [Office ソリューションのコントロールにデータをバインドする](../vsto/binding-data-to-controls-in-office-solutions.md)
- [データをデータベースに保存する](../data-tools/save-data-back-to-the-database.md)
- [TableAdapter を使用してデータを更新する](../data-tools/update-data-by-using-a-tableadapter.md)
- [方法: ワークシート内のデータベースレコードをスクロールする](../vsto/how-to-scroll-through-database-records-in-a-worksheet.md)
- [方法: データベースのデータをワークシートに読み込む](../vsto/how-to-populate-worksheets-with-data-from-a-database.md)
- [方法: オブジェクトのデータをドキュメントに読み込む](../vsto/how-to-populate-documents-with-data-from-objects.md)
- [方法: データベースのデータをドキュメントに読み込む](../vsto/how-to-populate-documents-with-data-from-a-database.md)
- [方法: サービスのデータをドキュメントに読み込む](../vsto/how-to-populate-documents-with-data-from-services.md)
