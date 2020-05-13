---
title: TableAdapters を使用してデータセットを入力する
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- datasets [Visual Basic]
- datasets [Visual Basic], loading data
- data retrieval
- retrieving data
- datasets [Visual Basic], filling
- data [Visual Studio], retrieving
- data [Visual Studio], datasets
ms.assetid: 55f3bfbe-db78-4486-add3-c62f49e6b9a0
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: a79f7b781944bb93a60794e748eefb9375723384
ms.sourcegitcommit: 95f26af1da51d4c83ae78adcb7372b32364d8a2b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79301195"
---
# <a name="fill-datasets-by-using-tableadapters"></a>TableAdapters を使用してデータセットを入力する

TableAdapter コンポーネントは、指定した 1 つ以上のクエリまたはストアド プロシージャに基づいて、データベースのデータをデータセットに格納します。 TableAdapter では、データベースに対して追加、更新、および削除を実行して、データセットに加えた変更を保持することもできます。 また、特定のテーブルとは無関係なグローバル コマンドを発行することもできます。

> [!NOTE]
> テーブルアダプターは、Visual Studio デザイナーによって生成されます。 プログラムでデータセットを作成する場合は、.NET クラスである DataAdapter を使用します。

TableAdapter 操作の詳細については、次のトピックのいずれかに直接スキップできます。

|トピック|説明|
|-----------|-----------------|
|[Tableadapter の作成および構成](../data-tools/create-and-configure-tableadapters.md)|デザイナーを使用して TableAdapter を作成および構成する方法|
|[パラメーター付きの TableAdapter クエリを作成する](../data-tools/create-parameterized-tableadapter-queries.md)|ユーザーが TableAdapter プロシージャまたはクエリに引数を指定できるようにする方法|
|[TableAdapter で直接データベースにアクセスする](../data-tools/directly-access-the-database-with-a-tableadapter.md)|テーブルアダプタの Dbdirect メソッドの使用方法|
|[データセットの読み込み中に制約をオフにする](../data-tools/turn-off-constraints-while-filling-a-dataset.md)|データを更新するときに外部キー制約を使用する方法|
|[方法 : TableAdapter の機能を拡張する](../data-tools/fill-datasets-by-using-tableadapters.md)|カスタム コードをテーブルアダプターに追加する方法|
|[XML データのデータセットへの読み込み](../data-tools/read-xml-data-into-a-dataset.md)|XML の操作方法|

<a name="tableadapter-overview"></a>

## <a name="tableadapter-overview"></a>TableAdapter の概要

TableAdapter は、データベースに接続し、クエリまたはストアド プロシージャを実行し、返されたデータを DataTable に格納するデザイナー生成コンポーネントです。 また、更新されたデータをアプリケーションからデータベースに送信します。 TableAdapter が関連付けられているテーブルのスキーマに準拠するデータを返す限り、クエリを TableAdapter で必要な数だけ実行できます。 次の図は、TableAdapter がメモリ内のデータベースやその他のオブジェクトと対話する方法を示しています。

![クライアント アプリケーションのデータ フロー](../data-tools/media/clientdatadiagram.gif)

TableAdapter は**データセット デザイナー**を使用して設計されていますが、 TableAdapter クラスは<xref:System.Data.DataSet>入れ子になったクラスとして生成されません。 これらは、各データセットに固有の個別の名前空間に配置されます。 たとえば、 という`NorthwindDataSet`名前のデータセットがある場合、 の<xref:System.Data.DataTable>`NorthwindDataSet`s に関連付けられている TableAdapter は`NorthwindDataSetTableAdapters`名前空間に含まれます。 プログラムで特定の TableAdapter にアクセスするには、TableAdapter の新しいインスタンスを宣言する必要があります。 次に例を示します。

