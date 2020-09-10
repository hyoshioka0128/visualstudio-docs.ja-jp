---
title: データセットデザイナーを使用してデータセットを作成する
ms.date: 09/11/2017
ms.topic: conceptual
helpviewer_keywords:
- datasets [Visual Basic], walkthroughs
- XML schemas, creating datasets
- data [Visual Studio], Dataset Designer
- Dataset Designer, walkthroughs
- datasets [Visual Basic], creating
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 07d61ec32d48e5cb9b5421e397d743cd8c95b523
ms.sourcegitcommit: 2a201c93ed526b0f7e5848657500f1111b08ac2a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2020
ms.locfileid: "89742927"
---
# <a name="walkthrough-create-a-dataset-with-the-dataset-designer"></a>チュートリアル: データセットデザイナーを使用したデータセットの作成

このチュートリアルでは、 **データセットデザイナー**を使用してデータセットを作成します。 この記事では、新しいプロジェクトを作成し、そのプロジェクトに新しい **データセット** アイテムを追加するプロセスについて説明します。 ウィザードを使用せずに、データベース内のテーブルに基づいてテーブルを作成する方法について説明します。

## <a name="prerequisites"></a>前提条件

このチュートリアルでは SQL Server Express LocalDB と Northwind サンプルデータベースを使用します。

1. LocalDB SQL Server Express ない場合は、 [SQL Server Express ダウンロードページ](https://www.microsoft.com/sql-server/sql-server-editions-express)からインストールするか、 **Visual Studio インストーラー**を使用してインストールします。 Visual Studio インストーラーでは、SQL Server Express LocalDB は、 **データストレージと処理** ワークロードの一部として、または個々のコンポーネントとしてインストールできます。

2. 次の手順に従って、Northwind サンプルデータベースをインストールします。

    1. Visual Studio で、[ **SQL Server オブジェクトエクスプローラー** ] ウィンドウを開きます。 (SQL Server オブジェクトエクスプローラーは、Visual Studio インストーラーの **データストレージと処理** ワークロードの一部としてインストールされます)。[ **SQL Server** ] ノードを展開します。 LocalDB インスタンスを右クリックし、[ **新しいクエリ**] をクリックします。

       クエリエディターウィンドウが開きます。

    2. [Northwind transact-sql スクリプト](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true)をクリップボードにコピーします。 この T-sql スクリプトでは、Northwind データベースを最初から作成し、データを設定します。

    3. T-sql スクリプトをクエリエディターに貼り付け、[ **実行** ] ボタンをクリックします。

       しばらくすると、クエリの実行が完了し、Northwind データベースが作成されます。

## <a name="create-a-new-windows-forms-application-project"></a>新しい Windows フォーム アプリケーション プロジェクトを作成します。

1. Visual Studio の **[ファイル]** メニューで､ **[新規作成]**  >  **[プロジェクト]** を選択します。

2. 左側のペインで [ **Visual C#** ] または [ **Visual Basic** を展開し、[ **Windows デスクトップ**] を選択します。

3. 中央のウィンドウで、[ **Windows フォーム App** ] プロジェクトの種類を選択します。

4. プロジェクトに **Datasetデザイナチュートリアル**という名前を指定し、[ **OK]** をクリックします。

     Visual Studio によってプロジェクトが **ソリューションエクスプローラー** に追加され、デザイナーに新しいフォームが表示されます。

## <a name="add-a-new-dataset-to-the-application"></a>アプリケーションに新しいデータセットを追加する

1. **[プロジェクト]** メニューで、 **[新しい項目の追加]** を選択します。

     **[新しい項目の追加]** ダイアログ ボックスが表示されます。

2. 左側のウィンドウで、[ **データ**] を選択し、中央のペインで [データ **セット** ] を選択します。

3. データセットに **NorthwindDataset**という名前を指定し、[ **追加**] を選択します。

     Visual Studio によって、 **NorthwindDataset** という名前のファイルがプロジェクトに追加され、 **データセットデザイナー**で開かれます。

## <a name="create-a-data-connection-in-server-explorer"></a>サーバーエクスプローラーでのデータ接続の作成

1. **[表示]** メニューの **[サーバー エクスプローラー]** をクリックします。

2. **サーバー エクスプローラー**で、**[データベースへの接続]** をクリックします。

3. Northwind サンプル データベースへの接続を作成します。

## <a name="create-the-tables-in-the-dataset"></a>データセットにテーブルを作成する

このセクションでは、データセットにテーブルを追加する方法について説明します。

### <a name="to-create-the-customers-table"></a>Customers テーブルを作成するには

1. **サーバー エクスプローラー**で作成したデータ接続を展開し、**[テーブル]** ノードを展開します。

2. **サーバー エクスプローラー**から**データセット デザイナー**に **Customers** テーブルをドラッグします。

     **Customers** データ テーブルと **CustomersTableAdapter** がデータセットに追加されます。

### <a name="to-create-the-orders-table"></a>Orders テーブルを作成するには

- **サーバー エクスプローラー**から**データセット デザイナー**に **Orders** テーブルをドラッグします。

     **Orders** データ テーブル、**OrdersTableAdapter**、および **Customers** テーブルと **Orders** テーブル間のリレーションシップが、データセットに追加されます。

### <a name="to-create-the-orderdetails-table"></a>OrderDetails テーブルを作成するには

- **サーバー エクスプローラー**から**データセット デザイナー**に **Order Details** テーブルをドラッグします。

     **Order Details** data Table、 **OrderDetailsTableAdapter**、および**Orders**テーブルと**OrderDetails**テーブル間のデータリレーションシップがデータセットに追加されます。

## <a name="next-steps"></a>次の手順

- データセットを保存します。

- **[データ ソース]** ウィンドウの項目を選択し、フォームにドラッグします。 詳細については、「 [Visual Studio でのデータへの Windows フォームコントロールのバインド](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)」を参照してください。

- TableAdapter に他のクエリを追加します。

- データセット内のデータ テーブルの <xref:System.Data.DataTable.ColumnChanging> イベントまたは <xref:System.Data.DataTable.RowChanging> イベントに検証ロジックを追加します。 詳細については、「 [データセット内のデータの検証](../data-tools/validate-data-in-datasets.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [Visual Studio でデータセットを作成および構成する](../data-tools/create-and-configure-datasets-in-visual-studio.md)
- [Visual Studio でのデータへの Windows フォーム コントロールのバインド](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
- [Visual Studio でのデータへのコントロールのバインド](../data-tools/bind-controls-to-data-in-visual-studio.md)
- [データの検証](../data-tools/validate-data-in-datasets.md)
