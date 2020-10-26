---
title: DataContext メソッドの戻り値の型を変更しても、元に戻すことはできません |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
ms.assetid: 76b161fc-5075-4192-8d94-f15b02e199e9
caps.latest.revision: 6
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: f020aed4c1213d3db008862386704c0f63b86bde
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72662465"
---
# <a name="changing-the-return-type-of-a-datacontext-method-cannot-be-undone"></a>DataContext メソッドの戻り値の型を変更すると、元に戻せなくなります
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

DataContext メソッドの戻り値の型を変更すると、元に戻せなくなります。 自動生成された型に戻すには、項目をサーバー エクスプローラー/データベース エクスプローラーから O/R デザイナーにもう一度ドラッグする必要があります。 戻り値の型を変更してもよろしいですか?

 <xref:System.Data.Linq.DataContext> メソッドの戻り値の型は、[!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]で項目をドロップする場所によって異なります。 既存のエンティティ クラスに項目を直接ドロップすると、そのエンティティ クラスを戻り値の型とする <xref:System.Data.Linq.DataContext> メソッドが作成されます。 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]の空の領域に項目をドロップすると、自動生成された型を返す <xref:System.Data.Linq.DataContext> メソッドが作成されます。 <xref:System.Data.Linq.DataContext> メソッドをメソッド ペインに追加した後に、その戻り値の型を変更できます。 <xref:System.Data.Linq.DataContext> メソッドの戻り値の型を確認または変更するには、**[プロパティ]** ウィンドウでそのメソッドを選択し、**[Return Type]** プロパティをクリックします。

### <a name="to-change-the-return-type-of-a-datacontext"></a>DataContext の戻り値の型を変更するには

- **[はい]** をクリックします。

### <a name="to-exit-the-message-box-and-leave-the-return-type-unchanged"></a>メッセージ ボックスを終了し、現在の戻り値の型を維持するには

- **[いいえ]** をクリックします。

### <a name="to-revert-to-the-original-return-type-after-changing-the-return-type"></a>戻り値の型を変更した後で、元の戻り値の型に戻すには

1. <xref:System.Data.Linq.DataContext> で [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] メソッドを選択し、削除します。

2. **サーバー エクスプローラー/データベース エクスプローラー**で項目を探し、[!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] にドラッグします。

     元の既定の戻り値の型で <xref:System.Data.Linq.DataContext> メソッドが作成されます。

## <a name="see-also"></a>参照
 [LINQ to SQL Tools For Visual Studio](../data-tools/linq-to-sql-tools-in-visual-studio2.md) [DataContext メソッド (o/r デザイナー)](../data-tools/datacontext-methods-o-r-designer.md) [方法: ストアドプロシージャおよび関数にマップされる datacontext メソッドを作成する (o/r デザイナー)](../data-tools/how-to-create-datacontext-methods-mapped-to-stored-procedures-and-functions-o-r-designer.md) [LINQ to SQL](https://msdn.microsoft.com/library/73d13345-eece-471a-af40-4cc7a2f11655)
