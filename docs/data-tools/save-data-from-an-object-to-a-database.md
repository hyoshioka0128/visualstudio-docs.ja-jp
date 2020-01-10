---
title: オブジェクトからデータベースにデータを保存する
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data [Visual Studio], saving
- data access [Visual Studio], objects
- saving data
ms.assetid: efd6135a-40cf-4b0d-8f8b-41a5aaea7057
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 509910730d4da095b6db622212716a8f958495d7
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75586264"
---
# <a name="save-data-from-an-object-to-a-database"></a>オブジェクトからデータベースにデータを保存する

オブジェクトの値を TableAdapter の DBDirect メソッドの1つ (`TableAdapter.Insert`など) に渡すことによって、オブジェクトのデータをデータベースに保存できます。 詳細については、「 [TableAdapter](../data-tools/create-and-configure-tableadapters.md)」を参照してください。

オブジェクトのコレクションからデータを保存するには、オブジェクトのコレクションをループ処理し (たとえば、for-next ループ)、TableAdapter の `DBDirect` メソッドのいずれかを使用して、各オブジェクトの値をデータベースに送信します。

既定では、`DBDirect` のメソッドは、データベースに対して直接実行できる TableAdapter に作成されます。 これらのメソッドは、直接呼び出すことができます。また、更新をデータベースに送信するために変更を調整するために、<xref:System.Data.DataSet> または <xref:System.Data.DataTable> オブジェクトを必要としません。

> [!NOTE]
> TableAdapter を構成する場合、メインクエリでは、`DBDirect` メソッドを作成するための十分な情報を提供する必要があります。 たとえば、主キー列が定義されていないテーブルのデータをクエリするように TableAdapter が構成されている場合、`DBDirect` メソッドは生成されません。

|TableAdapter DBDirect メソッド|説明|
| - |-----------------|
|`TableAdapter.Insert`|データベースに新しいレコードを追加し、個々の列の値をメソッドのパラメーターとして渡すことができるようにします。|
|`TableAdapter.Update`|データベース内の既存のレコードを更新します。 `Update` メソッドは、元の列と新しい列の値をメソッドのパラメーターとして受け取ります。 元の値は元のレコードを検索するために使用され、新しい値はそのレコードを更新するために使用されます。<br /><br /> `TableAdapter.Update` メソッドは、<xref:System.Data.DataSet>、<xref:System.Data.DataTable>、<xref:System.Data.DataRow>、または <xref:System.Data.DataRow>s の配列をメソッドパラメーターとして取得することによって、データセットの変更をデータベースに戻すためにも使用されます。|
|`TableAdapter.Delete`|メソッドパラメーターとして渡された元の列の値に基づいて、データベースから既存のレコードを削除します。|

## <a name="to-save-new-records-from-an-object-to-a-database"></a>オブジェクトからデータベースに新しいレコードを保存するには

- `TableAdapter.Insert` メソッドに値を渡してレコードを作成します。

     次の例では、`currentCustomer` オブジェクトの値を `TableAdapter.Insert` メソッドに渡すことによって、`Customers` テーブルに新しい顧客レコードを作成します。

     [!code-csharp[VbRaddataSaving#23](../data-tools/codesnippet/CSharp/save-data-from-an-object-to-a-database_1.cs)]
     [!code-vb[VbRaddataSaving#23](../data-tools/codesnippet/VisualBasic/save-data-from-an-object-to-a-database_1.vb)]

## <a name="to-update-existing-records-from-an-object-to-a-database"></a>オブジェクトの既存のレコードをデータベースに更新するには

- レコードを変更するには、`TableAdapter.Update` メソッドを呼び出し、新しい値を渡してレコードを更新し、元の値を渡してレコードを検索します。

    > [!NOTE]
    > オブジェクトは、`Update` メソッドに渡すために、元の値を保持する必要があります。 この例では、`orig` プレフィックスを持つプロパティを使用して、元の値を格納します。

     次の例では、`Customer` オブジェクトの新しい値と元の値を `TableAdapter.Update` メソッドに渡すことによって、`Customers` テーブル内の既存のレコードを更新します。

     [!code-csharp[VbRaddataSaving#24](../data-tools/codesnippet/CSharp/save-data-from-an-object-to-a-database_2.cs)]
     [!code-vb[VbRaddataSaving#24](../data-tools/codesnippet/VisualBasic/save-data-from-an-object-to-a-database_2.vb)]

## <a name="to-delete-existing-records-from-a-database"></a>データベースから既存のレコードを削除するには

- レコードを削除するには、`TableAdapter.Delete` メソッドを呼び出し、元の値を渡してレコードを検索します。

    > [!NOTE]
    > オブジェクトは、`Delete` メソッドに渡すために、元の値を保持する必要があります。 この例では、`orig` プレフィックスを持つプロパティを使用して、元の値を格納します。

     次の例では、`Customer` オブジェクトの元の値を `TableAdapter.Delete` メソッドに渡すことによって、`Customers` テーブルからレコードを削除します。

     [!code-csharp[VbRaddataSaving#25](../data-tools/codesnippet/CSharp/save-data-from-an-object-to-a-database_3.cs)]
     [!code-vb[VbRaddataSaving#25](../data-tools/codesnippet/VisualBasic/save-data-from-an-object-to-a-database_3.vb)]

## <a name="net-security"></a>.NET セキュリティ

データベースのテーブルで、選択した `INSERT`、`UPDATE`、または `DELETE` を実行する権限が必要です。

## <a name="see-also"></a>関連項目

- [データをデータベースに保存する](../data-tools/save-data-back-to-the-database.md)
