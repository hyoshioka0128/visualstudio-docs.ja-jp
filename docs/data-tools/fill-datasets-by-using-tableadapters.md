---
title: TableAdapters を使用してデータセットを入力する
ms.date: 11/04/2016
ms.topic: how-to
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
ms.openlocfilehash: 888e2ac47348d7e61d115f51e3ea52d15ea9f447
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85282437"
---
# <a name="fill-datasets-by-using-tableadapters"></a>TableAdapters を使用してデータセットを入力する

TableAdapter コンポーネントは、指定された1つ以上のクエリまたはストアドプロシージャに基づいて、データベースのデータをデータセットに格納します。 Tableadapter では、データベースの追加、更新、および削除を実行して、データセットに加えた変更を保持することもできます。 また、特定のテーブルに関連付けられていないグローバルコマンドを発行することもできます。

> [!NOTE]
> Tableadapter は、Visual Studio デザイナーによって生成されます。 プログラムによってデータセットを作成する場合は、.NET クラスである DataAdapter を使用します。

TableAdapter 操作の詳細については、次のトピックのいずれかに直接進むことができます。

|トピック|説明|
|-----------|-----------------|
|[Tableadapter の作成および構成](../data-tools/create-and-configure-tableadapters.md)|デザイナーを使用して Tableadapter を作成および構成する方法|
|[パラメーター付きの TableAdapter クエリを作成する](../data-tools/create-parameterized-tableadapter-queries.md)|ユーザーが TableAdapter プロシージャまたはクエリに引数を指定できるようにする方法|
|[TableAdapter で直接データベースにアクセスする](../data-tools/directly-access-the-database-with-a-tableadapter.md)|Tableadapter の Dbdirect メソッドを使用する方法|
|[データセットの読み込み中に制約をオフにする](../data-tools/turn-off-constraints-while-filling-a-dataset.md)|データの更新時に外部キー制約を使用する方法|
|[方法 : TableAdapter の機能を拡張する](../data-tools/fill-datasets-by-using-tableadapters.md)|Tableadapter にカスタムコードを追加する方法|
|[XML データのデータセットへの読み込み](../data-tools/read-xml-data-into-a-dataset.md)|XML を操作する方法|

<a name="tableadapter-overview"></a>

## <a name="tableadapter-overview"></a>TableAdapter の概要

Tableadapter は、データベースに接続し、クエリまたはストアドプロシージャを実行し、返されたデータを DataTable に格納するデザイナーで生成されたコンポーネントです。 また、Tableadapter は、更新されたデータをアプリケーションからデータベースに送り返します。 Tableadapter が関連付けられているテーブルのスキーマに準拠するデータが返される限り、TableAdapter に対して必要な数のクエリを実行できます。 次の図は、Tableadapter がメモリ内のデータベースやその他のオブジェクトとどのように対話するかを示しています。

![クライアント アプリケーションのデータ フロー](../data-tools/media/clientdatadiagram.gif)

Tableadapter は**データセットデザイナー**で設計されていますが、tableadapter クラスはの入れ子になったクラスとして生成されません <xref:System.Data.DataSet> 。 各データセットに固有の個別の名前空間に配置されます。 たとえば、という名前のデータセットがある場合、 `NorthwindDataSet` のに関連付けられている tableadapter は、 <xref:System.Data.DataTable> `NorthwindDataSet` `NorthwindDataSetTableAdapters` 名前空間にあります。 プログラムで特定の TableAdapter にアクセスするには、TableAdapter の新しいインスタンスを宣言する必要があります。 次に例を示します。

