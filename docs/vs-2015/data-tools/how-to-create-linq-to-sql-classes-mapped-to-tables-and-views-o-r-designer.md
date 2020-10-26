---
title: '方法: テーブルとビューにマップされた LINQ to SQL クラスを作成する (O/R デザイナー) |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
ms.assetid: 0fb78bbc-7a78-4ab4-b32f-85ece912e660
caps.latest.revision: 7
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 7a63e81abcae508487afa40d0778c0f9e9b9caf4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72665926"
---
# <a name="how-to-create-linq-to-sql-classes-mapped-to-tables-and-views-or-designer"></a>方法: テーブルとビューにマップされた LINQ to SQL クラスを作成する (O/R デザイナー)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]
データベーステーブルおよびビューにマップされている LINQ to SQL クラスは、 *エンティティクラス*と呼ばれます。 エンティティ クラスはレコードにマップされますが、エンティティ クラスの個々のプロパティはレコードを構成する個々の列にマップされます。 テーブルまたはビューを**サーバーエクスプローラー** / **データベースエクスプローラー**から[Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)にドラッグして、データベースのテーブルまたはビューに基づくエンティティクラスを作成します。 によって [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] クラスが生成され、特定の [!有効にする属性の LINQ to SQL [!LINQ to SQL 機能 (のデータ通信と編集機能 <xref:System.Data.Linq.DataContext> )。 詳細については、「」を参照してください。LINQ to SQL クラスについては、「 [LINQ to SQL オブジェクトモデル](https://msdn.microsoft.com/library/81dd0c37-e2a4-4694-83b0-f2e49e693810)」を参照してください。

> [!NOTE]
> は、 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] 1:1 のマッピング関係のみをサポートするため、単純なオブジェクトリレーショナルマッパーです。 つまり、エンティティ クラスには、データベース テーブルまたはビューとの 1:1 のマッピング関係しか持たせることができません。 1 つのエンティティ クラスを複数のテーブルにマップするなど、複雑なマッピングはサポートされていません。 ただし、複数の関連テーブルを結合するビューにエンティティ クラスをマップすることはできます。

## <a name="create-linq-to-sql-classes-that-are-mapped-to-database-tables-or-views"></a>データベース テーブルまたはビューにマップされる LINQ to SQL クラスの作成
 テーブルまたはビューを**サーバーエクスプローラー**データベースエクスプローラーからにドラッグする / **Database Explorer**と、 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] <xref:System.Data.Linq.DataContext> 更新の実行に使用されるメソッドに加えて、エンティティクラスが作成されます。

 既定では、[!LINQ to SQL ランタイムは、更新可能なエンティティクラスからデータベースに変更を保存するロジックを作成します。 このロジックは、テーブルのスキーマ (列定義と主キー情報) に基づいています。 この動作が不要な場合は、既定の [! を使用する代わりに、ストアドプロシージャを使用して挿入、更新、および削除を実行するようにエンティティクラスを構成することができます。実行時の動作を LINQ to SQL します。 詳細については、「 [方法: 更新、挿入、および削除を実行するストアドプロシージャを割り当てる (O/R デザイナー)](../data-tools/how-to-assign-stored-procedures-to-perform-updates-inserts-and-deletes-o-r-designer.md)」を参照してください。

 [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]

#### <a name="to-create-linq-to-sql-classes-that-are-mapped-to-database-tables-or-views"></a>データベース テーブルまたはビューにマップされる LINQ to SQL クラスを作成するには

1. **サーバー** / **データベースエクスプローラー**で、[**テーブル**] または [**ビュー** ] を展開し、アプリケーションで使用するデータベーステーブルまたはビューを探します。

2. テーブルまたはビューを [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]にドラッグします。

     エンティティ クラスが作成され、デザイン サーフェイスに表示されます。 このエンティティ クラスには、選択されたテーブルまたはビューの列にマップされるプロパティが含まれています。

## <a name="create-an-object-data-source-and-display-the-data-on-a-form"></a>オブジェクト データ ソースの作成とフォームへのデータの表示
 を使用してエンティティクラスを作成した後は、 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] オブジェクトデータソースを作成し、エンティティクラスを使用して [ [データソース] ウィンドウ](https://msdn.microsoft.com/library/0d20f699-cc95-45b3-8ecb-c7edf1f67992) を設定できます。

#### <a name="to-create-an-object-data-source-based-on-linq-to-sql-entity-classes"></a>LINQ to SQL エンティティ クラスに基づいてオブジェクト データ ソースを作成するには

1. **[ビルド]** メニューの **[ソリューションのビルド]** をクリックしてプロジェクトをビルドします。

2. **[データ]** メニューの **[データ ソースの表示]** をクリックします。

3. **[データ ソース]** ウィンドウで、 **[新しいデータ ソースの追加]** をクリックします。

4. **[データソースの種類を選択]** ページで、**[オブジェクト]** をクリックし、**[次へ]** をクリックします。

5. ノードを展開し、クラスを探して選択します。

    > [!NOTE]
    > **Customer** クラスが使用可能でない場合は、ウィザードをキャンセルし、プロジェクトをビルドしてからウィザードを再実行します。

6. **[完了]** をクリックしてデータ ソースを作成し、**Customer** エンティティ クラスを **[データ ソース]** ウィンドウに追加します。

7. **[データ ソース]** ウィンドウからフォームに項目をドラッグします。

## <a name="see-also"></a>こちらもご覧ください

- [Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
- [チュートリアル: LINQ to SQL クラスの作成 (O/R デザイナー)](https://msdn.microsoft.com/library/35aad4a4-2e8a-46e2-ae09-5fbfd333c233)
- [DataContext メソッド (O/R デザイナー)](../data-tools/datacontext-methods-o-r-designer.md)
- [方法: ストアド プロシージャや関数にマップされる DataContext メソッドを作成する (O/R デザイナー)](../data-tools/how-to-create-datacontext-methods-mapped-to-stored-procedures-and-functions-o-r-designer.md)
- [LINQ to SQL オブジェクト モデル](https://msdn.microsoft.com/library/81dd0c37-e2a4-4694-83b0-f2e49e693810)
- [チュートリアル: エンティティ クラスの挿入、更新、および削除の動作のカスタマイズ](../data-tools/walkthrough-customizing-the-insert-update-and-delete-behavior-of-entity-classes.md)
- [チュートリアル: エンティティ クラスに検証を追加する](https://msdn.microsoft.com/library/85b06a02-b2e3-4534-95b8-d077c8d4c1d7)
- [方法: LINQ to SQL クラス間の関連付け (リレーションシップ) を作成する (O/R デザイナー)](../data-tools/how-to-create-an-association-relationship-between-linq-to-sql-classes-o-r-designer.md)