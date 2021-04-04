---
title: データセットのデータの検証
description: データセット内のデータを検証する方法について説明します。 データを検証するには、データオブジェクトに入力された値がデータセットのスキーマ内の制約に準拠していることを確認する必要があります。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
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
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: 82cfcf1ce030cfe597c3ae7bfe85c528184c548a
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106215670"
---
# <a name="validate-data-in-datasets"></a>データセットのデータの検証
データの検証は、データオブジェクトに入力される値がデータセットのスキーマ内の制約に準拠していることを確認するプロセスです。 また、検証プロセスでは、これらの値が、アプリケーションに対して設定されている規則に従っていることも確認します。 基になるデータベースに更新を送信する前に、データを検証することをお勧めします。 これにより、エラーが減少し、アプリケーションとデータベース間で発生する可能性のあるラウンドトリップの回数も減ります。

データセットに書き込まれるデータが、データセット自体に検証チェックを組み込むことによって有効であることを確認できます。 データセットは、フォーム内のコントロール、コンポーネント内、またはその他の方法で、更新の実行方法に関係なくデータを確認できます。 データセットはアプリケーションの一部であるため (データベースバックエンドとは異なります)、アプリケーション固有の検証を構築するための論理的な場所です。

アプリケーションに検証を追加する最適な場所は、データセットの部分クラスファイルです。 [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]またはで [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] **データセットデザイナー** を開き、検証を作成する列またはテーブルをダブルクリックします。 この操作により、 <xref:System.Data.DataTable.ColumnChanging> イベントハンドラーまたはイベントハンドラーが自動的に作成さ <xref:System.Data.DataTable.RowChanging> れます。

## <a name="validate-data"></a>データの検証
データセット内の検証は、次の方法で実現されます。

- 変更時に個々のデータ列の値を確認できる、独自のアプリケーション固有の検証を作成する。 詳細については、「 [方法: 列の変更時にデータを検証する](validate-data-in-datasets.md)」を参照してください。

- データ行全体が変更されている間にデータを値にチェックできる独自のアプリケーション固有の検証を作成する。 詳細については、「 [方法: 行の変更時にデータを検証する](validate-data-in-datasets.md)」を参照してください。

- データセットの実際のスキーマ定義の一部として、キー、一意の制約などを作成する。

- オブジェクトのプロパティ (、、など) を設定する <xref:System.Data.DataColumn> <xref:System.Data.DataColumn.MaxLength%2A> <xref:System.Data.DataColumn.AllowDBNull%2A> <xref:System.Data.DataColumn.Unique%2A> 。

<xref:System.Data.DataTable>レコードで変更が発生すると、オブジェクトによっていくつかのイベントが発生します。

- <xref:System.Data.DataTable.ColumnChanging>イベントと <xref:System.Data.DataTable.ColumnChanged> イベントは、個々の列を変更するたびおよび後に発生します。 イベントは、 <xref:System.Data.DataTable.ColumnChanging> 特定の列の変更を検証する場合に便利です。 提案された変更に関する情報は、イベントの引数として渡されます。
- <xref:System.Data.DataTable.RowChanging>およびイベントは、 <xref:System.Data.DataTable.RowChanged> 行の変更中および変更後に発生します。 <xref:System.Data.DataTable.RowChanging>イベントの方が一般的です。 行のどこかで変更が行われていることを示していますが、変更された列はわかりません。

既定では、列を変更するたびに4つのイベントが発生します。 1つ目は <xref:System.Data.DataTable.ColumnChanging> 、 <xref:System.Data.DataTable.ColumnChanged> 変更されている特定の列のイベントとイベントです。 次に、 <xref:System.Data.DataTable.RowChanging> イベントとイベントを示し <xref:System.Data.DataTable.RowChanged> ます。 行に対して複数の変更が行われている場合、各変更に対してイベントが発生します。

> [!NOTE]
> データ行のメソッドは、 <xref:System.Data.DataRow.BeginEdit%2A> 個々の <xref:System.Data.DataTable.RowChanging> 列が変更された後、イベントおよびイベントをオフにし <xref:System.Data.DataTable.RowChanged> ます。 その場合、イベントは、メソッドが呼び出されるまで発生しません <xref:System.Data.DataRow.EndEdit%2A> 。この場合、イベント <xref:System.Data.DataTable.RowChanging> と <xref:System.Data.DataTable.RowChanged> イベントが1回だけ発生します。 詳細については、「 [データセットの読み込み中に制約をオフにする](../data-tools/turn-off-constraints-while-filling-a-dataset.md)」を参照してください。

