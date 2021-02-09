---
title: ADO.NET を使用した単純なデータ アプリケーションの作成
description: Visual Studio で Windows フォームと ADO.NET を使用して、簡単なフォーム対データアプリケーションを作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 08/23/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
ms.assetid: 2222841f-e443-4a3d-8c70-4506aa905193
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: 71e6c03c4ed0319b45c5b6ef0b79f65abbfc9f73
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99867192"
---
# <a name="create-a-simple-data-application-by-using-adonet"></a>ADO.NET を使用した単純なデータ アプリケーションの作成

データベースのデータを処理するアプリケーションの作成では、接続文字列の定義、データの挿入、ストアド プロシージャの実行などの基本的なタスクを実行します。 このトピックでは、Visual C# または Visual Basic と ADO.NET を使用して、単純な Windows フォーム "フォームオーバーデータ" アプリケーション内からデータベースと対話する方法について説明します。  データセット、LINQ to SQL、Entity Framework を含むすべての .NET データテクノロジは、最終的にこの記事に記載されている手順とよく似た手順を実行します。

この記事では、迅速な方法でデータベースからデータを取得する簡単な方法を示します。 アプリケーションで単純な方法でデータを変更し、データベースを更新する必要がある場合は、Entity Framework を使用し、データバインディングを使用して、基になるデータの変更にユーザーインターフェイスコントロールを自動的に同期することを検討してください。

> [!IMPORTANT]
> コードをシンプルにするため、運用環境で使用する例外処理は含まれていません。

## <a name="prerequisites"></a>前提条件

アプリケーションの作成には、次が必要です:

- 見ることができます。

