---
title: データセットのクエリ
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
ms.assetid: 7b1a91cf-8b5a-4fc0-ac36-0dc2d336fa1b
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 4080866de58e17c5e11ed01d61740c2f83aed9a7
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75586342"
---
# <a name="query-datasets"></a>データセットのクエリ
データセット内の特定のレコードを検索するには、DataTable の `FindBy` メソッドを使用し、テーブルの Rows コレクションをループ処理する独自の foreach ステートメントを記述するか、 [LINQ to DataSet](/dotnet/framework/data/adonet/linq-to-dataset)を使用します。

## <a name="dataset-case-sensitivity"></a>データセットの大文字と小文字の区別
データセット内では、テーブル名と列名は既定で大文字と小文字が区別されません。つまり、"Customers" というデータセット内のテーブルは "customers" と呼ばれることもあります。 これは、SQL Server を含む多くのデータベースの名前付け規則に一致します。 SQL Server の既定の動作では、データ要素の名前を大文字小文字のみで区別することはできません。

> [!NOTE]
> データセットとは異なり、XML ドキュメントでは大文字と小文字が区別されるため、スキーマで定義されているデータ要素の名前では大文字と小文字が区別されます。 たとえば、スキーマプロトコルでは、"Customers" という名前のテーブルと "customers" という別のテーブルを定義できます。 これにより、大文字と小文字のみが異なる要素を含むスキーマが dataset クラスの生成に使用されるときに、名前の競合が発生する可能性があります。

ただし、大文字と小文字の区別は、データセット内でのデータの解釈方法によって決まります。 たとえば、データセットテーブルのデータをフィルター処理する場合、比較で大文字と小文字が区別されるかどうかによって、検索条件によって異なる結果が返されることがあります。 データセットの <xref:System.Data.DataSet.CaseSensitive%2A> プロパティを設定することによって、フィルター処理、検索、および並べ替えの大文字と小文字の区別を制御できます。 データセット内のすべてのテーブルは、既定でこのプロパティの値を継承します。 (テーブルの <xref:System.Data.DataTable.CaseSensitive%2A> プロパティを設定して、個々のテーブルに対してこのプロパティをオーバーライドできます)。

## <a name="locate-a-specific-row-in-a-data-table"></a>データテーブル内の特定の行の検索

#### <a name="to-find-a-row-in-a-typed-dataset-with-a-primary-key-value"></a>主キーの値を使用して型指定されたデータセット内の行を検索するには

