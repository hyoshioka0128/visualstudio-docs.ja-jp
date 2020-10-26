---
title: フォーム間でデータを渡す
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- walkthroughs [Windows Forms], data
- walkthroughs [Visual Studio], data
- data [Visual Studio], passing between forms
- forms, passing data between
- Windows Forms, walkthroughs
ms.assetid: 78bf038b-9296-4fbf-b0e8-d881d1aff0df
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 198eb09cabe16c72415520aa493a3395cdbf6d48
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85281878"
---
# <a name="pass-data-between-forms"></a>フォーム間でデータを渡す

このチュートリアルでは、フォーム間でデータを渡す手順について説明します。 Northwind の customers テーブルと orders テーブルを使用すると、1つのフォームで顧客を選択できます。2番目のフォームでは、選択した顧客の注文が表示されます。 このチュートリアルでは、最初のフォームからデータを受け取る2番目のフォームでメソッドを作成する方法について説明します。

> [!NOTE]
> このチュートリアルでは、フォーム間でデータを渡す 1 つの方法についてのみ説明します。 データを受信するための2番目のコンストラクターの作成や、最初のフォームのデータを使用して設定できるパブリックプロパティの作成など、データをフォームに渡すためのオプションは他にもあります。

このチュートリアルでは、以下のタスクを行います。

- 新しい **Windows フォーム アプリケーション** プロジェクトを作成します。

- [データソース構成ウィザード](../data-tools/media/data-source-configuration-wizard.png)を使用したデータセットの作成と構成

- **[データ ソース]** ウィンドウから項目をドラッグしたときにフォーム上に作成するコントロールを選択します。 詳細については、「[ [データソース] ウィンドウからドラッグしたときに作成されるコントロールを設定する](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)」を参照してください。

- **[データ ソース]** ウィンドウからフォームに項目をドラッグして、データ バインド コントロールを作成します。

- データを表示するグリッドのある 2 番目のフォームを作成します。

- 特定の顧客の注文をフェッチする TableAdapter クエリを作成します。

- フォーム間でデータを渡します。

## <a name="prerequisites"></a>前提条件

このチュートリアルでは SQL Server Express LocalDB と Northwind サンプルデータベースを使用します。