選択するイベントは、検証に必要な粒度によって異なります。 列が変更されたときにエラーをすぐにキャッチすることが重要な場合は、イベントを使用して検証をビルドし <xref:System.Data.DataTable.ColumnChanging> ます。 それ以外の場合は、 <xref:System.Data.DataTable.RowChanging> イベントを使用します。これにより、一度に複数のエラーがキャッチされる可能性があります。 さらに、ある列の値が別の列の内容に基づいて検証されるようにデータが構造化されている場合は、イベント中に検証を実行し <xref:System.Data.DataTable.RowChanging> ます。

レコードが更新されると、オブジェクトは、変更 <xref:System.Data.DataTable> が発生した後、変更が行われた後に応答できるイベントを発生させます。

アプリケーションで型指定されたデータセットを使用する場合は、厳密に型指定されたイベントハンドラーを作成できます。 これにより `dataTableNameRowChanging` 、、、、およびのハンドラーを作成するための、追加で型指定された4つのイベントが追加さ `dataTableNameRowChanged` `dataTableNameRowDeleting` れます `dataTableNameRowDeleted` 。 これらの型指定されたイベントハンドラーは、コードの記述と読み取りが簡単になるように、テーブルの列名を含む引数を渡します。

## <a name="data-update-events"></a>データ更新イベント

|Event|説明|
|-----------|-----------------|
|<xref:System.Data.DataTable.ColumnChanging>|列の値が変更されています。 イベントは、提案された新しい値と共に行と列を渡します。|
|<xref:System.Data.DataTable.ColumnChanged>|列の値が変更されました。 イベントは、提案された値と共に行と列を渡します。|
|<xref:System.Data.DataTable.RowChanging>|オブジェクトに対して行われた変更は、 <xref:System.Data.DataRow> データセットに再度コミットされます。 メソッドを呼び出していない場合は、 <xref:System.Data.DataRow.BeginEdit%2A> <xref:System.Data.DataTable.RowChanging> イベントが発生した直後に列が変更されるたびにイベントが発生し <xref:System.Data.DataTable.ColumnChanging> ます。 <xref:System.Data.DataRow.BeginEdit%2A>変更を加える前にを呼び出した場合、 <xref:System.Data.DataTable.RowChanging> イベントは、メソッドを呼び出したときにのみ発生し <xref:System.Data.DataRow.EndEdit%2A> ます。<br /><br /> イベントは、行と、実行されているアクションの種類 (変更、挿入など) を示す値を渡します。|
|<xref:System.Data.DataTable.RowChanged>|行が変更されました。 イベントは、行と、実行されているアクションの種類 (変更、挿入など) を示す値を渡します。|
|<xref:System.Data.DataTable.RowDeleting>|行が削除されています。 イベントは、実行されているアクションの種類 (削除) を示す値と共に、行をユーザーに渡します。|
|<xref:System.Data.DataTable.RowDeleted>|行が削除されました。 イベントは、実行されているアクションの種類 (削除) を示す値と共に、行をユーザーに渡します。|

<xref:System.Data.DataTable.ColumnChanging>、 <xref:System.Data.DataTable.RowChanging> 、およびの各 <xref:System.Data.DataTable.RowDeleting> イベントは、更新プロセス中に発生します。 これらのイベントを使用して、データを検証したり、他の種類の処理を実行したりすることができます。 更新はこれらのイベント中に処理中であるため、例外をスローすることで取り消すことができます。これにより、更新が終了するのを防ぐことができます。

<xref:System.Data.DataTable.ColumnChanged>、、 <xref:System.Data.DataTable.RowChanged> およびの各 <xref:System.Data.DataTable.RowDeleted> イベントは、更新が正常に完了したときに発生する通知イベントです。 これらのイベントは、更新が正常に行われたことに基づいてさらにアクションを実行する場合に便利です。

## <a name="validate-data-during-column-changes"></a>列の変更時にデータを検証する

> [!NOTE]
> **データセットデザイナー** は、検証ロジックをデータセットに追加できる部分クラスを作成します。 デザイナーで生成されたデータセットでは、部分クラスのコードは削除または変更されません。

データ列の値がイベントに応答して変化したときにデータを検証でき <xref:System.Data.DataTable.ColumnChanging> ます。 このイベントが発生すると、 <xref:System.Data.DataColumnChangeEventArgs.ProposedValue%2A> 現在の列に対して提示されている値を含むイベント引数 () が渡されます。 の内容に基づいて `e.ProposedValue` 、次のことができます。

