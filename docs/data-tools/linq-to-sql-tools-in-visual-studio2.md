---
title: LINQ to SQL の O/R デザイナーの概要
description: Visual Studio の LINQ to SQL ツールの概要を取得します。 オブジェクト リレーショナル デザイナー (O/R デザイナー) について学習します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: overview
ms.assetid: 45e477c0-5c6b-41f9-b2d0-2808fb4f6537
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: 20473125814b1ee0569579c7248b7b940cd31500
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99858645"
---
# <a name="linq-to-sql-tools-in-visual-studio"></a>Visual Studio の LINQ to SQL ツール

LINQ to SQL は、Microsoft によってリリースされた最初のオブジェクト リレーショナル マッピング テクノロジです。 これは基本のシナリオで適切に動作し、Visual Studio で今後もサポートされますが、開発はもうされません。 LINQ to SQL は、既にそれが使用されているレガシ アプリケーションの保守時、または SQL Server を使用する、複数のテーブルとマッピングする必要がない単純なアプリケーションで使用してください。 一般に、新しいアプリケーションでオブジェクト リレーショナル マッピング レイヤーが必要な場合は、Entity Framework を使用してください。

## <a name="install-the-linq-to-sql-tools"></a>LINQ to SQL ツールをインストールする

Visual Studio で、SQL テーブルを表す LINQ to SQL クラスを作成するには、**オブジェクト リレーショナル デザイナー** (**O/R デザイナー**) を使用します。 O/R デザイナーは、.dbml ファイルを編集するための UI です。 デザイン サーフェイスで .dbml ファイルを編集する場合、LINQ to SQL ツールが必要です。これは、Visual Studio のどのワークロードの一部としても既定ではインストールされません。

LINQ to SQL ツールをインストールするには、Visual Studio のインストーラーを起動して **[変更]** 、 **[個別のコンポーネント]** タブを順に選択し、次いで **[コード ツール]** カテゴリの下の **[LINQ to SQL ツール]** を選択します。

## <a name="what-is-the-or-designer"></a>O/R デザイナーとは

**O/R デザイナー** のデザイン サーフェイスには、左側のエンティティ ウィンドウと右側のメソッド ウィンドウの 2 つ明確な領域があります。 エンティティ ペインは、エンティティ クラス、関連付け、および継承階層を表示するメインのデザイン サーフェイスです。 メソッド ペインは、ストアド プロシージャと関数にマッピングされる <xref:System.Data.Linq.DataContext> のメソッドを表示するデザイン サーフェイスです。

**O/R デザイナー** には、[LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/index) のエンティティ クラスと、データベース内のオブジェクトを使用した関連付け (リレーションシップ) を作成するビジュアル デザイン サーフェイスがあります。 つまり、**O/R デザイナー** では、データベース内のオブジェクトにマップするオブジェクト モデルをアプリケーション内に作成できます。 また、エンティティ クラスとデータベース間でデータを送受信できる、厳密に型指定された <xref:System.Data.Linq.DataContext> も生成できます。 **O/R デザイナー** には、<xref:System.Data.Linq.DataContext> のメソッドにストアド プロシージャと関数をマップする、データを返し、エンティティ クラスに指定する機能もあります。 最後に、**O/R デザイナー** には、エンティティ クラス間で継承関係をデザインする機能もあります。

## <a name="open-the-or-designer"></a>O/R デザイナーを開く

自分のプロジェクトに LINQ to SQL エンティティ モデルを追加するには、 **[プロジェクト]**  >  **[新しい項目の追加]** の順に選択し、プロジェクト項目の一覧から **[LINQ to SQL クラス]** を選択します。

![LINQ to SQL クラス](../data-tools/media/raddata-linq-to-sql-classes.png)

Visual Studio によって、 *.dbml* ファイルが作成され、それがお使いのソリューションに追加されます。 これが、XML マッピング ファイルとそれに関連するコード ファイルです。

![ソリューション エクスプローラーでの LINQ to SQL クラス](../data-tools/media/raddata-linq-to-sql-classes-in-solution-explorer.png)

*.dbml* ファイルを選択すると、Visual Studio により、モデルを視覚的に作成する、**O/R デザイナー** 画面が表示されます。 次の図は、Northwind の `Customers` テーブルと `Orders` テーブルが **サーバー エクスプローラー** からドラッグされた後のデザイナーを示しています。 テーブル間の関係に着目してください。

![LINQ to SQL デザイナー](../data-tools/media/raddata-linq-to-sql-designer.png)

> [!IMPORTANT]
> **O/R デザイナー** は、1:1 のマッピング関係のみがサポートされる単純なオブジェクト リレーショナル マッパーです。 つまり、エンティティ クラスには、データベース テーブルまたはビューとの 1:1 のマッピング関係しか持たせることができません。 結合テーブルにエンティティ クラスをマッピングする場合などの複雑なマッピングは、サポートされていません。複雑なマッピングには、Entity Framework を使用します。 また、デザイナーは一方向のコード ジェネレーターです。 つまり、デザイナー サーフェイスに加えた変更だけがコード ファイルに反映されます。 **O/R デザイナー** には、コード ファイルに手動で加えた変更は反映されません。 コード ファイルに手動で加えた変更は、デザイナーを保存してコードを再生成するときに上書きされます。 ユーザー コードを追加し、によって生成されたクラスを拡張する方法については、 **O/R デザイナー** を参照してください [方法。O/R デザイナーで生成されたコードを拡張する](../data-tools/how-to-extend-code-generated-by-the-o-r-designer.md)。

## <a name="create-and-configure-the-datacontext"></a>DataContext を作成および構成する

