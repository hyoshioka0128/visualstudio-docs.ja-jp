---
title: データを検索する Windows フォームを作成する
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Windows Forms, searching data
- Windows Forms, displaying data
- parameters, displaying filtered data
- data [Visual Studio], parameterizing queries
- data [Visual Studio], searching
ms.assetid: 65ca79a9-7458-466c-af55-978cd24c549e
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: df6f2245f06a594e35febe07d5aab2d7e83c48fd
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75586810"
---
# <a name="create-a-windows-form-to-search-data"></a>データを検索する Windows フォームを作成する

一般的なアプリケーションのシナリオでは、選択したデータをフォーム上に表示します。 たとえば、特定の顧客の注文、特定の注文の明細などを表示する場合があります。 このシナリオでは、ユーザーがフォームに情報を入力した後、ユーザーの入力をパラメーターとして使用してクエリが実行されます。つまり、パラメーター クエリに基づいてデータが選択されます。 クエリは、ユーザーが入力した条件を満たすデータのみを返します。 ここでは、特定の都市にいる顧客を返すクエリを作成する方法、およびユーザー インターフェイスを変更して、ユーザーが都市の名前を入力してクエリを実行するボタンを押すことができるようにする方法について説明します。

パラメーター クエリを使用することにより、データベースが最も得意とする作業 (レコードの迅速なフィルター処理) をデータベースに任せることができるため、アプリケーションの効率が高まります。 一方、データベース テーブル全体を要求し、それをネットワークを通じて転送し、アプリケーション ロジックを使用して必要なレコードを見つける場合は、アプリケーションが低速になり、効率が低下する可能性があります。

**[検索条件ビルダー]** ダイアログボックスを使用して、任意の TableAdapter (および、パラメーター値を受け入れるコントロールとクエリを実行するコントロール) にパラメーター化されたクエリを追加できます。 このダイアログ ボックスを開くには、 **[データ]** メニュー (または TableAdapter スマート タグ) の **[クエリの追加]** をクリックします。

このチュートリアルでは、以下のタスクを行います。

- **データソース構成**ウィザードを使用して、アプリケーションでデータソースを作成および構成します。

- **[データソース]** ウィンドウの項目のドロップタイプを設定します。

- **[データ ソース]** ウィンドウからフォームに項目をドラッグし、データを表示するコントロールを作成します。

- データを表示するコントロールをフォームに追加します。

- **[検索条件ビルダー]** ダイアログボックスを完了しています。

- フォームにパラメーターを入力し、パラメーター化されたクエリを実行します。

## <a name="prerequisites"></a>Prerequisites

このチュートリアルでは SQL Server Express LocalDB と Northwind サンプルデータベースを使用します。

