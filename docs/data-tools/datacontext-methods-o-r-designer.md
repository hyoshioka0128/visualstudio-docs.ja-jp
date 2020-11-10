---
title: DataContext メソッド (O-R デザイナー)
description: LINQ to SQL tools for Visual Studio のコンテキストでの DataContext メソッドについて説明します。 これらのメソッドは、データベースでストアドプロシージャおよび関数を実行します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: c149f4e5-3b61-4c33-892e-3e26d47f3eeb
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 30091a5bfd613ba9bd3738731e23153565ec4c8e
ms.sourcegitcommit: ed26b6e313b766c4d92764c303954e2385c6693e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/10/2020
ms.locfileid: "94436590"
---
# <a name="datacontext-methods-or-designer"></a>DataContext メソッド (O/R デザイナー)

<xref:System.Data.Linq.DataContext> メソッド ( [Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)のコンテキスト) は、 <xref:System.Data.Linq.DataContext> データベース内のストアドプロシージャおよび関数を実行するクラスのメソッドです。

<xref:System.Data.Linq.DataContext> クラスは、SQL Server データベースと、そのデータベースにマップされる [!INCLUDE[vbtecdlinq](../data-tools/includes/vbtecdlinq_md.md)] エンティティ クラスの間のパイプ役として機能する [!INCLUDE[vbtecdlinq](../data-tools/includes/vbtecdlinq_md.md)] クラスです。 <xref:System.Data.Linq.DataContext> クラスには、接続文字列の情報と、データベースへの接続およびデータベース内のデータの操作を行うメソッドが含まれています。 既定では、<xref:System.Data.Linq.DataContext> クラスには、更新されたデータを [!INCLUDE[vbtecdlinq](../data-tools/includes/vbtecdlinq_md.md)] クラスからデータベースに送信する <xref:System.Data.Linq.DataContext.SubmitChanges%2A> メソッドなど、呼び出すことのできるいくつかのメソッドがあります。 また、ストアド プロシージャおよび関数にマップされる追加の <xref:System.Data.Linq.DataContext> メソッドを作成することもできます。 つまり、これらのカスタムメソッドを呼び出すと、メソッドのマップ先のデータベースでストアドプロシージャまたは関数が実行され <xref:System.Data.Linq.DataContext> ます。 メソッドを追加して任意のクラスを拡張するのと同じように、<xref:System.Data.Linq.DataContext> クラスに新しいメソッドを追加できます。 ただし、 <xref:System.Data.Linq.DataContext> **O/R デザイナー** のコンテキストでのメソッドについては、説明され <xref:System.Data.Linq.DataContext> ているストアドプロシージャおよび関数にマップされるメソッドがあります。

## <a name="methods-pane"></a>メソッド ペイン

<xref:System.Data.Linq.DataContext>ストアドプロシージャおよび関数にマップされるメソッドは、 **O/R デザイナー** の [ **メソッド** ] ペインに表示されます。 **[メソッド]** ペインは、 **[エンティティ]** ペイン (メインのデザイン サーフェイス) の横に表示されているペインです。 **メソッド** ペインには、 <xref:System.Data.Linq.DataContext> **O/R デザイナー** を使用して作成したすべてのメソッドが一覧表示されます。 既定では、 **メソッド** ペインは空です。ストアドプロシージャまたは関数を **サーバーエクスプローラー** または **データベースエクスプローラー** から **O/R デザイナー** にドラッグし <xref:System.Data.Linq.DataContext> て、メソッドを作成し、 **メソッド** ペインにデータを設定します。 詳細については、「 [方法: ストアドプロシージャおよび関数にマップされる DataContext メソッドを作成する (O/R デザイナー)](../data-tools/how-to-create-datacontext-methods-mapped-to-stored-procedures-and-functions-o-r-designer.md)」を参照してください。

> [!NOTE]
> メソッドペインを開いて閉じます。そのためには、 **O/R デザイナー** を右クリックし、[ **メソッドペインの非表示]** または [ **メソッドペインの表示** ] をクリックするか、キーボードショートカットの **CTRL** + **1** を使用します。

## <a name="two-types-of-datacontext-methods"></a>2 種類の DataContext メソッド

DataContext メソッドは、データベース内のストアド プロシージャおよび関数にマップされるメソッドです。 DataContext メソッドは、 **O/R デザイナー** の [ **メソッド** ] ペインで作成および追加できます。 <xref:System.Data.Linq.DataContext> メソッドには、1 つ以上の結果セットを返すものと結果セットを返さないものの 2 種類があります。

