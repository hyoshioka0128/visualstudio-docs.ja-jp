---
title: 選択したクラスは、1 つ以上の DataContext メソッドで戻り値の型として使用されているため、削除できません
ms.date: 11/04/2016
ms.topic: error-reference
ms.assetid: d68254a0-f3a1-47e2-aed3-a83471e1d711
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: faea45cc7198be91a45d0bb57a62ce2730011ee2
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85281332"
---
# <a name="the-selected-class-cannot-be-deleted-because-it-is-used-as-a-return-type-for-one-or-more-datacontext-methods"></a>選択したクラスは、1 つ以上の DataContext メソッドで戻り値の型として使用されているため、削除できません

1 つ以上の <xref:System.Data.Linq.DataContext> メソッドの戻り値の型が、選択されたエンティティ クラスになっています。 メソッドの戻り値の型として使用されているエンティティクラスを削除 <xref:System.Data.Linq.DataContext> すると、プロジェクトのコンパイルが失敗します。 選択したエンティティ クラスを削除するには、そのエンティティ クラスを使用する <xref:System.Data.Linq.DataContext> メソッドを特定し、戻り値の型を別のエンティティ クラスに設定します。

<xref:System.Data.Linq.DataContext> メソッドの戻り値の型を元の自動生成型に戻すには、まず**メソッド** ペインから <xref:System.Data.Linq.DataContext> メソッドを削除し、次に**サーバー エクスプローラー**/**データベース エクスプローラー**から、オブジェクトをもう一度 **O/R デザイナー**にドラッグします。

## <a name="to-correct-this-error"></a>このエラーを解決するには

1. エンティティ クラスを戻り値の型として使用する <xref:System.Data.Linq.DataContext> メソッドを特定します。そのためには、**メソッド** ペインで <xref:System.Data.Linq.DataContext> メソッドを選択し、**[プロパティ]** ウィンドウで **[戻り値の型]** プロパティを調べます。

2. **[戻り値の型]** を別のエンティティ クラスに設定するか、メソッド ペインから <xref:System.Data.Linq.DataContext> メソッドを削除します。

## <a name="see-also"></a>関連項目

- [Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
