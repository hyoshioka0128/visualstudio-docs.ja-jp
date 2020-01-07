---
title: データセットのデータの検証
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- DataTable.ColumnChanging
- System.Data.DataTable.ColumnChanging
- System.Data.DataTable.RowChanging
- DataTable.RowChanging
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data validation, datasets
- data validation
- validating data, datasets
- updating datasets, validating data
ms.assetid: 79500596-1e4d-478e-a991-a636fd73a622
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: ed115e851e9c2291dfc9d00f4bb36f670a7f3e00
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75586069"
---
# <a name="validate-data-in-datasets"></a>データセットのデータの検証
データの検証は、データオブジェクトに入力される値がデータセットのスキーマ内の制約に準拠していることを確認するプロセスです。 また、検証プロセスでは、これらの値が、アプリケーションに対して設定されている規則に従っていることも確認します。 基になるデータベースに更新を送信する前に、データを検証することをお勧めします。 これにより、エラーが減少し、アプリケーションとデータベース間で発生する可能性のあるラウンドトリップの回数も減ります。

データセットに書き込まれるデータが、データセット自体に検証チェックを組み込むことによって有効であることを確認できます。 データセットは、フォーム内のコントロール、コンポーネント内、またはその他の方法で、更新の実行方法に関係なくデータを確認できます。 データセットはアプリケーションの一部であるため (データベースバックエンドとは異なります)、アプリケーション固有の検証を構築するための論理的な場所です。

アプリケーションに検証を追加する最適な場所は、データセットの部分クラスファイルです。 [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] または [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)]で、**データセットデザイナー**を開き、検証を作成する列またはテーブルをダブルクリックします。 この操作により、<xref:System.Data.DataTable.ColumnChanging> または <xref:System.Data.DataTable.RowChanging> イベントハンドラーが自動的に作成されます。

## <a name="validate-data"></a>データの検証
データセット内の検証は、次の方法で実現されます。

- 変更時に個々のデータ列の値を確認できる、独自のアプリケーション固有の検証を作成する。 詳細については、「[方法: 列の変更時にデータを検証する](validate-data-in-datasets.md)」を参照してください。

- データ行全体が変更されている間にデータを値にチェックできる独自のアプリケーション固有の検証を作成する。 詳細については、「[方法: 行の変更時にデータを検証する](validate-data-in-datasets.md)」を参照してください。

- データセットの実際のスキーマ定義の一部として、キー、一意の制約などを作成する。

- <xref:System.Data.DataColumn.MaxLength%2A>、<xref:System.Data.DataColumn.AllowDBNull%2A>、<xref:System.Data.DataColumn.Unique%2A>などの <xref:System.Data.DataColumn> オブジェクトのプロパティを設定する。

レコードで変更が発生すると、<xref:System.Data.DataTable> オブジェクトによっていくつかのイベントが発生します。

- <xref:System.Data.DataTable.ColumnChanging> イベントと <xref:System.Data.DataTable.ColumnChanged> イベントは、個々の列を変更するたびおよび後に発生します。 <xref:System.Data.DataTable.ColumnChanging> イベントは、特定の列の変更を検証する場合に便利です。 提案された変更に関する情報は、イベントの引数として渡されます。
- <xref:System.Data.DataTable.RowChanging> イベントと <xref:System.Data.DataTable.RowChanged> イベントは、行の変更中および変更後に発生します。 <xref:System.Data.DataTable.RowChanging> イベントの方が一般的です。 行のどこかで変更が行われていることを示していますが、変更された列はわかりません。

既定では、列を変更するたびに4つのイベントが発生します。 1つ目は、変更されている特定の列の <xref:System.Data.DataTable.ColumnChanging> イベントと <xref:System.Data.DataTable.ColumnChanged> イベントです。 次に、<xref:System.Data.DataTable.RowChanging> イベントと <xref:System.Data.DataTable.RowChanged> イベントを示します。 行に対して複数の変更が行われている場合、各変更に対してイベントが発生します。