[!code-csharp[VbRaddataTableAdapters#7](../data-tools/codesnippet/CSharp/fill-datasets-by-using-tableadapters_1.cs)]
[!code-vb[VbRaddataTableAdapters#7](../data-tools/codesnippet/VisualBasic/fill-datasets-by-using-tableadapters_1.vb)]

## <a name="associated-datatable-schema"></a>関連付けられた DataTable スキーマ

TableAdapter を作成する場合は、最初のクエリまたはストアドプロシージャを使用して、関連付けられている TableAdapter のスキーマを定義し <xref:System.Data.DataTable> ます。 この最初のクエリまたはストアドプロシージャを実行するには、TableAdapter の `Fill` メソッド (tableadapter に関連付けられている) を呼び出し <xref:System.Data.DataTable> ます。 TableAdapter のメインクエリに対して行われたすべての変更は、関連付けられたデータテーブルのスキーマに反映されます。 たとえば、メインクエリから列を削除すると、関連付けられているデータテーブルからも列が削除されます。 TableAdapter に対する追加のクエリで、メインクエリに含まれていない列を返す SQL ステートメントが使用されている場合、デザイナーはメインクエリと追加のクエリとの間で列の変更を同期しようとします。

## <a name="tableadapter-update-commands"></a>TableAdapter 更新コマンド

TableAdapter の更新機能は、 **Tableadapter ウィザード**のメインクエリで使用できる情報の量に依存します。 たとえば、(を使用して) 複数のテーブルから値をフェッチするように構成されている Tableadapter、 `JOIN` スカラー値、ビュー、または集計関数の結果は、基になるデータベースに更新を戻す機能を使用して最初に作成されるわけではありません。 ただし、、、およびの各コマンドは、[ `INSERT` `UPDATE` `DELETE` **プロパティ**] ウィンドウで手動で構成できます。

## <a name="tableadapter-queries"></a>TableAdapter クエリ

![複数のクエリがある TableAdapter](../data-tools/media/tableadapter.gif)

Tableadapter には、関連付けられたデータテーブルを埋めるために複数のクエリを含めることができます。 それぞれのクエリが、関連するデータ テーブルと同じスキーマに従ったデータを返す限り、アプリケーションに必要なクエリをいくつでも TableAdapter に定義できます。 この機能により、TableAdapter は異なる条件に基づいて異なる結果を読み込むことができます。

たとえば、顧客名を含むテーブルがアプリケーションに含まれている場合、特定の文字で始まるすべての顧客名をテーブルに入力するクエリと、同じ州にあるすべての顧客をテーブルに格納するクエリを作成できます。 特定の状態の顧客を含むテーブルにデータを格納するには `Customers` 、 `FillByState` 状態の値のパラメーターを受け取るクエリを次のように作成します `SELECT * FROM Customers WHERE State = @State` 。 このクエリを実行するには、メソッドを呼び出し、次の `FillByState` ようにパラメーター値を渡し `CustomerTableAdapter.FillByState("WA")` ます。

TableAdapter のデータテーブルと同じスキーマのデータを返すクエリを追加するだけでなく、スカラー (単一) 値を返すクエリを追加することもできます。 たとえば、 `SELECT Count(*) From Customers` `CustomersTableAdapter,` 返されたデータがテーブルのスキーマに準拠していない場合でも、顧客数 () を返すクエリは、に対して有効です。

## <a name="clearbeforefill-property"></a>ClearBeforeFill プロパティ

既定では、TableAdapter のデータテーブルにデータを格納するクエリを実行するたびに、既存のデータが消去され、クエリの結果だけがテーブルに読み込まれます。 `ClearBeforeFill` `false` クエリから返されたデータをデータテーブルの既存のデータに追加またはマージする場合は、TableAdapter のプロパティをに設定します。 データをクリアするかどうかにかかわらず、更新プログラムを永続化する場合は、データベースに明示的に送信する必要があります。 そのため、テーブルのデータに対する変更は、テーブルに入力する別のクエリを実行する前に保存してください。 詳細については、「TableAdapter を使用して[データを更新](../data-tools/update-data-by-using-a-tableadapter.md)する」を参照してください。

## <a name="tableadapter-inheritance"></a>TableAdapter の継承

Tableadapter は、構成されたクラスをカプセル化することによって、標準データアダプターの機能を拡張し <xref:System.Data.Common.DataAdapter> ます。 既定では、TableAdapter はクラスから継承され、 <xref:System.ComponentModel.Component> クラスにキャストすることはできません <xref:System.Data.Common.DataAdapter> 。 TableAdapter をクラスにキャストすると、 <xref:System.Data.Common.DataAdapter> <xref:System.InvalidCastException> エラーが発生します。 TableAdapter の基底クラスを変更するには、 <xref:System.ComponentModel.Component> **データセットデザイナー**の Tableadapter の**基本クラス**プロパティで、から派生するクラスを指定します。

## <a name="tableadapter-methods-and-properties"></a>TableAdapter のメソッドとプロパティ

TableAdapter クラスは .NET 型ではありません。 つまり、ドキュメントや**オブジェクトブラウザー**では検索できません。 前に説明したウィザードのいずれかを使用すると、デザイン時に作成されます。 作成時に TableAdapter に割り当てられる名前は、使用しているテーブルの名前に基づいています。 たとえば、という名前のデータベース内のテーブルに基づいて TableAdapter を作成する場合、 `Orders` tableadapter にはという名前が付けられ `OrdersTableAdapter` ます。 TableAdapter のクラス名は、**データセット デザイナー**の **Name** プロパティを使用して変更できます。

Tableadapter の一般的に使用されるメソッドとプロパティを次に示します。

|メンバー|説明|
|------------|-----------------|
|`TableAdapter.Fill`|Tableadapter の関連するデータテーブルに TableAdapter のコマンドの結果を設定し `SELECT` ます。|
|`TableAdapter.Update`|変更をデータベースに送り返し、更新によって影響を受ける行の数を表す整数を返します。 詳細については、「TableAdapter を使用して[データを更新](../data-tools/update-data-by-using-a-tableadapter.md)する」を参照してください。|
|`TableAdapter.GetData`|<xref:System.Data.DataTable>データを格納する新しいを返します。|
|`TableAdapter.Insert`|データ テーブル内に新しい行を作成します。 詳細については、「[データベースへの新しいレコードの挿入](../data-tools/insert-new-records-into-a-database.md)」を参照してください。|
|`TableAdapter.ClearBeforeFill`|いずれかの `Fill` メソッドを呼び出す前に、データ テーブルが空になっているかどうかを確認します。|

## <a name="tableadapter-update-method"></a>TableAdapter 更新メソッド

TableAdapter では、データ コマンドを使用して、データベースからの読み取りと書き込みを実行します。 TableAdapter の最初の (メイン) クエリを基にして、関連付けられた `Fill` データテーブルのスキーマと、 `InsertCommand` `UpdateCommand` `DeleteCommand` メソッドに関連付けられている、、およびの各コマンドを作成し `TableAdapter.Update` ます。 Tableadapter のメソッドを呼び出すと、tableadapter `Update` **クエリの構成ウィザード**で追加した追加のクエリの1つではなく、tableadapter の最初の構成時に作成されたステートメントが実行されます。

TableAdapter を使用すると、通常実行するコマンドと同じ操作が効率的に実行されます。 たとえば、アダプターのメソッドを呼び出すと、 `Fill` アダプターはそのプロパティでデータコマンドを実行 `SelectCommand` し、データリーダー (など) を使用して <xref:System.Data.SqlClient.SqlDataReader> 結果セットをデータテーブルに読み込みます。 同様に、アダプターのメソッドを呼び出すと、 `Update` `UpdateCommand` `InsertCommand` `DeleteCommand` データテーブル内の変更された各レコードについて、適切なコマンド (、、およびの各プロパティ) が実行されます。

> [!NOTE]
> メインのクエリに十分な情報がある場合、TableAdapter の生成時に既定で `InsertCommand`、`UpdateCommand`、および `DeleteCommand` の各コマンドが作成されます。 TableAdapter のメインクエリが1つのテーブルステートメントよりも多い場合は、デザイナーで、、およびを生成できない可能性があり `SELECT` `InsertCommand` `UpdateCommand` `DeleteCommand` ます。 これらのコマンドが生成されない場合は、メソッドの実行時にエラーが発生することがあり `TableAdapter.Update` ます。

## <a name="tableadapter-generatedbdirectmethods"></a>TableAdapter の GenerateDbDirectMethods

、、およびに加えて、 `InsertCommand` `UpdateCommand` データベースに `DeleteCommand` 対して直接実行できるメソッドを使用して tableadapter が作成されます。 これらのメソッド ( `TableAdapter.Insert` 、 `TableAdapter.Update` 、および) を直接呼び出して、 `TableAdapter.Delete` データベース内のデータを操作できます。 つまり、 `TableAdapter.Update` 関連付けられたデータテーブルに対して保留中の挿入、更新、および削除を処理するのではなく、コードからこれらの個別のメソッドを呼び出すことができます。

これらのダイレクトメソッドを作成しない場合は、TableAdapter の**Generatedbdirectmethods**プロパティを `false` ([**プロパティ**] ウィンドウの) に設定します。 TableAdapter に追加されるその他のクエリはスタンドアロンクエリであり、これらのメソッドは生成されません。

## <a name="tableadapter-support-for-nullable-types"></a>TableAdapter での Null 許容型のサポート

Tableadapter では、null 許容型とがサポートさ `Nullable(Of T)` `T?` れます。 Visual Basic での null 許容型について詳しくは、「[null 許容値型](/dotnet/visual-basic/programming-guide/language-features/data-types/nullable-value-types)」をご覧ください。 C# での null 許容型の詳細については、「 [null 許容型の使用](/dotnet/csharp/programming-guide/nullable-types/using-nullable-types)」を参照してください。

<a name="tableadaptermanager-reference"></a>

## <a name="tableadaptermanager-reference"></a>TableAdapterManager リファレンス

既定では、関連テーブルを含むデータセットを作成すると、TableAdapterManager クラスが生成されます。 クラスが生成されないようにするには、 `Hierarchical Update` データセットのプロパティの値を false に変更します。 Windows フォームまたは WPF ページのデザインサーフェイスにリレーションシップを持つテーブルをドラッグすると、Visual Studio はクラスのメンバー変数を宣言します。 データバインドを使用しない場合は、手動で変数を宣言する必要があります。

TableAdapterManager クラスは .NET 型ではありません。 このため、ドキュメントでは確認できません。 これは、デザイン時にデータセット作成プロセスの一部として作成されます。

クラスのよく使用されるメソッドとプロパティを次に示し `TableAdapterManager` ます。

|メンバー|説明|
|------------|-----------------|
|`UpdateAll` メソッド|すべてのデータテーブルのすべてのデータを保存します。|
|`BackUpDataSetBeforeUpdate` プロパティ|メソッドを実行する前に、データセットのバックアップコピーを作成するかどうかを決定し `TableAdapterManager.UpdateAll` ます。演算.|
|*tableName* `TableAdapter`"|TableAdapter を表します。 生成された TableAdapterManager には、it が管理するそれぞれのプロパティが含まれてい `TableAdapter` ます。 たとえば、Customers テーブルと Orders テーブルを含むデータセットでは、プロパティとプロパティを含む TableAdapterManager が生成され `CustomersTableAdapter` `OrdersTableAdapter` ます。|
|`UpdateOrder` プロパティ|個々の insert、update、および delete コマンドの順序を制御します。 列挙体のいずれかの値に設定 `TableAdapterManager.UpdateOrderOption` します。<br /><br /> 既定では、 `UpdateOrder` は**Insertupdatedelete**に設定されています。 これは、データセット内のすべてのテーブルに対して、挿入、更新、および削除が実行されることを意味します。|

## <a name="security"></a>Security

CommandType プロパティがに設定されたデータコマンドを使用する場合は <xref:System.Data.CommandType.Text> 、クライアントから送信された情報をデータベースに渡す前に慎重に確認してください。 悪意のあるユーザーが、承認なしでデータベースにアクセスしたり、データベースを破壊したりする目的で、変更した SQL ステートメントや追加の SQL ステートメントの送信 (挿入) を試みる場合があります。 ユーザー入力をデータベースに転送する前に、その情報が有効であることを必ず確認してください。 可能な限り、パラメーター化されたクエリまたはストアドプロシージャを常に使用することをお勧めします。

## <a name="see-also"></a>関連項目

- [データセットツール](../data-tools/dataset-tools-in-visual-studio.md)
