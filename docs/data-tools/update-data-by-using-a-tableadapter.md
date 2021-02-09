---
title: TableAdapter を使用してデータを更新する
description: データセット内のデータを更新します。 TableAdapter の Update メソッドを呼び出して、データをデータベースに送り返します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data [Visual Studio], saving
- data [Visual Studio], TableAdapters
- updating data, TableAdapters
- TableAdapters, updating data
- data [Visual Studio], updating
- saving data
ms.assetid: 5e32e10e-9bac-4969-9bdd-b8f6919d3516
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: 5d03a6dbe728d77fb9158ec02e1f59016e7c4a99
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99858281"
---
# <a name="update-data-by-using-a-tableadapter"></a>TableAdapter を使用してデータを更新する

データセット内のデータを変更および検証した後は、TableAdapter のメソッドを呼び出すことによって、更新されたデータをデータベースに戻すことができ `Update` ます。 [](../data-tools/create-and-configure-tableadapters.md) メソッドは、 `Update` 1 つのデータテーブルを更新し、 <xref:System.Data.DataRow.RowState%2A> テーブル内の各データ行のに基づいて、適切なコマンド (INSERT、UPDATE、または DELETE) を実行します。 データセットに関連テーブルがある場合、Visual Studio によって、更新を実行するために使用する TableAdapterManager クラスが生成されます。 TableAdapterManager クラスは、データベースで定義されている外部キー制約に基づいて、更新が正しい順序で行われることを保証します。 データバインドコントロールを使用すると、データバインディングアーキテクチャによって tableAdapterManager という TableAdapterManager クラスのメンバー変数が作成されます。

> [!NOTE]
> データセットの内容を使用してデータソースを更新しようとすると、エラーが発生することがあります。 エラーを回避するには、アダプターのメソッドを呼び出すコードをブロック内に配置することをお勧めし `Update` `try` / `catch` ます。

データソースを更新するための正確な手順は、ビジネスニーズによって異なりますが、次の手順が含まれます。

1. ブロックでアダプターの `Update` メソッドを呼び出し `try` / `catch` ます。

2. 例外が検出された場合は、エラーを引き起こしたデータ行を探します。

3. データ行の問題を調整する (可能な場合はプログラムによって、ユーザーに無効な行を表示することによって変更する場合)、もう一度更新を実行し <xref:System.Data.DataRow.HasErrors%2A> ます (、 <xref:System.Data.DataTable.GetErrors%2A> )。

## <a name="save-data-to-a-database"></a>データベースにデータを保存する

`Update`TableAdapter のメソッドを呼び出します。 データベースに書き込まれる値を含むデータテーブルの名前を渡します。

### <a name="to-update-a-database-by-using-a-tableadapter"></a>TableAdapter を使用してデータベースを更新するには

- TableAdapter のメソッドを `Update` ブロックで囲み `try` / `catch` ます。 次の例では、内のテーブルの内容を `Customers` ブロック内から更新する方法を示し `NorthwindDataSet` `try` / `catch` ます。

     [!code-csharp[VbRaddataSaving#9](../data-tools/codesnippet/CSharp/update-data-by-using-a-tableadapter_1.cs)]
     [!code-vb[VbRaddataSaving#9](../data-tools/codesnippet/VisualBasic/update-data-by-using-a-tableadapter_1.vb)]

## <a name="see-also"></a>関連項目

- [データをデータベースに保存する](../data-tools/save-data-back-to-the-database.md)
