---
title: データベースファイルを作成し、テーブルデザイナーを使用する
description: Visual Studio のテーブルデザイナーを使用してデータベースにテーブルと外部キーを追加する方法について説明するチュートリアルです。 また、グラフィカルインターフェイスを使用してデータを追加する方法についても説明します。
ms.date: 09/19/2019
ms.topic: conceptual
helpviewer_keywords:
- database tables, creating
- database files, creating
- table designer
ms.assetid: 99c2b06f-47aa-414e-8057-a3453712fd23
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: e31be90ff24f110fda66449187d3372976f269a7
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85282723"
---
# <a name="create-a-database-and-add-tables-in-visual-studio"></a>Visual Studio でデータベースを作成し、テーブルを追加する

Visual Studio を使用して SQL Server Express LocalDB でローカルデータベースファイルを作成および更新できます。 また、Visual Studio の**SQL Server オブジェクトエクスプローラー**ツールウィンドウで transact-sql ステートメントを実行して、データベースを作成することもできます。 このトピックでは、テーブルデザイナーを使用して、 *.mdf*ファイルを作成し、テーブルとキーを追加します。

## <a name="prerequisites"></a>必須コンポーネント

このチュートリアルを完了するには、Visual Studio に **.net デスクトップ開発**と**データストレージおよび処理**ワークロードがインストールされている必要があります。 これらをインストールするには、 **Visual Studio インストーラー**を開き、変更する Visual Studio のバージョンの横にある [**変更**(または**その他**の  >  **変更**)] を選択します。

> [!NOTE]
> この記事の手順は、.NET Core Windows フォームプロジェクトではなく、.NET Framework Windows フォームプロジェクトにのみ適用されます。

## <a name="create-a-project-and-a-local-database-file"></a>プロジェクトとローカル データベース ファイルを作成する

1. 新しい**Windows フォーム App (.NET Framework)** プロジェクトを作成し、「 **sampledatabasewalkthrough**」という名前を指定します。

2. メニューバーで、[**プロジェクト**] [  >  **新しい項目の追加**] を選択します。

3. 項目テンプレートの一覧で下にスクロールし、[**サービスベースのデータベース**] を選択します。

   ![[アイテム テンプレート] ダイアログ ボックス](../data-tools/media/raddata-vsitemtemplates.png)

4. データベースに「 **Sampledatabase**」という名前を指定し、[**追加**] をクリックします。

### <a name="add-a-data-source"></a>データ ソースの追加

1. [**データソース**] ウィンドウが開いていない場合は、 **Shift** + **Alt** + **D**キーを押すか**View**  >  、メニューバーの [**他の Windows**  >  **データソース**の表示] をクリックして開きます。

1. [**データソース**] ウィンドウで、[**新しいデータソースの追加**] を選択します。

   ![Visual Studio での新しいデータソースの追加](media/add-new-data-source.png)

   **データソース構成ウィザード**が開きます。

1. [**データソースの種類を選択**] ページで、[**データベース**] を選択し、[**次へ**] をクリックします。

1. [**データベースモデルの選択**] ページで、[**次へ**] をクリックして既定の設定 (データセット) を受け入れます。

1. [**データ接続の選択**] ページで、ドロップダウンリストから**sampledatabase .mdf**ファイルを選択し、[**次へ**] を選択します。

1. [**アプリケーション構成ファイルに接続文字列を保存**] ページで、[**次へ**] を選択します。

1. [**データベースオブジェクトの選択**] ページに、"データベースにオブジェクトが含まれていません" というメッセージが表示されます。 **[完了]** をクリックします。

### <a name="view-properties-of-the-data-connection"></a>データ接続のプロパティを表示する

データ接続のプロパティウィンドウを開くと、 *Sampledatabase .mdf*ファイルの接続文字列を表示できます。

- [SQL Server オブジェクトエクスプローラーの**表示**] を選択し  >  **SQL Server Object Explorer**て [ **SQL Server オブジェクトエクスプローラー** ] ウィンドウを開きます。 **(Localdb) \MSSQLLocalDB**データベースを展開し、[  >  **sampledatabase**] *SampleDatabase.mdf*を右クリックして、[**プロパティ**] を選択します。

- または、[サーバーエクスプローラーの**表示**] を選択することもでき  >  **Server Explorer**ます (そのウィンドウがまだ開いていない場合)。 [**データ接続**] ノードを展開して [ *sampledatabase. .mdf*] を右クリックし、[**プロパティ**] を選択して、プロパティウィンドウを開きます。

  > [!TIP]
  > [データ接続] ノードを展開できない場合、または [SampleDatabase. .mdf] 接続が表示されていない場合は、サーバーエクスプローラーツールバーの [**データベースへの接続**] をクリックします。 [**接続の追加**] ダイアログボックスで、[**データソース**] の下の**Microsoft SQL Server データベースファイル**が選択されていることを確認し、sampledatabase .mdf ファイルを参照して選択します。 **[OK]** を選択して、接続の追加を完了します。

## <a name="create-tables-and-keys-by-using-table-designer"></a>テーブルデザイナーを使用したテーブルとキーの作成

このセクションでは、2つのテーブル、各テーブルの主キー、およびいくつかのサンプルデータを作成します。 また、外部キーを作成して、1つのテーブル内のレコードが他のテーブルのレコードにどのように対応するかを指定します。

### <a name="create-the-customers-table"></a>Customers テーブルを作成する

