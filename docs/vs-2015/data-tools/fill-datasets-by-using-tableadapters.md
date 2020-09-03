---
title: Tableadapter を使用してデータセットにデータを読み込む |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- datasets [Visual Basic]
- datasets [Visual Basic], loading data
- data retrieval
- retrieving data
- datasets [Visual Basic], filling
- data [Visual Studio], retrieving
- data [Visual Studio], datasets
ms.assetid: 55f3bfbe-db78-4486-add3-c62f49e6b9a0
caps.latest.revision: 35
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 5fd1dcf464b7628e345845ca9f371ef6de1efe88
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72672347"
---
# <a name="fill-datasets-by-using-tableadapters"></a>TableAdapters を使用してデータセットを入力する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

TableAdapter コンポーネントは、指定された1つ以上のクエリまたはストアドプロシージャに基づいて、データベースのデータをデータセットに格納します。 Tableadapter では、データベースの追加、更新、および削除を実行して、データセットに加えた変更を保持することもできます。 また、特定のテーブルに関連付けられていないグローバルコマンドを発行することもできます。

> [!NOTE]
> Tableadapter は、Visual Studio デザイナーによって生成されます。 プログラムによってデータセットを作成する場合は、.NET Framework クラスである DataAdapter を使用します。

 TableAdapter 操作の詳細については、次のトピックのいずれかに直接進むことができます。

|トピック|説明|
|-----------|-----------------|
|[Tableadapter の作成および構成](../data-tools/create-and-configure-tableadapters.md)|デザイナーを使用して Tableadapter を作成および構成する方法|
|[パラメーター付きの TableAdapter クエリを作成する](../data-tools/create-parameterized-tableadapter-queries.md)|ユーザーが TableAdapter プロシージャまたはクエリに引数を指定できるようにする方法|
|[TableAdapter で直接データベースにアクセスする](../data-tools/directly-access-the-database-with-a-tableadapter.md)|Tableadapter の Dbdirect メソッドを使用する方法|
|[データセットの読み込み中に制約をオフにする](../data-tools/turn-off-constraints-while-filling-a-dataset.md)|データの更新時に外部キー制約を使用する方法|
|[方法 : TableAdapter の機能を拡張する](../data-tools/fill-datasets-by-using-tableadapters.md)|Tableadapter にカスタムコードを追加する方法|
|[XML データのデータセットへの読み込み](../data-tools/read-xml-data-into-a-dataset.md)|XML を操作する方法|

