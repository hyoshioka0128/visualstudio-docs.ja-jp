---
title: DataContext メソッド (O/R デザイナー) |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
ms.assetid: c149f4e5-3b61-4c33-892e-3e26d47f3eeb
caps.latest.revision: 10
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: e9d7e0eee35e0f1e62247865bd539aab8d21349d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72657398"
---
# <a name="datacontext-methods-or-designer"></a>DataContext メソッド (O/R デザイナー)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

DataContext] (assetId:/qualifyHint = False&autoUpgrade = True) メソッド ( [Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)のコンテキスト) は、 <xref:System.Data.Linq.DataContext> データベース内のストアドプロシージャと関数を実行するクラスのメソッドです (Visual Studio の場合)。

 <xref:System.Data.Linq.DataContext> クラスは、SQL Server データベースと、そのデータベースにマップされる [!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)] エンティティ クラスの間のパイプ役として機能する [!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)] クラスです。 <xref:System.Data.Linq.DataContext> クラスには、接続文字列の情報と、データベースへの接続およびデータベース内のデータの操作を行うメソッドが含まれています。 既定では、<xref:System.Data.Linq.DataContext> クラスには、更新されたデータを [!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)] クラスからデータベースに送信する <xref:System.Data.Linq.DataContext.SubmitChanges%2A> メソッドなど、呼び出すことのできるいくつかのメソッドがあります。 また、ストアド プロシージャおよび関数にマップされる追加の <xref:System.Data.Linq.DataContext> メソッドを作成することもできます。 つまり、これらのカスタム メソッドを呼び出すと、<xref:System.Data.Linq.DataContext> メソッドのマップ先となっているデータベース内のストアド プロシージャまたは関数が実行されます。 メソッドを追加して任意のクラスを拡張するのと同じように、<xref:System.Data.Linq.DataContext> クラスに新しいメソッドを追加できます。 ただし、のコンテキストでのメソッドについては、説明され <xref:System.Data.Linq.DataContext> [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] ている <xref:System.Data.Linq.DataContext> ストアドプロシージャおよび関数にマップされるメソッドがあります。

## <a name="methods-pane"></a>メソッド ペイン
 <xref:System.Data.Linq.DataContext> ストアドプロシージャおよび関数にマップされるメソッドは、のメソッドペインに表示され [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] ます。 [メソッド] ペインは、[ **エンティティ** ] ペイン (メインデザインサーフェイス) の側面に沿ったペインです。 メソッドペインには、を使用して作成したすべてのメソッドが一覧表示 <xref:System.Data.Linq.DataContext> され [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] ます。 既定では、メソッドペインは空です。ストアドプロシージャまたは関数を**サーバーエクスプローラー**データベースエクスプローラーからにドラッグして / **Database Explorer** 、 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] <xref:System.Data.Linq.DataContext> メソッドを作成し、メソッドペインにデータを設定します。 詳細については、「 [方法: ストアドプロシージャおよび関数にマップされる DataContext メソッドを作成する (O/R デザイナー)](../data-tools/how-to-create-datacontext-methods-mapped-to-stored-procedures-and-functions-o-r-designer.md)」を参照してください。

> [!NOTE]
> メソッドペインを開いて閉じるには、を右クリックし、 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] [ **メソッドペインの非表示]** または [ **メソッドペインの表示**] をクリックするか、キーボードショートカットの CTRL + 1 を使用します。

## <a name="two-types-of-datacontext-methods"></a>2 種類の DataContext メソッド
 DataContext メソッドは、データベース内のストアド プロシージャおよび関数にマップされるメソッドです。 DataContext メソッドは、[!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]のメソッド ペインで作成および追加できます。 <xref:System.Data.Linq.DataContext> メソッドには、1 つ以上の結果セットを返すものと結果セットを返さないものの 2 種類があります。

- 1 つ以上の結果セットを返す <xref:System.Data.Linq.DataContext> メソッド

     この種類の <xref:System.Data.Linq.DataContext> メソッドは、アプリケーションでデータベース内のストアド プロシージャおよび関数を実行し、結果を返すことだけが必要な場合に作成します。 詳細については、「[方法: ストアドプロシージャおよび関数にマップされる DataContext メソッドを作成する (O/R デザイナー)](../data-tools/how-to-create-datacontext-methods-mapped-to-stored-procedures-and-functions-o-r-designer.md)」、「ISingleResult」、および「」を参照してください。 \<T> <xref:System.Data.Linq.IMultipleResults>

