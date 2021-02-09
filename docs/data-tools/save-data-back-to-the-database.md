---
title: データをデータベースに保存する
description: データセットツールを使用して、データをデータベースに保存し直します。 データセットは、変更された場合にデータベースに保存し直す必要がある、メモリ内のデータのコピーです。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- datasets [Visual Basic], validating data
- data validation, datasets
- data [Visual Studio], saving
- row version
- updating datasets, constraints
- datasets [Visual Basic], about datasets
- datasets [Visual Basic], merging
- updates, constraints in datasets
- saving data, about saving data
- datasets [Visual Basic], constraints
- TableAdapters
ms.assetid: afe6cb8a-dc6a-428b-b07b-903ac02c890b
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: bdbfba867fd1fa898ff376d3d1e60f33f58c32a0
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99866594"
---
# <a name="save-data-back-to-the-database"></a>データをデータベースに保存する

データセットは、メモリ内のデータのコピーです。 そのデータを変更する場合は、これらの変更をデータベースに保存し直すことをお勧めします。 これを行うには、次の3つの方法のいずれかを使用します。

- TableAdapter のメソッドの1つを呼び出すことによって `Update`

- TableAdapter のメソッドの1つを呼び出すことによって `DBDirect`

- データセット `UpdateAll` 内の他のテーブルに関連付けられているテーブルが dataset に含まれている場合に、Visual Studio によって生成される TableAdapterManager に対してメソッドを呼び出すことによって

データセットテーブルを Windows フォームまたは XAML ページのコントロールにデータバインドすると、データバインディングアーキテクチャによってすべての作業が実行されます。

Tableadapter を使い慣れている場合は、次のトピックのいずれかに直接移動できます。

|トピック|説明|
|-----------|-----------------|
|[データベースに新しいレコードを挿入する](../data-tools/insert-new-records-into-a-database.md)|Tableadapter またはコマンドオブジェクトを使用して更新と挿入を実行する方法|
|[TableAdapter を使用してデータを更新する](../data-tools/update-data-by-using-a-tableadapter.md)|Tableadapter を使用して更新プログラムを実行する方法|
|[階層更新](../data-tools/hierarchical-update.md)|2つ以上の関連テーブルを含むデータセットから更新を実行する方法|
|[コンカレンシー例外を処理する](../data-tools/handle-a-concurrency-exception.md)|2人のユーザーが同時にデータベース内の同じデータを変更しようとしたときに例外を処理する方法|
|[方法: トランザクションを使用してデータを保存する](../data-tools/save-data-by-using-a-transaction.md)|システムを使用してトランザクションにデータを保存する方法。 トランザクションの名前空間と TransactionScope オブジェクト|
|[トランザクションにデータを保存する](../data-tools/save-data-in-a-transaction.md)|トランザクション内のデータベースにデータを保存する方法を示す Windows フォームアプリケーションを作成するチュートリアル|
|[データベースへのデータの保存 (複数テーブル)](../data-tools/save-data-to-a-database-multiple-tables.md)|レコードを編集して複数のテーブルの変更をデータベースに保存する方法|
|[オブジェクトからデータベースにデータを保存する](../data-tools/save-data-from-an-object-to-a-database.md)|TableAdapter DbDirect メソッドを使用してデータセットに含まれていないオブジェクトのデータをデータベースに渡す方法|
|[TableAdapter DBDirect メソッドを使用してデータを保存する](../data-tools/save-data-with-the-tableadapter-dbdirect-methods.md)|TableAdapter を使用して SQL クエリをデータベースに直接送信する方法|
|[データセットを XML として保存する](../data-tools/save-a-dataset-as-xml.md)|XML ドキュメントにデータセットを保存する方法|

## <a name="two-stage-updates"></a>2 段階の更新

データソースの更新は、2段階のプロセスです。 最初の手順では、新しいレコード、変更されたレコード、または削除されたレコードを使用してデータセットを更新します。 アプリケーションがこれらの変更をデータソースに送信することがない場合は、更新が完了しています。

変更をデータベースに返送する場合は、2番目の手順を実行する必要があります。 データバインドコントロールを使用していない場合は、データ `Update` セットの設定に使用したものと同じ TableAdapter (またはデータアダプター) のメソッドを手動で呼び出す必要があります。 ただし、別のアダプターを使用することもできます。たとえば、データソース間でデータを移動したり、複数のデータソースを更新したりすることができます。 データバインディングを使用せず、関連するテーブルの変更を保存する場合は、自動生成されたクラスの変数を手動でインスタンス化してから、メソッドを呼び出す必要があり `TableAdapterManager` `UpdateAll` ます。

