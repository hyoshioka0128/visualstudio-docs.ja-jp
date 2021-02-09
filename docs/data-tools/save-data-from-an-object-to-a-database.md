---
title: オブジェクトからデータベースにデータを保存する
description: Visual Studio のデータセットツールを使用して、オブジェクトのデータをデータベースに保存します。 「新しいレコードを保存する方法」、「既存のレコードを更新する」、および「既存のレコードを削除する」を参照してください。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
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
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: 52bd4f95160165ee67c0a35816d094238786bc38
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99866568"
---
# <a name="save-data-from-an-object-to-a-database"></a>オブジェクトからデータベースにデータを保存する

オブジェクトの値を TableAdapter の DBDirect メソッドの1つ (たとえば、) に渡すことによって、オブジェクトのデータをデータベースに保存でき `TableAdapter.Insert` ます。 詳細については、「 [TableAdapter](../data-tools/create-and-configure-tableadapters.md)」を参照してください。

オブジェクトのコレクションからデータを保存するには、オブジェクトのコレクションをループ処理し (たとえば、for-next ループ)、TableAdapter のメソッドのいずれかを使用して、各オブジェクトの値をデータベースに送信し `DBDirect` ます。

既定で `DBDirect` は、データベースに対して直接実行できる TableAdapter にメソッドが作成されます。 これらのメソッドは直接呼び出すことができ <xref:System.Data.DataSet> 、 <xref:System.Data.DataTable> 更新をデータベースに送信するために、またはオブジェクトによる変更の調整を必要としません。

> [!NOTE]
> TableAdapter を構成する場合、メインクエリでは、メソッドを作成するための十分な情報を提供する必要があり `DBDirect` ます。 たとえば、主キー列が定義されていないテーブルのデータをクエリするように TableAdapter が構成されている場合、メソッドは生成されません `DBDirect` 。

|TableAdapter DBDirect メソッド|Description|
| - |-----------------|
|`TableAdapter.Insert`|データベースに新しいレコードを追加し、個々の列の値をメソッドのパラメーターとして渡すことができるようにします。|
|`TableAdapter.Update`|データベース内の既存のレコードを更新します。 メソッドは、 `Update` 元の列と新しい列の値をメソッドのパラメーターとして受け取ります。 元の値は元のレコードを検索するために使用され、新しい値はそのレコードを更新するために使用されます。<br /><br /> `TableAdapter.Update`メソッドは、 <xref:System.Data.DataSet> <xref:System.Data.DataTable> <xref:System.Data.DataRow> <xref:System.Data.DataRow> メソッドパラメーターとして、、、またはの配列を取得することによって、データセットの変更をデータベースに戻すためにも使用されます。|
|`TableAdapter.Delete`|メソッドパラメーターとして渡された元の列の値に基づいて、データベースから既存のレコードを削除します。|

## <a name="to-save-new-records-from-an-object-to-a-database"></a>オブジェクトからデータベースに新しいレコードを保存するには

- 値をメソッドに渡すことで、レコードを作成し `TableAdapter.Insert` ます。

     次の例では、オブジェクトの値を `Customers` メソッドに渡すことによって、テーブルに新しい顧客レコードを作成し `currentCustomer` `TableAdapter.Insert` ます。

     [!code-csharp[VbRaddataSaving#23](../data-tools/codesnippet/CSharp/save-data-from-an-object-to-a-database_1.cs)]
     [!code-vb[VbRaddataSaving#23](../data-tools/codesnippet/VisualBasic/save-data-from-an-object-to-a-database_1.vb)]

## <a name="to-update-existing-records-from-an-object-to-a-database"></a>オブジェクトの既存のレコードをデータベースに更新するには

- メソッドを呼び出してレコードを変更 `TableAdapter.Update` し、新しい値を渡してレコードを更新し、元の値を渡してレコードを検索します。

    > [!NOTE]
    > オブジェクトは、メソッドに渡すために元の値を保持する必要があり `Update` ます。 この例では、プレフィックスを持つプロパティを使用して `orig` 、元の値を格納します。

     次の例では、 `Customers` オブジェクトの新しい値と元の値をメソッドに渡すことによって、テーブル内の既存のレコードを更新し `Customer` `TableAdapter.Update` ます。

     [!code-csharp[VbRaddataSaving#24](../data-tools/codesnippet/CSharp/save-data-from-an-object-to-a-database_2.cs)]
     [!code-vb[VbRaddataSaving#24](../data-tools/codesnippet/VisualBasic/save-data-from-an-object-to-a-database_2.vb)]

## <a name="to-delete-existing-records-from-a-database"></a>データベースから既存のレコードを削除するには

- レコードを削除するには、メソッドを呼び出し、 `TableAdapter.Delete` 元の値を渡してレコードを検索します。

    > [!NOTE]
    > オブジェクトは、メソッドに渡すために元の値を保持する必要があり `Delete` ます。 この例では、プレフィックスを持つプロパティを使用して `orig` 、元の値を格納します。

     次の例では、オブジェクトの `Customers` 元の値をメソッドに渡して、テーブルからレコードを削除し `Customer` `TableAdapter.Delete` ます。

     [!code-csharp[VbRaddataSaving#25](../data-tools/codesnippet/CSharp/save-data-from-an-object-to-a-database_3.cs)]
     [!code-vb[VbRaddataSaving#25](../data-tools/codesnippet/VisualBasic/save-data-from-an-object-to-a-database_3.vb)]

## <a name="net-security"></a>.NET セキュリティ

データベースのテーブルで、選択した `INSERT` 、、またはを実行する権限が必要 `UPDATE` `DELETE` です。

## <a name="see-also"></a>関連項目

- [データをデータベースに保存する](../data-tools/save-data-back-to-the-database.md)
