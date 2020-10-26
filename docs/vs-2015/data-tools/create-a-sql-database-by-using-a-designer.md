---
title: デザイナーを使用して SQL データベースを作成する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- SQL Server Express
- local data
- LocalDB
- SQLEXPRESS
- data [Visual Studio], Local data
- SQL Express
- data [Visual Studio], walkthroughs
- databases, creating
- database files, creating
ms.assetid: 99c2b06f-47aa-414e-8057-a3453712fd23
caps.latest.revision: 54
author: jillre
ms.author: jillfra
manager: jillfra
robots: noindex,nofollow
ms.openlocfilehash: 33b97050f04fd23a9fa3b6c3c641faa5dfe4802f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72651057"
---
# <a name="create-a-sql-database-by-using-a-designer"></a>デザイナーを使用して SQL データベースを作成する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio を使用して SQL Server Express LocalDB でローカルデータベースファイルを作成および更新することで、テーブルの追加や列の定義などの基本的なタスクを調べることができます。 このチュートリアルを終了すると、ローカル データベースを使用してさらに高度な機能を使用できるようになり、こうした機能を必要とする他のチュートリアルへの準備となります。

 また、Visual Studio の **SQL Server オブジェクトエクスプローラー** ツールウィンドウで SQL Server Management Studio (個別のダウンロード) または transact-sql ステートメントを使用してデータベースを作成することもできます。

 このチュートリアルには次のタスクがあります。