1. LocalDB SQL Server Express ない場合は、 [SQL Server Express ダウンロードページ](https://www.microsoft.com/sql-server/sql-server-editions-express)からインストールするか、 **Visual Studio インストーラー**を使用してインストールします。 **Visual Studio インストーラー**では、**データストレージと処理**ワークロードの一部として SQL Server Express LocalDB をインストールすることも、個々のコンポーネントとしてインストールすることもできます。

2. 次の手順に従って、Northwind サンプルデータベースをインストールします。

    1. Visual Studio で、 **[SQL Server オブジェクトエクスプローラー]** ウィンドウを開きます。 (SQL Server オブジェクトエクスプローラーは、 **Visual Studio インストーラー**の**データストレージと処理**ワークロードの一部としてインストールされます)。 **[SQL Server]** ノードを展開します。 LocalDB インスタンスを右クリックし、 **[新しいクエリ]** をクリックします。

       クエリエディターウィンドウが開きます。

    2. [Northwind transact-sql スクリプト](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true)をクリップボードにコピーします。 この T-sql スクリプトでは、Northwind データベースを最初から作成し、データを設定します。

    3. T-sql スクリプトをクエリエディターに貼り付け、 **[実行]** ボタンをクリックします。

       しばらくすると、クエリの実行が完了し、Northwind データベースが作成されます。

## <a name="create-the-windows-forms-application"></a>Windows フォームアプリケーションを作成する

または Visual Basic 用の新しい**Windows フォームアプリ**プロジェクトを作成します。 C# プロジェクトに **WindowsSearchForm** という名前を付けます。

## <a name="create-the-data-source"></a>データソースを作成する

この手順では、**データ ソース構成**ウィザードを使用して、データベースからデータ ソースを作成します。

1. データ **[ソース]** ウィンドウを開くには、 **[データ]** メニューの **[データソースの表示]** をクリックします。

2. **[データ ソース]** ウィンドウで、 **[新しいデータ ソースの追加]** をクリックして**データ ソース構成**ウィザードを起動します。

3. **[データソースの種類を選択]** ページで、 **[データベース]** をクリックし、 **[次へ]** をクリックします。

4. **[データ接続の選択]** ページで、次のいずれかの操作を行います。

    - Northwind サンプル データベースへのデータ接続がドロップダウン リストに表示されている場合は選択します。

    - **[新しい接続]** を選択して **[接続の追加] または [接続の変更]** ダイアログ ボックスを表示します。

5. データベースにパスワードが必要な場合は、該当するオプションを選択して重要情報を含め、 **[次へ]** をクリックします。

6. **[アプリケーション構成ファイルに接続文字列を保存]** ページで、 **[次へ]** をクリックします。

7. **[データベース オブジェクトの選択]** ページで、 **[テーブル]** ノードを展開します。

8. **Customers** テーブルを選択し、 **[完了]** をクリックします。

     プロジェクトに **NorthwindDataSet** が追加され、 **[データ ソース]** ウィンドウに **Customers** テーブルが表示されます。

## <a name="create-the-form"></a>フォームを作成する

**[データ ソース]** ウィンドウからフォームに項目をドラッグして、データ バインド コントロールを作成します。

1. **[データ ソース]** ウィンドウの **[Customers]** ノードを展開します。

2. **[Customers]** ノードを **[データ ソース]** ウィンドウからフォームにドラッグします。

     <xref:System.Windows.Forms.DataGridView> と、レコード間を移動するためのツール ストリップ (<xref:System.Windows.Forms.BindingNavigator>) がフォーム上に表示されます。 [NorthwindDataSet](../data-tools/dataset-tools-in-visual-studio.md)、CustomersTableAdapter、<xref:System.Windows.Forms.BindingSource>、<xref:System.Windows.Forms.BindingNavigator> がコンポーネント トレイに表示されます。

## <a name="add-parameterization-search-functionality-to-the-query"></a>クエリへのパラメーター化 (検索機能) の追加

**[検索条件ビルダー]** ダイアログボックスを使用して、元のクエリに where 句を追加できます。

1. <xref:System.Windows.Forms.DataGridView> コントロールを選択し、 **[データ]** メニューの **[クエリの追加]** をクリックします。

2. **[検索条件ビルダー]** ダイアログボックスの **[新しいクエリ名]** 領域に「 **fillbycity** 」と入力します。

3. **[クエリ テキスト]** 領域でクエリに `WHERE City = @City` を追加します。

     クエリは次のようになります。

     ```sql
     SELECT CustomerID, CompanyName, ContactName, ContactTitle,
          Address, City, Region, PostalCode, Country, Phone, Fax
     FROM Customers
     WHERE City = @City
     ```

    > [!NOTE]
    > データソースへのアクセスと OLE DB では、疑問符 ('? ') を使用してパラメーターを指定するため、WHERE 句は次のようになります。 `WHERE City = ?`。

4. **[OK]** をクリックして **[検索条件ビルダー]** ダイアログ ボックスを閉じます。

     **FillByCityToolStrip** がフォームに追加されます。

## <a name="test-the-application"></a>アプリのテスト

アプリケーションを実行すると、フォームが開き、パラメーターを入力として取得できるようになります。

1. **F5** キーを押してアプリケーションを実行します。

2. **[City]** ボックスに「**London**」と入力し、 **[FillByCity]** をクリックします。

     データグリッドには、条件を満たす顧客が設定されます。 この例では、 **[City]** 列の値が **London** の顧客だけがデータ グリッドに表示されます。

## <a name="next-steps"></a>次のステップ:

アプリケーションの要件に応じて、パラメーター付きのフォームを作成した後に、追加の操作を実行できます。 このチュートリアルで行うことができる拡張には次のものがあります。

- 関連するデータを表示するコントロールを追加します。 詳細については、「[データセット内のリレーションシップ](relationships-in-datasets.md)」を参照してください。

- データセットを編集し、データベース オブジェクトの追加または削除を行います。 詳細については、[データセットの作成と構成](../data-tools/create-and-configure-datasets-in-visual-studio.md)に関するページを参照してください。

## <a name="see-also"></a>関連項目

- [Visual Studio でのデータへの Windows フォーム コントロールのバインド](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
