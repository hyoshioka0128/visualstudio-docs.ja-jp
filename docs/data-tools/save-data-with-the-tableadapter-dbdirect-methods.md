---
title: TableAdapter DBDirect メソッドを使用してデータを保存する
description: このチュートリアルでは、TableAdapter の DBDirect メソッドを使用して、データベースに対して SQL ステートメントを直接実行します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- TableAdapters, walkthroughs
- data [Visual Studio], saving
- saving data, walkthroughs
- data [Visual Studio], TableAdapter
ms.assetid: 74a6773b-37e1-4d96-a39c-63ee0abf49b1
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 5d79b2081e2d30d77ae3507884b44421f0f14bae
ms.sourcegitcommit: ed26b6e313b766c4d92764c303954e2385c6693e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/10/2020
ms.locfileid: "94434572"
---
# <a name="save-data-with-the-tableadapter-dbdirect-methods"></a>TableAdapter DBDirect メソッドを使用してデータを保存する

このチュートリアルでは、TableAdapter の DBDirect メソッドを使用してデータベースに対して SQL ステートメントを直接実行するための詳細な手順について説明します。 TableAdapter の DBDirect メソッドを使用すると、データベースの更新をきめ細かいレベルで制御できます。 これらのメソッドを使用すると、 `Insert` `Update` `Delete` ( `Update` UPDATE、INSERT、および DELETE ステートメントをすべて1回の呼び出しで実行するオーバーロードされたメソッドではなく) 個々の、、およびメソッドを呼び出すことによって、特定の SQL ステートメントおよびストアドプロシージャを実行できます。

このチュートリアルでは、次の作業を行う方法について説明します。

- 新しい **Windows フォームアプリケーション** を作成します。

- [データソース構成ウィザード](../data-tools/media/data-source-configuration-wizard.png)を使用して、データセットを作成および構成します。

- **[データ ソース]** ウィンドウから項目をドラッグしたときにフォーム上に作成されるコントロールを選択します。 詳細については、「[ [データソース] ウィンドウからドラッグしたときに作成されるコントロールを設定する](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)」を参照してください。

- **[データ ソース]** ウィンドウからフォームに項目をドラッグして、データ バインド フォームを作成します。

- データベースに直接アクセスして、挿入、更新、および削除を実行するメソッドを追加します。

## <a name="prerequisites"></a>前提条件

このチュートリアルでは SQL Server Express LocalDB と Northwind サンプルデータベースを使用します。

