---
title: TableAdapter を使用してデータを更新する
ms.date: 11/04/2016
ms.topic: conceptual
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
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: ffb5139e148fba6facd1d437d4f7977d8d7e0b28
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75586082"
---
# <a name="update-data-by-using-a-tableadapter"></a>TableAdapter を使用してデータを更新する

データセット内のデータを変更および検証した後は、 [TableAdapter](../data-tools/create-and-configure-tableadapters.md)の `Update` メソッドを呼び出すことによって、更新されたデータをデータベースに戻すことができます。 `Update` メソッドは、テーブル内の各データ行の <xref:System.Data.DataRow.RowState%2A> に基づいて、1つのデータテーブルを更新し、適切なコマンド (INSERT、UPDATE、または DELETE) を実行します。 データセットに関連テーブルがある場合、Visual Studio によって、更新を実行するために使用する TableAdapterManager クラスが生成されます。 TableAdapterManager クラスは、データベースで定義されている外部キー制約に基づいて、更新が正しい順序で行われることを保証します。 データバインドコントロールを使用すると、データバインディングアーキテクチャによって tableAdapterManager という TableAdapterManager クラスのメンバー変数が作成されます。

> [!NOTE]
> データセットの内容を使用してデータソースを更新しようとすると、エラーが発生することがあります。 エラーを回避するには、アダプターの `Update` メソッドを呼び出すコードを `catch` ブロック /`try`内に配置することをお勧めします。

データソースを更新するための正確な手順は、ビジネスニーズによって異なりますが、次の手順が含まれます。

1. `try`/`catch` ブロックで、アダプターの `Update` メソッドを呼び出します。

2. 例外が検出された場合は、エラーを引き起こしたデータ行を探します。

3. データ行の問題を調整する (可能な場合、またはユーザーに無効な行を表示して変更することによってプログラムで実行する) 場合は、更新を再試行します (<xref:System.Data.DataRow.HasErrors%2A>、<xref:System.Data.DataTable.GetErrors%2A>)。

## <a name="save-data-to-a-database"></a>データベースにデータを保存する

TableAdapter の `Update` メソッドを呼び出します。 データベースに書き込まれる値を含むデータテーブルの名前を渡します。

### <a name="to-update-a-database-by-using-a-tableadapter"></a>TableAdapter を使用してデータベースを更新するには

- TableAdapter の`Update` メソッドを `try`/`catch` ブロックで囲みます。 次の例では、`try`/`catch` ブロック内から `NorthwindDataSet` の `Customers` テーブルの内容を更新する方法を示します。

     [!code-csharp[VbRaddataSaving#9](../data-tools/codesnippet/CSharp/update-data-by-using-a-tableadapter_1.cs)]
     [!code-vb[VbRaddataSaving#9](../data-tools/codesnippet/VisualBasic/update-data-by-using-a-tableadapter_1.vb)]

## <a name="see-also"></a>関連項目

- [データをデータベースに保存する](../data-tools/save-data-back-to-the-database.md)