![データセットの更新の概念図](../data-tools/media/vbdatasetupdates.gif)

データセットには、行のコレクションを含むテーブルのコレクションが含まれます。 基になるデータソースを後で更新する場合は、 `DataTable.DataRowCollection` 行を追加または削除するときに、プロパティのメソッドを使用する必要があります。 これらのメソッドは、データソースを更新するために必要な変更の追跡を実行します。 Rows プロパティでコレクションを呼び出すと、 `RemoveAt` 削除はデータベースに返されません。

## <a name="merge-datasets"></a>データセットのマージ

データセットを別のデータセットに *マージ* することによって、データセットの内容を更新できます。 これには、 *ソース* データセットの内容を呼び出し元のデータセット ( *ターゲット* データセットと呼びます) にコピーする作業が含まれます。 データセットをマージすると、ソース データセットの新しいレコードはターゲット データセットに追加されます。 また、ソース データセットのその他の列もターゲット データセットに追加されます。 データセットのマージは、ローカルデータセットがあり、別のアプリケーションから2番目のデータセットを取得する場合に便利です。 また、XML web サービスなどのコンポーネントから2番目のデータセットを取得する場合や、複数のデータセットのデータを統合する必要がある場合にも便利です。

データセットをマージする場合は、 `preserveChanges` <xref:System.Data.DataSet.Merge%2A> ターゲットデータセット内の既存の変更を保持するかどうかをメソッドに示すブール型引数 () を渡すことができます。 データセットはレコードの複数のバージョンを保持しているため、レコードの複数のバージョンがマージされるということに留意することは重要です。 次の表は、2つのデータセットのレコードをマージする方法を示しています。

|DataRowVersion|ターゲット データセット|ソース データセット|
| - | - | - |
|変更元|James Wilson|James c. Wilson|
|Current|Jim Wilson|James c. Wilson|

を使用して前のテーブルのメソッドを呼び出す <xref:System.Data.DataSet.Merge%2A> と `preserveChanges=false targetDataset.Merge(sourceDataset)` 、次のデータが返されます。

|DataRowVersion|ターゲット データセット|ソース データセット|
| - | - | - |
|変更元|James c. Wilson|James c. Wilson|
|Current|James c. Wilson|James c. Wilson|

<xref:System.Data.DataSet.Merge%2A>を使用してメソッドを呼び出すと `preserveChanges = true targetDataset.Merge(sourceDataset, true)` 、次のデータが返されます。

|DataRowVersion|ターゲット データセット|ソース データセット|
| - | - | - |
|変更元|James c. Wilson|James c. Wilson|
|Current|Jim Wilson|James c. Wilson|

> [!CAUTION]
> このシナリオでは、 `preserveChanges = true` <xref:System.Data.DataSet.RejectChanges%2A> ターゲットデータセット内のレコードに対してメソッドが呼び出された場合、 *ソース* データセットの元のデータに戻ります。 つまり、対象のデータセットを使用して元のデータソースを更新しようとすると、更新する元の行を見つけることができないことがあります。 データソースから更新されたレコードを別のデータセットに読み込んで、同時実行違反を防ぐためにマージを実行することで、同時実行違反を防ぐことができます。 (コンカレンシー違反は、データセットにレコードが格納された後で別のユーザーがデータ ソース内のレコードを変更すると発生します。)

## <a name="update-constraints"></a>制約の更新

既存のデータ行に変更を加えるには、個々の列のデータを追加または更新します。 データセットに制約 (外部キーまたは null 非許容の制約など) が含まれている場合は、レコードを更新するときに、レコードが一時的にエラー状態になる可能性があります。 つまり、1つの列の更新が完了した後、次の列に到達する前に、エラー状態になることがあります。

早期に制約違反を防ぐために、更新制約を一時的に中断できます。 これは、次の 2 つの目的があります。

- 1つの列の更新が完了しても、別の列の更新を開始していない場合、エラーがスローされないようにします。

- 特定の更新イベントが発生しないようにします (多くの場合、検証に使用されるイベント)。