1. LocalDB SQL Server Express ない場合は、 [SQL Server Express ダウンロードページ](https://www.microsoft.com/sql-server/sql-server-editions-express)からインストールするか、 **Visual Studio インストーラー** を使用してインストールします。 **Visual Studio インストーラー** では、 **データストレージと処理** ワークロードの一部として SQL Server Express LocalDB をインストールすることも、個々のコンポーネントとしてインストールすることもできます。

2. 次の手順に従って、Northwind サンプルデータベースをインストールします。

    1. Visual Studio で、[ **SQL Server オブジェクトエクスプローラー** ] ウィンドウを開きます。 (SQL Server オブジェクトエクスプローラーは、Visual Studio インストーラーの **データストレージと処理** ワークロードの一部としてインストールされます)。[ **SQL Server** ] ノードを展開します。 LocalDB インスタンスを右クリックし、[ **新しいクエリ** ] をクリックします。

       クエリエディターウィンドウが開きます。

    2. [Northwind transact-sql スクリプト](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true)をクリップボードにコピーします。 この T-sql スクリプトでは、Northwind データベースを最初から作成し、データを設定します。

    3. T-sql スクリプトをクエリエディターに貼り付け、[ **実行** ] ボタンをクリックします。

       しばらくすると、クエリの実行が完了し、Northwind データベースが作成されます。

## <a name="create-a-windows-forms-application"></a>Windows フォーム アプリケーションを作成する

最初の手順では、 **Windows フォームアプリケーション** を作成します。

1. Visual Studio の **[ファイル]** メニューで､ **[新規作成]**  >  **[プロジェクト]** を選択します。

2. 左側のペインで [ **Visual C#** ] または [ **Visual Basic** を展開し、[ **Windows デスクトップ** ] を選択します。

3. 中央のウィンドウで、[ **Windows フォーム App** ] プロジェクトの種類を選択します。

4. プロジェクトに **TableAdapterDbDirectMethodsWalkthrough** という名前を入力し、[ **OK]** をクリックします。

     **TableAdapterDbDirectMethodsWalkthrough** プロジェクトが作成されて **ソリューション エクスプローラー** に追加されます。

## <a name="create-a-data-source-from-your-database"></a>データベースからデータソースを作成する

この手順では、 **データ ソース構成ウィザード** を使用して、Northwind サンプル データベースの `Region` テーブルに基づいてデータ ソースを作成します。 接続を作成するには、Northwind サンプル データベースへのアクセス権を持っている必要があります。 Northwind サンプルデータベースの設定の詳細については、「 [方法: サンプルデータベースをインストール](../data-tools/installing-database-systems-tools-and-samples.md)する」を参照してください。

### <a name="to-create-the-data-source"></a>データ ソースを作成するには

1. **[データ]** メニューで、 **[データ ソースの表示]** を選択します。

   **[データ ソース]** ウィンドウが開きます。

2. [ **データソース** ] ウィンドウで [ **新しいデータソースの追加** ] を選択して、 **データソース構成ウィザード** を開始します。

3. [ **データソースの種類を選択** ] 画面で、[ **データベース** ] を選択し、[ **次へ** ] を選択します。

4. [ **データ接続の選択** ] 画面で、次のいずれかの操作を行います。

    - Northwind サンプル データベースへのデータ接続がドロップダウン リストに表示されている場合は選択します。

         - または -

    - **[新しい接続]** を選択して **[接続の追加] または [接続の変更]** ダイアログ ボックスを表示します。

5. データベースにパスワードが必要な場合は、機密データを含めるオプションを選択し、[ **次へ** ] を選択します。

6. [ **アプリケーション構成ファイルへの接続文字列の保存** ] 画面で、[ **次へ** ] を選択します。

7. [ **データベースオブジェクトの選択** ] 画面で、[ **テーブル** ] ノードを展開します。

8. テーブルを選択し、[ `Region` **完了** ] を選択します。

     プロジェクトに **NorthwindDataSet** が追加され、 **[データ ソース]** ウィンドウに `Region` テーブルが表示されます。

## <a name="add-controls-to-the-form-to-display-the-data"></a>フォームにコントロールを追加してデータを表示する

**[データ ソース]** ウィンドウからフォームに項目をドラッグして、データ バインド コントロールを作成します。

Windows フォームにデータバインドコントロールを作成するには、[ **データソース** ] ウィンドウからフォームにメイン **領域** ノードをドラッグします。

レコード間をナビゲートするための <xref:System.Windows.Forms.DataGridView> コントロールとツール ストリップ (<xref:System.Windows.Forms.BindingNavigator>) がフォームに表示されます。 コンポーネントトレイには、 [NorthwindDataSet](../data-tools/dataset-tools-in-visual-studio.md)、、 `RegionTableAdapter` <xref:System.Windows.Forms.BindingSource> 、およびが <xref:System.Windows.Forms.BindingNavigator> 表示されます。

### <a name="to-add-buttons-that-will-call-the-individual-tableadapter-dbdirect-methods"></a>個々の TableAdapter DbDirect メソッドを呼び出すボタンを追加するには

1. **ツールボックス** から 3 つの <xref:System.Windows.Forms.Button> コントロールを **RegionDataGridView** の下の **Form1** にドラッグします。

2. 各ボタンの **[名前]** および **[テキスト]** プロパティを設定します。

    |名前|テキスト|
    |----------|----------|
    |`InsertButton`|**挿入**|
    |`UpdateButton`|**アップデート**|
    |`DeleteButton`|**削除**|

### <a name="to-add-code-to-insert-new-records-into-the-database"></a>データベースに新しいレコードを挿入するコードを追加するには

1. [ **Insertbutton** ] を選択して、クリックイベントのイベントハンドラーを作成し、コードエディターでフォームを開きます。

2. `InsertButton_Click` イベント ハンドラーを次のコードで置き換えます。

     [!code-vb[VbRaddataSaving#1](../data-tools/codesnippet/VisualBasic/save-data-with-the-tableadapter-dbdirect-methods_1.vb)]
     [!code-csharp[VbRaddataSaving#1](../data-tools/codesnippet/CSharp/save-data-with-the-tableadapter-dbdirect-methods_1.cs)]

### <a name="to-add-code-to-update-records-in-the-database"></a>データベースのレコードを更新するコードを追加するには

1. **[UpdateButton]** をダブルクリックして、クリック イベントのイベント ハンドラーを作成し、コード エディターでフォームを開きます。

2. `UpdateButton_Click` イベント ハンドラーを次のコードで置き換えます。

     [!code-vb[VbRaddataSaving#2](../data-tools/codesnippet/VisualBasic/save-data-with-the-tableadapter-dbdirect-methods_2.vb)]
     [!code-csharp[VbRaddataSaving#2](../data-tools/codesnippet/CSharp/save-data-with-the-tableadapter-dbdirect-methods_2.cs)]

### <a name="to-add-code-to-delete-records-from-the-database"></a>データベースからレコードを削除するコードを追加するには

1. [ **Deletebutton** ] を選択して、クリックイベントのイベントハンドラーを作成し、コードエディターでフォームを開きます。

2. `DeleteButton_Click` イベント ハンドラーを次のコードで置き換えます。

     [!code-vb[VbRaddataSaving#3](../data-tools/codesnippet/VisualBasic/save-data-with-the-tableadapter-dbdirect-methods_3.vb)]
     [!code-csharp[VbRaddataSaving#3](../data-tools/codesnippet/CSharp/save-data-with-the-tableadapter-dbdirect-methods_3.cs)]

## <a name="run-the-application"></a>アプリケーションの実行

- **F5 キーを押し** てアプリケーションを実行します。

- [ **挿入** ] ボタンを選択し、新しいレコードがグリッドに表示されていることを確認します。

- [ **更新** ] ボタンを選択し、グリッドでレコードが更新されていることを確認します。

- [ **削除** ] ボタンを選択し、レコードがグリッドから削除されていることを確認します。

## <a name="next-steps"></a>次のステップ

アプリケーションの要件によっては、データバインドフォームの作成後に実行する必要があるいくつかの手順があります。 このチュートリアルで行うことができる拡張には次のものがあります。

- フォームに検索機能を追加します。

- **[データ ソース]** ウィンドウの **[ウィザードで DataSet を構成]** を選択して、データセットにテーブルを追加します。 関連するコードをフォームにドラッグすることによって、関連するデータを表示するコントロールを追加できます。 詳細については、「 [データセット内のリレーションシップ](relationships-in-datasets.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [データをデータベースに保存する](../data-tools/save-data-back-to-the-database.md)
