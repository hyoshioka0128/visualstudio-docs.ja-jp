---
title: LINQ to SQL クラスをテーブル/ビューにマップする (O/R デザイナー)
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 0fb78bbc-7a78-4ab4-b32f-85ece912e660
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: b0e3103c1b4faa62ff82dafe8ba4aa0ef9193f06
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75586498"
---
# <a name="how-to-create-linq-to-sql-classes-mapped-to-tables-and-views-or-designer"></a>方法: テーブルとビューにマップされた LINQ to SQL クラスを作成する (O/R デザイナー)

データベース テーブルおよびビューにマップされた [!INCLUDE[vbtecdlinq](../data-tools/includes/vbtecdlinq_md.md)] クラスは、*エンティティ クラス*と呼ばれます。 エンティティ クラスはレコードにマップされますが、エンティティ クラスの個々のプロパティはレコードを構成する個々の列にマップされます。 テーブルまたはビューを**サーバーエクスプローラー**から、または[Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)に**データベースエクスプローラー**ドラッグして、データベースのテーブルまたはビューに基づくエンティティクラスを作成します。 **O/R デザイナー**は、クラスを生成し、特定の [!INCLUDE[vbtecdlinq](../data-tools/includes/vbtecdlinq_md.md)] 属性を適用して [!INCLUDE[vbtecdlinq](../data-tools/includes/vbtecdlinq_md.md)] 機能 (<xref:System.Data.Linq.DataContext>のデータ通信と編集機能) を有効にします。 [!INCLUDE[vbtecdlinq](../data-tools/includes/vbtecdlinq_md.md)] クラスの詳細については、「 [LINQ to SQL オブジェクトモデル](/dotnet/framework/data/adonet/sql/linq/the-linq-to-sql-object-model)」を参照してください。

> [!NOTE]
> **O/R デザイナー**は、1:1 のマッピング関係のみをサポートするため、単純なオブジェクトリレーショナルマッパーです。 つまり、エンティティ クラスには、データベース テーブルまたはビューとの 1:1 のマッピング関係しか持たせることができません。 1 つのエンティティ クラスを複数のテーブルにマップするなど、複雑なマッピングはサポートされていません。 ただし、複数の関連テーブルを結合するビューにエンティティ クラスをマップすることはできます。

## <a name="create-linq-to-sql-classes-that-are-mapped-to-database-tables-or-views"></a>データベース テーブルまたはビューにマップされる LINQ to SQL クラスの作成

**サーバーエクスプローラー**または**データベースエクスプローラー**のテーブルまたはビューを**O/R デザイナー**にドラッグすると、更新の実行に使用される <xref:System.Data.Linq.DataContext> メソッドに加えて、エンティティクラスが作成されます。

既定では、[!INCLUDE[vbtecdlinq](../data-tools/includes/vbtecdlinq_md.md)] ランタイムによって、更新可能なエンティティ クラスの変更をデータベースに保存するロジックが作成されます。 このロジックは、テーブルのスキーマ (列定義と主キー情報) に基づいています。 この動作が不要な場合は、既定の [!INCLUDE[vbtecdlinq](../data-tools/includes/vbtecdlinq_md.md)] の実行時の動作を使用するのではなく、ストアドプロシージャを使用して挿入、更新、および削除を実行するようにエンティティクラスを構成することができます。 詳細については、「[方法: 更新、挿入、および削除を実行するストアドプロシージャを割り当てる (O/R デザイナー)](../data-tools/how-to-assign-stored-procedures-to-perform-updates-inserts-and-deletes-o-r-designer.md)」を参照してください。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

### <a name="to-create-linq-to-sql-classes-that-are-mapped-to-database-tables-or-views"></a>データベース テーブルまたはビューにマップされる LINQ to SQL クラスを作成するには

1. **サーバー エクスプローラー**または**データベース エクスプローラー**で、 **[テーブル]** または **[ビュー]** を展開し、アプリケーションで使用するデータベース テーブルまたはビューを探します。

2. テーブルまたはビューを**O/R デザイナー**にドラッグします。

     エンティティ クラスが作成され、デザイン サーフェイスに表示されます。 このエンティティ クラスには、選択されたテーブルまたはビューの列にマップされるプロパティが含まれています。

## <a name="create-an-object-data-source-and-display-the-data-on-a-form"></a>オブジェクト データ ソースの作成とフォームへのデータの表示

**O/R デザイナー**を使用してエンティティクラスを作成した後、オブジェクトデータソースを作成し、エンティティクラスを使用して [[データソース] ウィンドウ](add-new-data-sources.md#data-sources-window)を設定できます。

### <a name="to-create-an-object-data-source-based-on-linq-to-sql-entity-classes"></a>LINQ to SQL エンティティ クラスに基づいてオブジェクト データ ソースを作成するには

1. **[ビルド]** メニューの **[ソリューションのビルド]** をクリックしてプロジェクトをビルドします。

2. データ **[ソース]** ウィンドウを開くには、 **[データ]** メニューの **[データソースの表示]** をクリックします。

3. **[データ ソース]** ウィンドウで、 **[新しいデータ ソースの追加]** をクリックします。

4. **[データソースの種類を選択]** ページで、 **[オブジェクト]** をクリックし、 **[次へ]** をクリックします。

5. ノードを展開し、クラスを探して選択します。

    > [!NOTE]
    > **Customer** クラスが使用可能でない場合は、ウィザードをキャンセルし、プロジェクトをビルドしてからウィザードを再実行します。

6. **[完了]** をクリックしてデータ ソースを作成し、**Customer** エンティティ クラスを **[データ ソース]** ウィンドウに追加します。

7. **[データ ソース]** ウィンドウからフォームに項目をドラッグします。

## <a name="see-also"></a>関連項目

- [Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
- [チュートリアル: LINQ to SQL クラスの作成 (O-R デザイナー)](how-to-create-linq-to-sql-classes-mapped-to-tables-and-views-o-r-designer.md)
- [DataContext メソッド (O/R デザイナー)](../data-tools/datacontext-methods-o-r-designer.md)
- [方法: ストアド プロシージャや関数にマップされる DataContext メソッドを作成する (O/R デザイナー)](../data-tools/how-to-create-datacontext-methods-mapped-to-stored-procedures-and-functions-o-r-designer.md)
- [LINQ to SQL オブジェクト モデル](/dotnet/framework/data/adonet/sql/linq/the-linq-to-sql-object-model)
- [チュートリアル : エンティティ クラスの挿入、更新、および削除の動作のカスタマイズ](../data-tools/walkthrough-customizing-the-insert-update-and-delete-behavior-of-entity-classes.md)
- [方法: LINQ to SQL クラス間の関連付け (リレーションシップ) を作成する (O/R デザイナー)](../data-tools/how-to-create-an-association-relationship-between-linq-to-sql-classes-o-r-designer.md)