- [プロジェクトとローカル データベース ファイルを作成する](../data-tools/create-a-sql-database-by-using-a-designer.md#BKMK_CreateNewSQLDB)

- [テーブル、列、主キー、および外部キーを作成する](../data-tools/create-a-sql-database-by-using-a-designer.md#BKMK_CreateNewTbls)

- [テーブルにデータを読み込む](../data-tools/create-a-sql-database-by-using-a-designer.md#BKMK_Populating)

## <a name="prerequisites"></a>前提条件
 このチュートリアルを完了するには、SQL Server Data Tools インストールされていることを確認します。 [ **表示** ] メニューに **SQL Server オブジェクトエクスプローラー**が表示されます。 表示されていない場合は、[ **プログラムの追加と削除**]、[ **Visual Studio 2015**]、[ **変更**] の順にクリックし、[ **SQL Server Data Tools**] の横のボックスをオンにします。

## <a name="create-a-project-and-a-local-database-file"></a><a name="BKMK_CreateNewSQLDB"></a> プロジェクトとローカルデータベースファイルの作成

#### <a name="to-create-a-project-and-a-database-file"></a>プロジェクトとローカル データベース ファイルを作成するには

1. という名前の Windows フォームプロジェクトを作成 `SampleDatabaseWalkthrough` します。

2. メニューバーで、[**プロジェクト**] [  >  **新しい項目の追加**] を選択します。

3. 項目テンプレートの一覧で下にスクロールし、[ **サービスベースのデータベース**] を選択します。

    ![[アイテム テンプレート] ダイアログ ボックス](../data-tools/media/raddata-vsitemtemplates.png "レーダーデータ VSItemTemplates")

4. データベースに **Sampledatabase**という名前を指定し、[ **追加** ] ボタンを選択します。

5. [**データソース**] ウィンドウが開いていない場合は、Shift + Alt + D キーを押すか、メニューバーで [ **View**  >  **他の Windows**  >  **データソース**の表示] を選択して開きます。

6. [ **データソース** ] ウィンドウで、[ **新しいデータソースの追加** ] リンクを選択します。

7. **データソース構成ウィザード**で、[**次へ**] を4回クリックして既定の設定をそのまま使用し、[**完了**] をクリックします。

   データベースのプロパティ ウィンドウを開くと、その接続文字列と、プライマリ .mdf ファイルの位置を確認できます。 データベースファイルがプロジェクトフォルダーにあることがわかります。

- Visual Studio で、[**表示**] を選択し  >  て、そのウィンドウがまだ開いていない場合は**SQL Server オブジェクトエクスプローラー**します。 [ **データ接続** ] ノードを展開し、[sampledatabase .mdf] のショートカットメニューを開き、[ **プロパティ**] を選択して、[プロパティ] ウィンドウを開きます。

- または、[サーバーエクスプローラーの**表示**] を選択することもでき  >  **Server Explorer**ます (そのウィンドウがまだ開いていない場合)。 [ **データ接続** ] ノードを展開して、[プロパティ] ウィンドウを開きます。 SampleDatabase .mdf のショートカットメニューを開き、[ **プロパティ**] を選択します。

## <a name="create-tables-columns-primary-keys-and-foreign-keys"></a><a name="BKMK_CreateNewTbls"></a> テーブル、列、主キー、および外部キーを作成する
 このセクションでは、いくつかのテーブルと各テーブルの主キー、およびサンプル データの行を作成します。 次のチュートリアルでは、この情報がアプリケーションでどのように表示されるかを理解することができます。 また外部キーを作成して、1 つのテーブルのレコードが他のテーブルのレコードに対応する方法を指定できます。

#### <a name="to-create-the-customers-table"></a>Customers テーブルを作成するには

1. **サーバーエクスプローラー**または**SQL Server オブジェクトエクスプローラー**で、[**データ接続**] ノードを展開し、[ **sampledatabase. .mdf** ] ノードを展開します。

2. [ **テーブル**] のショートカットメニューを開き、[ **新しいテーブルの追加**] を選択します。

     **[テーブル デザイナー]** は、作成しているテーブルの 1 つの列を表す、1 つの既定の行のグリッドを開いて表示します。 行をグリッドに追加することによって、テーブルに列を追加します。

3. グリッドで、次のエントリのそれぞれに行を追加します。

    |列名|データ型|Null を許容|
    |-----------------|---------------|-----------------|
    |`CustomerID`|`nchar(5)`|false (オフ)|
    |`CompanyName`|`nvarchar(50)`|false (オフ)|
    |`ContactName`|`nvarchar (50)`|true (オン)|
    |`Phone`|`nvarchar (24)`|true (オン)|

4. 行のショートカットメニューを開き、[ `CustomerID` **主キーの設定**] を選択します。

5. 既定の行のショートカットメニューを開き、[ **削除**] を選択します。

6. スクリプト ペインの最初の行の次のサンプルのように更新して、Customers (顧客) をテーブルと名前を付けます:

    ```
    CREATE TABLE [dbo].[Customers]
    ```

     次のような結果が表示されます。

     ![テーブル デザイナー (Table Designer)](../data-tools/media/raddata-table-designer.png "テーブルデザイナーのレーダーデータ")

7. **テーブルデザイナー**の左上隅にある [**更新**] ボタンを選択します。

8. [ **データベースの更新のプレビュー** ] ダイアログボックスで、[データベースの **更新** ] ボタンを選択します。

     変更はローカル データベース ファイルに保存されます。

#### <a name="to-create-the-orders-table"></a>Orders テーブルを作成するには

1. 別のテーブルを追加し、次の表の各エントリの行を追加します。

    |列名|データ型|Null を許容|
    |-----------------|---------------|-----------------|
    |`OrderID`|`int`|false (オフ)|
    |`CustomerID`|`nchar(5)`|false (オフ)|
    |`OrderDate`|`datetime`|true (オン)|
    |`OrderQuantity`|`int`|true (オン)|

2. **OrderID**を主キーとして設定し、既定の行を削除します。

3. スクリプト ペインの最初の行の次のサンプルのように更新して、Orders (注文) をテーブルと名前を付けます:

    ```
    CREATE TABLE [dbo].[Orders]
    ```

4. **テーブルデザイナー**の左上隅にある [**更新**] ボタンを選択します。

5. [ **データベースの更新のプレビュー** ] ダイアログボックスで、[データベースの **更新** ] ボタンを選択します。

     変更はローカル データベース ファイルに保存されます。

#### <a name="to-create-a-foreign-key"></a>外部キーを作成するには

1. 次の図に示すように、グリッドの右側のコンテキストペインで、[ **外部キー**] のショートカットメニューを開き、[ **新しい外部キーの追加**] を選択します。

     ![テーブル デザイナーでの外部キーの追加](../data-tools/media/foreignkey.png "ForeignKey")

2. 表示されたテキストボックスで、 **ToTable** をに置き換え `Customers` ます。

3. T-sql ペインで、次の例に一致するように最後の行を更新します。

    ```
    CONSTRAINT [FK_Orders_Customers] FOREIGN KEY ([CustomerID]) REFERENCES [Customers]([CustomerID])
    ```

4. **テーブルデザイナー**の左上隅にある [**更新**] ボタンを選択します。

5. [ **データベースの更新のプレビュー** ] ダイアログボックスで、[データベースの **更新** ] ボタンを選択します。

     変更はローカル データベース ファイルに保存されます。

## <a name="populate-the-tables-with-data"></a><a name="BKMK_Populating"></a> テーブルにデータを読み込む

#### <a name="to-populate-the-tables-with-data"></a>テーブルにデータを読み込むには

1. **サーバーエクスプローラー**または**SQL Server オブジェクトエクスプローラー**で、サンプルデータベースのノードを展開します。

2. [ **テーブル** ] ノードのショートカットメニューを開き、[ **更新**] を選択し、[ **テーブル** ] ノードを展開します。

3. Customers テーブルのショートカットメニューを開き、[ **テーブルデータの表示**] を選択します。

4. 最低 3 人の Customer (顧客) に任意のデータを追加します。

     顧客 ID には任意の 5 文字を指定できます。この手順では、後で使用するために、少なくとも 1 つを選択します。

5. Orders テーブルのショートカットメニューを開き、[ **テーブルデータの表示**] を選択します。

6. 最低 3 件の注文データを追加します。

    > [!IMPORTANT]
    > すべての注文 ID および注文数量が整数であり、各顧客 ID が、Customers テーブルの CustomerID 列で指定した値と一致することを確認します。

7. メニューバーで、[**ファイル**] [すべてを保存] を選択し  >  **Save All**ます。

8. メニューバーで、[**ファイル**] [ソリューションの終了] を選択し  >  **Close Solution**ます。

    > [!NOTE]
    > ベスト プラクティスとして、データベースをコピーし、他の場所にそのコピーを貼り付ける、またはコピーに異なる名前を付けることによって、作成したデータベースのバックアップを実行します。

## <a name="next-steps"></a>次の手順
 いくつかのサンプルデータを含むローカルデータベースファイルが作成されたので、データベースタスクを説明するチュートリアルを完了できます。