> [!NOTE]
> データ行の <xref:System.Data.DataRow.BeginEdit%2A> メソッドは、個々の列が変更された後に、<xref:System.Data.DataTable.RowChanging> と <xref:System.Data.DataTable.RowChanged> イベントをオフにします。 その場合、イベントは、<xref:System.Data.DataRow.EndEdit%2A> メソッドが呼び出されるまで発生しません。これは、<xref:System.Data.DataTable.RowChanging> イベントと <xref:System.Data.DataTable.RowChanged> イベントが1回だけ発生する場合です。 詳細については、「[データセットの読み込み中に制約をオフにする](../data-tools/turn-off-constraints-while-filling-a-dataset.md)」を参照してください。

選択するイベントは、検証に必要な粒度によって異なります。 列が変更されたときにエラーをすぐにキャッチすることが重要な場合は、<xref:System.Data.DataTable.ColumnChanging> イベントを使用して検証をビルドします。 それ以外の場合は、<xref:System.Data.DataTable.RowChanging> イベントを使用します。これにより、一度に複数のエラーがキャッチされる可能性があります。 また、ある列の値が別の列の内容に基づいて検証されるようにデータが構造化されている場合は、<xref:System.Data.DataTable.RowChanging> イベント中に検証を実行します。

レコードが更新されると、<xref:System.Data.DataTable> オブジェクトによって、変更が発生した後、変更が行われた後に応答できるイベントが発生します。

アプリケーションで型指定されたデータセットを使用する場合は、厳密に型指定されたイベントハンドラーを作成できます。 これにより、`dataTableNameRowChanging`、`dataTableNameRowChanged`、`dataTableNameRowDeleting`、および `dataTableNameRowDeleted`のハンドラーを作成するための、追加で型指定された4つのイベントが追加されます。 これらの型指定されたイベントハンドラーは、コードの記述と読み取りが簡単になるように、テーブルの列名を含む引数を渡します。

## <a name="data-update-events"></a>データ更新イベント

|Event|説明|
|-----------|-----------------|
|<xref:System.Data.DataTable.ColumnChanging>|列の値が変更されています。 イベントは、提案された新しい値と共に行と列を渡します。|
|<xref:System.Data.DataTable.ColumnChanged>|列の値が変更されました。 イベントは、提案された値と共に行と列を渡します。|
|<xref:System.Data.DataTable.RowChanging>|<xref:System.Data.DataRow> オブジェクトに対して行われた変更は、データセットに再度コミットされます。 <xref:System.Data.DataRow.BeginEdit%2A> メソッドを呼び出していない場合は、<xref:System.Data.DataTable.ColumnChanging> イベントが発生した直後に列が変更されるたびに、<xref:System.Data.DataTable.RowChanging> イベントが発生します。 変更を行う前に <xref:System.Data.DataRow.BeginEdit%2A> を呼び出した場合、<xref:System.Data.DataTable.RowChanging> イベントは <xref:System.Data.DataRow.EndEdit%2A> メソッドを呼び出したときにのみ発生します。<br /><br /> イベントは、行と、実行されているアクションの種類 (変更、挿入など) を示す値を渡します。|
|<xref:System.Data.DataTable.RowChanged>|行が変更されました。 イベントは、行と、実行されているアクションの種類 (変更、挿入など) を示す値を渡します。|
|<xref:System.Data.DataTable.RowDeleting>|行が削除されています。 イベントは、実行されているアクションの種類 (削除) を示す値と共に、行をユーザーに渡します。|
|<xref:System.Data.DataTable.RowDeleted>|行が削除されました。 イベントは、実行されているアクションの種類 (削除) を示す値と共に、行をユーザーに渡します。|

<xref:System.Data.DataTable.ColumnChanging>、<xref:System.Data.DataTable.RowChanging>、および <xref:System.Data.DataTable.RowDeleting> イベントは、更新プロセス中に発生します。 これらのイベントを使用して、データを検証したり、他の種類の処理を実行したりすることができます。 更新はこれらのイベント中に処理中であるため、例外をスローすることで取り消すことができます。これにより、更新が終了するのを防ぐことができます。