1. LocalDB SQL Server Express ない場合は、 [SQL Server Express ダウンロードページ](https://www.microsoft.com/sql-server/sql-server-editions-express)からインストールするか、 **Visual Studio インストーラー**を使用してインストールします。 Visual Studio インストーラーでは、SQL Server Express LocalDB は、 **データストレージと処理** ワークロードの一部として、または個々のコンポーネントとしてインストールできます。

2. 次の手順に従って、Northwind サンプルデータベースをインストールします。

    1. Visual Studio で、[ **SQL Server オブジェクトエクスプローラー** ] ウィンドウを開きます。 (SQL Server オブジェクトエクスプローラーは、Visual Studio インストーラーの **データストレージと処理** ワークロードの一部としてインストールされます)。[ **SQL Server** ] ノードを展開します。 LocalDB インスタンスを右クリックし、[ **新しいクエリ**] をクリックします。

       クエリエディターウィンドウが開きます。

    2. [Northwind transact-sql スクリプト](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true)をクリップボードにコピーします。 この T-sql スクリプトでは、Northwind データベースを最初から作成し、データを設定します。

    3. T-sql スクリプトをクエリエディターに貼り付け、[ **実行** ] ボタンをクリックします。

       しばらくすると、クエリの実行が完了し、Northwind データベースが作成されます。

## <a name="create-the-windows-forms-app-project"></a>Windows フォームアプリプロジェクトを作成する

1. Visual Studio の **[ファイル]** メニューで､ **[新規作成]**  >  **[プロジェクト]** を選択します。

2. 左側のペインで [ **Visual C#** ] または [ **Visual Basic** を展開し、[ **Windows デスクトップ**] を選択します。

3. 中央のウィンドウで、[ **Windows フォーム App** ] プロジェクトの種類を選択します。

4. プロジェクトに「」という名前を入力し、[ **OK]****をクリック**します。

     **PassingDataBetweenForms** プロジェクトが作成され、**ソリューション エクスプローラー**に追加されます。

## <a name="create-the-data-source"></a>データソースを作成する

1. [データ **ソース** ] ウィンドウを開くには、[ **データ** ] メニューの [ **データソースの表示**] をクリックします。

2. **[データ ソース]** ウィンドウで、**[新しいデータ ソースの追加]** をクリックして**データ ソース構成**ウィザードを起動します。

3. **[データソースの種類を選択]** ページで、 **[データベース]** をクリックし、 **[次へ]** をクリックします。

4. **[データベース モデルの選択]** ページで、**[データセット]** が指定されていることを確認し、**[次へ]** をクリックします。

5. [ **データ接続の選択** ] ページで、次のいずれかの操作を行います。

    - Northwind サンプル データベースへのデータ接続がドロップダウン リストに表示されている場合は選択します。

    - **[新しい接続]** を選択して **[接続の追加] または [接続の変更]** ダイアログ ボックスを表示します。

6. データベースにパスワードが必要であり、重要情報を含めるオプションを有効にする場合は、このオプションを選択し、**[次へ]** をクリックします。

7. **[アプリケーション構成ファイルに接続文字列を保存]** ページで、**[次へ]** をクリックします。

8. **[データベース オブジェクトの選択]** ページで、**[テーブル]** ノードを展開します。

9. **Customers** テーブルと **Orders** テーブルを選択し、**[完了]** をクリックします。

     プロジェクトに **NorthwindDataSet** が追加され、**[データ ソース]** ウィンドウに **Customers** テーブルと **Orders** テーブルが表示されます。

## <a name="create-the-first-form-form1"></a>最初のフォームを作成する (Form1)

**[データ ソース]** ウィンドウから **Customers** ノードをフォームにドラッグして、データ バインド グリッド (<xref:System.Windows.Forms.DataGridView> コントロール) を作成します。

### <a name="to-create-a-data-bound-grid-on-the-form"></a>フォームにデータ バインド グリッドを作成するには

- **[データ ソース]** ウィンドウから **Form1** にメインの **[Customers]** ノードをドラッグします。

     <xref:System.Windows.Forms.DataGridView> と、レコード間を移動するためのツール ストリップ (<xref:System.Windows.Forms.BindingNavigator>) が **Form1** 上に表示されます。 [NorthwindDataSet](../data-tools/dataset-tools-in-visual-studio.md)、CustomersTableAdapter、<xref:System.Windows.Forms.BindingSource>、<xref:System.Windows.Forms.BindingNavigator> がコンポーネント トレイに表示されます。

## <a name="create-the-second-form"></a>2番目のフォームを作成する

データを渡す2番目のフォームを作成します。

1. **[プロジェクト]** メニューの **[Windows フォームの追加]** を選択します。

2. 名前を既定の **Form2** のままにして、**[追加]** をクリックします。

3. **[データ ソース]** ウィンドウから **Form2** にメインの **[Orders]** ノードをドラッグします。

     <xref:System.Windows.Forms.DataGridView> と、レコード間を移動するためのツール ストリップ (<xref:System.Windows.Forms.BindingNavigator>) が **Form2** 上に表示されます。 [NorthwindDataSet](../data-tools/dataset-tools-in-visual-studio.md)、CustomersTableAdapter、<xref:System.Windows.Forms.BindingSource>、<xref:System.Windows.Forms.BindingNavigator> がコンポーネント トレイに表示されます。

4. コンポーネント トレイから **OrdersBindingNavigator** を削除します。

     **Form2** から **OrdersBindingNavigator** が消えます。

## <a name="add-a-tableadapter-query"></a>TableAdapter クエリの追加

Form1 に、選択した顧客の注文を読み込む TableAdapter クエリを Form2 に追加します。

1. **ソリューション エクスプローラー**で、**NorthwindDataSet.xsd** ファイルをダブルクリックします。

2. **[OrdersTableAdapter]** を右クリックし、**[クエリの追加]** を選択します。

3. **[SQL ステートメントを使用する]** を既定のオプションのままにして、**[次へ]** をクリックします。

4. **[複数行を返す SELECT]** を既定のオプションのままにして、**[次へ]** をクリックします。

5. `CustomerID` に基づいて `Orders` を返すために、クエリに WHERE 句を追加します。 クエリは次のようになります。

    ```sql
    SELECT OrderID, CustomerID, EmployeeID, OrderDate, RequiredDate, ShippedDate, ShipVia, Freight, ShipName, ShipAddress, ShipCity, ShipRegion, ShipPostalCode, ShipCountry
    FROM Orders
    WHERE CustomerID = @CustomerID
    ```

    > [!NOTE]
    > データベースに対してパラメーターの構文が正しいことを確認します。 たとえば、Microsoft Access では、WHERE 句は `WHERE CustomerID = ?` のようになります。

6. **[次へ]** をクリックします。

7. [ **DataTableMethod 名を**入力してください] に、「」と入力 `FillByCustomerID` します。

8. **[DataTable を返す]** オプションをオフにして、**[次へ]** をクリックします。

9. **[完了]** をクリックします。

## <a name="create-a-method-on-form2-to-pass-data-to"></a>Form2 にデータを渡すメソッドを作成します。

1. **Form2** を右クリックし、**[コードの表示]** を選択して**コード エディター**で **Form2** を開きます。

2. **Form2** の `Form2_Load` メソッドの後に次のコードを追加します。

     [!code-vb[VbRaddataDisplaying#1](../data-tools/codesnippet/VisualBasic/pass-data-between-forms_1.vb)]
     [!code-csharp[VbRaddataDisplaying#1](../data-tools/codesnippet/CSharp/pass-data-between-forms_1.cs)]

## <a name="create-a-method-on-form1-to-pass-data-and-display-form2"></a>Form1 にデータを渡して Form2 を表示するメソッドを作成する

1. **Form1** の Customer データ グリッドを右クリックし、**[プロパティ]** をクリックします。

2. **[プロパティ]** ウィンドウで、**[イベント]** をクリックします。

3. **CellDoubleClick** イベントをダブルクリックします。

     コード エディターが表示されます。

4. メソッド定義を次のサンプルのように更新します。

     [!code-csharp[VbRaddataDisplaying#2](../data-tools/codesnippet/CSharp/pass-data-between-forms_2.cs)]
     [!code-vb[VbRaddataDisplaying#2](../data-tools/codesnippet/VisualBasic/pass-data-between-forms_2.vb)]

## <a name="run-the-app"></a>アプリを実行する

- **F5** キーを押してアプリケーションを実行します。

- **Form1** で顧客レコードをダブルクリックして、その顧客の注文を表示する **Form2** を開きます。

## <a name="next-steps"></a>次のステップ

フォーム間でデータを渡した後に、アプリケーションの要件に応じてさらに操作を追加して実行できます。 このチュートリアルで行うことができる拡張には次のものがあります。

- データセットを編集し、データベース オブジェクトの追加または削除を行います。 詳細については、「 [データセットの作成と構成](../data-tools/create-and-configure-datasets-in-visual-studio.md)」を参照してください。

- データベースにデータを戻して保存する機能を追加します。 詳細については、「 [データベースにデータを保存する](../data-tools/save-data-back-to-the-database.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [Visual Studio でのデータへの Windows フォーム コントロールのバインド](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
