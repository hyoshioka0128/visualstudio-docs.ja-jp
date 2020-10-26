---
title: LINQ to SQL ツール |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
ms.assetid: 45e477c0-5c6b-41f9-b2d0-2808fb4f6537
caps.latest.revision: 15
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 470cfabd54fa5f2b92001a635477c60d45fac538
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72651517"
---
# <a name="linq-to-sql-tools-in-visual-studio"></a>Visual Studio の LINQ to SQL ツール
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

LINQ to SQL は、Microsoft によってリリースされた最初のオブジェクトリレーショナルマッピングテクノロジです。 これは基本的なシナリオで適切に動作し、Visual Studio で引き続きサポートされますが、アクティブな開発ではなくなります。 LINQ to SQL は、既に使用しているレガシアプリケーションを維持する場合や、SQL Server を使用し、複数テーブルマッピングを必要としない単純なアプリケーションの場合に使用します。 一般に、オブジェクトリレーショナルマッパーレイヤーが必要な場合は、新しいアプリケーションで Entity Framework を使用する必要があります。

 Visual Studio では、を使用して SQL テーブルを表す LINQ to SQL クラスを作成し [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] ます。

 の [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] デザイン画面には、左側の [エンティティ] ペインと右側の [メソッド] ペインの2つの異なる領域があります。 エンティティ ペインは、エンティティ クラス、関連付け、および継承階層を表示するメインのデザイン サーフェイスです。 メソッド ペインは、ストアド プロシージャと関数にマッピングされる <xref:System.Data.Linq.DataContext> のメソッドを表示するデザイン サーフェイスです。

 [!INCLUDE[vs_ordesigner_long](../includes/vs-ordesigner-long-md.md)]() は、 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] データベース内のオブジェクトに基づくエンティティクラスと関連付け (リレーションシップ) を[LINQ to SQL](https://msdn.microsoft.com/library/73d13345-eece-471a-af40-4cc7a2f11655)作成するためのビジュアルデザインサーフェイスを提供します。 つまり、[!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]は、データベース内のオブジェクトにマップされるオブジェクト モデルをアプリケーションに作成するために使用されます。 また、エンティティ クラスとデータベース間でデータを送受信するために使用する、厳密に型指定された <xref:System.Data.Linq.DataContext> も生成します。 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]は、データを返し、エンティティ クラスを設定するために、ストアド プロシージャと関数を <xref:System.Data.Linq.DataContext> のメソッドにマップする機能も提供します。 最後に、[!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]では、エンティティ クラス間の継承関係をデザインすることもできます。

## <a name="opening-the-or-designer"></a>O/R デザイナーを開く
 プロジェクトに LINQ to SQL エンティティモデルを追加するには、[&#124; プロジェクト]、[ **新しい項目の追加** ] の順に選択し、プロジェクト項目の一覧から [  **LINQ to SQL クラス** ] を選択します。

 ![LINQ to SQL クラス](../data-tools/media/raddata-linq-to-sql-classes.png "レーダーデータ LINQ to SQL クラス")

 Visual Studio によって .dbml ファイルが作成され、ソリューションに追加されます。 これは、XML マッピングファイルとそれに関連するコードファイルです。

 ![ソリューションエクスプローラーの LINQ to SQL クラス](../data-tools/media/raddata-linq-to-sql-classes-in-solution-explorer.png "ソリューションエクスプローラーの LINQ to SQL クラスのレーダーデータ")

 .Dbml ファイルを選択すると、Visual Studio には、モデルを視覚的に作成できる O/R デザイナー画面が表示されます。 次の図は、Northwind の Customers テーブルと Orders テーブルをサーバーエクスプローラーからドラッグした後のデザイナーを示しています。 テーブル間のリレーションシップに注意してください。

 ![LINQ to SQL デザイナー](../data-tools/media/raddata-linq-to-sql-designer.png "レーダーデータ LINQ to SQL デザイナー")

> [!IMPORTANT]
> は、 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] 1:1 のマッピング関係のみをサポートするため、単純なオブジェクトリレーショナルマッパーです。 つまり、エンティティ クラスには、データベース テーブルまたはビューとの 1:1 のマッピング関係しか持たせることができません。 結合テーブルへのエンティティクラスのマッピングなど、複雑なマッピングはサポートされていません。複雑なマッピングには Entity Framework を使用します。 また、デザイナーは一方向のコード ジェネレーターです。 つまり、デザイナー サーフェイスに加えた変更だけがコード ファイルに反映されます。 コード ファイルに手動で加えた変更は、[!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]に反映されません。 コード ファイルに手動で加えた変更は、デザイナーを保存してコードを再生成するときに上書きされます。 ユーザーコードを追加し、によって生成されるクラスを拡張する方法の詳細については [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] 、「 [方法: O/R デザイナーによって生成されたコードを拡張](../data-tools/how-to-extend-code-generated-by-the-o-r-designer.md)する」を参照してください。

## <a name="creating-and-configuring-the-datacontext"></a>DataContext の作成と構成
 **LINQ to SQL クラス**の項目をプロジェクトに追加してを開くと [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] 、空のデザインサーフェイスは、構成の準備が整っている空のを表し <xref:System.Data.Linq.DataContext> ます。 は、 <xref:System.Data.Linq.DataContext> デザインサーフェイスにドラッグされる最初の項目によって提供される接続情報で構成されます。「」を参照してください。 したがって、<xref:System.Data.Linq.DataContext> は、デザイン サーフェイスにドロップされた最初の項目の接続情報によって構成されます。 クラスの詳細につい <xref:System.Data.Linq.DataContext> ては、「 [DataContext メソッド (O/R デザイナー)](../data-tools/datacontext-methods-o-r-designer.md)」を参照してください。

## <a name="creating-entity-classes-that-map-to-database-tables-and-views"></a>データベース テーブルおよびビューにマップされるエンティティ クラスの作成
 テーブルとビューにマップされたエンティティクラスを作成するには、**サーバーエクスプローラー**データベースエクスプローラーからにデータベーステーブルおよびビューをドラッグし / **Database Explorer** [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] ます。 前のセクションで示したように、<xref:System.Data.Linq.DataContext> は、デザイン サーフェイスにドラッグされる最初の項目が提供する接続情報で構成されます。 別の接続を使用する項目が後で [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]に追加された場合は、<xref:System.Data.Linq.DataContext> の接続を変更できます。 詳細については、「 [方法: テーブルとビューにマップされた LINQ to SQL クラスを作成する (O/R デザイナー)](../data-tools/how-to-create-linq-to-sql-classes-mapped-to-tables-and-views-o-r-designer.md)」を参照してください。

## <a name="creating-datacontext-methods-that-call-stored-procedures-and-functions"></a>ストアド プロシージャおよび関数を呼び出す DataContext メソッドの作成
 <xref:System.Data.Linq.DataContext>ストアドプロシージャおよび関数を**サーバーエクスプローラー**データベースエクスプローラーからにドラッグすることによって、ストアドプロシージャおよび関数を呼び出す (マップされる) メソッドを作成でき / **Database Explorer** [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] ます。 ストアド プロシージャと関数は、[!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]に <xref:System.Data.Linq.DataContext> のメソッドとして追加されます。

> [!NOTE]
> ストアドプロシージャおよび関数を**サーバーエクスプローラー**データベースエクスプローラーからにドラッグした場合 / **Database Explorer** [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] 、生成されたメソッドの戻り値の型は、 <xref:System.Data.Linq.DataContext> アイテムをドロップする場所によって異なります。 詳しくは、「[DataContext メソッド (O/R デザイナー)](../data-tools/datacontext-methods-o-r-designer.md)」をご覧ください。

## <a name="configuring-a-datacontext-to-use-stored-procedures-to-save-data-between-entity-classes-and-a-database"></a>ストアド プロシージャを使用してエンティティ クラスとデータベース間でデータを保存するための DataContext の構成
 前に述べたように、ストアド プロシージャと関数を呼び出す <xref:System.Data.Linq.DataContext> のメソッドを作成できます。 また、挿入、更新、および削除を実行する既定の [!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)] ランタイムの動作の代わりに使用できる、ストアド プロシージャを割り当てることもできます。 詳細については、「 [方法: 更新、挿入、および削除を実行するストアドプロシージャを割り当てる (O/R デザイナー)](../data-tools/how-to-assign-stored-procedures-to-perform-updates-inserts-and-deletes-o-r-designer.md)」を参照してください。

