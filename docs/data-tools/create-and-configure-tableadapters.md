---
title: Tableadapter の作成および構成
ms.date: 09/01/2017
ms.topic: conceptual
helpviewer_keywords:
- table adapters, creating
- creating TableAdapters
- data [Visual Studio], creating data components
- data [Visual Studio], TableAdapters
- data [Visual Studio], creating table adapters
ms.assetid: 08630d69-0d6c-4e8f-b42d-2922f45f8415
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 4e5a557aeeee3fca2bef0367a630dfaca04b3a74
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75586784"
---
# <a name="create-and-configure-tableadapters"></a>Tableadapter の作成および構成

TableAdapter を使用すると、アプリケーションとデータベース間で通信できます。 これらのユーザーは、データベースに接続し、クエリまたはストアドプロシージャを実行して、新しいデータテーブルを返すか、または返されたデータを既存の <xref:System.Data.DataTable> に入力します。 Tableadapter では、更新されたデータをアプリケーションからデータベースに送信することもできます。

Tableadapter は、次のいずれかの操作を実行すると作成されます。

- **サーバーエクスプローラー**から**データセットデザイナー**にデータベースオブジェクトをドラッグします。

- データソース構成ウィザードを実行し、**データベース**または**Web サービス**のいずれかのデータソースの種類を選択します。

   ![Visual Studio のデータソース構成ウィザード](media/data-source-configuration-wizard.png)

また、新しい TableAdapter を作成し、データソースで構成することもできます。そのためには、**ツールボックス**から**データセットデザイナー**サーフェイスの空の領域に tableadapter をドラッグします。

Tableadapter の概要については、「Tableadapter を使用した[データセットの読み込み](../data-tools/fill-datasets-by-using-tableadapters.md)」を参照してください。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

## <a name="use-the-tableadapter-configuration-wizard"></a>TableAdapter 構成ウィザードの使用

Tableadapter とそれに関連する Datatable を作成または編集するには、 **Tableadapter 構成ウィザード**を実行します。 **データセットデザイナー**で既存の TableAdapter を右クリックして構成できます。

![レーダーデータテーブルアダプター構成ウィザード](../data-tools/media/raddata-table-adapter-configuration-wizard.png)

**データセットデザイナー**にフォーカスがあるときにツールボックスから新しい TableAdapter をドラッグすると、ウィザードが起動し、tableadapter が接続するデータソースを指定するように求められます。 次のページでは、SQL ステートメントまたはストアドプロシージャのいずれかで、データベースとの通信に使用する必要があるコマンドの種類がウィザードによって確認されます。 (これは、既にデータソースに関連付けられている TableAdapter を構成している場合は表示されません)。

- データベースに対する適切な権限を持っている場合は、基になるデータベースに新しいストアドプロシージャを作成することもできます。 これらのアクセス許可がない場合、これはオプションではありません。

- また、TableAdapter の**SELECT**、 **INSERT**、 **UPDATE**、および**DELETE**の各コマンドに対して、既存のストアドプロシージャを実行することもできます。 たとえば、 **Update**コマンドに割り当てられているストアドプロシージャは、`TableAdapter.Update()` メソッドが呼び出されたときに実行されます。

選択したストアド プロシージャのパラメーターを、データ テーブルの対応する列に割り当てます。 たとえば、ストアドプロシージャがテーブルの `CompanyName` 列に渡す `@CompanyName` という名前のパラメーターを受け取る場合は、`@CompanyName` パラメーターの**Source 列**を `CompanyName`に設定します。

> [!NOTE]
> SELECT コマンドに割り当てられているストアドプロシージャは、ウィザードの次の手順で名前を指定した TableAdapter のメソッドを呼び出すことによって実行されます。 既定のメソッドは `Fill`であるため、通常は SELECT プロシージャを実行するために使用されるコードが `TableAdapter.Fill(tableName)`ます。 既定の名前を `Fill`から変更する場合は、`Fill` を割り当てた名前に置き換え、"TableAdapter" を TableAdapter の実際の名前 (たとえば、`CustomersTableAdapter`) に置き換えます。

- **[更新を直接データベースに送信するメソッドを作成する]** オプションを選択することは、`GenerateDBDirectMethods` プロパティを true に設定することと同じです。 元の SQL ステートメントに十分な情報が含まれていないか、クエリが更新可能なクエリではない場合、このオプションは使用できません。 たとえば、**結合**クエリや、単一の (スカラー) 値を返すクエリで、このような状況が発生する可能性があります。

ウィザードの **[詳細設定] オプション**を使用すると、次のことができます。

- **[SQL ステートメントの生成]** ページで定義されている select ステートメントに基づいて INSERT、UPDATE、および DELETE ステートメントを生成します。
- [オプティミスティック コンカレンシーを使用する]
- INSERT ステートメントおよび UPDATE ステートメントの実行後にデータテーブルを更新するかどうかを指定します。

## <a name="configure-a-tableadapters-fill-method"></a>TableAdapter の Fill メソッドを構成する

