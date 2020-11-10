---
title: コンカレンシー例外を処理する
description: 同時実行例外 (System.data.dbconcurrencyexception) を処理します。これは、2人のユーザーが同時にデータベース内の同じデータを変更しようとしたときに発生します。
ms.custom: SEO-VS-2020
ms.date: 09/11/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- concurrency control, exceptions
- datasets [Visual Basic], errors
- exception handling, concurrency issues
- data concurrency, walkthroughs
- updating datasets, errors
- concurrency control, walkthroughs
ms.assetid: 73ee9759-0a90-48a9-bf7b-9d6fc17bff93
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 5fcd8bb06cf9c88466b4dfa3cfaf2dfd8093bd3d
ms.sourcegitcommit: ed26b6e313b766c4d92764c303954e2385c6693e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/10/2020
ms.locfileid: "94436447"
---
# <a name="handle-a-concurrency-exception"></a>コンカレンシー例外を処理する

2 人のユーザーが同じデータベースの同じデータを同時に変更しようとすると、コンカレンシー例外 (<xref:System.Data.DBConcurrencyException?displayProperty=fullName>) が発生します。 このチュートリアルでは、をキャッチする方法、 <xref:System.Data.DBConcurrencyException> エラーの原因となった行を特定する方法、およびその処理方法の方法を説明する Windows アプリケーションを作成します。

ここでは次の手順を実行します。

1. 新しい **Windows フォームアプリケーション** プロジェクトを作成します。

2. Northwind の Customers テーブルに基づいて新しいデータセットを作成します。

3. データを表示する <xref:System.Windows.Forms.DataGridView> を備えたフォームを作成します。

4. Northwind データベースの Customers テーブルのデータをデータセットに格納します。

5. **サーバーエクスプローラー** の [ **テーブルデータの表示]** 機能を使用して、Customers テーブルのデータにアクセスし、レコードを変更します。

6. 同じレコードを別の値に変更し、データセットを更新して、データベースへの変更の書き込みを試行します。これにより、同時実行エラーが発生します。

7. エラーをキャッチし、操作を継続してデータベースを更新するか、または更新をキャンセルするかを判断できるように、レコードの異なるバージョンを表示します。

## <a name="prerequisites"></a>前提条件

このチュートリアルでは SQL Server Express LocalDB と Northwind サンプルデータベースを使用します。

