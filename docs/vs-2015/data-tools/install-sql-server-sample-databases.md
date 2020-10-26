---
title: SQL Server サンプルデータベースのインストール |Microsoft Docs
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.date: 11/15/2016
ms.topic: conceptual
ms.assetid: 38840167-c3f8-4cb3-8d15-8af04a0a20a1
caps.latest.revision: 14
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 3915351bff74f35ceb5fc462cb29dfd2f322fb6a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "74299630"
---
# <a name="install-sql-server-sample-databases"></a>SQL Server サンプル データベースをインストールする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

サンプルデータベースは、SQL および LINQ クエリ、データバインド、Entity Framework モデリングなどを試してみるのに役立ちます。  各データベース製品には、独自のサンプルデータベースがあります。 Northwind と AdventureWorks は、2つの一般的な SQL Server サンプルデータベースです。

 **AdventureWorks** は、SQL Server 製品用に提供されている現在のサンプルデータベースです。 これは、 [Codeplex の AdventureWorks ページ](https://archive.codeplex.com/?p=msftdbprodsamples)から .mdf ファイルとしてダウンロードできます。 ここでは、データベースの標準および簡易 (LT) バージョンが用意されています。 ほとんどのシナリオでは、複雑になるため、LT バージョンが推奨されています。

 **Northwind** は、数年にわたって使用されている比較的単純な SQL Server データベースです。 これは、 [CodePlex の Northwind データベースページ](https://northwinddatabase.codeplex.com/)から .bak ファイルとしてダウンロードできます。 アクセス許可の問題を回避するには、ユーザーフォルダーの下にない新しいフォルダーにファイルを解凍します。

#### <a name="to-restore-a-database-from-a-bak-file-in-visual-studio"></a>Visual Studio で .bak ファイルからデータベースを復元するには

1. Microsoft SQL Server データベースをバックアップすると、結果は .bak ファイルになります。 .Bak ファイルをデータベースファイルとして再度使用できるようにするには、そのファイルを *復元*する必要があります。 メインメニューで、[SQL Server オブジェクトエクスプローラーの**表示**] を選択し  >  **SQL Server Object Explorer**ます。 表示されない場合は、インストールする必要があります。 [**コントロールパネル]**[  >  **プログラムと機能**] に移動し、Microsoft Visual Studio 2015 を見つけて、[**変更**] ボタンをクリックします。 インストールされているコンポーネントの一覧がインストーラーウィンドウに表示されたら、[ **SQL Server オブジェクトエクスプローラー** ] チェックボックスをオンにして、インストールを続行します。

2. SQL Server オブジェクトエクスプローラーで、任意の SQL Server データベースエンジン (localdb など) を右クリックし、[**新しいクエリ**] を選択します。

     ![新しいクエリの SQL Server オブジェクトエクスプローラー](../data-tools/media/raddata-sql-server-object-explorer-new-query.png "新しいクエリ SQL Server オブジェクトエクスプローラーのレーダーデータ")

3. まず、データベースの論理名と、.bak ファイル内のログファイルが必要です。 これを取得するには、SQL クエリエディターに次のクエリを入力し、ウィンドウの上部にある緑色の [ **実行** ] ボタンを選択します。 必要に応じてファイルパスを変更し、.bak ファイルをポイントします。

    ```
    RESTORE FILELISTONLY
    FROM DISK = 'C:\nw\northwind.bak'
    GO
    ```

     [結果] ウィンドウに表示される論理名を書き留めます。  Northwind データベースの場合、2つの論理名は Northwind と Northwind_log です。

4. ここで、次のクエリを実行してデータベースを作成します。 必要に応じて、ソースとターゲットのパス、論理データベース名、Northwind の物理ファイル名に置き換えます。 .Mdf ファイルと .ldf ファイル拡張子を保持します。

    ```
    RESTORE DATABASE Northwind
    FROM DISK = 'c:\nw\northwind.bak'
    WITH MOVE 'Northwind' TO 'c:\nw\northwind.mdf',
    MOVE 'Northwind_log' TO 'c:\nw\northwind.ldf'
    ```

5. SQL Server オブジェクトエクスプローラーで、[ **データベース** ] ノードを右クリックすると、Northwind データベースノードが表示されます。 そうでない場合は、[データベース] を右クリックし、[ **新しいデータベースの追加**] を選択します。 先ほど作成した .mdf ファイルの名前と場所を入力します。

6. これで、データベースを Visual Studio のデータソースとして使用する準備ができました。

#### <a name="to-restore-a-database-from-a-bak-file-in-sql-server-management-studio"></a>SQL Server Management Studio の .bak ファイルからデータベースを復元するには

1. ダウンロードサイトから SQL Server Management Studio をダウンロードします。

2. SSMS **オブジェクトエクスプローラー** ウィンドウで、[ **データベース** ] ノードを右クリックし、[**データベースの復元**] を選択して、.bak ファイルの場所を指定します。

     ![SSMS データベースの復元](../data-tools/media/raddata-ssms-restore-database.png "レーダーデータ SSMS データベースの復元")
