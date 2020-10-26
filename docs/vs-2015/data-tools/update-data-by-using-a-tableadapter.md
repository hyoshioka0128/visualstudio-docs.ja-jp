---
title: TableAdapter を使用してデータを更新する |Microsoft Docs
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
- data [Visual Studio], saving
- data [Visual Studio], TableAdapters
- updating data, TableAdapters
- TableAdapters, updating data
- data [Visual Studio], updating
- saving data
ms.assetid: 5e32e10e-9bac-4969-9bdd-b8f6919d3516
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 312bf75100d2b9b270b45776c5f7ded21ab6ac52
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72602332"
---
# <a name="update-data-by-using-a-tableadapter"></a>TableAdapter を使用してデータを更新する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

データセット内のデータを変更し、検証した後、TableAdapter のメソッドを呼び出すことによって、更新されたデータを databaseby 返すことができ `Update` ます。 メソッドは、 `Update` 1 つのデータテーブルを更新し、 <xref:System.Data.DataRow.RowState%2A> テーブル内の各データ行のに基づいて、適切なコマンド (INSERT、UPDATE、または DELETE) を実行します。 データセットに関連テーブルがある場合、Visual Studio によって、更新を実行するために使用する TableAdapterManager クラスが生成されます。 TableAdapterManager クラスは、データベースで定義されている外部キー制約に基づいて、更新が正しい順序で行われることを保証します。 データバインドコントロールを使用すると、データバインディングアーキテクチャによって tableAdapterManager という TableAdapterManager クラスのメンバー変数が作成されます。 詳細については、「 [階層更新の概要](https://msdn.microsoft.com/library/c4f8e8b9-e4a5-4a02-8462-d03d1e8222d6)」を参照してください。

> [!NOTE]
> データセットの内容を使用してデータソースを更新しようとすると、エラーが発生することがあります。エラーを回避するには、アダプターのメソッドを呼び出すコードをブロック内に配置することをお勧めし `Update` `try` / `catch` ます。

 データソースを更新するための正確な手順は、ビジネスニーズによって異なりますが、次の手順が含まれます。

1. ブロックでアダプターの `Update` メソッドを呼び出し `try` / `catch` ます。

2. 例外が検出された場合は、エラーを引き起こしたデータ行を探します。 詳細については、「 [方法: エラーのある行を検索する](https://msdn.microsoft.com/library/1fa907c5-fe66-4f29-a253-2b97b900050c)」を参照してください。

3. データ行の問題を調整する (可能な場合はプログラムによって、ユーザーに無効な行を表示することによって変更する場合)、もう一度更新を実行し <xref:System.Data.DataRow.HasErrors%2A> ます (、 <xref:System.Data.DataTable.GetErrors%2A> )。

## <a name="savedata-to-a-database"></a>データベースへの Savedata
 `Update`TableAdapter のメソッドを呼び出します。 データベースに書き込まれる値を含むデータテーブルの名前を渡します。

#### <a name="to-update-a-database-by-using-a-tableadapter"></a>TableAdapter を使用してデータベースを更新するには

- TableAdapter のメソッドを `Update` ブロックで囲み `try` / `catch` ます。 次の例では、内のテーブルの内容を `Customers` ブロック内から更新する方法を示し `NorthwindDataSet` `try` / `catch` ます。

     [!code-csharp[VbRaddataSaving#9](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form3.cs#9)]
     [!code-vb[VbRaddataSaving#9](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form3.vb#9)]

## <a name="see-also"></a>参照
 [データをデータベースに保存する](../data-tools/save-data-back-to-the-database.md)
