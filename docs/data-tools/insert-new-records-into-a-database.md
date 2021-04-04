---
title: データベースに新しいレコードを挿入する
description: TableAdapter. Update メソッド、TableAdapter の DBDirect メソッド、またはコマンドオブジェクトを使用して、データベースに新しいレコードを挿入します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
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
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: 6e1046dfd114e4cad69445b8f4e1432c03aac0e5
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106216463"
---
# <a name="insert-new-records-into-a-database"></a>データベースに新しいレコードを挿入する

新しいレコードをデータベースに挿入するには、メソッド、 `TableAdapter.Update` または TableAdapter の DBDirect メソッド (具体的にはメソッド) のいずれかを使用でき `TableAdapter.Insert` ます。 詳細については、「 [TableAdapter](../data-tools/create-and-configure-tableadapters.md)」を参照してください。

アプリケーションで Tableadapter を使用しない場合は、コマンドオブジェクト (など) を使用し  <xref:System.Data.SqlClient.SqlCommand> てデータベースに新しいレコードを挿入できます。

アプリケーションでデータセットを使用してデータを格納する場合は、メソッドを使用し `TableAdapter.Update` ます。 メソッドは、 `Update` すべての変更 (更新、挿入、および削除) をデータベースに送信します。

アプリケーションでオブジェクトを使用してデータを格納する場合、またはデータベースで新しいレコードの作成をより細かく制御する必要がある場合は、メソッドを使用し `TableAdapter.Insert` ます。

TableAdapter にメソッドがない場合 `Insert` は、tableadapter がストアドプロシージャを使用するように構成されているか、その `GenerateDBDirectMethods` プロパティがに設定されていることを意味し `false` ます。 `GenerateDBDirectMethods`データセットデザイナー内から TableAdapter のプロパティをに設定し、 `true` データセットを保存します。 これにより、TableAdapter が再生成されます。 TableAdapter にメソッドがまだない場合 `Insert` 、テーブルには、個別の行を区別するための十分なスキーマ情報がない可能性があります (たとえば、テーブルに主キーが設定されていない可能性があります)。

## <a name="insert-new-records-by-using-tableadapters"></a>Tableadapter を使用して新しいレコードを挿入する

Tableadapter には、アプリケーションの要件に応じて、データベースに新しいレコードを挿入するためのさまざまな方法が用意されています。

アプリケーションでデータセットを使用してデータを格納する場合は、単にデータセット内の目的のに新しいレコードを追加し、メソッドを呼び出すことができ <xref:System.Data.DataTable> `TableAdapter.Update` ます。 `TableAdapter.Update`メソッドは、データベースに変更を送信し <xref:System.Data.DataTable> ます (変更されたレコードと削除されたレコードを含む)。

### <a name="to-insert-new-records-into-a-database-by-using-the-tableadapterupdate-method"></a>TableAdapter. Update メソッドを使用して新しいレコードをデータベースに挿入するには

1. 新しいレコードを <xref:System.Data.DataTable> 作成し、コレクションに追加して、目的のに新しいレコードを追加し <xref:System.Data.DataRow> <xref:System.Data.DataTable.Rows%2A> ます。

2. 新しい行をに追加した後 <xref:System.Data.DataTable> 、メソッドを呼び出し `TableAdapter.Update` ます。 更新するデータの量を制御するには、全体 <xref:System.Data.DataSet> 、、のいずれか <xref:System.Data.DataTable> の配列、 <xref:System.Data.DataRow> または1つを渡し <xref:System.Data.DataRow> ます。

   次のコードは、に新しいレコードを追加し、 <xref:System.Data.DataTable> メソッドを呼び出して `TableAdapter.Update` 新しい行をデータベースに保存する方法を示しています。 (この例では、 `Region` Northwind データベースのテーブルを使用します)。

   :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form5.vb" id="Snippet14":::
   :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form5.cs" id="Snippet14":::

### <a name="to-insert-new-records-into-a-database-by-using-the-tableadapterinsert-method"></a>TableAdapter. Insert メソッドを使用して新しいレコードをデータベースに挿入するには

アプリケーションでオブジェクトを使用してデータを格納している場合は、メソッドを使用して `TableAdapter.Insert` データベースに直接新しい行を作成できます。 メソッドは、 `Insert` 各列の個別の値をパラメーターとして受け取ります。 メソッドを呼び出すと、渡されたパラメーター値を使用して新しいレコードがデータベースに挿入されます。

- TableAdapter の `Insert` メソッドを呼び出し、各列の値をパラメーターとして渡します。

次の手順では、メソッドを使用して行を挿入する方法を示し `TableAdapter.Insert` ます。 この例では、Northwind データベースのテーブルにデータを挿入 `Region` します。

> [!NOTE]
> 使用可能なインスタンスがない場合は、使用する TableAdapter をインスタンス化します。

:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Class1.vb" id="Snippet15":::
:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Class1.cs" id="Snippet15":::

## <a name="insert-new-records-by-using-command-objects"></a>コマンドオブジェクトを使用して新しいレコードを挿入する

コマンドオブジェクトを使用して、新しいレコードをデータベースに直接挿入できます。

### <a name="to-insert-new-records-into-a-database-by-using-command-objects"></a>コマンドオブジェクトを使用して新しいレコードをデータベースに挿入するには

- 新しい command オブジェクトを作成し、、、の各プロパティを設定し `Connection` `CommandType` `CommandText` ます。

次の例では、command オブジェクトを使用してデータベースにレコードを挿入する方法を示します。 Northwind データベースのテーブルにデータを挿入 `Region` します。

:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Class1.vb" id="Snippet16":::
:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Class1.cs" id="Snippet16":::

## <a name="net-security"></a>.NET セキュリティ

接続しようとしているデータベースへのアクセス権と、目的のテーブルに挿入を実行する権限が必要です。

## <a name="see-also"></a>関連項目

- [データをデータベースに保存する](../data-tools/save-data-back-to-the-database.md)
