---
title: データセットのクエリ
description: クエリデータセットについて理解する。 データセットの大文字小文字の区別について説明します。 データテーブル内の特定の行を検索し、列の値で行を検索して、関連レコードにアクセスします。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
ms.assetid: 7b1a91cf-8b5a-4fc0-ac36-0dc2d336fa1b
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: c5f085cae185a48f3d41c6fa4bca5cad7afb46b3
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106215800"
---
# <a name="query-datasets"></a>データセットのクエリ
データセット内の特定のレコードを検索するには、 `FindBy` DataTable に対してメソッドを使用し、テーブルの Rows コレクションをループ処理する独自の foreach ステートメントを記述するか、 [LINQ to DataSet](/dotnet/framework/data/adonet/linq-to-dataset)を使用します。

## <a name="dataset-case-sensitivity"></a>データセットの大文字と小文字の区別
データセット内では、テーブル名と列名は既定で大文字と小文字が区別されません。つまり、"Customers" というデータセット内のテーブルは "customers" と呼ばれることもあります。 これは、SQL Server を含む多くのデータベースの名前付け規則に一致します。 SQL Server の既定の動作では、データ要素の名前を大文字小文字のみで区別することはできません。

> [!NOTE]
> データセットとは異なり、XML ドキュメントでは大文字と小文字が区別されるため、スキーマで定義されているデータ要素の名前では大文字と小文字が区別されます。 たとえば、スキーマプロトコルでは、"Customers" という名前のテーブルと "customers" という別のテーブルを定義できます。 これにより、大文字と小文字のみが異なる要素を含むスキーマが dataset クラスの生成に使用されるときに、名前の競合が発生する可能性があります。

ただし、大文字と小文字の区別は、データセット内でのデータの解釈方法によって決まります。 たとえば、データセットテーブルのデータをフィルター処理する場合、比較で大文字と小文字が区別されるかどうかによって、検索条件によって異なる結果が返されることがあります。 データセットのプロパティを設定することにより、フィルター処理、検索、および並べ替えの大文字と小文字の区別を制御できます <xref:System.Data.DataSet.CaseSensitive%2A> 。 データセット内のすべてのテーブルは、既定でこのプロパティの値を継承します。 (テーブルのプロパティを設定することによって、個々のテーブルに対してこのプロパティをオーバーライドでき <xref:System.Data.DataTable.CaseSensitive%2A> ます)。

## <a name="locate-a-specific-row-in-a-data-table"></a>データテーブル内の特定の行の検索

#### <a name="to-find-a-row-in-a-typed-dataset-with-a-primary-key-value"></a>主キーの値を使用して型指定されたデータセット内の行を検索するには

- 行を検索するには、 `FindBy` テーブルの主キーを使用する厳密に型指定されたメソッドを呼び出します。

     次の例では、 `CustomerID` 列がテーブルの主キーです `Customers` 。 これは、生成されたメソッドがであることを意味 `FindBy` `FindByCustomerID` します。 この例では、生成されたメソッドを使用して、特定のを変数に割り当てる方法を示し <xref:System.Data.DataRow> `FindBy` ます。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet18":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet18":::

#### <a name="to-find-a-row-in-an-untyped-dataset-with-a-primary-key-value"></a>主キーの値を持つ型指定されていないデータセット内の行を検索するには

- <xref:System.Data.DataRowCollection.Find%2A>コレクションのメソッドを呼び出し <xref:System.Data.DataRowCollection> 、プライマリキーをパラメーターとして渡します。

     次の例は、という新しい行を宣言 `foundRow` し、メソッドの戻り値を割り当てる方法を示して <xref:System.Data.DataRowCollection.Find%2A> います。 主キーが見つかった場合は、列インデックス1の内容がメッセージボックスに表示されます。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet19":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet19":::

## <a name="find-rows-by-column-values"></a>列の値で行を検索

#### <a name="to-find-rows-based-on-the-values-in-any-column"></a>任意の列の値に基づいて行を検索するには

