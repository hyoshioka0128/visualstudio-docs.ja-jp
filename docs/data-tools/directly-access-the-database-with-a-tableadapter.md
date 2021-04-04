---
title: TableAdapter で直接データベースにアクセスする
description: Insert、Update、Delete などのメソッドを使用してデータベース内のデータを直接操作し、TableAdapter を使用してデータベースに直接アクセスします。
ms.custom: SEO-VS-2020
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
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: 30248632eacde07cfcc94213aeeb75ecac8dcf70
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106215917"
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

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Class1.vb" id="Snippet15":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Class1.cs" id="Snippet15":::

### <a name="to-update-records-directly-in-a-database"></a>データベース内のレコードを直接更新するには

- TableAdapter のメソッドを呼び出し `Update` 、各列の新しい値と元の値をパラメーターとして渡します。

    > [!NOTE]
    > 使用可能なインスタンスがない場合は、使用する TableAdapter をインスタンス化します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Class1.vb" id="Snippet18":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Class1.cs" id="Snippet18":::

### <a name="to-delete-records-directly-from-a-database"></a>レコードをデータベースから直接削除するには

- TableAdapter の `Delete` メソッドを呼び出し、各列の値をメソッドのパラメーターとして渡し `Delete` ます。 次の手順では、 `Region` Northwind データベースのテーブルを例として使用します。

    > [!NOTE]
    > 使用可能なインスタンスがない場合は、使用する TableAdapter をインスタンス化します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Class1.vb" id="Snippet21":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Class1.cs" id="Snippet21":::

## <a name="see-also"></a>関連項目

- [TableAdapters を使用してデータセットを入力する](../data-tools/fill-datasets-by-using-tableadapters.md)