> [!NOTE]
> Windows フォームでは、datagrid に組み込まれているデータバインディングアーキテクチャは、フォーカスが行の外に移動するまで制約チェックを中断するため、 <xref:System.Data.DataRow.BeginEdit%2A> 、 <xref:System.Data.DataRow.EndEdit%2A> 、またはの各メソッドを明示的に呼び出す必要はありません <xref:System.Data.DataRow.CancelEdit%2A> 。

データセットで <xref:System.Data.DataSet.Merge%2A> メソッドが呼び出されると、制約は自動的に無効になります。 マージが完了すると、有効にできないデータセットに制約がある場合は、 <xref:System.Data.ConstraintException> がスローされます。 この場合、<xref:System.Data.DataSet.EnforceConstraints%2A> プロパティが `false,` に設定されるので、すべての制約違反を解決してから <xref:System.Data.DataSet.EnforceConstraints%2A> プロパティを `true` に設定し直す必要があります。

更新が完了したら、制約チェックを再度有効にすることができます。これにより、更新イベントが再度有効になり、イベントが発生します。

イベントの中断の詳細については、「 [データセットの読み込み中に制約をオフにする](../data-tools/turn-off-constraints-while-filling-a-dataset.md)」を参照してください。

## <a name="dataset-update-errors"></a>データセットの更新エラー

データセットのレコードを更新するときにエラーが発生する場合があります。 たとえば、誤った型のデータを列に誤って書き込んだ場合や、データが長すぎる場合や、他の整合性の問題が発生している場合などが考えられます。 また、更新イベントのいずれかの段階でカスタムエラーが発生する可能性がある、アプリケーション固有の検証チェックがある場合もあります。 詳細については、「 [データセット内のデータの検証](../data-tools/validate-data-in-datasets.md)」を参照してください。

## <a name="maintain-information-about-changes"></a>変更に関する情報を保持する

データセットの変更に関する情報は、変更されたことを示す行にフラグを設定するか ( <xref:System.Data.DataRow.RowState%2A> )、レコードの複数のコピーを保持する () ことによって、次の2つの方法で保持されます。 <xref:System.Data.DataRowVersion> 変更に関する情報を使用することにより、プロセスはデータセットの変更内容を確認し、適切な更新内容をデータ ソースに送信できます。

### <a name="rowstate-property"></a>RowState プロパティ

<xref:System.Data.DataRow.RowState%2A> オブジェクトの <xref:System.Data.DataRow> プロパティは、データの特定の行のステータスに関する情報を提供する値です。

<xref:System.Data.DataRowState> 列挙定数に使用できる値の詳細を次の表に示します。

|DataRowState 列挙定数の値|Description|
| - |-----------------|
|<xref:System.Data.DataRowState.Added>|行は項目として <xref:System.Data.DataRowCollection> に追加されました。 (この状態の行は、最後のメソッドが呼び出されたときに存在しなかったため、対応する元のバージョンがありません <xref:System.Data.DataRow.AcceptChanges%2A> )。|
|<xref:System.Data.DataRowState.Deleted>|行は <xref:System.Data.DataRow.Delete%2A> オブジェクトの <xref:System.Data.DataRow> を使用して削除されました。|
|<xref:System.Data.DataRowState.Detached>|行は作成されましたが、<xref:System.Data.DataRowCollection> の一部ではありません。 オブジェクトは、作成され <xref:System.Data.DataRow> た直後、コレクションに追加される前、およびコレクションから削除された後に、この状態になります。|
|<xref:System.Data.DataRowState.Modified>|行の列の値がなんらかの方法で変更されました。|
|<xref:System.Data.DataRowState.Unchanged>|行は <xref:System.Data.DataRow.AcceptChanges%2A> が最後に呼び出されてから変更されていません。|

### <a name="datarowversion-enumeration"></a>DataRowVersion 列挙型

データセットはレコードの複数のバージョンを保持します。 フィールドは、 <xref:System.Data.DataRowVersion> <xref:System.Data.DataRow> <xref:System.Data.DataRow.Item%2A> オブジェクトのプロパティまたはメソッドを使用して、で見つかった値を取得するときに使用され <xref:System.Data.DataRow.GetChildRows%2A> <xref:System.Data.DataRow> ます。

<xref:System.Data.DataRowVersion> 列挙定数に使用できる値の詳細を次の表に示します。