1. **サーバーエクスプローラー**で、[**データ接続**] ノードを展開し、[ **sampledatabase. .mdf** ] ノードを展開します。

   [データ接続] ノードを展開できない場合、または [SampleDatabase. .mdf] 接続が表示されていない場合は、サーバーエクスプローラーツールバーの [**データベースへの接続**] をクリックします。 [**接続の追加**] ダイアログボックスで、[**データソース**] の下の**Microsoft SQL Server データベースファイル**が選択されていることを確認し、sampledatabase .mdf ファイルを参照して選択します。 **[OK]** を選択して、接続の追加を完了します。

2. [**テーブル**] を右クリックし、[**新しいテーブルの追加**] をクリックします。

   [テーブル デザイナー] は、作成しているテーブルの 1 つの列を表す、1 つの既定の行のグリッドを開いて表示します。 行をグリッドに追加することによって、テーブルに列を追加します。

3. グリッドで、次のエントリのそれぞれに行を追加します。

   |列名|データ型|Null を許容|
   |-----------------|---------------|-----------------|
   |`CustomerID`|`nchar(5)`|false (オフ)|
   |`CompanyName`|`nvarchar(50)`|false (オフ)|
   |`ContactName`|`nvarchar (50)`|true (オン)|
   |`Phone`|`nvarchar (24)`|true (オン)|

4. 行を右クリックし、[ `CustomerID` **主キーの設定**] をクリックします。

5. 既定の行 () を右クリック `Id` し、[**削除**] を選択します。

6. スクリプト ペインの最初の行の次のサンプルのように更新して、Customers (顧客) をテーブルと名前を付けます:

   ```sql
   CREATE TABLE [dbo].[Customers]
   ```

   次のような結果が表示されます。

   ![テーブル デザイナー (Table Designer)](../data-tools/media/table-designer.png)

7. **テーブルデザイナー**の左上隅にある [**更新**] を選択します。

8. [**データベースの更新のプレビュー** ] ダイアログボックスで、[データベースの**更新**] を選択します。

   Customers テーブルは、ローカルデータベースファイルに作成されます。

### <a name="create-the-orders-table"></a>Orders テーブルを作成する

1. 別のテーブルを追加し、次の表の各エントリの行を追加します。

   |列名|データ型|Null を許容|
   |-----------------|---------------|-----------------|
   |`OrderID`|`int`|false (オフ)|
   |`CustomerID`|`nchar(5)`|false (オフ)|
   |`OrderDate`|`datetime`|true (オン)|
   |`OrderQuantity`|`int`|true (オン)|

2. **OrderID**を主キーとして設定し、既定の行を削除します。

3. スクリプト ペインの最初の行の次のサンプルのように更新して、Orders (注文) をテーブルと名前を付けます:

   ```sql
   CREATE TABLE [dbo].[Orders]
   ```

4. **テーブルデザイナー**の左上隅にある [**更新**] を選択します。

5. [**データベースの更新のプレビュー** ] ダイアログボックスで、[データベースの**更新**] を選択します。

   Orders テーブルは、ローカルデータベースファイルに作成されます。 サーバーエクスプローラーの [**テーブル**] ノードを展開すると、次の2つのテーブルが表示されます。

   ![サーバーエクスプローラーで展開されたテーブルノード](media/server-explorer-tables-node.png)

### <a name="create-a-foreign-key"></a>外部キーを作成する

1. Orders テーブルのテーブルデザイナーグリッドの右側にあるコンテキストペインで、[**外部キー** ] を右クリックし、[**新しい外部キーの追加**] を選択します。

   ![Visual Studio でテーブルデザイナーに外部キーを追加する](../data-tools/media/add-foreign-key.png)

2. 表示されたテキストボックスで、 **ToTable**というテキストを「 **Customers**」に置き換えます。

3. T-sql ペインで、次の例に一致するように最後の行を更新します。

   ```sql
   CONSTRAINT [FK_Orders_Customers] FOREIGN KEY ([CustomerID]) REFERENCES [Customers]([CustomerID])
   ```

4. **テーブルデザイナー**の左上隅にある [**更新**] を選択します。

5. [**データベースの更新のプレビュー** ] ダイアログボックスで、[データベースの**更新**] を選択します。

   外部キーが作成されます。

## <a name="populate-the-tables-with-data"></a>テーブルにデータを読み込む

1. **サーバーエクスプローラー**または**SQL Server オブジェクトエクスプローラー**で、サンプルデータベースのノードを展開します。

2. [**テーブル**] ノードのショートカットメニューを開き、[**更新**] を選択し、[**テーブル**] ノードを展開します。

3. Customers テーブルのショートカットメニューを開き、[**テーブルデータの表示**] を選択します。

4. 一部の顧客に対して任意のデータを追加します。

    顧客 ID には任意の 5 文字を指定できます。この手順では、後で使用するために、少なくとも 1 つを選択します。

5. Orders テーブルのショートカットメニューを開き、[**テーブルデータの表示**] を選択します。

6. いくつかの注文のデータを追加します。

    > [!IMPORTANT]
    > すべての注文 Id と注文数量が整数であり、各顧客 ID が Customers テーブルの**CustomerID**列で指定した値と一致していることを確認します。

7. メニューバーで、[**ファイル**] [すべてを保存] を選択し  >  **Save All**ます。

## <a name="see-also"></a>関連項目

- [Visual Studio でのデータへのアクセス](accessing-data-in-visual-studio.md)