- 結果セットを返さない <xref:System.Data.Linq.DataContext> メソッド (特定のエンティティ クラスの挿入、更新、削除など)

     この種類の <xref:System.Data.Linq.DataContext> メソッドは、エンティティ クラスとデータベース間で変更されたデータを保存するために、既定の [!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)] の動作を使用するのではなく、アプリケーションでストアド プロシージャを実行する必要がある場合に作成します。 詳細については、「 [方法: 更新、挿入、および削除を実行するストアドプロシージャを割り当てる (O/R デザイナー)](../data-tools/how-to-assign-stored-procedures-to-perform-updates-inserts-and-deletes-o-r-designer.md)」を参照してください。

## <a name="return-types-of-datacontext-methods"></a>DataContext メソッドの戻り値の型
 ストアドプロシージャおよび関数を**サーバーエクスプローラー**データベースエクスプローラーからにドラッグした場合 / **Database Explorer** [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] 、生成されたメソッドの戻り値の型は、 <xref:System.Data.Linq.DataContext> アイテムをドロップする場所によって異なります。 既存のエンティティクラスに項目を直接ドロップする <xref:System.Data.Linq.DataContext> と、エンティティクラスの戻り値の型を持つメソッドが作成されます。の空の領域 (いずれかのペイン) に項目をドロップすると、 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] <xref:System.Data.Linq.DataContext> 自動的に生成された型を返すメソッドが作成されます。 作成される自動生成の型は、ストアド プロシージャ名または関数名に一致する名前と、そのストアド プロシージャまたは関数によって返される各フィールドにマップされるプロパティを持ちます。

> [!NOTE]
> <xref:System.Data.Linq.DataContext> メソッドをメソッド ペインに追加した後に、その戻り値の型を変更できます。 <xref:System.Data.Linq.DataContext> メソッドの戻り値の型を確認または変更するには、**[プロパティ]** ウィンドウでメソッドを選択し、**[戻り値の型]** プロパティを調べます。 詳細については、「 [方法: DataContext メソッドの戻り値の型を変更する (O/R デザイナー)](../data-tools/how-to-change-the-return-type-of-a-datacontext-method-o-r-designer.md)」を参照してください。

 データベースから O/R デザイナー画面にドラッグしたオブジェクトには、データベース内のオブジェクトの名前に基づいて自動的に名前が付けられます。 同じオブジェクトを複数回ドラッグすると、新しい名前の末尾に名前を区別する番号が付けられます。 データベース オブジェクト名にスペースや Visual Basic または C# でサポートされない文字が含まれている場合、そのスペースまたは無効な文字はアンダースコアに置き換えられます。

## <a name="see-also"></a>参照
 [Visual LINQ to SQL Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)[ストアド](https://msdn.microsoft.com/library/73d13345-eece-471a-af40-4cc7a2f11655)[プロシージャ](https://msdn.microsoft.com/library/4d23dd7a-a85f-44ff-a717-af7d0950c0fc)の[作成方法: ストアドプロシージャおよび関数にマップされた DataContext メソッドを作成する (o/r デザイナー)](../data-tools/how-to-create-datacontext-methods-mapped-to-stored-procedures-and-functions-o-r-designer.md) [方法: 更新、挿入、および削除を実行するストアドプロシージャを割り当てる (o/r デザイナー)](../data-tools/how-to-assign-stored-procedures-to-perform-updates-inserts-and-deletes-o-r-designer.md) [チュートリアル: エンティティクラスの挿入、更新、および削除の動作のカスタマイズ](../data-tools/walkthrough-customizing-the-insert-update-and-delete-behavior-of-entity-classes.md)[チュートリアル: LINQ to SQL クラスの作成 (o-r デザイナー)](https://msdn.microsoft.com/library/35aad4a4-2e8a-46e2-ae09-5fbfd333c233)
