---
title: 新しいレコードをデータベースに挿入する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- TableAdapters, inserting new records into
- data [Visual Studio], saving
- databases, inserting new records into
- records, inserting
- saving data
ms.assetid: ea118fff-69b1-4675-b79a-e33374377f04
caps.latest.revision: 14
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 3c686a764f42f50a3e59da3e8b37b219ddb7b11c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72651560"
---
# <a name="insert-new-records-into-a-database"></a>データベースに新しいレコードを挿入する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

新しいレコードをデータベースに挿入するには、メソッド、 `TableAdapter.Update` または TableAdapter の DBDirect メソッド (具体的にはメソッド) のいずれかを使用でき `TableAdapter.Insert` ます。

 アプリケーションで Tableadapter を使用しない場合は、コマンドオブジェクト (など) を使用し  <xref:System.Data.SqlClient.SqlCommand> てデータベースに新しいレコードを挿入できます。

 アプリケーションでデータセットを使用してデータを格納する場合は、メソッドを使用し `TableAdapter.Update` ます。 メソッドは、 `Update` すべての変更 (更新、挿入、および削除) をデータベースに送信します。

 アプリケーションでオブジェクトを使用してデータを格納する場合、またはデータベースで新しいレコードの作成をより細かく制御する必要がある場合は、メソッドを使用し `TableAdapter.Insert` ます。

 TableAdapter にメソッドがない場合 `Insert` は、tableadapter がストアドプロシージャを使用するように構成されているか、その `GenerateDBDirectMethods` プロパティがに設定されていることを意味し `false` ます。 `GenerateDBDirectMethods`データセットデザイナー内から TableAdapter のプロパティをに設定し、 `true` データセットを保存します。 これにより、TableAdapter が再生成されます。 TableAdapter にメソッドがまだない場合 `Insert` 、テーブルには、個々の行を区別するための十分なスキーマ情報が得られない可能性があります (たとえば、テーブルに主キーが設定されていない場合など)。

## <a name="insert-new-records-by-using-tableadapters"></a>Tableadapter を使用して新しいレコードを挿入する
 Tableadapter には、アプリケーションの要件に応じて、データベースに新しいレコードを挿入するためのさまざまな方法が用意されています。

 アプリケーションでデータセットを使用してデータを格納する場合は、単にデータセット内の目的のに新しいレコードを追加 <xref:System.Data.DataTable> し、メソッドを呼び出すことができ `TableAdapter.Update` ます。 `TableAdapter.Update`メソッドは、データベースに変更を送信し <xref:System.Data.DataTable> ます (変更されたレコードと削除されたレコードを含む)。

#### <a name="to-insert-new-records-into-a-database-by-using-the-tableadapterupdate-method"></a>TableAdapter. Update メソッドを使用して新しいレコードをデータベースに挿入するには

1. 新しいレコードを <xref:System.Data.DataTable> 作成し、コレクションに追加して、目的のに新しいレコードを追加し <xref:System.Data.DataRow> <xref:System.Data.DataTable.Rows%2A> ます。 詳細については、「 [方法: DataTable に行を追加](https://msdn.microsoft.com/library/78ebbb43-c402-49cf-81da-0715289487bf)する」を参照してください。

2. 新しい行をに追加した後 <xref:System.Data.DataTable> 、メソッドを呼び出し `TableAdapter.Update` ます。 更新するデータの量を制御するには、全体 <xref:System.Data.DataSet> 、、のいずれか <xref:System.Data.DataTable> の配列、 <xref:System.Data.DataRow> または1つを渡し <xref:System.Data.DataRow> ます。

    次のコードは、に新しいレコードを追加し、 <xref:System.Data.DataTable> メソッドを呼び出して `TableAdapter.Update` 新しい行をデータベースに保存する方法を示しています。 (この例では、 `Region` Northwind データベースのテーブルを使用します)。

    [!code-csharp[VbRaddataSaving#14](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form5.cs#14)]
    [!code-vb[VbRaddataSaving#14](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form5.vb#14)]

   アプリケーションでオブジェクトを使用してデータを格納している場合は、メソッドを使用して `TableAdapter.Insert` データベースに直接新しい行を作成できます。 メソッドは、 `Insert` 各列の個別の値をパラメーターとして受け取ります。 メソッドを呼び出すと、渡されたパラメーター値を使用して新しいレコードがデータベースに挿入されます。

   次の手順では、 `Region` Northwind データベースのテーブルを例として使用します。

#### <a name="to-insert-new-records-into-a-database-by-using-the-tableadapterinsert-method"></a>TableAdapter. Insert メソッドを使用して新しいレコードをデータベースに挿入するには

- TableAdapter の `Insert` メソッドを呼び出し、各列の値をパラメーターとして渡します。

    > [!NOTE]
    > 使用可能なインスタンスがない場合は、使用する TableAdapter をインスタンス化します。

     [!code-csharp[VbRaddataSaving#15](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Class1.cs#15)]
     [!code-vb[VbRaddataSaving#15](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Class1.vb#15)]

## <a name="insert-new-records-by-using-command-objects"></a>コマンドオブジェクトを使用して新しいレコードを挿入する
 次の例では、コマンドオブジェクトを使用して、新しいレコードをデータベースに直接挿入します。

 次の手順では、 `Region` Northwind データベースのテーブルを例として使用します。

#### <a name="to-insert-new-records-into-a-database-by-using-command-objects"></a>コマンドオブジェクトを使用して新しいレコードをデータベースに挿入するには

- 新しい command オブジェクトを作成し、、、の各プロパティを設定し `Connection` `CommandType` `CommandText` ます。

     [!code-csharp[VbRaddataSaving#16](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Class1.cs#16)]
     [!code-vb[VbRaddataSaving#16](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Class1.vb#16)]

## <a name="net-framework-security"></a>.NET Framework のセキュリティ
 接続しようとしているデータベースへのアクセス権と、目的のテーブルに挿入を実行する権限が必要です。

## <a name="see-also"></a>参照
 [データをデータベースに保存する](../data-tools/save-data-back-to-the-database.md)