- データテーブルは、メソッドを使用して作成され <xref:System.Data.DataTable.Select%2A> ます。このメソッドは、 <xref:System.Data.DataRow> メソッドに渡された式に基づいての配列を返し <xref:System.Data.DataTable.Select%2A> ます。 有効な式の作成の詳細については、プロパティに関するページの「式の構文」セクションを参照してください <xref:System.Data.DataColumn.Expression%2A> 。

     次の例は、のメソッドを使用して特定の行を検索する方法を示して <xref:System.Data.DataTable.Select%2A> <xref:System.Data.DataTable> います。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet20":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet20":::

## <a name="access-related-records"></a>関連レコードへのアクセス
データセット内のテーブルが関連付けられている場合、オブジェクトは、 <xref:System.Data.DataRelation> 関連するレコードを別のテーブルで使用できるようにすることができます。 たとえば、テーブルとテーブルを含むデータセットを使用できるようにする `Customers` `Orders` ことができます。

オブジェクトを使用し <xref:System.Data.DataRelation> て、 <xref:System.Data.DataRow.GetChildRows%2A> 親テーブルでのメソッドを呼び出すことによって、関連するレコードを検索でき <xref:System.Data.DataRow> ます。 このメソッドは、関連する子レコードの配列を返します。 または、子テーブルののメソッドを呼び出すことができ <xref:System.Data.DataRow.GetParentRow%2A> <xref:System.Data.DataRow> ます。 このメソッドは、親テーブルから単一のを返し <xref:System.Data.DataRow> ます。

このページでは、型指定されたデータセットを使用する例を示します。 型指定されていないデータセット内のリレーションシップのナビゲートの詳細については、「 [datarelation のナビゲート](/dotnet/framework/data/adonet/dataset-datatable-dataview/navigating-datarelations)

> [!NOTE]
> Windows フォームアプリケーションで作業していて、データバインディング機能を使用してデータを表示している場合は、デザイナーで生成されたフォームによってアプリケーションに十分な機能が提供されることがあります。 詳細については、「 [Visual Studio でのデータへのコントロールのバインド](../data-tools/bind-controls-to-data-in-visual-studio.md)」を参照してください。 具体的には、「 [データセット内のリレーションシップ](relationships-in-datasets.md)」を参照してください。

次のコード例は、型指定されたデータセット内の上下関係を移動する方法を示しています。 このコード例では、型 <xref:System.Data.DataRow> s ( `NorthwindDataSet.OrdersRow` ) および生成された FindBy *PrimaryKey* ( `FindByCustomerID` ) メソッドを使用して目的の行を検索し、関連レコードを返します。 これらの例は、次のものがある場合にのみ、正しくコンパイルされて実行されます。

- テーブルを持つという名前のデータセットのインスタンス `NorthwindDataSet` `Customers` 。

- `Orders`テーブル。

- `FK_Orders_Customers`2 つのテーブルを関連付けるという名前のリレーションシップ。

また、返されるレコードのデータを両方のテーブルに格納する必要があります。

#### <a name="to-return-the-child-records-of-a-selected-parent-record"></a>選択した親レコードの子レコードを取得するには

- <xref:System.Data.DataRow.GetChildRows%2A>特定のデータ行のメソッドを呼び出し、 `Customers` テーブルから行の配列を返し `Orders` ます。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataDatasets/CS/Form1.cs" id="Snippet6":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataDatasets/VB/Form1.vb" id="Snippet6":::

#### <a name="to-return-the-parent-record-of-a-selected-child-record"></a>選択した子レコードの親レコードを取得するには

- <xref:System.Data.DataRow.GetParentRow%2A>特定のデータ行のメソッドを呼び出し、 `Orders` テーブルから1つの行を返し `Customers` ます。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataDatasets/CS/Form1.cs" id="Snippet7":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataDatasets/VB/Form1.vb" id="Snippet7":::

## <a name="see-also"></a>関連項目

- [Visual Studio のデータセット ツール](../data-tools/dataset-tools-in-visual-studio.md)