## <a name="tableadapters-overview"></a>TableAdapter の概要
 Tableadapter は、データベースに接続し、クエリまたはストアドプロシージャを実行し、返されたデータを DataTable に格納するデザイナーで生成されたコンポーネントです。 また、Tableadapter は、更新されたデータをアプリケーションからデータベースに送り返します。 Tableadapter が関連付けられているテーブルのスキーマに準拠するデータが返される限り、TableAdapter に対して必要な数のクエリを実行できます。 次の図は、Tableadapter がメモリ内のデータベースやその他のオブジェクトとどのように対話するかを示しています。

 ![クライアント アプリケーションのデータ フロー](../data-tools/media/clientdatadiagram.gif "ClientDataDiagram")

 Tableadapter は **データセットデザイナー**で設計されていますが、tableadapter クラスはの入れ子になったクラスとして生成されません  <xref:System.Data.DataSet> 。 各データセットに固有の個別の名前空間に配置されます。 たとえば、という名前のデータセットがある場合、 `NorthwindDataSet` のに関連付けられている tableadapter は、  <xref:System.Data.DataTable> `NorthwindDataSet` `NorthwindDataSetTableAdapters` 名前空間にあります。 プログラムで特定の TableAdapter にアクセスするには、TableAdapter の新しいインスタンスを宣言する必要があります。 次に例を示します。

 [!code-csharp[VbRaddataTableAdapters#7](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataTableAdapters/CS/Class1.cs#7)]
 [!code-vb[VbRaddataTableAdapters#7](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataTableAdapters/VB/Class1.vb#7)]

## <a name="associated-datatable-schema"></a>関連付けられた DataTable スキーマ
 TableAdapter を作成する場合は、最初のクエリまたはストアドプロシージャを使用して、関連付けられている TableAdapter のスキーマを定義し <xref:System.Data.DataTable> ます。 この最初のクエリまたはストアドプロシージャを実行するには、TableAdapter の `Fill` メソッド (tableadapter に関連付けられている) を呼び出し <xref:System.Data.DataTable> ます。 TableAdapter のメインクエリに対して行われたすべての変更は、関連付けられたデータテーブルのスキーマに反映されます。 たとえば、メインクエリから列を削除すると、関連付けられているデータテーブルからも列が削除されます。 TableAdapter に対する追加のクエリで、メインクエリに含まれていない列を返す SQL ステートメントが使用されている場合、デザイナーはメインクエリと追加のクエリとの間で列の変更を同期しようとします。 詳細については、「 [方法: tableadapter を編集する](https://msdn.microsoft.com/library/ca178745-e35a-45f1-a395-23cddfd8f855)」を参照してください。

## <a name="tableadapter-update-commands"></a>TableAdapter 更新コマンド
 TableAdapter の更新機能は、TableAdapter ウィザードのメインクエリで使用できる情報の量に依存します。 たとえば、複数のテーブル (JOIN)、スカラー値、ビュー、または集約関数の結果から値を取得するように設定された TableAdapter の場合、最初の作成時には、基になるデータベースに更新を戻す機能がありません。 ただし、[ **プロパティ** ] ウィンドウでは、挿入、更新、および削除の各コマンドを手動で構成できます。

## <a name="tableadapter-queries"></a>TableAdapter クエリ
 ![複数のクエリがある TableAdapter](../data-tools/media/tableadapter.gif "TableAdapter")

 Tableadapter には、関連付けられたデータテーブルを埋めるために複数のクエリを含めることができます。 それぞれのクエリが、関連するデータ テーブルと同じスキーマに従ったデータを返す限り、アプリケーションに必要なクエリをいくつでも TableAdapter に定義できます。 この機能により、TableAdapter は異なる条件に基づいて異なる結果を読み込むことができます。

 たとえば、顧客名を含むテーブルがアプリケーションに含まれている場合、特定の文字で始まるすべての顧客名をテーブルに入力するクエリと、同じ州にあるすべての顧客をテーブルに格納するクエリを作成できます。 特定の状態の顧客を含むテーブルにデータを格納するには `Customers` 、 `FillByState` 状態の値のパラメーターを受け取るクエリを次のように作成します `SELECT * FROM Customers WHERE State = @State` 。 このクエリを実行するには、メソッドを呼び出し、次の `FillByState` ようにパラメーター値を渡し `CustomerTableAdapter.FillByState("WA")` ます。

 TableAdapter のデータテーブルと同じスキーマのデータを返すクエリを追加するだけでなく、スカラー (単一) 値を返すクエリを追加することもできます。 たとえば、 `SELECT Count(*) From Customers` `CustomersTableAdapter,` 返されたデータがテーブルのスキーマに準拠していない場合でも、顧客数 () を返すクエリは、に対して有効です。

## <a name="clearbeforefill-property"></a>ClearBeforeFill プロパティ
 既定では、TableAdapter のデータテーブルにデータを格納するクエリを実行するたびに、既存のデータが消去され、クエリの結果だけがテーブルに読み込まれます。 `ClearBeforeFill` `false` クエリから返されたデータをデータテーブルの既存のデータに追加またはマージする場合は、TableAdapter のプロパティをに設定します。 データをクリアするかどうかにかかわらず、更新プログラムを永続化する場合は、データベースに明示的に送信する必要があります。 そのため、テーブルのデータに対する変更は、テーブルに入力する別のクエリを実行する前に保存してください。 詳細については、「TableAdapter を使用して [データを更新](../data-tools/update-data-by-using-a-tableadapter.md)する」を参照してください。

## <a name="tableadapter-inheritance"></a>TableAdapter の継承
 Tableadapter は、構成されたクラスをカプセル化することによって、標準データアダプターの機能を拡張し <xref:System.Data.Common.DataAdapter> ますか? qualifyHint = False&autoUpgrade = True。 既定では、TableAdapter はクラスから継承され、 <xref:System.ComponentModel.Component> クラスにキャストすることはできません <xref:System.Data.Common.DataAdapter> 。 TableAdapter をクラスにキャストすると、 <xref:System.Data.Common.DataAdapter> <xref:System.InvalidCastException> エラーが発生しますか? QualifyHint = False&AutoUpgrade = True です。 TableAdapter の基底クラスを変更するには、 <xref:System.ComponentModel.Component> **データセットデザイナー**の Tableadapter の**基本クラス**プロパティで、から派生するクラスを入力します。

## <a name="tableadapter-methods-and-properties"></a>TableAdapter のメソッドとプロパティ
 TableAdapter クラスは、の一部ではありません [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 。 つまり、ドキュメントや **オブジェクトブラウザー**では検索できません。 前に説明したウィザードのいずれかを使用すると、デザイン時に作成されます。 作成時に TableAdapter に割り当てられる名前は、使用しているテーブルの名前に基づいています。 たとえば、という名前のデータベース内のテーブルに基づいて TableAdapter を作成する場合、 `Orders` tableadapter にはという名前が付けられ `OrdersTableAdapter` ます。 TableAdapter のクラス名は、**データセット デザイナー**の **Name** プロパティを使用して変更できます。

 Tableadapter の一般的に使用されるメソッドとプロパティを次に示します。

|メンバー|説明|
|------------|-----------------|
|`TableAdapter.Fill`|TableAdapter の関連付けられたデータ テーブルに、TableAdapter の SELECT コマンドの実行結果が格納されます。|
|`TableAdapter.Update`|変更をデータベースに送り返し、更新によって影響を受ける行の数を表す整数を返します。 詳細については、「TableAdapter を使用して [データを更新](../data-tools/update-data-by-using-a-tableadapter.md)する」を参照してください。|
|`TableAdapter.GetData`|<xref:System.Data.DataTable>データを格納する新しいを返します。|
|`TableAdapter.Insert`|データ テーブル内に新しい行を作成します。 詳細については、「 [データベースへの新しいレコードの挿入](../data-tools/insert-new-records-into-a-database.md)」を参照してください。|
|`TableAdapter.ClearBeforeFill`|いずれかの `Fill` メソッドを呼び出す前に、データ テーブルが空になっているかどうかを確認します。|

## <a name="tableadapter-update-method"></a>TableAdapter 更新メソッド
 TableAdapter では、データ コマンドを使用して、データベースからの読み取りと書き込みを実行します。 TableAdapter の最初の `Fill` (メイン) クエリは、関連付けられたデータテーブルのスキーマを作成するための基礎として使用され `InsertCommand` `UpdateCommand` `DeleteCommand` ます。また、メソッドに関連付けられている、、およびの各コマンドも使用され `TableAdapter.Update` ます。 Tableadapter のメソッドを呼び出すと、tableadapter `Update` **クエリの構成ウィザード**を使用して追加された追加のクエリの1つではなく、tableadapter の最初の構成時に作成されたステートメントが実行されます。

 TableAdapter を使用すると、通常実行するコマンド操作を効果的に実行できます。 たとえば、アダプターのメソッドを呼び出すと、 `Fill` アダプターはそのプロパティでデータコマンドを実行 `SelectCommand` し、データリーダー (など) を使用して <xref:System.Data.SqlClient.SqlDataReader> 結果セットをデータテーブルに読み込みます。 同様に、アダプターのメソッドを呼び出すと、 `Update` `UpdateCommand` `InsertCommand` `DeleteCommand` データテーブル内の変更された各レコードについて、適切なコマンド (、、およびの各プロパティ) が実行されます。

> [!NOTE]
> メインのクエリに十分な情報がある場合、TableAdapter の生成時に既定で `InsertCommand`、`UpdateCommand`、および `DeleteCommand` の各コマンドが作成されます。 TableAdapter のメインクエリが1つのテーブルの SELECT ステートメントよりも多い場合は、デザイナーで、、およびを生成できない可能性があり  `InsertCommand` `UpdateCommand` `DeleteCommand` ます。 これらのコマンドが生成されない場合、メソッドの実行時にエラーが発生することがあり `TableAdapter.Update` ます。

## <a name="tableadapter-generatedbdirectmethods"></a>TableAdapter の GenerateDbDirectMethods
 、、およびに加えて、  `InsertCommand` `UpdateCommand` `DeleteCommand` データベースに対して直接実行できるメソッドを使用して tableadapter が作成されます。 これらのメソッド (`TableAdapter.Insert`、`TableAdapter.Update`、および `TableAdapter.Delete`) は、データベース内でデータを直接操作するために呼び出すことができます。 つまり、 `TableAdapter.Update` 関連付けられたデータテーブルに対して保留中の挿入、更新、および削除を処理するのではなく、コードからこれらの個別のメソッドを呼び出すことができます。

 これらのダイレクトメソッドを作成しない場合は、TableAdapter の **Generatedbdirectmethods** プロパティを `false` ([ **プロパティ** ] ウィンドウの) に設定します。 TableAdapter に追加されるその他のクエリはスタンドアロンクエリであり、これらのメソッドは生成されません。

## <a name="tableadapter-support-for-nullable-types"></a>TableAdapter での Null 許容型のサポート
 Tableadapter では、null 許容型とがサポートさ `Nullable(Of T)` `T?` れます。 Visual Basic での null 許容型について詳しくは、「[null 許容値型](https://msdn.microsoft.com/library/9ac3b602-6f96-4e6d-96f7-cd4e81c468a6)」をご覧ください。 C# での null 許容型の詳細については、「 [Null 許容型の使用](https://msdn.microsoft.com/library/0bacbe72-ce15-4b14-83e1-9c14e6380c28)」を参照してください。

## <a name="security"></a>Security
 プロパティがに設定されたデータコマンドを使用する場合は `CommandType` <xref:System.Data.CommandType> 、クライアントから送信された情報をデータベースに渡す前に注意して確認してください。 悪意のあるユーザーが、承認なしでデータベースにアクセスしたり、データベースを破壊したりする目的で、変更した SQL ステートメントや追加の SQL ステートメントの送信 (挿入) を試みる場合があります。 ユーザー入力をデータベースに転送する前に、その情報が有効であることを必ず確認してください。 可能な限り、パラメーター化されたクエリまたはストアドプロシージャを常に使用することをお勧めします。

## <a name="see-also"></a>参照
 [Visual Studio のデータセットツール](../data-tools/dataset-tools-in-visual-studio.md)