## <a name="inheritance-and-the-or-designer"></a>継承と O/R デザイナー
 [!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)] クラスは、他のオブジェクトと同様に、継承を使用して他のクラスから派生できます。 データベースでは、継承関係が複数の方法で作成されます。 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]では、多くのリレーショナル システムに実装されている単一テーブル継承の概念がサポートされています。 詳細については、「 [方法: O/R デザイナーを使用して継承を構成する](../data-tools/how-to-configure-inheritance-by-using-the-o-r-designer.md)」を参照してください。

## <a name="linq-to-sql-queries"></a>LINQ to SQL クエリ
 によって作成されたエンティティクラス [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] は、 [LINQ (統合言語クエリ)](https://msdn.microsoft.com/library/a73c4aec-5d15-4e98-b962-1274021ea93d)で使用できるように設計されています。 詳細については、「 [方法: 情報を照会する](https://msdn.microsoft.com/library/e538d288-2070-40ca-9da6-4fbc68cd6ad0)」を参照してください。

## <a name="separating-the-generated-datacontext-and-entity-class-code-into-different-namespaces"></a>生成された DataContext とエンティティ クラス コードの異なる名前空間への分離
 は、の [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] **コンテキスト名前空間** プロパティと **エンティティ名前空間** プロパティを提供し <xref:System.Data.Linq.DataContext> ます。 これらのプロパティは、<xref:System.Data.Linq.DataContext> およびエンティティ クラスのコードが生成される名前空間を決定します。 既定では、これらのプロパティは空であり、<xref:System.Data.Linq.DataContext> およびエンティティ クラスはアプリケーションの名前空間に生成されます。 アプリケーションの名前空間以外の名前空間にコードを生成するには、**[Context Namespace]** プロパティ、**[Entity Namespace]** プロパティ、またはその両方に値を入力します。

## <a name="in-this-section"></a>このセクションの内容
 [DataContext メソッド (O/R デザイナー)](../data-tools/datacontext-methods-o-r-designer.md)<xref:System.Data.Linq.DataContext>メソッドとその作成方法について説明します。

 [データクラスの継承 (O/R デザイナー)](../data-tools/data-class-inheritance-o-r-designer.md) 単一テーブル継承の概念と、それがに実装される方法について説明し [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] ます。

 [方法: テーブルとビューにマップされた LINQ to SQL クラスを作成する (O/R デザイナー)](../data-tools/how-to-create-linq-to-sql-classes-mapped-to-tables-and-views-o-r-designer.md) データベース内のテーブルおよびビューにマップされるエンティティクラスを作成する方法について説明します。

 [方法: LINQ to SQL クラス間の関連付け (リレーションシップ) を作成する (O/R デザイナー)](../data-tools/how-to-create-an-association-relationship-between-linq-to-sql-classes-o-r-designer.md) エンティティクラス間のリレーションシップを作成する方法について説明し [!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)] ます。

 [方法: ストアドプロシージャおよび関数にマップされた DataContext メソッドを作成する (O/R デザイナー)](../data-tools/how-to-create-datacontext-methods-mapped-to-stored-procedures-and-functions-o-r-designer.md)<xref:System.Data.Linq.DataContext>ストアドプロシージャまたは関数が呼び出されたときにその関数を実行するメソッドを作成する方法について説明します。

 [方法: 更新、挿入、および削除を実行するストアドプロシージャを割り当てる (O/R デザイナー)](../data-tools/how-to-assign-stored-procedures-to-perform-updates-inserts-and-deletes-o-r-designer.md)<xref:System.Data.Linq.DataContext>エンティティクラスからデータベースにデータを保存するときにストアドプロシージャを使用するようにを構成する方法について説明します。

 [方法: DataContext メソッドの戻り値の型を変更する (O/R デザイナー)](../data-tools/how-to-change-the-return-type-of-a-datacontext-method-o-r-designer.md) メソッドの戻り値の型 <xref:System.Data.Linq.DataContext> を、エンティティクラスの型、または O/R デザイナーによって作成された自動生成型に設定する方法について説明します。

 [方法: エンティティクラスに検証を追加](../data-tools/how-to-add-validation-to-entity-classes.md) するプロパティの変更時およびエンティティクラスの更新時にコードを追加できる部分メソッドを生成する方法について説明します。

 [方法: 複数形化をオンまたはオフにする (O/R デザイナー)](../data-tools/how-to-turn-pluralization-on-and-off-o-r-designer.md) に追加されるクラスの名前を自動変更する方法について説明し [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] ます。

 [方法: O/R デザイナーを使用して継承を構成する](../data-tools/how-to-configure-inheritance-by-using-the-o-r-designer.md) で単一テーブルの継承を使用してエンティティクラスを構成する方法について説明し [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] ます。

 [方法: O/R デザイナーによって生成されたコードを拡張する](../data-tools/how-to-extend-code-generated-by-the-o-r-designer.md) O/R デザイナーでオブジェクトを変更したときに上書きされないコードを追加する方法と場所について説明します。

 [チュートリアル: 単一テーブル継承を使用した LINQ to SQL クラスの作成 (O/R デザイナー)](../data-tools/walkthrough-creating-linq-to-sql-classes-by-using-single-table-inheritance-o-r-designer.md) で単一テーブル継承を使用してエンティティクラスを構成する手順について説明 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] します。

 [チュートリアル: エンティティクラスの挿入、更新、および削除の動作のカスタマイズ](../data-tools/walkthrough-customizing-the-insert-update-and-delete-behavior-of-entity-classes.md)<xref:System.Data.Linq.DataContext>エンティティクラスからデータベースにデータを保存するときにストアドプロシージャを使用するようにを構成する手順について説明します。

## <a name="reference-content"></a>参照コンテンツ
 <xref:System.Linq>

 <xref:System.Data.Linq>

## <a name="see-also"></a>参照
 Visual [studio data tools for .net に関して](../data-tools/visual-studio-data-tools-for-dotnet.md)[よく寄せられる質問](https://msdn.microsoft.com/library/252ed666-0679-4eea-b71b-2f14117ef443) [LINQ to SQL](https://msdn.microsoft.com/library/73d13345-eece-471a-af40-4cc7a2f11655) [visual studio でのデータへのアクセス](../data-tools/accessing-data-in-visual-studio.md)LINQ to SQL