- 何もせずに、指示された値を受け入れます。

- 列変更イベントハンドラー内から列 error () を設定して、提示された値を拒否し <xref:System.Data.DataRow.SetColumnError%2A> ます。

- オプションで <xref:System.Windows.Forms.ErrorProvider> コントロールを使用して、ユーザーにエラー メッセージを表示します。 詳細については、「[ErrorProvider コンポーネント](/dotnet/framework/winforms/controls/errorprovider-component-windows-forms)」を参照してください。

検証は、イベント中に実行することもでき <xref:System.Data.DataTable.RowChanging> ます。

## <a name="validate-data-during-row-changes"></a>行の変更中にデータを検証する
検証する各列にアプリケーションの要件を満たすデータが格納されていることを検証するコードを記述できます。 これを行うには、提案された値が許容できない場合にエラーが含まれていることを示すように列を設定します。 `Quantity` 列が 0 以下の場合に列エラーを設定する例を次に示します。 行変更イベント ハンドラーは、次のように記述します。

### <a name="to-validate-data-when-a-row-changes-visual-basic"></a>行の変更時にデータを検証するには (Visual Basic)

1. **データセット デザイナー** でご自分のデータセットを開きます。 詳細については、「 [チュートリアル: データセットデザイナーでのデータセットの作成](walkthrough-creating-a-dataset-with-the-dataset-designer.md)」を参照してください。

2. 検証するテーブルのタイトル バーをダブルクリックします。 この操作により、データセットの部分クラス ファイルに <xref:System.Data.DataTable.RowChanging> の <xref:System.Data.DataTable> イベント ハンドラーが自動的に作成されます。

    > [!TIP]
    > テーブル名の左側をダブルクリックして、行変更イベント ハンドラーを作成します。 テーブル名をダブルクリックすると、そのテーブルを編集できます。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataValidating/VB/NorthwindDataSet.vb" id="Snippet3":::

### <a name="to-validate-data-when-a-row-changes-c"></a>行の変更時にデータ検証するには (C#)

1. **データセット デザイナー** でご自分のデータセットを開きます。 詳細については、「 [チュートリアル: データセットデザイナーでのデータセットの作成](walkthrough-creating-a-dataset-with-the-dataset-designer.md)」を参照してください。

2. 検証するテーブルのタイトル バーをダブルクリックします。 この操作により、<xref:System.Data.DataTable> の部分クラス ファイルが作成されます。

    > [!NOTE]
    > **データセット デザイナー** では、<xref:System.Data.DataTable.RowChanging> イベントのイベント ハンドラーが自動作成されません。 イベントを処理するメソッドを作成し、コードを実行して、 <xref:System.Data.DataTable.RowChanging> テーブルの初期化メソッドでイベントをフックする必要があります。

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
データテーブルの各行には、 <xref:System.Data.DataRow.RowState%2A> 列挙体の値を使用してその行の現在の状態を追跡するプロパティがあり <xref:System.Data.DataRowState> ます。 またはのメソッドを呼び出すことによって、データセットまたはデータテーブルから変更された行を返すことができ `GetChanges` <xref:System.Data.DataSet> <xref:System.Data.DataTable> ます。 `GetChanges`データセットのメソッドを呼び出すことによって、が呼び出される前に変更が存在することを確認でき <xref:System.Data.DataSet.HasChanges%2A> ます。

> [!NOTE]
> (メソッドを呼び出すことによって) データセットまたはデータテーブルへの変更をコミットした後 <xref:System.Data.DataSet.AcceptChanges%2A> 、 `GetChanges` メソッドはデータを返しません。 アプリケーションで変更された行を処理する必要がある場合は、メソッドを呼び出す前に、変更を処理する必要があり `AcceptChanges` ます。

データ <xref:System.Data.DataSet.GetChanges%2A> セットまたはデータテーブルのメソッドを呼び出すと、変更されたレコードのみを含む新しいデータセットまたはデータテーブルが返されます。 新しいレコードのみ、または変更されたレコードのみを取得する場合は、列挙体の値を <xref:System.Data.DataRowState> パラメーターとしてメソッドに渡すことができ `GetChanges` ます。

<xref:System.Data.DataRowVersion>異なるバージョンの行にアクセスするには、列挙体を使用します (たとえば、行を処理する前の元の値)。

