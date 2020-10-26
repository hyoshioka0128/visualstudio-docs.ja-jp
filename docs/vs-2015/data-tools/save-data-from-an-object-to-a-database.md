---
title: オブジェクトのデータをデータベースに保存する |Microsoft Docs
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
- data access [Visual Studio], objects
- saving data
ms.assetid: efd6135a-40cf-4b0d-8f8b-41a5aaea7057
caps.latest.revision: 12
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 6c1470c831177e74e7670d696b44fc2b0119a9a9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72607457"
---
# <a name="save-data-from-an-object-to-a-database"></a>オブジェクトからデータベースにデータを保存する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

オブジェクトの値を TableAdapter の DBDirect メソッドの1つ (たとえば、) に渡すことによって、オブジェクトのデータをデータベースに保存でき `TableAdapter.Insert` ます。

 オブジェクトのコレクションからデータを保存するには、オブジェクトのコレクションをループ処理し (たとえば、for-next ループ)、TableAdapter の DBDirect メソッドのいずれかを使用して、各オブジェクトの値をデータベースに送信します。

 既定では、データベースに対して直接実行できる TableAdapter に DBDirect メソッドが作成されます。 これらのメソッドは直接呼び出すことができ <xref:System.Data.DataSet> 、 <xref:System.Data.DataTable> 更新をデータベースに送信するために、またはオブジェクトによる変更の調整を必要としません。

> [!NOTE]
> TableAdapter を構成するときは、メインクエリで DBDirect メソッドを作成するための十分な情報が提供されている必要があります。 たとえば、主キー列が定義されていないテーブルのデータをクエリするように TableAdapter が構成されている場合、DBDirect メソッドは生成されません。

|TableAdapter DBDirect メソッド|説明|
|----------------------------------|-----------------|
|`TableAdapter.Insert`|データベースに新しいレコードを追加し、個々の列の値をメソッドのパラメーターとして渡すことができるようにします。|
|`TableAdapter.Update`|データベース内の既存のレコードを更新します。 メソッドは、 `Update` 元の列と新しい列の値をメソッドのパラメーターとして受け取ります。 元の値は元のレコードを検索するために使用され、新しい値はそのレコードを更新するために使用されます。<br /><br /> `TableAdapter.Update`メソッドは、 <xref:System.Data.DataSet> <xref:System.Data.DataTable> <xref:System.Data.DataRow> <xref:System.Data.DataRow> メソッドパラメーターとして、、、またはの配列を取得することによって、データセットの変更をデータベースに戻すためにも使用されます。|
|`TableAdapter.Delete`|メソッドパラメーターとして渡された元の列の値に基づいて、データベースから既存のレコードを削除します。|

### <a name="to-save-new-records-from-an-object-to-a-database"></a>オブジェクトからデータベースに新しいレコードを保存するには

- 値をメソッドに渡すことで、レコードを作成し `TableAdapter.Insert` ます。

     次の例では、オブジェクトの値を `Customers` メソッドに渡すことによって、テーブルに新しい顧客レコードを作成し `currentCustomer` `TableAdapter.Insert` ます。

     [!code-csharp[VbRaddataSaving#23](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form3.cs#23)]
     [!code-vb[VbRaddataSaving#23](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form3.vb#23)]

### <a name="to-update-existing-records-from-an-object-to-a-database"></a>オブジェクトの既存のレコードをデータベースに更新するには

- メソッドを呼び出してレコードを変更 `TableAdapter.Update` し、新しい値を渡してレコードを更新し、元の値を渡してレコードを検索します。

    > [!NOTE]
    > オブジェクトは、メソッドに渡すために元の値を保持する必要があり `Update` ます。 この例では、プレフィックスを持つプロパティを使用して `orig` 、元の値を格納します。

     次の例では、 `Customers` オブジェクトの新しい値と元の値をメソッドに渡すことによって、テーブル内の既存のレコードを更新し `Customer` `TableAdapter.Update` ます。

     [!code-csharp[VbRaddataSaving#24](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form3.cs#24)]
     [!code-vb[VbRaddataSaving#24](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form3.vb#24)]

### <a name="to-delete-existing-records-from-a-database"></a>データベースから既存のレコードを削除するには

- レコードを削除するには、メソッドを呼び出し、 `TableAdapter.Delete` 元の値を渡してレコードを検索します。

    > [!NOTE]
    > オブジェクトは、メソッドに渡すために元の値を保持する必要があり `Delete` ます。 この例では、プレフィックスを持つプロパティを使用して `orig` 、元の値を格納します。

     次の例では、オブジェクトの `Customers` 元の値をメソッドに渡して、テーブルからレコードを削除し `Customer` `TableAdapter.Delete` ます。

     [!code-csharp[VbRaddataSaving#25](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form3.cs#25)]
     [!code-vb[VbRaddataSaving#25](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form3.vb#25)]

## <a name="net-framework-security"></a>.NET Framework のセキュリティ
 データベースのテーブルで、選択した挿入、更新、または削除を実行する権限が必要です。

## <a name="see-also"></a>参照
 [データをデータベースに保存する](../data-tools/save-data-back-to-the-database.md)