[!code-csharp[VbRaddataTableAdapters#7](../data-tools/codesnippet/CSharp/fill-datasets-by-using-tableadapters_1.cs)]
[!code-vb[VbRaddataTableAdapters#7](../data-tools/codesnippet/VisualBasic/fill-datasets-by-using-tableadapters_1.vb)]

## <a name="associated-datatable-schema"></a>関連付けられた DataTable スキーマ

TableAdapter を作成するときに、最初のクエリまたはストアド プロシージャを使用して、TableAdapter に関連付けられた<xref:System.Data.DataTable>のスキーマを定義します。 この最初のクエリまたはストアド プロシージャを実行するには、TableAdapter`Fill`のメソッド (TableAdapter の関連付けられた<xref:System.Data.DataTable>を埋めます) を呼び出します。 TableAdapter のメイン クエリに対して行われた変更は、関連付けられたデータ テーブルのスキーマに反映されます。 たとえば、メイン クエリから列を削除すると、関連付けられたデータ テーブルから列も削除されます。 TableAdapter の追加のクエリがメイン クエリにない列を返す SQL ステートメントを使用する場合、デザイナーはメイン クエリと追加クエリの間で列の変更を同期しようとします。

## <a name="tableadapter-update-commands"></a>TableAdapter 更新コマンド

TableAdapter の更新機能は、テーブルアダプター ウィザードのメイン クエリで使用できる情報の量に依存**します**。 たとえば、複数のテーブルから値をフェッチするように構成されている TableAdapter (を`JOIN`使用して) スカラー値、ビュー、または集計関数の結果は、最初は基になるデータベースに更新を送り返す機能を使用して作成されません。 ただし、プロパティ ウィンドウで`INSERT`、 `UPDATE`、`DELETE`および コマンドを**Properties**手動で構成できます。

## <a name="tableadapter-queries"></a>TableAdapter クエリ

![複数のクエリがある TableAdapter](../data-tools/media/tableadapter.gif)

テーブルアダプタには、関連付けられたデータ テーブルを埋めるために複数のクエリを含めることができます。 それぞれのクエリが、関連するデータ テーブルと同じスキーマに従ったデータを返す限り、アプリケーションに必要なクエリをいくつでも TableAdapter に定義できます。 この機能により、TableAdapter は、異なる条件に基づいて異なる結果を読み込むことができます。

たとえば、アプリケーションに顧客名を持つテーブルが含まれている場合、特定の文字で始まるすべての顧客名をテーブルに格納するクエリと、同じ状態にあるすべての顧客をテーブルに入力するクエリを作成できます。 特定の状態`Customers`の顧客をテーブルに入力するには、次のように状態値`FillByState`のパラメーターを受け取るクエリを作成します。 `SELECT * FROM Customers WHERE State = @State` このクエリを実行するには、メソッド`FillByState`を呼び出し、次のようなパラメーター値`CustomerTableAdapter.FillByState("WA")`を渡します。

TableAdapter のデータ テーブルと同じスキーマのデータを返すクエリを追加するだけでなく、スカラー (単一) 値を返すクエリを追加できます。 たとえば、返されたデータがテーブルのスキーマに準拠していない`SELECT Count(*) From Customers``CustomersTableAdapter,`場合でも、顧客数 ( ) を返すクエリは、 に対して有効です。

## <a name="clearbeforefill-property"></a>ClearBeforeFill プロパティ

既定では、TableAdapter のデータ テーブルにデータを入力するクエリを実行するたびに、既存のデータがクリアされ、クエリの結果のみがテーブルに読み込まれます。 クエリから返されるデータを`ClearBeforeFill`データ`false`テーブルの既存のデータに追加またはマージする場合は、TableAdapter のプロパティを設定します。 データをクリアするかどうかに関係なく、更新をデータベースに明示的に送信する必要があります。 そのため、テーブルに入力する別のクエリを実行する前に、テーブル内のデータに対する変更を保存してください。 詳細については、「 [TableAdapter を使用してデータを更新する」を参照してください。](../data-tools/update-data-by-using-a-tableadapter.md)

## <a name="tableadapter-inheritance"></a>TableAdapter の継承

TableAdapter は、構成<xref:System.Data.Common.DataAdapter>されたクラスをカプセル化することによって、標準データ アダプターの機能を拡張します。 既定では、TableAdapter は<xref:System.ComponentModel.Component>クラスから継承し、<xref:System.Data.Common.DataAdapter>クラスにキャストすることはできません。 クラスにテーブルアダプターをキャスト<xref:System.Data.Common.DataAdapter>すると、エラーが<xref:System.InvalidCastException>発生します。 TableAdapter の基本クラスを変更するには、データセット<xref:System.ComponentModel.Component>**デザイナー**の TableAdapter の**基本クラス**プロパティで派生元のクラスを指定できます。

## <a name="tableadapter-methods-and-properties"></a>TableAdapter のメソッドとプロパティ

クラスは .NET 型ではありません。 つまり、ドキュメントや**オブジェクト ブラウザ**で検索することはできません。 このウィザードは、前述のウィザードのいずれかを使用するときに、デザイン時に作成されます。 作成するときに TableAdapter に割り当てられる名前は、作業中のテーブルの名前に基づいています。 たとえば、 という名前`Orders`のデータベース内のテーブルに基づいて TableAdapter を作成すると、その名前`OrdersTableAdapter`が付けられます。 TableAdapter のクラス名は、**データセット デザイナー**の **Name** プロパティを使用して変更できます。

TableAdapter の一般的なメソッドとプロパティを次に示します。

|メンバー|説明|
|------------|-----------------|
|`TableAdapter.Fill`|テーブルアダプタの`SELECT`関連付けられたデータ テーブルに、TableAdapter のコマンドの結果を設定します。|
|`TableAdapter.Update`|変更をデータベースに返し、更新の影響を受ける行数を表す整数を返します。 詳細については、「 [TableAdapter を使用してデータを更新する」を参照してください。](../data-tools/update-data-by-using-a-tableadapter.md)|
|`TableAdapter.GetData`|データが格納<xref:System.Data.DataTable>された新しい値を返します。|
|`TableAdapter.Insert`|データ テーブル内に新しい行を作成します。 詳細については、「[データベースに新しいレコードを挿入する](../data-tools/insert-new-records-into-a-database.md)」を参照してください。|
|`TableAdapter.ClearBeforeFill`|いずれかの `Fill` メソッドを呼び出す前に、データ テーブルが空になっているかどうかを確認します。|

## <a name="tableadapter-update-method"></a>TableAdapter 更新メソッド

TableAdapter では、データ コマンドを使用して、データベースからの読み取りと書き込みを実行します。 TableAdapter の`Fill`初期 (メイン) クエリは、`InsertCommand``UpdateCommand``DeleteCommand``TableAdapter.Update`関連付けられたデータ テーブルのスキーマを作成する際の基礎として使用します。 TableAdapter の`Update`メソッドを呼び出すと、TableAdapter クエリ**構成ウィザード**で追加した追加のクエリの 1 つではなく、TableAdapter が最初に構成されたときに作成されたステートメントが実行されます。

TableAdapter を使用すると、通常実行するコマンドと同じ操作が効果的に実行されます。 たとえば、アダプターの`Fill`メソッドを呼び出すと、アダプターは、そのプロパティでデータ コマンド`SelectCommand`を実行し、データ リーダー (たとえば<xref:System.Data.SqlClient.SqlDataReader>、 ) を使用して結果セットをデータ テーブルに読み込みます。 同様に、アダプターのメソッドを呼び`Update`出すと、データ テーブル内の変更された`UpdateCommand`各`InsertCommand`レコードに`DeleteCommand`対して適切なコマンド (、、、およびプロパティ) が実行されます。

> [!NOTE]
> メインのクエリに十分な情報がある場合、TableAdapter の生成時に既定で `InsertCommand`、`UpdateCommand`、および `DeleteCommand` の各コマンドが作成されます。 TableAdapter`SELECT`のメイン クエリが複数のテーブル ステートメントである場合、デザイナーが 、 、`InsertCommand``UpdateCommand`および`DeleteCommand`を生成できない可能性があります。 これらのコマンドが生成されない場合は、メソッドの実行時にエラーが表示されることがあります`TableAdapter.Update`。

## <a name="tableadapter-generatedbdirectmethods"></a>TableAdapter の GenerateDbDirectMethods

に加えて`InsertCommand``UpdateCommand`、 、`DeleteCommand`および TableAdapter は、データベースに対して直接実行できるメソッドを使用して作成されます。 これらのメソッド (`TableAdapter.Insert`、 `TableAdapter.Update`、および`TableAdapter.Delete`) を直接呼び出して、データベース内のデータを操作できます。 つまり、関連付けられたデータ テーブルに対して保留中の挿入`TableAdapter.Update`、更新、および削除を処理する代わりに、コードからこれらの個々のメソッドを呼び出すことができます。

これらのダイレクト メソッドを作成しない場合は、([**プロパティ]** ウィンドウで) にテーブルアダプターの`false`**GenerateDbDirectMethods**プロパティを設定します。 TableAdapter に追加される追加のクエリはスタンドアロン クエリであり、これらのメソッドは生成しません。

## <a name="tableadapter-support-for-nullable-types"></a>TableAdapter での Null 許容型のサポート

テーブルアダプタは、null 許容`Nullable(Of T)`型`T?`と . Visual Basic での null 許容型について詳しくは、「[null 許容値型](/dotnet/visual-basic/programming-guide/language-features/data-types/nullable-value-types)」をご覧ください。 C# での null 許容型の詳細については、「null[許容型を使用](/dotnet/csharp/programming-guide/nullable-types/using-nullable-types)する」を参照してください。

<a name="tableadaptermanager-reference"></a>

## <a name="tableadaptermanager-reference"></a>リファレンス

既定では、クラスは、関連するテーブルを含むデータセットを作成するときに生成されます。 クラスが生成されないようにするには、データセットの`Hierarchical Update`プロパティの値を false に変更します。 Windows フォームまたは WPF ページのデザインサーフェイスにリレーションシップを持つテーブルをドラッグすると、Visual Studio はクラスのメンバー変数を宣言します。 データバインディングを使用しない場合は、変数を手動で宣言する必要があります。

クラスは .NET 型ではありません。 したがって、ドキュメントで調けることはできません。 これは、データセットの作成プロセスの一環として、デザイン時に作成されます。

クラスの頻繁に使用されるメソッドとプロパティを`TableAdapterManager`次に示します。

|メンバー|説明|
|------------|-----------------|
|`UpdateAll` メソッド|すべてのデータ テーブルのすべてのデータを保存します。|
|`BackUpDataSetBeforeUpdate` プロパティ|メソッドを実行する前にデータセットのバックアップ コピーを作成するかどうかを`TableAdapterManager.UpdateAll`決定します。ブール。|
|*テーブル名*`TableAdapter`プロパティ|TableAdapter を表します。 生成されたテーブルアダプター マネージャーには、管理する`TableAdapter`各プロパティが含まれています。 たとえば、"得意先" テーブルと "受注" テーブルを持つデータセットは`CustomersTableAdapter`、`OrdersTableAdapter`プロパティを含む TableAdapterManager を使用して生成します。|
|`UpdateOrder` プロパティ|個々の挿入、更新、および削除コマンドの順序を制御します。 `TableAdapterManager.UpdateOrderOption`これを列挙体の値のいずれかに設定します。<br /><br /> 既定では、`UpdateOrder`は **[更新の削除の挿入]** に設定されています。 つまり、挿入、更新、および削除は、データセット内のすべてのテーブルに対して実行されます。|

## <a name="security"></a>Security

CommandType プロパティをに設定したデータ コマンドを<xref:System.Data.CommandType.Text>使用する場合は、クライアントから送信される情報をデータベースに渡す前に、慎重に確認します。 悪意のあるユーザーが、承認なしでデータベースにアクセスしたり、データベースを破壊したりする目的で、変更した SQL ステートメントや追加の SQL ステートメントの送信 (挿入) を試みる場合があります。 ユーザー入力をデータベースに転送する前に、必ず情報が有効であることを確認してください。 可能な場合は、常にパラメータ化されたクエリまたはストアド プロシージャを使用することをお勧めします。

## <a name="see-also"></a>関連項目

- [データセット ツール](../data-tools/dataset-tools-in-visual-studio.md)
