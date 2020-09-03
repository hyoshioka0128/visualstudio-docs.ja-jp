---
title: スクリプトを使用して SQL データベースを作成する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
- aspx
ms.assetid: 36f913c0-f5a7-4831-83a0-baba721ac95c
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 3bef7c4be2f38d0f50b2a13c7745cb212204769b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72670093"
---
# <a name="create-a-sql-database-by-using-a-script"></a>スクリプトを使用して SQL データベースを作成する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このチュートリアルでは、Visual Studio を使用して、 [ADO.NET を使用して単純なデータアプリケーションを作成](../data-tools/create-a-simple-data-application-by-using-adonet.md)するためのサンプルコードを含む小規模なデータベースを作成します。

 **このトピックの内容**

- [データベース スキーマを含むスクリプトを作成する](../data-tools/create-a-sql-database-by-using-a-script.md#CreateScript)

- [データベースプロジェクトを作成してスキーマをインポートする](../data-tools/create-a-sql-database-by-using-a-script.md#CreateProject)

- [データベースの配置](../data-tools/create-a-sql-database-by-using-a-script.md#DeployDatabase)

## <a name="prerequisites"></a>前提条件
 このチュートリアルを完了するには SQL Server Express LocalDB または別の SQL データベースがインストールされている必要があります。

## <a name="create-a-script-that-contains-a-database-schema"></a><a name="CreateScript"></a> データベーススキーマを含むスクリプトを作成する

#### <a name="to-create-a-script-from-which-you-can-import-a-schema"></a>スキーマのインポート元となるスクリプトを作成するには

1. の [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] メニューバーで、[**ファイル**] [  >  **新しい**ファイル] を選択し  >  **File**ます。

     **[新しいファイル]** ダイアログ ボックスが表示されます。

2. [ **カテゴリ** ] ボックスの一覧で [ **全般**] を選択します。

3. [ **テンプレート** ] ボックスの一覧で [ **Sql ファイル**] を選択し、[ **開く** ] をクリックします。

     Transact-sql エディターが開きます。

4. 次の Transact-sql コードをコピーし、Transact-sql エディターに貼り付けます。

    ```
    PRINT N'Creating Sales...';
    GO
    CREATE SCHEMA [Sales]
        AUTHORIZATION [dbo];
    GO
    PRINT N'Creating Sales.Customer...';
    GO
    CREATE TABLE [Sales].[Customer] (
        [CustomerID]   INT           IDENTITY (1, 1) NOT NULL,
        [CustomerName] NVARCHAR (40) NOT NULL,
        [YTDOrders]    INT           NOT NULL,
        [YTDSales]     INT           NOT NULL
    );
    GO
    PRINT N'Creating Sales.Orders...';
    GO
    CREATE TABLE [Sales].[Orders] (
        [CustomerID] INT      NOT NULL,
        [OrderID]    INT      IDENTITY (1, 1) NOT NULL,
        [OrderDate]  DATETIME NOT NULL,
        [FilledDate] DATETIME NULL,
        [Status]     CHAR (1) NOT NULL,
        [Amount]     INT      NOT NULL
    );
    GO
    PRINT N'Creating Sales.Def_Customer_YTDOrders...';
    GO
    ALTER TABLE [Sales].[Customer]
        ADD CONSTRAINT [Def_Customer_YTDOrders] DEFAULT 0 FOR [YTDOrders];
    GO
    PRINT N'Creating Sales.Def_Customer_YTDSales...';
    GO
    ALTER TABLE [Sales].[Customer]
        ADD CONSTRAINT [Def_Customer_YTDSales] DEFAULT 0 FOR [YTDSales];
    GO
    PRINT N'Creating Sales.Def_Orders_OrderDate...';
    GO
    ALTER TABLE [Sales].[Orders]
        ADD CONSTRAINT [Def_Orders_OrderDate] DEFAULT GetDate() FOR [OrderDate];
    GO
    PRINT N'Creating Sales.Def_Orders_Status...';
    GO
    ALTER TABLE [Sales].[Orders]
        ADD CONSTRAINT [Def_Orders_Status] DEFAULT 'O' FOR [Status];
    GO
    PRINT N'Creating Sales.PK_Customer_CustID...';
    GO
    ALTER TABLE [Sales].[Customer]
        ADD CONSTRAINT [PK_Customer_CustID] PRIMARY KEY CLUSTERED ([CustomerID] ASC) WITH (ALLOW_PAGE_LOCKS = ON, ALLOW_ROW_LOCKS = ON, PAD_INDEX = OFF, IGNORE_DUP_KEY = OFF, STATISTICS_NORECOMPUTE = OFF);
    GO
    PRINT N'Creating Sales.PK_Orders_OrderID...';
    GO
    ALTER TABLE [Sales].[Orders]
        ADD CONSTRAINT [PK_Orders_OrderID] PRIMARY KEY CLUSTERED ([OrderID] ASC) WITH (ALLOW_PAGE_LOCKS = ON, ALLOW_ROW_LOCKS = ON, PAD_INDEX = OFF, IGNORE_DUP_KEY = OFF, STATISTICS_NORECOMPUTE = OFF);
    GO
    PRINT N'Creating Sales.FK_Orders_Customer_CustID...';
    GO
    ALTER TABLE [Sales].[Orders]
        ADD CONSTRAINT [FK_Orders_Customer_CustID] FOREIGN KEY ([CustomerID]) REFERENCES [Sales].[Customer] ([CustomerID]) ON DELETE NO ACTION ON UPDATE NO ACTION;
    GO
    PRINT N'Creating Sales.CK_Orders_FilledDate...';
    GO
    ALTER TABLE [Sales].[Orders]
        ADD CONSTRAINT [CK_Orders_FilledDate] CHECK ((FilledDate >= OrderDate) AND (FilledDate < '01/01/2020'));
    GO
    PRINT N'Creating Sales.CK_Orders_OrderDate...';
    GO
    ALTER TABLE [Sales].[Orders]
        ADD CONSTRAINT [CK_Orders_OrderDate] CHECK ((OrderDate > '01/01/2005') and (OrderDate < '01/01/2020'));
    GO
    PRINT N'Creating Sales.uspCancelOrder...';
    GO
    CREATE PROCEDURE [Sales].[uspCancelOrder]
    @OrderID INT
    AS
    BEGIN
    DECLARE @Delta INT, @CustomerID INT
    BEGIN TRANSACTION
        SELECT @Delta = [Amount], @CustomerID = [CustomerID]
         FROM [Sales].[Orders] WHERE [OrderID] = @OrderID;

    UPDATE [Sales].[Orders]
       SET [Status] = 'X'
    WHERE [OrderID] = @OrderID;

    UPDATE [Sales].[Customer]
       SET
       YTDOrders = YTDOrders - @Delta
        WHERE [CustomerID] = @CustomerID
    COMMIT TRANSACTION
    END
    GO
    PRINT N'Creating Sales.uspFillOrder...';
    GO
    CREATE PROCEDURE [Sales].[uspFillOrder]
    @OrderID INT, @FilledDate DATETIME
    AS
    BEGIN
    DECLARE @Delta INT, @CustomerID INT
    BEGIN TRANSACTION
        SELECT @Delta = [Amount], @CustomerID = [CustomerID]
         FROM [Sales].[Orders] WHERE [OrderID] = @OrderID;

    UPDATE [Sales].[Orders]
       SET [Status] = 'F',
           [FilledDate] = @FilledDate
    WHERE [OrderID] = @OrderID;

    UPDATE [Sales].[Customer]
       SET
       YTDSales = YTDSales + @Delta
        WHERE [CustomerID] = @CustomerID
    COMMIT TRANSACTION
    END
    GO
    PRINT N'Creating Sales.uspNewCustomer...';
    GO
    CREATE PROCEDURE [Sales].[uspNewCustomer]
    @CustomerName NVARCHAR (40),
    @CustomerID INT OUTPUT
    AS
    BEGIN
    INSERT INTO [Sales].[Customer] (CustomerName) VALUES (@CustomerName);
    SET @CustomerID = SCOPE_IDENTITY();
    RETURN @@ERROR
    END
    GO
    PRINT N'Creating Sales.uspPlaceNewOrder...';
    GO
    CREATE PROCEDURE [Sales].[uspPlaceNewOrder]
    @CustomerID INT, @Amount INT, @OrderDate DATETIME, @Status CHAR (1)='O'
    AS
    BEGIN
    DECLARE @RC INT
    BEGIN TRANSACTION
    INSERT INTO [Sales].[Orders] (CustomerID, OrderDate, FilledDate, Status, Amount)
         VALUES (@CustomerID, @OrderDate, NULL, @Status, @Amount)
    SELECT @RC = SCOPE_IDENTITY();
    UPDATE [Sales].[Customer]
       SET
       YTDOrders = YTDOrders + @Amount
        WHERE [CustomerID] = @CustomerID
    COMMIT TRANSACTION
    RETURN @RC
    END
    GO
    CREATE PROCEDURE [Sales].[uspShowOrderDetails]
    @CustomerID INT=0
    AS
    BEGIN
    SELECT [C].[CustomerName], CONVERT(date, [O].[OrderDate]), CONVERT(date, [O].[FilledDate]), [O].[Status], [O].[Amount]
      FROM [Sales].[Customer] AS C
      INNER JOIN [Sales].[Orders] AS O
         ON [O].[CustomerID] = [C].[CustomerID]
      WHERE [C].[CustomerID] = @CustomerID
    END
    GO
    ```

5. メニューバーで、[**ファイル**] [  >  **名前を付けて保存 SqlQuery_1**] を選択します。

     [ **ファイル名を付けて保存** ] ダイアログボックスが表示されます。

6. [ **ファイル名** ] ボックスに「」と入力し、 `SampleImportScript.sql` ファイルを保存する場所をメモして、[ **保存** ] ボタンを選択します。

7. メニューバーで、[**ファイル**] [ソリューションの終了] を選択し  >  **Close Solution**ます。

     次に、データベース プロジェクトを作成し、作成したスクリプトからスキーマをインポートします。

## <a name="create-a-database-project-and-import-a-schema"></a><a name="CreateProject"></a> データベースプロジェクトを作成してスキーマをインポートする

#### <a name="to-create-a-database-project"></a>データベース プロジェクトを作成するには

1. メニュー バーから、 **[ファイル]**  >  **[新規]**  >  **[プロジェクト]** の順に選択します。

     **[新しいプロジェクト]** ダイアログ ボックスが表示されます。

2. [ **インストール済み**] の下で [ **テンプレート** ] ノードを展開し、[ **その他の言語** ] ノードを展開して、[ **SQL Server** ] カテゴリを選択し、[ **SQL Server データベース] プロジェクト** テンプレートを選択します。

    > [!NOTE]
    > [ **その他の言語** のノードを Visual Studio のすべてのインストールに表示することはできません。

3. [ **名前** ] ボックスに「」と入力し `Small Database` ます。

4. まだ選択されていない場合は、[ **ソリューションのディレクトリを作成** ] チェックボックスをオンにします。

5. [ **ソース管理に追加** ] チェックボックスがまだオフになっていない場合はオフにし、[ **OK** ] をクリックします。

     データベース プロジェクトが作成され、 **ソリューション エクスプローラー**に表示されます。

     次に、スクリプトからデータベース スキーマをインポートします。

#### <a name="to-import-a-database-schema-from-a-script"></a>スクリプトからデータベース スキーマをインポートするには

1. メニューバーで、[**プロジェクト**] [スクリプトのインポート] を選択し  >  **Import**  >  **Script**ます。

2. [ **ようこそ** ] ページで、テキストを確認し、[ **次へ** ] をクリックします。

3. [ **単一ファイル** ] をクリックし、[ **参照** ] ボタンを選択します。

     [ **SQL スクリプトのインポート** ] ダイアログボックスが表示されます。

4. SampleImportScript .sql ファイルを保存したフォルダーを開き、ファイルを選択し、[ **開く** ] ボタンを選択します。

5. [ **完了** ] をクリックして、[ **SQL スクリプトのインポート** ] ダイアログボックスを閉じます。

     スクリプトがインポートされ、このスクリプトで定義したオブジェクトがデータベース プロジェクトに追加されます。

6. 概要を確認し、[ **完了** ] をクリックして [ **SQL スクリプトファイルのインポート** ] ダイアログボックスを閉じます。

7. **ソリューションエクスプローラー**で、プロジェクトの Sales、Scripts、および Security フォルダーを展開し、.sql ファイルが含まれていることを確認します。

8. **SQL Server オブジェクトエクスプローラー**で、データベースが [**プロジェクト**] ノードの下に表示されていることを確認します。

     この時点で、データベースには、テーブル、ストアド プロシージャなどのシステム オブジェクトのみが格納されています。 データベースを配置した後に、スクリプトに定義されたユーザー テーブルとストアド プロシージャが含まれます。

## <a name="deploy-the-database"></a><a name="DeployDatabase"></a> データベースを配置する
 **F5**キーを押すと、既定でデータベースを LocalDB データベースに配置 (または発行) します。 別の場所にデータベースを配置するには、プロジェクトの [プロパティ] ページを開き、[ **デバッグ** ] タブを選択してから、接続文字列を変更します。
