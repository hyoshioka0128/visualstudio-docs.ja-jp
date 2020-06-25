---
title: データベースへのデータの保存 (複数テーブル)
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- updating datasets, walkthroughs
- data [Visual Studio], saving
- saving data, walkthroughs
- data [Visual Studio], updating
ms.assetid: 7ebe03da-ce8c-4cbc-bac0-a2fde4ae4d07
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: b512263cd5d0ca8c83b0ba6848fb16feca1a71f6
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85281644"
---
# <a name="save-data-to-a-database-multiple-tables"></a>データベースへのデータの保存 (複数テーブル)

アプリケーション開発における最も一般的なシナリオの 1 つに、Windows アプリケーションのフォームにデータを表示して編集し、更新したデータをデータベースに返送する操作があります。 このチュートリアルでは、2 つの関連するテーブルのデータを表示するフォームを作成し、レコードを編集して変更内容をデータベースに保存する方法を示します。 この例では、Northwind サンプル データベースの `Customers` テーブルと `Orders` テーブルを使用します。

アプリケーション内のデータをデータベースに保存するには、TableAdapter の `Update` メソッドを呼び出します。 [**データソース**] ウィンドウからフォームにテーブルをドラッグすると、データを保存するために必要なコードが自動的に追加されます。 フォームに追加されるテーブルでは、このコードを手動で追加する必要があります。 ここでは、複数のテーブルから更新を保存するコードを追加する手順を示します。

このチュートリアルでは、以下のタスクを行います。

- [データソース構成ウィザード](../data-tools/media/data-source-configuration-wizard.png)を使用して、アプリケーションでのデータソースの作成と構成を行います。