<xref:System.Data.DataTable.ColumnChanged>、<xref:System.Data.DataTable.RowChanged>、および <xref:System.Data.DataTable.RowDeleted> イベントは、更新が正常に完了したときに発生する通知イベントです。 これらのイベントは、更新が正常に行われたことに基づいてさらにアクションを実行する場合に便利です。

## <a name="validate-data-during-column-changes"></a>列の変更時にデータを検証する

> [!NOTE]
> **データセットデザイナー**は、検証ロジックをデータセットに追加できる部分クラスを作成します。 デザイナーで生成されたデータセットでは、部分クラスのコードは削除または変更されません。

データ列の値が <xref:System.Data.DataTable.ColumnChanging> イベントに応答して変更されたときにデータを検証できます。 このイベントが発生すると、現在の列に対して提示されている値を含むイベント引数 (<xref:System.Data.DataColumnChangeEventArgs.ProposedValue%2A>) が渡されます。 `e.ProposedValue`の内容に基づいて、次のことができます。

- 何もせずに、指示された値を受け入れます。

- 列変更イベントハンドラー内から列エラー (<xref:System.Data.DataRow.SetColumnError%2A>) を設定して、提示された値を拒否します。

- オプションで <xref:System.Windows.Forms.ErrorProvider> コントロールを使用して、ユーザーにエラー メッセージを表示します。 詳細については、「[ErrorProvider コンポーネント](/dotnet/framework/winforms/controls/errorprovider-component-windows-forms)」を参照してください。

<xref:System.Data.DataTable.RowChanging> イベント中に検証を実行することもできます。

## <a name="validate-data-during-row-changes"></a>行の変更中にデータを検証する
検証する各列にアプリケーションの要件を満たすデータが格納されていることを検証するコードを記述できます。 これを行うには、提案された値が許容できない場合にエラーが含まれていることを示すように列を設定します。 `Quantity` 列が 0 以下の場合に列エラーを設定する例を次に示します。 行変更イベント ハンドラーは、次のように記述します。

### <a name="to-validate-data-when-a-row-changes-visual-basic"></a>行の変更時にデータを検証するには (Visual Basic)

1. **データセット デザイナー**でご自分のデータセットを開きます。 詳細については、「[チュートリアル: データセットデザイナーでのデータセットの作成](walkthrough-creating-a-dataset-with-the-dataset-designer.md)」を参照してください。