プロジェクトに **LINQ to SQL クラス** 項目を追加し、**O/R デザイナー** を開くと、空のデザイン サーフェイスに、構成の準備ができた空の <xref:System.Data.Linq.DataContext> が表示されます。 <xref:System.Data.Linq.DataContext> は、デザイン サーフェイスにドラッグされた最初の項目から提供される接続情報で構成されます。 したがって、<xref:System.Data.Linq.DataContext> は、デザイン サーフェイスにドロップされた最初の項目の接続情報によって構成されます。 <xref:System.Data.Linq.DataContext> クラスの詳細については、「[DataContext メソッド (O/R デザイナー)](../data-tools/datacontext-methods-o-r-designer.md)」を参照してください。

## <a name="create-entity-classes-that-map-to-database-tables-and-views"></a>データベース テーブルおよびビューにマップするエンティティ クラスを作成する

テーブルやビューにマッピングするエンティティ クラスを作成するには、データベース テーブルやビューを **サーバー エクスプローラー** または **データベース エクスプローラー** から **O/R デザイナー** にドラッグします。 前のセクションで示したように、<xref:System.Data.Linq.DataContext> は、デザイン サーフェイスにドラッグされる最初の項目が提供する接続情報で構成されます。 **O/R デザイナー** に別の接続を使用する項目が後で追加された場合は、<xref:System.Data.Linq.DataContext> の接続を変更できます。 詳細については、「[方法:テーブルとビューにマップされた LINQ to SQL クラスを作成する (O/R デザイナー)](../data-tools/how-to-create-linq-to-sql-classes-mapped-to-tables-and-views-o-r-designer.md)」を参照してください。

## <a name="create-datacontext-methods-that-call-stored-procedures-and-functions"></a>ストアド プロシージャおよび関数を呼び出す DataContext メソッドを作成する

ストアド プロシージャまたは関数を呼び出す (それらにマップされている) <xref:System.Data.Linq.DataContext> メソッドを作成するには、それらを **サーバー エクスプローラー** または **データベース エクスプローラー** から **O/R デザイナー** にドラッグします。 ストアド プロシージャと関数は、<xref:System.Data.Linq.DataContext> のメソッドとして **O/R デザイナー** に追加されます。

> [!NOTE]
> **サーバー エクスプローラー** または **データベース エクスプローラー** から **O/R デザイナー** にストアド プロシージャまたは関数をドラッグする場合、生成される <xref:System.Data.Linq.DataContext> メソッドの戻り値の型は、項目をドロップする場所によって異なります。 詳細については、「[DataContext メソッド (O/R デザイナー)](../data-tools/datacontext-methods-o-r-designer.md)」を参照してください。

## <a name="configure-a-datacontext-to-use-stored-procedures-to-save-data-between-entity-classes-and-a-database"></a>エンティティ クラスとデータベース間のデータを保存するようストアド プロシージャを使用して DataContext を構成する

前に述べたように、ストアド プロシージャと関数を呼び出す <xref:System.Data.Linq.DataContext> のメソッドを作成できます。 また、挿入、更新、削除を実行する LINQ to SQL の既定の実行時動作に使用できる、ストアド プロシージャを割り当てることもできます。 詳細については、「[方法:更新、挿入、および削除を実行するストアド プロシージャを割り当てる (O/R デザイナー)](../data-tools/how-to-assign-stored-procedures-to-perform-updates-inserts-and-deletes-o-r-designer.md)」を参照してください。

## <a name="inheritance-and-the-or-designer"></a>継承と O/R デザイナー

LINQ to SQL のクラスは、他のオブジェクトと同様に、継承を使用して他のクラスから派生させることができます。 データベースでは、継承関係が複数の方法で作成されます。 **O/R デザイナー** では、多くのリレーショナル システムに実装されている単一テーブル継承の概念があります。 詳細については、「[方法:O/R デザイナーを使用して継承を構成する](../data-tools/how-to-configure-inheritance-by-using-the-o-r-designer.md)」を参照してください。

## <a name="linq-to-sql-queries"></a>LINQ to SQL クエリ

**O/R デザイナー** で作成されたエンティティ クラスは、[統合言語クエリ (LINQ)](/dotnet/csharp/linq/) で使用するように設計されています。 詳細については、「[方法:クエリで情報を取得する](/dotnet/framework/data/adonet/sql/linq/how-to-query-for-information)」を参照してください。

## <a name="separate-the-generated-datacontext-and-entity-class-code-into-different-namespaces"></a>生成された DataContext とエンティティ クラス コードを別の名前空間に分離する

**O/R デザイナー** の <xref:System.Data.Linq.DataContext> には、**Context Namespace** プロパティと **Entity Namespace** プロパティがあります。 これらのプロパティは、<xref:System.Data.Linq.DataContext> およびエンティティ クラスのコードが生成される名前空間を決定します。 既定では、これらのプロパティは空であり、<xref:System.Data.Linq.DataContext> およびエンティティ クラスはアプリケーションの名前空間に生成されます。 アプリケーションの名前空間以外の名前空間にコードを生成するには、**[Context Namespace]** プロパティ、**[Entity Namespace]** プロパティ、またはその両方に値を入力します。

## <a name="reference-content"></a>リファレンス コンテンツ

- <xref:System.Linq>
- <xref:System.Data.Linq>

## <a name="see-also"></a>関連項目

- [LINQ to SQL (.NET Framework)](/dotnet/framework/data/adonet/sql/linq/index)
- [よく寄せられる質問 (.NET Framework)](/dotnet/framework/data/adonet/sql/linq/frequently-asked-questions)
