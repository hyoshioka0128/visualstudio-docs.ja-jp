---
title: '方法: トランザクションを使用してデータを保存する'
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- saving data, using transactions
- System.Transactions namespace
- transactions, saving data
- data [Visual Studio], saving
ms.assetid: 8b835e8f-34a3-413d-9bb5-ebaeb87f1198
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 40894adefb42d6de077a2e2812d26f90bc5f40dd
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85281696"
---
# <a name="how-to-save-data-by-using-a-transaction"></a>方法: トランザクションを使用してデータを保存する

トランザクションにデータを保存するには、 <xref:System.Transactions> 名前空間を使用します。 オブジェクトを使用して、 <xref:System.Transactions.TransactionScope> 自動的に管理されるトランザクションに参加します。

プロジェクト*は、system.string アセンブリへ*の参照を使用して作成されるわけではないため、トランザクションを使用するプロジェクトへの参照を手動で追加する必要があります。

トランザクションを実装する最も簡単な方法は、ステートメントでオブジェクトをインスタンス化することです <xref:System.Transactions.TransactionScope> `using` 。 (詳細については、「 [using ステートメント](/dotnet/visual-basic/language-reference/statements/using-statement)」および「 [using ステートメント](/dotnet/csharp/language-reference/keywords/using-statement)」を参照してください)。ステートメント内で実行されるコードは、 `using` トランザクションに参加します。

トランザクションをコミットするには、 <xref:System.Transactions.TransactionScope.Complete%2A> using ブロックの最後のステートメントとしてメソッドを呼び出します。

トランザクションをロールバックするには、メソッドを呼び出す前に例外をスローし <xref:System.Transactions.TransactionScope.Complete%2A> ます。

## <a name="to-add-a-reference-to-the-systemtransactionsdll"></a>System.Transactions.dll への参照を追加するには

1. **[プロジェクト]** メニューの **[参照の追加]** を選択します。

2. [ **.Net** ] タブ (SQL Server プロジェクトの [**SQL Server** ] タブ) で [ **system.string] を選択し**、[ **OK**] を選択します。

     *System.Transactions.dll*への参照がプロジェクトに追加されます。

## <a name="to-save-data-in-a-transaction"></a>トランザクションにデータを保存するには

- トランザクションを含む using ステートメント内にデータを保存するコードを追加します。 次のコードは、using ステートメントでオブジェクトを作成およびインスタンス化する方法を示してい <xref:System.Transactions.TransactionScope> ます。

     [!code-vb[VbRaddataSaving#11](../data-tools/codesnippet/VisualBasic/save-data-by-using-a-transaction_1.vb)]
     [!code-csharp[VbRaddataSaving#11](../data-tools/codesnippet/CSharp/save-data-by-using-a-transaction_1.cs)]

## <a name="see-also"></a>関連項目

- [データをデータベースに保存する](../data-tools/save-data-back-to-the-database.md)
- [チュートリアル: トランザクションにデータを保存する](../data-tools/save-data-in-a-transaction.md)