|DataRowVersion 列挙定数の値|Description|
| - |-----------------|
|<xref:System.Data.DataRowVersion.Current>|レコードの現在のバージョンには、前回が呼び出されてからレコードに対して行われたすべての変更が含まれてい <xref:System.Data.DataRow.AcceptChanges%2A> ます。 行が削除されている場合、現在のバージョンは存在しません。|
|<xref:System.Data.DataRowVersion.Default>|データセット スキーマまたはデータ ソースにより定義されたレコードの既定値です。|
|<xref:System.Data.DataRowVersion.Original>|レコードの元のバージョンは、データセットで最後の変更がコミットされたときのレコードのコピーです。 つまり、通常はデータ ソースから読み込まれたときのレコードのバージョンです。|
|<xref:System.Data.DataRowVersion.Proposed>|更新の実行中、つまり <xref:System.Data.DataRow.BeginEdit%2A> メソッドの呼び出しと <xref:System.Data.DataRow.EndEdit%2A> メソッドの呼び出しの間に一時的に利用できる、レコードの提案されたバージョンです。 通常は <xref:System.Data.DataTable.RowChanging> などのイベントのハンドラーで、レコードの提案されたバージョンにアクセスします。 <xref:System.Data.DataRow.CancelEdit%2A> メソッドを呼び出すと、変更は無効になり、データ行の提案されたバージョンは削除されます。|

元のバージョンおよび現在のバージョンは、更新情報をデータ ソースに送信する場合に役立ちます。 通常、更新情報をデータ ソースに送信すると、データベースの新しい情報がレコードの現在のバージョンに含まれます。 元のバージョンの情報は、更新するレコードを見つけるために使用されます。

たとえば、レコードの主キーが変更された場合は、変更を更新するために、データソース内の正しいレコードを検索する方法が必要になります。 元のバージョンがなかった場合、レコードはデータ ソースに追加される可能性が高く、結果として不要なレコードが作成されるだけでなく、不正確な古いレコードが 1 つ作成されることになります。 2つのバージョンは同時実行制御でも使用されます。 元のバージョンとデータソース内のレコードを比較して、レコードがデータセットに読み込まれてから変更されたかどうかを確認できます。

提案されたバージョンは、実際に変更をデータセットにコミットする前に検証が必要な場合に役立ちます。

レコードが変更されていても、その行の元のバージョンまたは現在のバージョンが必ず存在するわけではありません。 新しい行をテーブルに挿入した場合、元のバージョンは存在せず、現在のバージョンがあるだけです。 同様に、テーブルの `Delete` メソッドを呼び出すことにより行を削除した場合、元のバージョンはありますが現在のバージョンはありません。

データ行の <xref:System.Data.DataRow.HasVersion%2A> メソッドを照会することにより、レコードの特定のバージョンが存在するかどうかを確認するテストを行うことができます。 列の値を要求するときに <xref:System.Data.DataRowVersion> 列挙値をオプションの引数として渡すことにより、レコードのいずれかのバージョンにアクセスできます。

## <a name="get-changed-records"></a>変更されたレコードを取得する

通常は、データセット内のすべてのレコードを更新しないことをお勧めします。 たとえば、多数のレコードを表示する Windows フォームの <xref:System.Windows.Forms.DataGridView> コントロールをユーザーが使用しているとします。 このとき、ユーザーが一部のレコードだけを更新し、レコードを 1 つ削除し、新しいレコードを 1 つ挿入したとします。 そのような場合のために、データセットおよびデータ テーブルには、変更された行だけを返すためのメソッド (`GetChanges`) が用意されています。

データ テーブルの  メソッド () またはデータセットの  メソッド () を使って、変更されたレコードのサブセットを作成できます。 データ テーブルのメソッドを呼び出すと、変更されたレコードだけを含むテーブルのコピーが返されます。 同様に、データセットのメソッドを呼び出すと、変更されたレコードだけを含む新しいデータセットを取得できます。

`GetChanges` は、変更されたすべてのレコードを返します。 これに対し、目的のを <xref:System.Data.DataRowState> パラメーターとしてメソッドに渡すことで、 `GetChanges` 変更されたレコードのサブセットを指定できます。これには、新しく追加したレコード、削除対象としてマークされているレコード、デタッチされたレコード、または変更されたレコードが含まれます。

