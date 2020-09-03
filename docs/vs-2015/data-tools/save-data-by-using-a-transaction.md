---
title: トランザクションを使用してデータを保存する |Microsoft Docs
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
- saving data, using transactions
- System.Transactions namespace
- transactions, saving data
- data [Visual Studio], saving
ms.assetid: 8b835e8f-34a3-413d-9bb5-ebaeb87f1198
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 85f3584073523e748168faf569aa918ba912fbf8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72652833"
---
# <a name="save-data-by-using-a-transaction"></a>トランザクションを使用してデータを保存する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

トランザクションにデータを保存するには、 <xref:System.Transactions> 名前空間を使用します。 オブジェクトを使用して、 <xref:System.Transactions.TransactionScope> 自動的に管理されるトランザクションに参加します。

 プロジェクトは、system.string アセンブリへの参照を使用して作成されるわけではないため、トランザクションを使用するプロジェクトへの参照を手動で追加する必要があります。

> [!NOTE]
> <xref:System.Transactions>名前空間は、Windows 2000 以降でサポートされています。

 トランザクションを実装する最も簡単な方法は、ステートメントでオブジェクトをインスタンス化することです <xref:System.Transactions.TransactionScope> `using` 。 (詳細については、「 [Using ステートメント](https://msdn.microsoft.com/library/665d1580-dd54-4e96-a9a9-6be2a68948f1)」および「 [using ステートメント](https://msdn.microsoft.com/library/afc355e6-f0b9-4240-94dd-0d93f17d9fc3)」を参照してください)。ステートメント内で実行されるコードは、 `using` トランザクションに参加します。

 トランザクションをコミットするには、 <xref:System.Transactions.TransactionScope.Complete%2A> using ブロックの最後のステートメントとしてメソッドを呼び出します。

 トランザクションをロールバックするには、メソッドを呼び出す前に例外をスローし <xref:System.Transactions.TransactionScope.Complete%2A> ます。

 詳細については、「 [トランザクションにデータを保存する](../data-tools/save-data-in-a-transaction.md)」を参照してください。

### <a name="to-add-a-reference-to-the-systemtransactions-dll"></a>System.string dll への参照を追加するには

1. **[プロジェクト]** メニューの **[参照の追加]** を選択します。

2. [ **.Net** ] タブ (SQL Server プロジェクトの [**SQL Server** ] タブ) で [ **system.string] を選択し**、[ **OK**] を選択します。

     System.Transactions.dll への参照がプロジェクトに追加されます。

### <a name="to-save-data-in-a-transaction"></a>トランザクションにデータを保存するには

- トランザクションを含む using ステートメント内にデータを保存するコードを追加します。 次のコードは、using ステートメントでオブジェクトを作成およびインスタンス化する方法を示してい <xref:System.Transactions.TransactionScope> ます。

     [!code-csharp[VbRaddataSaving#11](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form2.cs#11)]
     [!code-vb[VbRaddataSaving#11](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form2.vb#11)]

## <a name="see-also"></a>参照
 [データをデータベースに保存する](../data-tools/save-data-back-to-the-database.md)