- [[データソース] ウィンドウ](add-new-data-sources.md#data-sources-window)の項目のコントロールを設定します。 詳細については、「[[データソース] ウィンドウからドラッグしたときに作成されるコントロールを設定する](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)」を参照してください。

- **[データ ソース]** ウィンドウからフォームに項目をドラッグして、データ バインド コントロールを作成します。

- データセット内の各テーブルのいくつかのレコードを変更する。

- データセット内の更新されたデータをデータベースに返送するコードを変更します。

## <a name="prerequisites"></a>必須コンポーネント

このチュートリアルでは SQL Server Express LocalDB と Northwind サンプルデータベースを使用します。

1. LocalDB SQL Server Express ない場合は、 [SQL Server Express ダウンロードページ](https://www.microsoft.com/sql-server/sql-server-editions-express)からインストールするか、 **Visual Studio インストーラー**を使用してインストールします。 **Visual Studio インストーラー**では、**データストレージと処理**ワークロードの一部として SQL Server Express LocalDB をインストールすることも、個々のコンポーネントとしてインストールすることもできます。

2. 次の手順に従って、Northwind サンプルデータベースをインストールします。

    1. Visual Studio で、[ **SQL Server オブジェクトエクスプローラー** ] ウィンドウを開きます。 (SQL Server オブジェクトエクスプローラーは、Visual Studio インストーラーの**データストレージと処理**ワークロードの一部としてインストールされます)。[ **SQL Server** ] ノードを展開します。 LocalDB インスタンスを右クリックし、[**新しいクエリ**] をクリックします。

       クエリエディターウィンドウが開きます。

    2. [Northwind transact-sql スクリプト](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true)をクリップボードにコピーします。 この T-sql スクリプトでは、Northwind データベースを最初から作成し、データを設定します。

    3. T-sql スクリプトをクエリエディターに貼り付け、[**実行**] ボタンをクリックします。

       しばらくすると、クエリの実行が完了し、Northwind データベースが作成されます。

## <a name="create-the-windows-forms-application"></a>Windows フォームアプリケーションを作成する

C# または Visual Basic 用の新しい**Windows フォームアプリ**プロジェクトを作成します。 プロジェクトに **UpdateMultipleTablesWalkthrough** という名前を付けます。

## <a name="create-the-data-source"></a>データソースを作成する

この手順では、**データ ソース構成ウィザード**を使用して、Northwind データベースからデータ ソースを作成します。 接続を作成するには、Northwind サンプル データベースへのアクセス権を持っている必要があります。 Northwind サンプルデータベースの設定の詳細については、「[方法: サンプルデータベースをインストール](../data-tools/installing-database-systems-tools-and-samples.md)する」を参照してください。

1. [**データ**] メニューの [**データソースの表示**] をクリックします。

   **[データ ソース]** ウィンドウが開きます。

2. [**データソース**] ウィンドウで [**新しいデータソースの追加**] を選択して、**データソース構成ウィザード**を開始します。

3. [**データソースの種類を選択**] 画面で、[**データベース**] を選択し、[**次へ**] を選択します。

4. [**データ接続の選択**] 画面で、次のいずれかの操作を行います。

    - Northwind サンプル データベースへのデータ接続がドロップダウン リストに表示されている場合は選択します。

         \- または -

    - **[新しい接続]** を選択して **[接続の追加] または [接続の変更]** ダイアログ ボックスを開きます。

5. データベースにパスワードが必要な場合は、機密データを含めるオプションを選択し、[**次へ**] を選択します。

6. [**接続文字列をアプリケーション構成ファイルに保存する**] で、[**次へ**] を選択します。

7. [**データベースオブジェクトの選択**] 画面で、[**テーブル**] ノードを展開します。

8. **Customers**テーブルと**Orders**テーブルを選択し、[**完了**] を選択します。

     自分のプロジェクトに **NorthwindDataSet** が追加され、**[データ ソース]** ウィンドウにテーブルが表示されます。

## <a name="set-the-controls-to-be-created"></a>作成するコントロールを設定する

このチュートリアルでは、テーブル内のデータは、 `Customers` 個々のコントロールにデータが表示される**詳細**レイアウトに含まれています。 テーブルのデータ `Orders` は、コントロールに表示される**グリッド**レイアウトに含まれてい <xref:System.Windows.Forms.DataGridView> ます。

### <a name="to-set-the-drop-type-for-the-items-in-the-data-sources-window"></a>[データ ソース] ウィンドウの項目にドロップ タイプを設定するには

1. [**データソース**] ウィンドウで、[ **Customers** ] ノードを展開します。

2. [ **Customers** ] ノードで、コントロールリストの [**詳細**] を選択して、 **customers**テーブルのコントロールを個々のコントロールに変更します。 詳細については、「[[データソース] ウィンドウからドラッグしたときに作成されるコントロールを設定する](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)」を参照してください。

## <a name="create-the-data-bound-form"></a>データバインドフォームを作成する

データバインドコントロールを作成するには、[**データソース**] ウィンドウからフォームに項目をドラッグします。

1. **[データ ソース]** ウィンドウから **Form1** にメインの **[Customers]** ノードをドラッグします。

     説明のラベルが付いたデータ バインド コントロールとレコード間を移動するためのツール ストリップ (<xref:System.Windows.Forms.BindingNavigator>) がフォームに表示されます。 コンポーネントトレイには、 [NorthwindDataSet](../data-tools/dataset-tools-in-visual-studio.md)、、 `CustomersTableAdapter` <xref:System.Windows.Forms.BindingSource> 、およびが <xref:System.Windows.Forms.BindingNavigator> 表示されます。

2. **[データ ソース]** ウィンドウから **Form1** に関連する **[Orders]** ノードをドラッグします。

    > [!NOTE]
    > 関連する **[Orders]** ノードは **[Fax]** 列の下にあり、**[Customers]** ノードの子ノードです。

     レコード間をナビゲートするための <xref:System.Windows.Forms.DataGridView> コントロールとツール ストリップ (<xref:System.Windows.Forms.BindingNavigator>) がフォームに表示されます。 `OrdersTableAdapter`とが <xref:System.Windows.Forms.BindingSource> コンポーネントトレイに表示されます。

## <a name="add-code-to-update-the-database"></a>データベースを更新するコードを追加する

**Customers** TableAdapter および **Orders** TableAdapter の `Update` メソッドを呼び出して、データベースを更新できます。 既定では、データベースに更新を送信するために、の [**保存**] ボタンのイベントハンドラー <xref:System.Windows.Forms.BindingNavigator> がフォームのコードに追加されます。 この手順では、更新プログラムを正しい順序で送信するようにコードを変更します。これにより、参照整合性エラーが発生する可能性がなくなります。 また、Update 呼び出しを try-catch ブロックにラップして、エラー処理も実装します。 アプリケーションの要件に適合するようにコードを変更できます。

> [!NOTE]
> わかりやすくするために、このチュートリアルではトランザクションを使用しません。 ただし、2つ以上の関連テーブルを更新する場合は、すべての更新ロジックをトランザクション内に含めます。 トランザクションとは、変更がコミットされる前に、データベースに関連するすべての変更が正常に行われることを保証するプロセスです。 詳しくは、「[トランザクションとコンカレンシー](/dotnet/framework/data/adonet/transactions-and-concurrency)」をご覧ください。

### <a name="to-add-update-logic-to-the-application"></a>アプリケーションに更新ロジックを追加するには

1. の [**保存**] ボタンを選択し <xref:System.Windows.Forms.BindingNavigator> ます。 これにより、コードエディターが開き、イベントハンドラーが表示され `bindingNavigatorSaveItem_Click` ます。

2. イベント ハンドラーのコードを、関連する TableAdapter の `Update` メソッドを呼び出すコードに置き換えます。 次のコードは、最初に、各 <xref:System.Data.DataRowState> (<xref:System.Data.DataRowState.Deleted>、<xref:System.Data.DataRowState.Added>、および <xref:System.Data.DataRowState.Modified>) の更新済み情報を保持する 3 つの一時的なデータ テーブルを作成します。 更新プログラムは正しい順序で実行されます。 コードは、次のようになります。

     [!code-vb[VbRaddataSaving#10](../data-tools/codesnippet/VisualBasic/save-data-to-a-database-multiple-tables_1.vb)]
     [!code-csharp[VbRaddataSaving#10](../data-tools/codesnippet/CSharp/save-data-to-a-database-multiple-tables_1.cs)]

## <a name="test-the-application"></a>アプリケーションをテストする

1. **F5**キーを押します。

2. 各テーブルの 1 つ以上のレコードのデータを変更します。

3. **[保存]** を選択します。

4. データベースの値をチェックし、変更が保存されたことを確認します。

## <a name="see-also"></a>関連項目

- [データをデータベースに保存する](../data-tools/save-data-back-to-the-database.md)