1. LocalDB SQL Server Express ない場合は、 [SQL Server Express ダウンロードページ](https://www.microsoft.com/sql-server/sql-server-editions-express)からインストールするか、 **Visual Studio インストーラー** を使用してインストールします。 **Visual Studio インストーラー** では、 **データストレージと処理** ワークロードの一部として SQL Server Express LocalDB をインストールすることも、個々のコンポーネントとしてインストールすることもできます。

2. 次の手順に従って、Northwind サンプルデータベースをインストールします。

    1. Visual Studio で、[ **SQL Server オブジェクトエクスプローラー** ] ウィンドウを開きます。 (SQL Server オブジェクトエクスプローラーは、Visual Studio インストーラーの **データストレージと処理** ワークロードの一部としてインストールされます)。[ **SQL Server** ] ノードを展開します。 LocalDB インスタンスを右クリックし、[ **新しいクエリ** ] をクリックします。

       クエリエディターウィンドウが開きます。

    2. [Northwind transact-sql スクリプト](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true)をクリップボードにコピーします。 この T-sql スクリプトでは、Northwind データベースを最初から作成し、データを設定します。

    3. T-sql スクリプトをクエリエディターに貼り付け、[ **実行** ] ボタンをクリックします。

       しばらくすると、クエリの実行が完了し、Northwind データベースが作成されます。

## <a name="create-a-new-project"></a>新しいプロジェクトを作成する

まず、新しい Windows フォームアプリケーションを作成します。

1. Visual Studio の **[ファイル]** メニューで､ **[新規作成]**  >  **[プロジェクト]** を選択します。

2. 左側のペインで [ **Visual C#** ] または [ **Visual Basic** を展開し、[ **Windows デスクトップ** ] を選択します。

3. 中央のウィンドウで、[ **Windows フォーム App** ] プロジェクトの種類を選択します。

4. プロジェクトに **ConcurrencyWalkthrough** という名前を入力し、[ **OK]** をクリックします。

     **ConcurrencyWalkthrough** プロジェクトが作成され **ソリューションエクスプローラー** に追加され、デザイナーで新しいフォームが開きます。

## <a name="create-the-northwind-dataset"></a>Northwind データセットの作成

次に、 **NorthwindDataSet** という名前のデータセットを作成します。

1. [ **データ** ] メニューの [ **新しいデータソースの追加** ] をクリックします。

   データ ソース構成ウィザードが開きます。

2. [ **データソースの種類を選択** ] 画面で、[ **データベース** ] を選択します。

   ![Visual Studio のデータソース構成ウィザード](media/data-source-configuration-wizard.png)

3. 使用可能な接続の一覧から、Northwind サンプルデータベースへの接続を選択します。 接続の一覧で接続が使用できない場合は、[ **新しい接続** ] を選択します。

    > [!NOTE]
    > ローカルデータベースファイルに接続している場合は、ファイルをプロジェクトに追加するかどうかを確認するメッセージが表示されたら、[ **いいえ** ] を選択します。

4. [ **アプリケーション構成ファイルへの接続文字列の保存** ] 画面で、[ **次へ** ] を選択します。

5. [ **テーブル** ] ノードを展開し、[ **Customers** ] テーブルを選択します。 データセットの既定の名前は **NorthwindDataSet** である必要があります。

6. [ **完了** ] を選択して、データセットをプロジェクトに追加します。

## <a name="create-a-data-bound-datagridview-control"></a>データバインド DataGridView コントロールを作成する

このセクションでは、 <xref:System.Windows.Forms.DataGridView?displayProperty=nameWithType> [ **データソース** ] ウィンドウから Windows フォームに **Customers** 項目をドラッグして、を作成します。

1. [データ **ソース** ] ウィンドウを開くには、[ **データ** ] メニューの [ **データソースの表示** ] をクリックします。

2. [ **データソース** ] ウィンドウで、[ **NorthwindDataSet** ] ノードを展開し、[ **Customers** ] テーブルを選択します。

3. テーブルノードの下矢印を選択し、ドロップダウンリストで [ **DataGridView** ] を選択します。

4. テーブルをフォームの空の領域にドラッグします。

     <xref:System.Windows.Forms.DataGridView>「」と **CustomersDataGridView** いう名前のコントロールが <xref:System.Windows.Forms.BindingNavigator> 、にバインドされているフォームに追加され **CustomersBindingNavigator** <xref:System.Windows.Forms.BindingSource> ます。 次に、NorthwindDataSet の Customers テーブルにバインドされます。

## <a name="test-the-form"></a>フォームをテストする

フォームをテストして、ここまでの設定が期待どおりに動作することを確認します。

1. **F5 キーを押し** てアプリケーションを実行します。

     フォームには、 <xref:System.Windows.Forms.DataGridView> Customers テーブルのデータを格納したコントロールが表示されます。

2. **[デバッグ]** メニューの **[デバッグの停止]** を選択します。

## <a name="handle-concurrency-errors"></a>同時実行エラーの処理

エラーの処理方法は、アプリケーションを管理する特定のビジネスルールによって異なります。 このチュートリアルでは、同時実行エラーを処理する方法の例として、次の方法を使用します。

アプリケーションは、次の3つのバージョンのレコードをユーザーに提示します。

- データベース内の現在のレコード

- データセットに読み込まれた元のレコード

- データセット内の提案された変更

ユーザーは、提案されたバージョンでデータベースを上書きするか、更新をキャンセルし、データベースから新しい値をデータセットに再読み込むことができます。

### <a name="to-enable-the-handling-of-concurrency-errors"></a>コンカレンシー エラーを処理できるようにするには

1. カスタム エラー ハンドラーの作成

2. ユーザーに対する選択肢の表示

3. ユーザーの応答の処理

4. 更新の再送、またはデータセット内のデータのリセット

### <a name="add-code-to-handle-the-concurrency-exception"></a>同時実行例外を処理するコードを追加する

更新を実行しようとしたときに例外が発生した場合、通常は、発生した例外によって提供された情報を使用して何らかの処理を行います。 このセクションでは、データベースの更新を試みるコードを追加します。 また <xref:System.Data.DBConcurrencyException> 、発生する可能性があるものや、その他の例外も処理します。

> [!NOTE]
> `CreateMessage`メソッドと `ProcessDialogResults` メソッドは、このチュートリアルの後半で追加します。

1. `Form1_Load` メソッドの下に次のコードを追加します。

   [!code-csharp[VbRaddataConcurrency#1](../data-tools/codesnippet/CSharp/handle-a-concurrency-exception_1.cs)]
   [!code-vb[VbRaddataConcurrency#1](../data-tools/codesnippet/VisualBasic/handle-a-concurrency-exception_1.vb)]

2. 次のように `CustomersBindingNavigatorSaveItem_Click` メソッドを `UpdateDatabase` メソッドの呼び出しに置き換えます。

   [!code-csharp[VbRaddataConcurrency#2](../data-tools/codesnippet/CSharp/handle-a-concurrency-exception_2.cs)]
   [!code-vb[VbRaddataConcurrency#2](../data-tools/codesnippet/VisualBasic/handle-a-concurrency-exception_2.vb)]

### <a name="display-choices-to-the-user"></a>ユーザーに対する選択肢の表示

上のコードにより `CreateMessage` プロシージャが呼び出され、ユーザーにエラー情報が表示されます。 このチュートリアルでは、メッセージボックスを使用して、レコードのさまざまなバージョンをユーザーに表示します。 これにより、ユーザーは、レコードを変更で上書きするか、編集をキャンセルするかを選択できます。 ユーザーがメッセージ ボックスのオプションを選択する (ボタンをクリックする) と、`ProcessDialogResult` メソッドに応答が渡されます。

**コード エディター** に次のコードを追加して、メッセージを作成します。 このコードは、`UpdateDatabase` メソッドの下に入力します。

[!code-csharp[VbRaddataConcurrency#4](../data-tools/codesnippet/CSharp/handle-a-concurrency-exception_3.cs)]
[!code-vb[VbRaddataConcurrency#4](../data-tools/codesnippet/VisualBasic/handle-a-concurrency-exception_3.vb)]

### <a name="process-the-users-response"></a>ユーザーの応答の処理

また、メッセージボックスに対するユーザーの応答を処理するコードも必要です。 オプションは、データベース内の現在のレコードを提案された変更で上書きするか、ローカルの変更を破棄し、現在データベース内にあるレコードを使用してデータテーブルを更新するかのどちらかです。 ユーザーが **[はい]** を選択すると、 <xref:System.Data.DataTable.Merge%2A> メソッドが呼び出され、 *preserveChanges* 引数が **true** に設定されます。 これにより、レコードの元のバージョンがデータベース内のレコードと一致するようになったため、更新が成功します。

前のセクションで追加したコードの下に次のコードを追加します。

[!code-csharp[VbRaddataConcurrency#3](../data-tools/codesnippet/CSharp/handle-a-concurrency-exception_4.cs)]
[!code-vb[VbRaddataConcurrency#3](../data-tools/codesnippet/VisualBasic/handle-a-concurrency-exception_4.vb)]

## <a name="test-the-form-behavior"></a>フォームの動作をテストする

フォームをテストして、期待どおりに動作することを確認します。 同時実行違反をシミュレートするには、NorthwindDataSet にデータを入力した後にデータベース内のデータを変更します。

1. **F5 キーを押し** てアプリケーションを実行します。

2. フォームが表示されたら、実行を継続したまま Visual Studio IDE に切り替えます。

3. **[表示]** メニューの **[サーバー エクスプローラー]** を選択します。

4. **サーバー エクスプローラー** で、アプリケーションで使用する接続を展開し、次に **[テーブル]** ノードを展開します。

5. **Customers** テーブルを右クリックし、[ **テーブルデータの表示** ] をクリックします。

6. 最初のレコード ( **ALFKI** ) で、[ **担当の担当** ] を [ **マリア Anders2** ] に変更します。

    > [!NOTE]
    > 別の行に移動し、変更をコミットします。

7. ConcurrencyWalkthrough の実行フォームに切り替えます。

8. フォーム ( **ALFKI** ) の最初のレコードで、[担当 **の担当** ] を [ **Anders1** ] に変更します。

9. **[保存]** ボタンを選択します。

     コンカレンシー エラーが発生し、メッセージ ボックスが表示されます。

   [ **いいえ** ] を選択すると、更新がキャンセルされ、現在データベース内にある値によってデータセットが更新されます。 **[はい]** を選択すると、提示された値がデータベースに書き込まれます。

## <a name="see-also"></a>関連項目

- [データをデータベースに保存する](../data-tools/save-data-back-to-the-database.md)