変更されたレコードのサブセットを取得することは、処理のために別のコンポーネントにレコードを送信する場合に便利です。 データセット全体を送信する代わりに、コンポーネントが必要としているレコードだけを取得することにより、ほかのコンポーネントとの通信によるオーバーヘッドを小さくできます。

## <a name="commit-changes-in-the-dataset"></a>データセットの変更をコミットする

データセットを変更すると、変更された行の <xref:System.Data.DataRow.RowState%2A> プロパティが設定されます。 レコードの元のバージョンと現在のバージョンは、プロパティによって確立され、維持され、使用できるようになり <xref:System.Data.DataRowView.RowVersion%2A> ます。 これらの変更された行のプロパティに格納されているメタデータは、正しい更新をデータソースに送信するために必要です。

変更内容がデータ ソースの現在の状態を反映している場合は、この情報を保持する必要はなくなります。 通常、データセットとそのソースの同期は以下の 2 通りの場合に保持されます。

- ソースからデータを読み込んだときなど、情報をデータセットに読み込んだ直後。

- データセットからデータソースに変更を送信した後 (ただし、変更内容をデータベースに送信するために必要な変更情報が失われる可能性があるため)。

保留中の変更は、<xref:System.Data.DataSet.AcceptChanges%2A> メソッドを呼び出してデータセットにコミットできます。 通常、 <xref:System.Data.DataSet.AcceptChanges%2A> は次のタイミングで呼び出されます。

- データセットを読み込んだ後。 TableAdapter の `Fill` メソッドを呼び出すことによりデータセットを読み込んだ場合、TableAdapter により変更が自動的にコミットされます。 ただし、別のデータセットをマージすることによりデータセットを読み込む場合は、変更を手動でコミットする必要があります。

    > [!NOTE]
    > アダプター `Fill` のプロパティをに設定することによって、メソッドを呼び出すときに、アダプターが自動的に変更をコミットしないようにすることができます `AcceptChangesDuringFill` `false` 。 がに設定 `false` されている場合 <xref:System.Data.DataRow.RowState%2A> は、塗りつぶし中に挿入される各行のがに設定され <xref:System.Data.DataRowState.Added> ます。

- XML web サービスなど、データセットの変更を別のプロセスに送信した後。

    > [!CAUTION]
    > この方法で変更をコミットすると、変更情報はすべて削除されます。 データセットに加えられた変更をアプリケーションで認識する必要がある操作の実行が完了するまで、変更をコミットしないでください。

この方法で実行できる処理は次のとおりです。

- <xref:System.Data.DataRowVersion.Current>レコードのバージョンをそのバージョンに書き込み、 <xref:System.Data.DataRowVersion.Original> 元のバージョンを上書きします。

- <xref:System.Data.DataRow.RowState%2A>プロパティがに設定されている行を削除 <xref:System.Data.DataRowState.Deleted> します。

- レコードの <xref:System.Data.DataRow.RowState%2A> プロパティを <xref:System.Data.DataRowState.Unchanged> に設定する。

<xref:System.Data.DataSet.AcceptChanges%2A> メソッドは、3 つのレベルで利用可能です。 オブジェクトに対してこのメソッドを呼び出すことで、 <xref:System.Data.DataRow> その行の変更をコミットできます。 また、オブジェクトに対して呼び出すこと <xref:System.Data.DataTable> で、テーブル内のすべての行をコミットすることもできます。 最後に、オブジェクトに対してこのメソッドを呼び出して、 <xref:System.Data.DataSet> データセットのすべてのテーブルのすべてのレコードのすべての保留中の変更をコミットできます。

メソッドが呼び出されたオブジェクトに基づいて、コミットされる変更を次の表に示します。

|Method|結果|
|------------|------------|
|<xref:System.Data.DataRow.AcceptChanges%2A?displayProperty=fullName>|変更は特定の行にだけコミットされます。|
|<xref:System.Data.DataTable.AcceptChanges%2A?displayProperty=fullName>|変更は特定のテーブルのすべての行にコミットされます。|
|<xref:System.Data.DataSet.AcceptChanges%2A?displayProperty=fullName>|変更はデータセットのすべてのテーブルのすべての行にコミットされます。|

> [!NOTE]
> TableAdapter のメソッドを呼び出すことによってデータセットを読み込む場合は `Fill` 、変更を明示的に受け入れる必要はありません。 既定では、 `Fill` メソッドは、 `AcceptChanges` データテーブルの設定が終了した後にメソッドを呼び出します。