場合によっては、TableAdapter のテーブルのスキーマを変更する必要があります。 これを行うには、TableAdapter のプライマリ `Fill` メソッドを変更します。 Tableadapter は、関連付けられたデータテーブルのスキーマを定義する主な `Fill` メソッドを使用して作成されます。 プライマリ `Fill` 方法は、最初に TableAdapter を構成したときに入力したクエリまたはストアドプロシージャに基づいています。 データセットデザイナーのデータテーブルの下にある最初の (最上位の) メソッドです。

![複数のクエリがある TableAdapter](../data-tools/media/tableadapter.gif)

TableAdapter の main `Fill` メソッドに対して行った変更は、関連付けられたデータテーブルのスキーマに反映されます。 たとえば、メインの `Fill` メソッドのクエリから列を削除すると、関連付けられているデータテーブルから列も削除されます。 また、main `Fill` メソッドから列を削除すると、その TableAdapter のその他のクエリから列が削除されます。

Tableadapter クエリの構成ウィザードを使用すると、TableAdapter の追加のクエリを作成および編集できます。 これらの追加のクエリは、スカラー値を返さない限り、テーブルスキーマに準拠している必要があります。  各追加クエリには、指定した名前が付いています。

次の例は、`FillByCity`という名前の追加のクエリを呼び出す方法を示しています。

`CustomersTableAdapter.FillByCity(NorthwindDataSet.Customers, "Seattle")`

### <a name="to-start-the-tableadapter-query-configuration-wizard-with-a-new-query"></a>新しいクエリを使用して TableAdapter クエリの構成ウィザードを開始するには

1. **データセット デザイナー**でご自分のデータセットを開きます。

2. 新しいクエリを作成する場合は、**ツールボックス**の **[データセット]** タブから**クエリ**オブジェクトを <xref:System.Data.DataTable>にドラッグするか、TableAdapter のショートカットメニューから **[クエリの追加]** を選択します。 **クエリ**オブジェクトを**データセットデザイナー**の空の領域にドラッグして、関連付けられた <xref:System.Data.DataTable>を含まない TableAdapter を作成することもできます。 これらのクエリは、単一の (スカラー) 値を返すことも、データベースに対して UPDATE、INSERT、または DELETE コマンドを実行することもできます。

3. **[データ接続の選択]** 画面で、クエリが使用する接続を選択または作成します。

    > [!NOTE]
    > この画面は、デザイナーが使用する適切な接続を判断できない場合、または接続が使用できない場合にのみ表示されます。

4. **[コマンドの種類を選択]** 画面で、データベースからデータをフェッチする方法を次の中から選択します。

    - **Sql**ステートメントを使用すると、データベースからデータを選択するための sql ステートメントを入力できます。

    - **新しいストアドプロシージャを作成**すると、指定した select ステートメントに基づいて、ウィザードで新しいストアドプロシージャ (データベース内) を作成できます。

    - **既存のストアドプロシージャを使用**すると、クエリの実行時に既存のストアドプロシージャを実行できます。

### <a name="to-start-the-tableadapter-query-configuration-wizard-on-an-existing-query"></a>既存のクエリで TableAdapter クエリの構成ウィザードを起動するには

- 既存の TableAdapter クエリを編集している場合は、クエリを右クリックし、ショートカットメニューの **[構成]** をクリックします。

    > [!NOTE]
    > TableAdapter のメインクエリを右クリックすると、TableAdapter と <xref:System.Data.DataTable> スキーマが再構成されます。 ただし、TableAdapter に対して追加のクエリを右クリックすると、選択したクエリのみが構成されます。 Tableadapter の**構成ウィザード**は tableadapter の定義を再構成しますが、 **Tableadapter クエリの構成ウィザード**では、選択したクエリのみを再構成します。

### <a name="to-add-a-global-query-to-a-tableadapter"></a>TableAdapter にグローバルクエリを追加するには

- グローバルクエリは、単一の (スカラー) 値または値を返さない SQL クエリです。 通常、グローバル関数は、挿入、更新、削除などのデータベース操作を実行します。 また、テーブル内の顧客の数や特定の注文のすべての品目の合計料金などの情報も集計されます。

     グローバルクエリを追加するには、 **[ツールボックス]** の **[データセット]** タブから**データセットデザイナー**の空の領域に**クエリ**オブジェクトをドラッグします。

- `SELECT COUNT(*) AS CustomerCount FROM Customers`など、目的のタスクを実行するクエリを指定します。

    > [!NOTE]
    > **クエリ**オブジェクトを**データセットデザイナー**に直接ドラッグすると、スカラー (単一) 値のみを返すメソッドが作成されます。 選択したクエリまたはストアドプロシージャで複数の値が返される場合がありますが、ウィザードによって作成されるメソッドは、1つの値のみを返します。 たとえば、クエリは、返されたデータの最初の行の最初の列を返す場合があります。

## <a name="see-also"></a>関連項目

- [TableAdapters を使用してデータセットを入力する](../data-tools/fill-datasets-by-using-tableadapters.md)