2. 検証するテーブルのタイトル バーをダブルクリックします。 この操作により、データセットの部分クラス ファイルに <xref:System.Data.DataTable.RowChanging> の <xref:System.Data.DataTable> イベント ハンドラーが自動的に作成されます。

    > [!TIP]
    > テーブル名の左側をダブルクリックして、行変更イベント ハンドラーを作成します。 テーブル名をダブルクリックすると、そのテーブルを編集できます。

     [!code-vb[VbRaddataValidating#3](../data-tools/codesnippet/VisualBasic/validate-data-in-datasets_1.vb)]

### <a name="to-validate-data-when-a-row-changes-c"></a>行の変更時にデータ検証するには (C#)

1. **データセット デザイナー**でご自分のデータセットを開きます。 詳細については、「[チュートリアル: データセットデザイナーでのデータセットの作成](walkthrough-creating-a-dataset-with-the-dataset-designer.md)」を参照してください。

2. 検証するテーブルのタイトル バーをダブルクリックします。 この操作により、<xref:System.Data.DataTable> の部分クラス ファイルが作成されます。

    > [!NOTE]
    > **データセット デザイナー**では、<xref:System.Data.DataTable.RowChanging> イベントのイベント ハンドラーが自動作成されません。 <xref:System.Data.DataTable.RowChanging> イベントを処理するメソッドを作成し、コードを実行して、テーブルの初期化メソッドでイベントをフックする必要があります。

3. 部分クラスに次のコードをコピーします。

    ```csharp
    public override void EndInit()
    {
        base.EndInit();
        Order_DetailsRowChanging += TestRowChangeEvent;
    }

    public void TestRowChangeEvent(object sender, Order_DetailsRowChangeEvent e)
    {
        if ((short)e.Row.Quantity <= 0)
        {
            e.Row.SetColumnError("Quantity", "Quantity must be greater than 0");
        }
        else
        {
            e.Row.SetColumnError("Quantity", "");
        }
    }
    ```

## <a name="to-retrieve-changed-rows"></a>変更された行を取得するには
データテーブルの各行には、<xref:System.Data.DataRowState> 列挙体の値を使用してその行の現在の状態を追跡する <xref:System.Data.DataRow.RowState%2A> プロパティがあります。 <xref:System.Data.DataSet> または <xref:System.Data.DataTable>の `GetChanges` メソッドを呼び出すことによって、データセットまたはデータテーブルから変更された行を返すことができます。 データセットの <xref:System.Data.DataSet.HasChanges%2A> メソッドを呼び出すことによって、`GetChanges` を呼び出す前に変更が存在することを確認できます。

> [!NOTE]
> (<xref:System.Data.DataSet.AcceptChanges%2A> メソッドを呼び出すことによって) データセットまたはデータテーブルに対する変更をコミットした後、`GetChanges` メソッドはデータを返しません。 アプリケーションで変更された行を処理する必要がある場合は、`AcceptChanges` メソッドを呼び出す前に、変更を処理する必要があります。

データセットまたはデータテーブルの <xref:System.Data.DataSet.GetChanges%2A> メソッドを呼び出すと、変更されたレコードのみを含む新しいデータセットまたはデータテーブルが返されます。 新しいレコードのみ、または変更されたレコードのみを取得する場合は、<xref:System.Data.DataRowState> 列挙体の値をパラメーターとして `GetChanges` メソッドに渡すことができます。

<xref:System.Data.DataRowVersion> 列挙体を使用して、行の異なるバージョン (たとえば、行に含まれていた元の値) にアクセスします。

### <a name="to-get-all-changed-records-from-a-dataset"></a>データセットから変更されたすべてのレコードを取得するには

- データセットの <xref:System.Data.DataSet.GetChanges%2A> メソッドを呼び出します。

     次の例では、`changedRecords` という名前の新しいデータセットを作成し、`dataSet1`という名前の別のデータセットから変更されたすべてのレコードを設定します。

     [!code-csharp[VbRaddataEditing#14](../data-tools/codesnippet/CSharp/validate-data-in-datasets_2.cs)]
     [!code-vb[VbRaddataEditing#14](../data-tools/codesnippet/VisualBasic/validate-data-in-datasets_2.vb)]

### <a name="to-get-all-changed-records-from-a-data-table"></a>データテーブルから変更されたすべてのレコードを取得するには

- DataTable の <xref:System.Data.DataTable.GetChanges%2A> メソッドを呼び出します。

     次の例では、`changedRecordsTable` という名前の新しいデータテーブルを作成し、`dataTable1`と呼ばれる別のデータテーブルの変更されたすべてのレコードをこのテーブルに追加します。

     [!code-csharp[VbRaddataEditing#15](../data-tools/codesnippet/CSharp/validate-data-in-datasets_3.cs)]
     [!code-vb[VbRaddataEditing#15](../data-tools/codesnippet/VisualBasic/validate-data-in-datasets_3.vb)]

### <a name="to-get-all-records-that-have-a-specific-row-state"></a>特定の行の状態を持つすべてのレコードを取得するには

- データセットまたはデータテーブルの `GetChanges` メソッドを呼び出し、<xref:System.Data.DataRowState> 列挙値を引数として渡します。

     次の例では、`addedRecords` という名前の新しいデータセットを作成し、`dataSet1` データセットに追加されたレコードのみを設定する方法を示します。

     [!code-csharp[VbRaddataEditing#16](../data-tools/codesnippet/CSharp/validate-data-in-datasets_4.cs)]
     [!code-vb[VbRaddataEditing#16](../data-tools/codesnippet/VisualBasic/validate-data-in-datasets_4.vb)]

     次の例は、`Customers` テーブルに最近追加されたすべてのレコードを返す方法を示しています。

     [!code-csharp[VbRaddataEditing#17](../data-tools/codesnippet/CSharp/validate-data-in-datasets_5.cs)]
     [!code-vb[VbRaddataEditing#17](../data-tools/codesnippet/VisualBasic/validate-data-in-datasets_5.vb)]

## <a name="access-the-original-version-of-a-datarow"></a>DataRow の元のバージョンにアクセスする
データ行を変更すると、データセットにその行の元のバージョン (<xref:System.Data.DataRowVersion.Original>) と新しいバージョン (<xref:System.Data.DataRowVersion.Current>) が保存されます。 たとえば、`AcceptChanges` メソッドを呼び出す前にレコードの別のバージョン (<xref:System.Data.DataRowVersion> 列挙定数で定義) にアクセスし、そのバージョンに応じて変更を処理できます。

> [!NOTE]
> 行の異なるバージョンが存在するのは、編集されてから `AcceptChanges` メソッドが呼び出された後のみです。 `AcceptChanges` メソッドの呼び出し後は、現在のバージョンと元のバージョンが同じになります。

<xref:System.Data.DataRowVersion> 値を列インデックス (文字列である列名) と共に渡すと、その列の特定の行バージョンから値が返されます。 変更された列は、<xref:System.Data.DataTable.ColumnChanging> イベントと <xref:System.Data.DataTable.ColumnChanged> イベント中に識別されます。 これは、検証のためにさまざまな行バージョンを検査するのに最適なタイミングです。 ただし、制約を一時的に中断している場合は、それらのイベントは発生せず、変更された列をプログラムで識別する必要があります。 <xref:System.Data.DataTable.Columns%2A> コレクションを反復処理し、異なる <xref:System.Data.DataRowVersion> 値を比較することにより変更された列を識別できます。

### <a name="to-get-the-original-version-of-a-record"></a>レコードの元のバージョンを取得するには

- 返される行の <xref:System.Data.DataRowVersion> を渡すことによって、列の値にアクセスします。

     次の例は、<xref:System.Data.DataRowVersion> 値を使用して、<xref:System.Data.DataRow>内の `CompanyName` フィールドの元の値を取得する方法を示しています。

     [!code-csharp[VbRaddataEditing#21](../data-tools/codesnippet/CSharp/validate-data-in-datasets_6.cs)]
     [!code-vb[VbRaddataEditing#21](../data-tools/codesnippet/VisualBasic/validate-data-in-datasets_6.vb)]

## <a name="access-the-current-version-of-a-datarow"></a>DataRow の現在のバージョンにアクセスする

### <a name="to-get-the-current-version-of-a-record"></a>レコードの現在のバージョンを取得するには

- 列の値にアクセスし、取得する行のバージョンを示すパラメーターをインデックスに追加します。

     次の例は、<xref:System.Data.DataRowVersion> 値を使用して、<xref:System.Data.DataRow>内の `CompanyName` フィールドの現在の値を取得する方法を示しています。

     [!code-csharp[VbRaddataEditing#22](../data-tools/codesnippet/CSharp/validate-data-in-datasets_7.cs)]
     [!code-vb[VbRaddataEditing#22](../data-tools/codesnippet/VisualBasic/validate-data-in-datasets_7.vb)]

## <a name="see-also"></a>関連項目

- [Visual Studio のデータセット ツール](../data-tools/dataset-tools-in-visual-studio.md)
- [方法: Windows フォーム DataGridView コントロールのデータを検証する](/dotnet/framework/winforms/controls/how-to-validate-data-in-the-windows-forms-datagridview-control)
- [方法: Windows フォーム ErrorProvider コンポーネントを使用してフォーム妥当性検査でエラー アイコンを表示する](/dotnet/framework/winforms/controls/display-error-icons-for-form-validation-with-wf-errorprovider)