- SQL Server Express LocalDB。 SQL Server Express LocalDB をお持ちでない場合は、 [SQL Server Express ダウンロードページ](https://www.microsoft.com/sql-server/sql-server-editions-express)からインストールできます。

このトピックでは、Visual Studio IDE の基本的な機能について理解していること、Windows フォームアプリケーションを作成する方法、プロジェクトにフォームを追加する方法、フォームにボタンやその他のコントロールを配置する方法、コントロールのプロパティを設定する方法、およびコード単純なイベントを使用する方法について説明します。 これらのタスクに慣れていない場合は、このチュートリアルを開始する前に、「 [Visual C# の概要と Visual Basic](../ide/quickstart-visual-basic-console.md) 」のトピックを完了することをお勧めします。

## <a name="set-up-the-sample-database"></a>サンプル データベースを設定する

次の手順に従って、サンプルデータベースを作成します。

1. Visual Studio で、[ **サーバーエクスプローラー** ] ウィンドウを開きます。

2. [ **データ接続** ] を右クリックし、[ **新しい SQL Server データベースの作成**] を選択します。

3. [ **サーバー名** ] ボックスに「 **(localdb) \mssqllocaldb**」と入力します。

4. [ **新しいデータベース名** ] ボックスに「 **Sales**」と入力し、[ **OK]** を選択します。

     空の **Sales** データベースが作成され、サーバーエクスプローラーの [データ接続] ノードに追加されます。

5. **Sales** data 接続を右クリックし、[**新しいクエリ**] を選択します。

     クエリエディターウィンドウが開きます。

6. [Sales transact-sql スクリプト](https://github.com/MicrosoftDocs/visualstudio-docs/raw/master/docs/data-tools/samples/sales.sql)をクリップボードにコピーします。

7. T-sql スクリプトをクエリエディターに貼り付け、[ **実行** ] ボタンをクリックします。

     しばらくすると、クエリの実行が完了し、データベースオブジェクトが作成されます。 データベースには、Customer と Orders という2つのテーブルが含まれています。 これらのテーブルにはデータが含まれていませんが、作成するアプリケーションを実行するときにデータを追加できます。 データベースには、4つの単純なストアドプロシージャも含まれています。

## <a name="create-the-forms-and-add-controls"></a>フォームを作成してコントロールを追加する

1. Windows フォーム アプリケーションのプロジェクトを作成し、**SimpleDataApp** という名前を付けます。

    Visual Studio は、**Form1** という名前の空の Windows フォームを含めた、いくつかのファイルとプロジェクトを作成します。

2. 2 つの Windows フォームをプロジェクトに追加し、合計 3 つのフォームに次の名前を付けます。

   - **ナビゲーション**

   - **NewCustomer**

   - **FillOrCancel**

3. 各フォームに、次の図に示されるように、テキスト ボックス、ボタン、および他のコントロールを追加します。 各コントロールに、テーブルを示すプロパティを設定します。

   > [!NOTE]
   > グループ ボックス、およびラベル コントロールは明確性を追加しますが、コードでは使用されません。

   **Navigation フォーム**

   ![ナビゲーション ダイアログ ボックス](../data-tools/media/simpleappnav.png)

|Navigation フォームのコントロール|Properties|
| - |----------------|
|Button|Name = btnGoToAdd|
|Button|Name = btnGoToFillOrCancel|
|Button|Name = btnExit|

**NewCustomer フォーム**

![新しい顧客を追加して注文を作成する](../data-tools/media/simpleappnewcust.png)

|NewCustomer フォームのコントロール|Properties|
| - |----------------|
|TextBox|Name = txtCustomerName|
|TextBox|Name = txtCustomerID<br /><br /> Readonly = True|
|Button|Name = btnCreateAccount|
|NumericUpdown|DecimalPlaces = 0<br /><br /> Maximum = 5000<br /><br /> Name = numOrderAmount|
|DateTimePicker|Format = Short<br /><br /> Name = dtpOrderDate|
|Button|Name = btnPlaceOrder|
|Button|Name = btnAddAnotherAccount|
|Button|Name = btnAddFinish|

**FillOrCancel フォーム**

![注文の入力または取り消し](../data-tools/media/simpleappcancelfill.png)

|FillOrCancel フォームのコントロール|Properties|
| - |----------------|
|TextBox|Name = txtOrderID|
|Button|Name = btnFindByOrderID|
|DateTimePicker|Format = Short<br /><br /> Name = dtpFillDate|
|DataGridView|Name = dgvCustomerOrders<br /><br /> Readonly = True<br /><br /> RowHeadersVisible = False|
|Button|Name = btnCancelOrder|
|Button|Name = btnFillOrder|
|Button|Name = btnFinishUpdates|

## <a name="store-the-connection-string"></a>接続文字列を保存する
アプリケーションがデータベースの接続を開くとき、アプリケーションは接続文字列にアクセスする必要があります。 各フォームに文字列を手動で入力しないようにするには、プロジェクトの *App.config* ファイルに文字列を格納し、アプリケーションの任意の形式からメソッドが呼び出されたときに文字列を返すメソッドを作成します。

接続文字列を見つけるには、**サーバーエクスプローラー** で **Sales** データ接続を右クリックし、[**プロパティ**] を選択します。 **ConnectionString** プロパティを見つけ、 **ctrl** + **A** キー、 **ctrl** + **C** キーを使用して、文字列を選択してクリップボードにコピーします。

1. C# を使用している場合は、 **ソリューションエクスプローラー** で、プロジェクトの [ **プロパティ** ] ノードを展開し、 **設定** ファイルを開きます。
    Visual Basic を使用している場合は、 **ソリューションエクスプローラー** で [ **すべてのファイルを表示**] をクリックし、[ **マイプロジェクト** ] ノードを展開して、 **設定の設定** ファイルを開きます。

2. [ **名前** ] 列に「」と入力し `connString` ます。

3. [ **種類** ] ボックスの一覧で [ **(接続文字列)**] を選択します。

4. [ **スコープ** ] ボックスの一覧で [ **アプリケーション**] を選択します。

5. [ **値** ] 列に、(引用符を除く) 接続文字列を入力し、変更を保存します。

> [!NOTE]
> 実際のアプリケーションでは、「 [接続文字列と構成ファイル](/dotnet/framework/data/adonet/connection-strings-and-configuration-files)」で説明されているように、接続文字列を安全に保存する必要があります。

## <a name="write-the-code-for-the-forms"></a>フォームのコードを記述する

ここでは、各フォームの機能の概要について説明します。 また、フォーム上のボタンがクリックされたときに、基になるロジックを定義するコードも提供します。

### <a name="navigation-form"></a>Navigation フォーム

Navigation フォームはアプリケーションを実行すると開きます。 **[Add an account]** ボタンは NewCustomer フォームを開きます。 **[Fill or cancel orders]** ボタンは FillOrCancel フォームを開きます。 **[Exit]** ボタンは、アプリケーションを閉じます。

#### <a name="make-the-navigation-form-the-startup-form"></a>Navigation フォームをスタートアップ フォームに設定

C# を使用している場合、**ソリューション エクスプローラー** で **Program.cs** を開き、`Application.Run` の行を `Application.Run(new Navigation());` に変更します。

Visual Basic を使用している場合は **ソリューションエクスプローラー** で [**プロパティ**] ウィンドウを開いて [**アプリケーション**] タブを選択し、[**スタートアップフォーム**] の一覧で [ **simpledataapp. ナビゲーション**] を選択します。

#### <a name="create-auto-generated-event-handlers"></a>自動生成されたイベントハンドラーを作成する

ナビゲーションフォームの3つのボタンをダブルクリックして、空のイベントハンドラーメソッドを作成します。 また、ボタンをダブルクリックすると、デザイナーのコードファイルに自動生成されたコードが追加され、ボタンをクリックしてイベントを発生させることができます。

#### <a name="add-code-for-the-navigation-form-logic"></a>ナビゲーションフォームロジックのコードを追加する

ナビゲーションフォームのコードページで、次のコードに示すように、3つのボタンクリックイベントハンドラーのメソッド本体を完成させます。

[!code-csharp[Navigation#1](../data-tools/codesnippet/CSharp/SimpleDataApp/Navigation.cs#1)]
[!code-vb[Navigation#1](../data-tools/codesnippet/VisualBasic/SimpleDataApp/Navigation.vb#1)]

### <a name="newcustomer-form"></a>NewCustomer フォーム

顧客名を入力して [ **アカウントの作成** ] ボタンを選択すると、newcustomer フォームによって顧客アカウントが作成され、SQL Server によって新しい顧客 ID として id 値が返されます。 次に、金額と注文日を指定し、[ **場所の順序** ] ボタンを選択して、新しいアカウントの注文を配置できます。

#### <a name="create-auto-generated-event-handlers"></a>自動生成されたイベントハンドラーを作成する

4つの各ボタンをダブルクリックして、NewCustomer フォームの各ボタンに空のクリックイベントハンドラーを作成します。 また、ボタンをダブルクリックすると、デザイナーのコードファイルに自動生成されたコードが追加され、ボタンをクリックしてイベントを発生させることができます。

#### <a name="add-code-for-the-newcustomer-form-logic"></a>NewCustomer フォームロジックのコードを追加する

NewCustomer フォームロジックを完了するには、次の手順を実行します。

1. `System.Data.SqlClient`名前空間をスコープにして、メンバーの名前を完全修飾する必要がないようにします。

     ```csharp
     using System.Data.SqlClient;
     ```

     ```vb
     Imports System.Data.SqlClient
     ```

2. 次のコードに示すように、クラスにいくつかの変数とヘルパーメソッドを追加します。

     [!code-csharp[NewCustomer#1](../data-tools/codesnippet/CSharp/SimpleDataApp/NewCustomer.cs#1)]
     [!code-vb[NewCustomer#1](../data-tools/codesnippet/VisualBasic/SimpleDataApp/NewCustomer.vb#1)]

3. 次のコードに示すように、4つのボタンクリックイベントハンドラーのメソッド本体を完成させます。

     [!code-csharp[NewCustomer#2](../data-tools/codesnippet/CSharp/SimpleDataApp/NewCustomer.cs#2)]
     [!code-vb[NewCustomer#2](../data-tools/codesnippet/VisualBasic/SimpleDataApp/NewCustomer.vb#2)]

### <a name="fillorcancel-form"></a>FillOrCancel フォーム

FillOrCancel フォームは、注文 ID を入力し、[ **検索順序** ] ボタンをクリックしたときに、注文を返すクエリを実行します。 戻された行は読み取り専用なデータ グリッドに表示されます。 [ **キャンセル順序** ] ボタンを選択した場合、注文をキャンセル (X) としてマークできます。または、[ **フィルの順序** ] ボタンを選択した場合は、注文を塗りつぶしとしてマークできます (F)。 [ **検索順序** ] ボタンをもう一度選択すると、更新された行が表示されます。

#### <a name="create-auto-generated-event-handlers"></a>自動生成されたイベントハンドラーを作成する

ボタンをダブルクリックして、FillOrCancel フォーム上の4つのボタンに対して空のクリックイベントハンドラーを作成します。 また、ボタンをダブルクリックすると、デザイナーのコードファイルに自動生成されたコードが追加され、ボタンをクリックしてイベントを発生させることができます。

#### <a name="add-code-for-the-fillorcancel-form-logic"></a>FillOrCancel フォームロジックのコードを追加する

FillOrCancel フォームロジックを完了するには、次の手順を実行します。

1. 次の2つの名前空間をスコープに取り込み、メンバーの名前を完全修飾する必要がないようにします。

     ```csharp
     using System.Data.SqlClient;
     using System.Text.RegularExpressions;
     ```

     ```vb
     Imports System.Data.SqlClient
     Imports System.Text.RegularExpressions
     ```

2. 次のコードに示すように、クラスに変数とヘルパーメソッドを追加します。

     [!code-csharp[FillOrCancel#1](../data-tools/codesnippet/CSharp/SimpleDataApp/FillOrCancel.cs#1)]
     [!code-vb[FillOrCancel#1](../data-tools/codesnippet/VisualBasic/SimpleDataApp/FillOrCancel.vb#1)]

3. 次のコードに示すように、4つのボタンクリックイベントハンドラーのメソッド本体を完成させます。

     [!code-csharp[FillOrCancel#2](../data-tools/codesnippet/CSharp/SimpleDataApp/FillOrCancel.cs#2)]
     [!code-vb[FillOrCancel#2](../data-tools/codesnippet/VisualBasic/SimpleDataApp/FillOrCancel.vb#2)]

## <a name="test-your-application"></a>アプリケーションのテスト

各クリック イベント ハンドラーをコードし、コードの記述を完了した後、**F5** キーを押してアプリケーションのビルドとテストを実行します。

## <a name="see-also"></a>関連項目

- [.NET 用の Visual Studio データ ツール](../data-tools/visual-studio-data-tools-for-dotnet.md)