- 行を検索するには、テーブルの主キーを使用する、厳密に型指定された `FindBy` メソッドを呼び出します。

     次の例では、`CustomerID` 列が `Customers` テーブルの主キーです。 これは、生成された `FindBy` メソッドが `FindByCustomerID`であることを意味します。 この例では、生成された `FindBy` メソッドを使用して、特定の <xref:System.Data.DataRow> を変数に割り当てる方法を示します。

     [!code-csharp[VbRaddataEditing#18](../data-tools/codesnippet/CSharp/query-datasets_1.cs)]
     [!code-vb[VbRaddataEditing#18](../data-tools/codesnippet/VisualBasic/query-datasets_1.vb)]

#### <a name="to-find-a-row-in-an-untyped-dataset-with-a-primary-key-value"></a>主キーの値を持つ型指定されていないデータセット内の行を検索するには

- <xref:System.Data.DataRowCollection> コレクションの <xref:System.Data.DataRowCollection.Find%2A> メソッドを呼び出して、プライマリキーをパラメーターとして渡します。

     次の例は、`foundRow` という名前の新しい行を宣言し、<xref:System.Data.DataRowCollection.Find%2A> メソッドの戻り値を割り当てる方法を示しています。 主キーが見つかった場合は、列インデックス1の内容がメッセージボックスに表示されます。

     [!code-csharp[VbRaddataEditing#19](../data-tools/codesnippet/CSharp/query-datasets_2.cs)]
     [!code-vb[VbRaddataEditing#19](../data-tools/codesnippet/VisualBasic/query-datasets_2.vb)]

## <a name="find-rows-by-column-values"></a>列の値で行を検索

#### <a name="to-find-rows-based-on-the-values-in-any-column"></a>任意の列の値に基づいて行を検索するには

- データテーブルは <xref:System.Data.DataTable.Select%2A> メソッドを使用して作成されます。このメソッドは、<xref:System.Data.DataTable.Select%2A> メソッドに渡される式に基づいて <xref:System.Data.DataRow>の配列を返します。 有効な式の作成の詳細については、<xref:System.Data.DataColumn.Expression%2A> プロパティに関するページの「式の構文」セクションを参照してください。

     次の例は、<xref:System.Data.DataTable> の <xref:System.Data.DataTable.Select%2A> メソッドを使用して特定の行を検索する方法を示しています。

     [!code-csharp[VbRaddataEditing#20](../data-tools/codesnippet/CSharp/query-datasets_3.cs)]
     [!code-vb[VbRaddataEditing#20](../data-tools/codesnippet/VisualBasic/query-datasets_3.vb)]

## <a name="access-related-records"></a>関連レコードへのアクセス
データセット内のテーブルが関連付けられている場合、<xref:System.Data.DataRelation> オブジェクトは、関連するレコードを別のテーブルで使用できるようにすることができます。 たとえば、`Customers` テーブルと `Orders` テーブルを含むデータセットを使用できるようにすることができます。

親テーブルの <xref:System.Data.DataRow> の <xref:System.Data.DataRow.GetChildRows%2A> メソッドを呼び出すことによって、<xref:System.Data.DataRelation> オブジェクトを使用して関連レコードを検索できます。 このメソッドは、関連する子レコードの配列を返します。 または、子テーブルの <xref:System.Data.DataRow> の <xref:System.Data.DataRow.GetParentRow%2A> メソッドを呼び出すこともできます。 このメソッドは、親テーブルから単一の <xref:System.Data.DataRow> を返します。

このページでは、型指定されたデータセットを使用する例を示します。 型指定されていないデータセット内のリレーションシップのナビゲートの詳細については、「 [datarelation のナビゲート](/dotnet/framework/data/adonet/dataset-datatable-dataview/navigating-datarelations)

> [!NOTE]
> Windows フォームアプリケーションで作業していて、データバインディング機能を使用してデータを表示している場合は、デザイナーで生成されたフォームによってアプリケーションに十分な機能が提供されることがあります。 詳細については、「 [Visual Studio でのデータへのコントロールのバインド](../data-tools/bind-controls-to-data-in-visual-studio.md)」を参照してください。 具体的には、「[データセット内のリレーションシップ](relationships-in-datasets.md)」を参照してください。

次のコード例は、型指定されたデータセット内の上下関係を移動する方法を示しています。 このコード例では、型指定された <xref:System.Data.DataRow>s (`NorthwindDataSet.OrdersRow`) および生成された FindBy*PrimaryKey* (`FindByCustomerID`) メソッドを使用して目的の行を検索し、関連するレコードを返します。 これらの例は、次のものがある場合にのみ、正しくコンパイルされて実行されます。

- `Customers` テーブルを持つ `NorthwindDataSet` という名前のデータセットのインスタンス。

- `Orders` テーブルです。

- 2つのテーブルを関連付ける `FK_Orders_Customers`という名前のリレーションシップ。

また、返されるレコードのデータを両方のテーブルに格納する必要があります。

#### <a name="to-return-the-child-records-of-a-selected-parent-record"></a>選択した親レコードの子レコードを取得するには

- 特定の `Customers` データ行の <xref:System.Data.DataRow.GetChildRows%2A> メソッドを呼び出し、`Orders` テーブルから行の配列を返します。

     [!code-csharp[VbRaddataDatasets#6](../data-tools/codesnippet/CSharp/query-datasets_4.cs)]
     [!code-vb[VbRaddataDatasets#6](../data-tools/codesnippet/VisualBasic/query-datasets_4.vb)]

#### <a name="to-return-the-parent-record-of-a-selected-child-record"></a>選択した子レコードの親レコードを取得するには

- 特定の `Orders` データ行の <xref:System.Data.DataRow.GetParentRow%2A> メソッドを呼び出し、`Customers` テーブルから1つの行を返します。

     [!code-csharp[VbRaddataDatasets#7](../data-tools/codesnippet/CSharp/query-datasets_5.cs)]
     [!code-vb[VbRaddataDatasets#7](../data-tools/codesnippet/VisualBasic/query-datasets_5.vb)]

## <a name="see-also"></a>関連項目

- [Visual Studio のデータセット ツール](../data-tools/dataset-tools-in-visual-studio.md)