- 1 つ以上の結果セットを返す <xref:System.Data.Linq.DataContext> メソッド

   この種類の <xref:System.Data.Linq.DataContext> メソッドは、アプリケーションでデータベース内のストアド プロシージャおよび関数を実行し、結果を返すことだけが必要な場合に作成します。 詳細については、「[方法: ストアドプロシージャおよび関数にマップされる DataContext メソッドを作成する (O/R デザイナー)](../data-tools/how-to-create-datacontext-methods-mapped-to-stored-procedures-and-functions-o-r-designer.md)」、「ISingleResult」、および「」を参照してください。 \<T> <xref:System.Data.Linq.IMultipleResults>

- 結果セットを返さない <xref:System.Data.Linq.DataContext> メソッド (特定のエンティティ クラスの挿入、更新、削除など)

   この種類の <xref:System.Data.Linq.DataContext> メソッドは、エンティティ クラスとデータベース間で変更されたデータを保存するために、既定の [!INCLUDE[vbtecdlinq](../data-tools/includes/vbtecdlinq_md.md)] の動作を使用するのではなく、アプリケーションでストアド プロシージャを実行する必要がある場合に作成します。 詳細については、「[方法:更新、挿入、および削除を実行するストアド プロシージャを割り当てる (O/R デザイナー)](../data-tools/how-to-assign-stored-procedures-to-perform-updates-inserts-and-deletes-o-r-designer.md)」を参照してください。

## <a name="return-types-of-datacontext-methods"></a>DataContext メソッドの戻り値の型

**サーバー エクスプローラー** または **データベース エクスプローラー** から **O/R デザイナー** にストアド プロシージャまたは関数をドラッグする場合、生成される <xref:System.Data.Linq.DataContext> メソッドの戻り値の型は、項目をドロップする場所によって異なります。 既存のエンティティクラスに項目を直接ドロップする <xref:System.Data.Linq.DataContext> と、エンティティクラスの戻り値の型を持つメソッドが作成されます。 **O/R デザイナー** の空の領域 (いずれかのペイン) に項目をドロップすると、 <xref:System.Data.Linq.DataContext> 自動的に生成された型を返すメソッドが作成されます。 自動的に生成される型には、ストアドプロシージャまたは関数の名前とプロパティに一致する名前が付けられます。この名前は、ストアドプロシージャまたは関数によって返されるフィールドにマップされます。

> [!NOTE]
> <xref:System.Data.Linq.DataContext> メソッドをメソッド ペインに追加した後に、その戻り値の型を変更できます。 <xref:System.Data.Linq.DataContext> メソッドの戻り値の型を確認または変更するには、 **[プロパティ]** ウィンドウでメソッドを選択し、 **[戻り値の型]** プロパティを調べます。 詳細については、「 [方法: DataContext メソッドの戻り値の型を変更する (O/R デザイナー)](../data-tools/how-to-change-the-return-type-of-a-datacontext-method-o-r-designer.md)」を参照してください。

データベースから O/R デザイナー画面にドラッグしたオブジェクトには、データベース内のオブジェクトの名前に基づいて自動的に名前が付けられます。 同じオブジェクトを複数回ドラッグすると、名前を区別する新しい名前の末尾に数字が追加されます。 データベース オブジェクト名にスペースや Visual Basic または C# でサポートされない文字が含まれている場合、そのスペースまたは無効な文字はアンダースコアに置き換えられます。

## <a name="see-also"></a>関連項目

- [Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
- [LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/index)
- [ストアド プロシージャ](/dotnet/framework/data/adonet/sql/linq/stored-procedures)
- [方法: ストアド プロシージャや関数にマップされる DataContext メソッドを作成する (O/R デザイナー)](../data-tools/how-to-create-datacontext-methods-mapped-to-stored-procedures-and-functions-o-r-designer.md)
- [方法: 更新、挿入、および削除を実行するストアド プロシージャを割り当てる (O/R デザイナー)](../data-tools/how-to-assign-stored-procedures-to-perform-updates-inserts-and-deletes-o-r-designer.md)
- [チュートリアル: エンティティ クラスの挿入、更新、および削除の動作のカスタマイズ](../data-tools/walkthrough-customizing-the-insert-update-and-delete-behavior-of-entity-classes.md)
- [チュートリアル: LINQ to SQL クラスの作成 (O-R デザイナー)](how-to-create-linq-to-sql-classes-mapped-to-tables-and-views-o-r-designer.md)