### <a name="to-get-all-changed-records-from-a-dataset"></a>データセットから変更されたすべてのレコードを取得するには

- <xref:System.Data.DataSet.GetChanges%2A>データセットのメソッドを呼び出します。

     次の例では、という新しいデータセットを作成し、と `changedRecords` いう名前の別のデータセットの変更されたすべてのレコードをこのデータセットに追加し `dataSet1` ます。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet14":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet14":::

### <a name="to-get-all-changed-records-from-a-data-table"></a>データテーブルから変更されたすべてのレコードを取得するには

- <xref:System.Data.DataTable.GetChanges%2A>DataTable のメソッドを呼び出します。

     次の例では、という新しいデータテーブルを作成し、と `changedRecordsTable` いう名前の別のデータテーブルの変更されたすべてのレコードをこのテーブルに格納し `dataTable1` ます。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet15":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet15":::

### <a name="to-get-all-records-that-have-a-specific-row-state"></a>特定の行の状態を持つすべてのレコードを取得するには

- `GetChanges`データセットまたはデータテーブルのメソッドを呼び出し、 <xref:System.Data.DataRowState> 列挙値を引数として渡します。

     次の例は、という新しいデータセットを作成 `addedRecords` し、データセットに追加されたレコードのみを設定する方法を示してい `dataSet1` ます。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet16":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet16":::

     次の例は、テーブルに最近追加されたすべてのレコードを返す方法を示してい `Customers` ます。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet17":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet17":::

## <a name="access-the-original-version-of-a-datarow"></a>DataRow の元のバージョンにアクセスする
データ行を変更すると、データセットにその行の元のバージョン (<xref:System.Data.DataRowVersion.Original>) と新しいバージョン (<xref:System.Data.DataRowVersion.Current>) が保存されます。 たとえば、`AcceptChanges` メソッドを呼び出す前にレコードの別のバージョン (<xref:System.Data.DataRowVersion> 列挙定数で定義) にアクセスし、そのバージョンに応じて変更を処理できます。

> [!NOTE]
> 行の異なるバージョンは、編集された後、メソッドが呼び出される前にのみ存在し `AcceptChanges` ます。 `AcceptChanges` メソッドの呼び出し後は、現在のバージョンと元のバージョンが同じになります。

<xref:System.Data.DataRowVersion> 値を列インデックス (文字列である列名) と共に渡すと、その列の特定の行バージョンから値が返されます。 変更された列は、イベントとイベント中に識別され <xref:System.Data.DataTable.ColumnChanging> <xref:System.Data.DataTable.ColumnChanged> ます。 これは、検証のためにさまざまな行バージョンを検査するのに最適なタイミングです。 ただし、制約を一時的に中断している場合は、それらのイベントは発生せず、変更された列をプログラムで識別する必要があります。 <xref:System.Data.DataTable.Columns%2A> コレクションを反復処理し、異なる <xref:System.Data.DataRowVersion> 値を比較することにより変更された列を識別できます。

### <a name="to-get-the-original-version-of-a-record"></a>レコードの元のバージョンを取得するには

- 返される行のを渡すことによって、列の値にアクセスし <xref:System.Data.DataRowVersion> ます。

     次の例は、値を使用し <xref:System.Data.DataRowVersion> て内のフィールドの元の値を取得する方法を示してい `CompanyName` <xref:System.Data.DataRow> ます。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet21":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet21":::

## <a name="access-the-current-version-of-a-datarow"></a>DataRow の現在のバージョンにアクセスする

### <a name="to-get-the-current-version-of-a-record"></a>レコードの現在のバージョンを取得するには

- 列の値にアクセスし、取得する行のバージョンを示すパラメーターをインデックスに追加します。

     次の例は、値を使用して内のフィールドの現在の値を取得する方法を示してい <xref:System.Data.DataRowVersion> `CompanyName` <xref:System.Data.DataRow> ます。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet22":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet22":::

## <a name="see-also"></a>関連項目

- [Visual Studio のデータセット ツール](../data-tools/dataset-tools-in-visual-studio.md)
- [方法: Windows フォーム DataGridView コントロールでデータを検証する](/dotnet/framework/winforms/controls/how-to-validate-data-in-the-windows-forms-datagridview-control)
- [方法: Windows フォーム ErrorProvider コンポーネントを使用してフォーム検証のエラーアイコンを表示する](/dotnet/framework/winforms/controls/display-error-icons-for-form-validation-with-wf-errorprovider)