関連するメソッドは、 <xref:System.Data.DataSet.RejectChanges%2A> <xref:System.Data.DataRowVersion.Original> バージョンをレコードのバージョンにコピーして、変更の影響を元に戻し <xref:System.Data.DataRowVersion.Current> ます。 また、 <xref:System.Data.DataRow.RowState%2A> 各レコードのをに設定し <xref:System.Data.DataRowState.Unchanged> ます。

## <a name="data-validation"></a>データの検証

アプリケーションのデータが、渡される対象プロセスの要件を満たしているかどうかを検査するために、検証を追加することが必要な場合もあります。 これには、フォーム内のユーザーのエントリが正しいかどうかの確認、別のアプリケーションによってアプリケーションに送信されるデータの検証、コンポーネント内で計算された情報がデータソースとアプリケーションの要件の範囲内にあることの確認などが含まれます。

データを検証するには次の方法があります。

- ビジネス層で、データを検証するコードをアプリケーションに追加する。 データセットでこれを行うことができます。 データセットでは、列および行の値が変更されるたびに変更を検証する機能など、バック エンド検証を活用できます。 詳細については、「 [データセット内のデータの検証](../data-tools/validate-data-in-datasets.md)」を参照してください。

- プレゼンテーション層で、検証をフォームに追加する。 詳細については、「 [Windows フォームでのユーザー入力の検証](/dotnet/framework/winforms/user-input-validation-in-windows-forms)」を参照してください。

- データのバック エンドで、データをデータベースなどのデータ ソースに送信し、データの受け入れまたは拒否を行うことができるようにする。 データの検証やエラー情報を提供する洗練された機能を備えたデータベースを使用している場合、実用的なアプローチになります。データのソースが何であるかにかかわらずデータを検証できるからです。 ただし、この方法は、アプリケーション固有の検証要件に対応していない可能性があります。 さらに、データソースによってデータが検証されると、アプリケーションがバックエンドで発生した検証エラーの解決方法によっては、データソースへのラウンドトリップが多数発生する可能性があります。

   > [!IMPORTANT]
   > に設定されているプロパティを使用してデータコマンドを使用する場合は <xref:System.Data.SqlClient.SqlCommand.CommandType%2A> <xref:System.Data.CommandType.Text> 、クライアントから送信された情報をデータベースに渡す前に慎重に確認してください。 悪意のあるユーザーが、承認なしでデータベースにアクセスしたり、データベースを破壊したりする目的で、変更した SQL ステートメントや追加の SQL ステートメントの送信 (挿入) を試みる場合があります。 ユーザー入力をデータベースに転送する前に、その情報が有効であることを必ず確認してください。 可能な限り、パラメーター化されたクエリまたはストアドプロシージャを常に使用することをお勧めします。

## <a name="transmit-updates-to-the-data-source"></a>データソースに更新を送信する

データセットを変更した後で、変更内容をデータ ソースに転送できます。 一般に、これは TableAdapter (またはデータ アダプター) の `Update` メソッドを呼び出すことによって行います。 メソッドは、データテーブル内の各レコードをループ処理し、必要な更新の種類 (更新、挿入、または削除) を決定し、適切なコマンドを実行します。

更新がどのように行われるかを示すために、アプリケーションで1つのデータテーブルを含むデータセットを使用するとします。 アプリケーションはデータベースから 2 つの行をフェッチします。 行の取得後、インメモリ データ テーブルは次のようになります。

```sql
(RowState)     CustomerID   Name             Status
(Unchanged)    c200         Robert Lyon      Good
(Unchanged)    c400         Nancy Buchanan    Pending
```

アプリケーションによって Nancy Buchanan のステータスが "Preferred" に変更されます。 この変更の結果、その行の <xref:System.Data.DataRow.RowState%2A> プロパティの値は、<xref:System.Data.DataRowState.Unchanged> から <xref:System.Data.DataRowState.Modified> に変更されます。 最初の行の <xref:System.Data.DataRow.RowState%2A> プロパティの値は、<xref:System.Data.DataRowState.Unchanged> のままです。 データ テーブルは次のようになります。

```sql
(RowState)     CustomerID   Name             Status
(Unchanged)    c200         Robert Lyon      Good
(Modified)     c400         Nancy Buchanan    Preferred
```

