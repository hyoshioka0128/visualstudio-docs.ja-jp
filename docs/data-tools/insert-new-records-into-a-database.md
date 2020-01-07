---
title: データベースに新しいレコードを挿入する
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- TableAdapters, inserting new records into
- data [Visual Studio], saving
- databases, inserting new records into
- records, inserting
- saving data
ms.assetid: ea118fff-69b1-4675-b79a-e33374377f04
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 3a3830c9dd1921939ced3577b7bafa22772b49f6
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75586420"
---
# <a name="insert-new-records-into-a-database"></a>データベースに新しいレコードを挿入する

新しいレコードをデータベースに挿入するには、`TableAdapter.Update` メソッド、または TableAdapter の DBDirect メソッド (具体的には `TableAdapter.Insert` メソッド) のいずれかを使用できます。 詳細については、「 [TableAdapter](../data-tools/create-and-configure-tableadapters.md)」を参照してください。

アプリケーションで Tableadapter を使用しない場合は、コマンドオブジェクト (<xref:System.Data.SqlClient.SqlCommand>など) を使用してデータベースに新しいレコードを挿入できます。

アプリケーションでデータセットを使用してデータを格納する場合は、`TableAdapter.Update` メソッドを使用します。 `Update` メソッドは、すべての変更 (更新、挿入、および削除) をデータベースに送信します。

アプリケーションでオブジェクトを使用してデータを格納する場合、またはデータベースで新しいレコードの作成をより細かく制御する必要がある場合は、`TableAdapter.Insert` メソッドを使用します。

TableAdapter に `Insert` メソッドがない場合は、TableAdapter がストアドプロシージャを使用するように構成されているか、その `GenerateDBDirectMethods` プロパティが `false`に設定されていることを意味します。 **データセットデザイナー**内から TableAdapter の `GenerateDBDirectMethods` プロパティを `true` に設定し、データセットを保存します。 これにより、TableAdapter が再生成されます。 TableAdapter に `Insert` メソッドがまだない場合、テーブルには、個々の行を区別するための十分なスキーマ情報がない可能性があります (たとえば、テーブルに主キーが設定されていない可能性があります)。

## <a name="insert-new-records-by-using-tableadapters"></a>Tableadapter を使用して新しいレコードを挿入する

Tableadapter には、アプリケーションの要件に応じて、データベースに新しいレコードを挿入するためのさまざまな方法が用意されています。

アプリケーションでデータセットを使用してデータを格納する場合は、単にデータセット内の目的の <xref:System.Data.DataTable> に新しいレコードを追加し、`TableAdapter.Update` メソッドを呼び出すことができます。 `TableAdapter.Update` メソッドは、<xref:System.Data.DataTable> 内のすべての変更をデータベースに送信します (変更されたレコードと削除されたレコードを含む)。

### <a name="to-insert-new-records-into-a-database-by-using-the-tableadapterupdate-method"></a>TableAdapter. Update メソッドを使用して新しいレコードをデータベースに挿入するには

1. 新しい <xref:System.Data.DataRow> を作成して <xref:System.Data.DataTable.Rows%2A> コレクションに追加することで、目的の <xref:System.Data.DataTable> に新しいレコードを追加します。

2. 新しい行が <xref:System.Data.DataTable>に追加されたら、`TableAdapter.Update` メソッドを呼び出します。 更新するデータの量を制御するには、<xref:System.Data.DataSet>全体、<xref:System.Data.DataTable>、<xref:System.Data.DataRow>の配列、または1つの <xref:System.Data.DataRow>を渡します。

   次のコードは、<xref:System.Data.DataTable> に新しいレコードを追加し、`TableAdapter.Update` メソッドを呼び出して、新しい行をデータベースに保存する方法を示しています。 (この例では、Northwind データベースの `Region` テーブルを使用しています)。

   [!code-vb[VbRaddataSaving#14](../data-tools/codesnippet/VisualBasic/insert-new-records-into-a-database_1.vb)]
   [!code-csharp[VbRaddataSaving#14](../data-tools/codesnippet/CSharp/insert-new-records-into-a-database_1.cs)]

### <a name="to-insert-new-records-into-a-database-by-using-the-tableadapterinsert-method"></a>TableAdapter. Insert メソッドを使用して新しいレコードをデータベースに挿入するには

アプリケーションでオブジェクトを使用してデータを格納している場合は、`TableAdapter.Insert` メソッドを使用して、データベースに直接新しい行を作成できます。 `Insert` メソッドは、各列の個別の値をパラメーターとして受け取ります。 メソッドを呼び出すと、渡されたパラメーター値を使用して新しいレコードがデータベースに挿入されます。

- TableAdapter の `Insert` メソッドを呼び出し、各列の値をパラメーターとして渡します。

次の手順では、`TableAdapter.Insert` メソッドを使用して行を挿入する方法を示します。 この例では、Northwind データベースの `Region` テーブルにデータを挿入します。

> [!NOTE]
> 使用可能なインスタンスがない場合は、使用する TableAdapter をインスタンス化します。

[!code-vb[VbRaddataSaving#15](../data-tools/codesnippet/VisualBasic/insert-new-records-into-a-database_2.vb)]
[!code-csharp[VbRaddataSaving#15](../data-tools/codesnippet/CSharp/insert-new-records-into-a-database_2.cs)]

## <a name="insert-new-records-by-using-command-objects"></a>コマンドオブジェクトを使用して新しいレコードを挿入する

コマンドオブジェクトを使用して、新しいレコードをデータベースに直接挿入できます。

### <a name="to-insert-new-records-into-a-database-by-using-command-objects"></a>コマンドオブジェクトを使用して新しいレコードをデータベースに挿入するには

- 新しい command オブジェクトを作成し、その `Connection`、`CommandType`、および `CommandText` の各プロパティを設定します。

次の例では、command オブジェクトを使用してデータベースにレコードを挿入する方法を示します。 Northwind データベースの `Region` テーブルにデータを挿入します。

[!code-vb[VbRaddataSaving#16](../data-tools/codesnippet/VisualBasic/insert-new-records-into-a-database_3.vb)]
[!code-csharp[VbRaddataSaving#16](../data-tools/codesnippet/CSharp/insert-new-records-into-a-database_3.cs)]

## <a name="net-security"></a>.NET セキュリティ

接続しようとしているデータベースへのアクセス権と、目的のテーブルに挿入を実行する権限が必要です。

## <a name="see-also"></a>関連項目

- [データをデータベースに保存する](../data-tools/save-data-back-to-the-database.md)
