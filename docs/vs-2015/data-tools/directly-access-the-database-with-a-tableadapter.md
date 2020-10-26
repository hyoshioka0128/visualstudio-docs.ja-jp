---
title: TableAdapter を使用してデータベースに直接アクセスする |Microsoft Docs
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
caps.latest.revision: 15
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 58500e59a624dac55824033b8b9667754a9040c5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72657376"
---
# <a name="directly-access-the-database-with-a-tableadapter"></a>TableAdapter で直接データベースにアクセスする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

、、およびに加えて、 `InsertCommand` `UpdateCommand` データベースに `DeleteCommand` 対して直接実行できるメソッドを使用して tableadapter が作成されます。 これらのメソッド ( `TableAdapter.Insert` 、 `TableAdapter.Update` 、および `TableAdapter.Delete` ) を呼び出すと、データベース内のデータを直接操作できます。

 これらのダイレクトメソッドを作成しない場合は、 `GenerateDbDirectMethods` `false` [ **プロパティ** ] ウィンドウで TableAdapter のプロパティをに設定します。 Tableadapter のメインクエリに加えて、TableAdapter にクエリが追加されると、これらの DbDirect メソッドを生成しないスタンドアロンクエリになります。

## <a name="sendcommandsdirectly-to-a-database"></a>Send@ を直接データベースに
 実行しようとしているタスクを実行する TableAdapter DbDirect メソッドを呼び出します。

#### <a name="to-insert-new-records-directly-into-a-database"></a>新しいレコードをデータベースに直接挿入するには

- TableAdapter の `Insert` メソッドを呼び出し、各列の値をパラメーターとして渡します。 次の手順では、 `Region` Northwind データベースのテーブルを例として使用します。

    > [!NOTE]
    > 使用可能なインスタンスがない場合は、使用する TableAdapter をインスタンス化します。

     [!code-csharp[VbRaddataSaving#15](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Class1.cs#15)]
     [!code-vb[VbRaddataSaving#15](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Class1.vb#15)]

#### <a name="to-update-records-directly-in-a-database"></a>データベース内のレコードを直接更新するには

- TableAdapter のメソッドを呼び出し `Update` 、各列の新しい値と元の値をパラメーターとして渡します。

    > [!NOTE]
    > 使用可能なインスタンスがない場合は、使用する TableAdapter をインスタンス化します。

     [!code-csharp[VbRaddataSaving#18](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Class1.cs#18)]
     [!code-vb[VbRaddataSaving#18](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Class1.vb#18)]

#### <a name="to-delete-records-directly-from-a-database"></a>レコードをデータベースから直接削除するには

- TableAdapter の `Delete` メソッドを呼び出し、各列の値をメソッドのパラメーターとして渡し `Delete` ます。 次の手順では、 `Region` Northwind データベースのテーブルを例として使用します。

    > [!NOTE]
    > 使用可能なインスタンスがない場合は、使用する TableAdapter をインスタンス化します。

     [!code-csharp[VbRaddataSaving#21](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Class1.cs#21)]
     [!code-vb[VbRaddataSaving#21](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Class1.vb#21)]

## <a name="see-also"></a>参照
 [TableAdapters を使用してデータセットを入力する](../data-tools/fill-datasets-by-using-tableadapters.md)