アプリケーションは `Update` メソッドを呼び出し、データセットをデータベースに転送します。 このメソッドは各行を順に調べます。 最初の行はデータベースからフェッチされた行であり、変更されていないため、このメソッドではデータベースに SQL ステートメントを転送しません。

ただし、2番目の行では、メソッドによって `Update` 自動的に適切なデータコマンドが呼び出され、データベースに転送されます。 SQL ステートメントの特定の構文は、基になるデータストアでサポートされている SQL の言語によって異なります。 しかし、転送される SQL ステートメントには次のような一般的な特徴があります。

- 転送される SQL ステートメントは UPDATE ステートメントである。 <xref:System.Data.DataRow.RowState%2A> プロパティの値が <xref:System.Data.DataRowState.Modified> であるため、このアダプターは UPDATE ステートメントを使用します。

- 転送される SQL ステートメントには、UPDATE ステートメントの転送先が `CustomerID = 'c400'` の行であることを示す WHERE 句が含まれている。 `CustomerID` は転送先のテーブルの主キーであるため、SELECT ステートメントのこの部分により転送先の行を他の行と区別します。 WHERE 句の情報は、 `DataRowVersion.Original` 行を識別するために必要な値が変更された場合に備えて、レコードの元のバージョン () から派生します。

- 転送される SQL ステートメントには SET 句が含まれており、変更された列の新しい値を設定する。

   > [!NOTE]
   > TableAdapter の `UpdateCommand` プロパティにストアド プロシージャの名前が設定されている場合、TableAdapter は SQL ステートメントを作成しません。 その代わりに、適切なパラメーターを渡してストアド プロシージャを呼び出します。

## <a name="pass-parameters"></a>パラメーターを渡す

通常、パラメーターを使用して、データベースで更新されるレコードの値を渡します。 TableAdapter のメソッドが UPDATE ステートメントを実行するときは、 `Update` パラメーター値を入力する必要があります。 この値は、該当するデータ コマンドの `Parameters` コレクションから取得します。この場合は TableAdapter の `UpdateCommand` オブジェクトです。

Visual Studio ツールを使用してデータアダプターを生成した場合、オブジェクトには、 `UpdateCommand` ステートメント内の各パラメータープレースホルダーに対応するパラメーターのコレクションが格納されます。

各パラメーターの <xref:System.Data.SqlClient.SqlParameter.SourceColumn%2A?displayProperty=fullName> プロパティは、データ テーブル内の列を指しています。 たとえば、 `SourceColumn` `au_id` パラメーターとパラメーターのプロパティ `Original_au_id` は、データテーブル内の作成者 id が格納されている任意の列に設定されます。アダプターのメソッドを `Update` 実行すると、更新されているレコードから author id 列が読み取られ、その値がステートメントに入力されます。

UPDATE ステートメントでは、新しい値 (レコードに書き込まれる値) と古い値 (レコードがデータベースに配置されるようにするため) の両方を指定する必要があります。 したがって、それぞれの値に 2 つのパラメーターがあります。SET 句に 1 つ、WHERE 句に 1 つのパラメーターです。 どちらのパラメーターも、更新されるレコードからデータを読み取りますが、パラメーターのプロパティに基づいて異なるバージョンの列値を取得し <xref:System.Data.SqlClient.SqlParameter.SourceVersion> ます。 SET 句のパラメーターは現在のバージョンを取得し、WHERE 句のパラメーターは元のバージョンを取得します。

> [!NOTE]
> `Parameters` コレクションの値はコードで設定することもできます。通常はデータ アダプターの <xref:System.Data.DataTable.RowChanging> イベントのイベント ハンドラーで設定します。

## <a name="see-also"></a>関連項目

- [Visual Studio のデータセット ツール](../data-tools/dataset-tools-in-visual-studio.md)
- [Tableadapter の作成および構成](create-and-configure-tableadapters.md)
- [TableAdapter を使用してデータを更新する](../data-tools/update-data-by-using-a-tableadapter.md)
- [Visual Studio でのデータへのコントロールのバインド](../data-tools/bind-controls-to-data-in-visual-studio.md)
- [データの検証](validate-data-in-datasets.md)
- [方法: エンティティを追加、変更、および削除する (WCF data services)](/dotnet/framework/data/wcf/how-to-add-modify-and-delete-entities-wcf-data-services)
