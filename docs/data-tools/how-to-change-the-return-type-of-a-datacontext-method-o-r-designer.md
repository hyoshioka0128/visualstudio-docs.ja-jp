---
title: DataContext メソッドの戻り値の型を変更する
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: c5b66bff-6dbb-43c0-bffa-317133ca5b9e
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: da1dc0437ccd4a7fad2a24b40542a58d8310bf17
ms.sourcegitcommit: 4ae5e9817ad13edd05425febb322b5be6d3c3425
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/11/2020
ms.locfileid: "90036666"
---
# <a name="how-to-change-the-return-type-of-a-datacontext-method-or-designer"></a>方法: DataContext メソッドの戻り値の型を変更する (O/R デザイナー)
ストアドプロシージャまたは関数に基づいて作成されたメソッドの戻り値の型は、 <xref:System.Data.Linq.DataContext> **O/R デザイナー**でストアドプロシージャまたは関数を削除した場所によって異なります。 既存のエンティティ クラスに項目を直接ドロップすると、そのエンティティ クラスを戻り値の型とする <xref:System.Data.Linq.DataContext> メソッドが作成されます (ストアド プロシージャまたは関数によって返されるデータのスキーマがエンティティ クラスの形状と一致する場合)。 **O/R デザイナー**の空の領域に項目をドロップすると、 <xref:System.Data.Linq.DataContext> 自動的に生成された型を返すメソッドが作成されます。 <xref:System.Data.Linq.DataContext> メソッドをメソッド ペインに追加した後に、その戻り値の型を変更できます。 <xref:System.Data.Linq.DataContext> メソッドの戻り値の型を確認または変更するには、**[プロパティ]** ウィンドウでそのメソッドを選択し、**[Return Type]** プロパティをクリックします。

> [!NOTE]
> **[プロパティ]** ウィンドウを使用しても、戻り値の型がエンティティ クラスに設定されている <xref:System.Data.Linq.DataContext> メソッドは、自動生成型を返すようには変更できません。 <xref:System.Data.Linq.DataContext>自動生成型を返すようにメソッドを戻すには、元のデータベースオブジェクトを**O/R デザイナー**にもう一度ドラッグする必要があります。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

## <a name="to-change-the-return-type-of-a-datacontext-method-from-the-auto-generated-type-to-an-entity-class"></a>DataContext メソッドの戻り値の型を、自動生成型からエンティティ クラスに変更するには

1. メソッド ペインで <xref:System.Data.Linq.DataContext> メソッドを選択します。

2. **[プロパティ]** ウィンドウの **[戻り値の型]** を選択し、**[戻り値の型]** リストで使用可能なエンティティ クラスを選択します。 目的のエンティティクラスが一覧にない場合は、それをに追加するか、 **O/R デザイナー** で作成して一覧に追加します。

3. *.Dbml*ファイルを保存します。

## <a name="to-change-the-return-type-of-a-datacontext-method-from-an-entity-class-back-to-the-auto-generated-type"></a>DataContext メソッドの戻り値の型を、エンティティ クラスから自動生成型に変更するには

1. メソッド <xref:System.Data.Linq.DataContext> ペインでメソッドを**Methods**選択し、削除します。

2. **サーバーエクスプローラー**または**データベースエクスプローラー**から、 **O/R デザイナー**の空の領域にデータベースオブジェクトをドラッグします。

3. *.Dbml*ファイルを保存します。

## <a name="see-also"></a>参照

- [Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
- [LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/index)
- [DataContext メソッド (O/R デザイナー)](../data-tools/datacontext-methods-o-r-designer.md)
- [方法: ストアド プロシージャや関数にマップされる DataContext メソッドを作成する (O/R デザイナー)](../data-tools/how-to-create-datacontext-methods-mapped-to-stored-procedures-and-functions-o-r-designer.md)
