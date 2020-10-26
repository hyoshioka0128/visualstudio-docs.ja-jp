---
title: TableAdapter で直接データベースにアクセスする
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- databases [Visual Basic], accessing with a TableAdapter
- DBDirect methods
- datasets [Visual Basic], adding to projects
- data [Visual Studio], saving
- TableAdapter.Delete method
- GenerateDbDirectMethods property
- TableAdapter.Insert method
- TableAdapter.GenerateDBDirectMethods property
- TableAdapter.Update method
- saving data
- TableAdapters
ms.assetid: 012c5924-91f7-4790-b2a6-f51402b7014b
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 22d84e9b4beafd64cc629a295bcfa7f9f67afb6d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85282567"
---
# <a name="directly-access-the-database-with-a-tableadapter"></a>TableAdapter で直接データベースにアクセスする

、、およびに加えて、 `InsertCommand` `UpdateCommand` データベースに `DeleteCommand` 対して直接実行できるメソッドを使用して tableadapter が作成されます。 これらのメソッド ( `TableAdapter.Insert` 、 `TableAdapter.Update` 、および) を呼び出すと、 `TableAdapter.Delete` データベース内のデータを直接操作できます。

これらのダイレクトメソッドを作成しない場合は、 `GenerateDbDirectMethods` `false` [ **プロパティ** ] ウィンドウで TableAdapter のプロパティをに設定します。 Tableadapter のメインクエリに加えて、TableAdapter にクエリが追加されると、これらのメソッドを生成しないスタンドアロンクエリになり `DbDirect` ます。

## <a name="send-commands-directly-to-a-database"></a>コマンドをデータベースに直接送信する

`DbDirect`実行しようとしているタスクを実行する TableAdapter メソッドを呼び出します。

### <a name="to-insert-new-records-directly-into-a-database"></a>新しいレコードをデータベースに直接挿入するには

- TableAdapter の `Insert` メソッドを呼び出し、各列の値をパラメーターとして渡します。 次の手順では、 `Region` Northwind データベースのテーブルを例として使用します。

    > [!NOTE]
    > 使用可能なインスタンスがない場合は、使用する TableAdapter をインスタンス化します。

     [!code-vb[VbRaddataSaving#15](../data-tools/codesnippet/VisualBasic/directly-access-the-database-with-a-tableadapter_1.vb)]
     [!code-csharp[VbRaddataSaving#15](../data-tools/codesnippet/CSharp/directly-access-the-database-with-a-tableadapter_1.cs)]

### <a name="to-update-records-directly-in-a-database"></a>データベース内のレコードを直接更新するには

- TableAdapter のメソッドを呼び出し `Update` 、各列の新しい値と元の値をパラメーターとして渡します。

    > [!NOTE]
    > 使用可能なインスタンスがない場合は、使用する TableAdapter をインスタンス化します。

     [!code-vb[VbRaddataSaving#18](../data-tools/codesnippet/VisualBasic/directly-access-the-database-with-a-tableadapter_2.vb)]
     [!code-csharp[VbRaddataSaving#18](../data-tools/codesnippet/CSharp/directly-access-the-database-with-a-tableadapter_2.cs)]

### <a name="to-delete-records-directly-from-a-database"></a>レコードをデータベースから直接削除するには

- TableAdapter の `Delete` メソッドを呼び出し、各列の値をメソッドのパラメーターとして渡し `Delete` ます。 次の手順では、 `Region` Northwind データベースのテーブルを例として使用します。

    > [!NOTE]
    > 使用可能なインスタンスがない場合は、使用する TableAdapter をインスタンス化します。

     [!code-vb[VbRaddataSaving#21](../data-tools/codesnippet/VisualBasic/directly-access-the-database-with-a-tableadapter_3.vb)]
     [!code-csharp[VbRaddataSaving#21](../data-tools/codesnippet/CSharp/directly-access-the-database-with-a-tableadapter_3.cs)]

## <a name="see-also"></a>関連項目

- [TableAdapters を使用してデータセットを入力する](../data-tools/fill-datasets-by-using-tableadapters.md)
