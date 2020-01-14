---
title: 'チュートリアル : n 層データ アプリケーションの作成'
ms.date: 09/08/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- n-tier applications, creating
- n-tier applications, walkthroughs
ms.assetid: d15e4d31-2839-48d9-9e0e-2e73404d82a2
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: a88f0382a93027cc952dfe44f0027e6ab1076a45
ms.sourcegitcommit: 939407118f978162a590379997cb33076c57a707
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/13/2020
ms.locfileid: "75916494"
---
# <a name="walkthrough-create-an-n-tier-data-application"></a>チュートリアル: n 層データアプリケーションの作成
*n 層*データ アプリケーションとは、データにアクセスするアプリケーションの中でも、複数の論理レイヤー、つまり*層*に分離されるアプリケーションです。 アプリケーション コンポーネントをこのように別個の層に分離すると、アプリケーションの保守容易性とスケーラビリティが向上します。 これは、ソリューション全体を再設計しなくても 1 つの層に適用できる、新しい技術を簡単に導入できるようにすることで実現されます。 n 層アーキテクチャには、プレゼンテーション層、中間層、およびデータ層が存在します。 通常、中間層には、データ アクセス層、ビジネス ロジック層、および認証や検証などの共有コンポーネントが含まれます。 データ層には、リレーショナル データベースが含まれます。 通常、n 層アプリケーションでは、機密情報が中間層のデータ アクセス層に格納され、プレゼンテーション層にアクセスするエンド ユーザーから分離されます。 詳細については、「 [N 層データアプリケーションの概要](../data-tools/n-tier-data-applications-overview.md)」を参照してください。

n 層アプリケーションで各層を分離する 1 つの方法は、アプリケーションに組み込む層ごとに別個のプロジェクトを作成することです。 型指定されたデータセットには、生成されたデータセットと `DataSet Project` コードの格納先となるプロジェクトを決定する、`TableAdapter` プロパティが含まれています。

このチュートリアルでは、**データセット デザイナー**を使用して、別個のクラス ライブラリ プロジェクトにデータセットと `TableAdapter` コードを分離する方法を示します。 データセットと TableAdapter コードを分離した後、 [Visual Studio サービスで Windows Communication Foundation サービスと WCF Data Services](../data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio.md)を作成して、データアクセス層を呼び出すことができます。 最後に、プレゼンテーション層として Windows フォームアプリケーションを作成します。 この層は、データ サービスからデータにアクセスします。

このチュートリアルでは、次の手順を実行します。

- 複数のプロジェクトを含む新しい n 層ソリューションを作成します。

- この n 層ソリューションに 2 つのクラス ライブラリ プロジェクトを追加する。

- **データ ソース構成ウィザード**を実行して、型指定されたデータセットを作成する。

- 生成された[tableadapter](create-and-configure-tableadapters.md)とデータセットコードを個別のプロジェクトに分割します。

- データ アクセス層を呼び出す Windows Communication Foundation (WCF) サービスを作成する。

- このサービスに、データ アクセス層からデータを取得する関数を作成する。

- プレゼンテーション層として機能する Windows フォーム アプリケーションを作成する。

- Windows フォーム コントロールを作成し、データ ソースにバインドする。

- データ テーブルにデータを読み込むコードを記述する。

![ビデオへのリンク](../data-tools/media/playvideo.gif)このトピックのビデオ版について、次を参照してください[ビデオ操作方法: n 層データ アプリケーションの作成](/previous-versions/visualstudio/visual-studio-2008/cc178916(v=vs.90))。

## <a name="prerequisites"></a>[前提条件]
このチュートリアルでは SQL Server Express LocalDB と Northwind サンプルデータベースを使用します。

1. LocalDB SQL Server Express ない場合は、 [SQL Server Express ダウンロードページ](https://www.microsoft.com/sql-server/sql-server-editions-express)からインストールするか、 **Visual Studio インストーラー**を使用してインストールします。 **Visual Studio インストーラー**では、SQL Server Express LocalDB を **.net デスクトップ開発**ワークロードの一部として、または個々のコンポーネントとしてインストールできます。

2. 次の手順に従って、Northwind サンプルデータベースをインストールします。

    1. Visual Studio で、 **[SQL Server オブジェクトエクスプローラー]** ウィンドウを開きます。 (**SQL Server オブジェクトエクスプローラー**は、Visual Studio インストーラーの**データストレージと処理**ワークロードの一部としてインストールされます)。 **[SQL Server]** ノードを展開します。 LocalDB インスタンスを右クリックし、 **[新しいクエリ]** をクリックします。

       クエリエディターウィンドウが開きます。

    2. [Northwind transact-sql スクリプト](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true)をクリップボードにコピーします。 この T-sql スクリプトでは、Northwind データベースを最初から作成し、データを設定します。

    3. T-sql スクリプトをクエリエディターに貼り付け、 **[実行]** ボタンをクリックします。

       しばらくすると、クエリの実行が完了し、Northwind データベースが作成されます。

## <a name="create-the-n-tier-solution-and-class-library-to-hold-the-dataset-dataentitytier"></a>データセットを保持する n 層ソリューションとクラスライブラリを作成する (DataEntityTier)
このチュートリアルでは、まず、1 つのソリューションと 2 つのクラス ライブラリ プロジェクトを作成します。 最初のクラスライブラリは、データセット (生成された型指定された `DataSet` クラスと、アプリケーションのデータを保持する Datatable) を保持します。 このプロジェクトは、アプリケーションのデータ エンティティ層として使用され、通常は中間層に配置されます。 データセットは初期データセットを作成し、コードを自動的に2つのクラスライブラリに分割します。

> [!NOTE]
> **[OK]** をクリックする前に、必ずプロジェクトとソリューションに適切な名前を付けてください。 これにより、チュートリアルの完了が容易になります。

### <a name="to-create-the-n-tier-solution-and-dataentitytier-class-library"></a>n 層ソリューションと DataEntityTier クラス ライブラリを作成するには

1. Visual Studio の **[ファイル]** メニューで､ **[新規作成]**  >  **[プロジェクト]** を選択します。

2. 左側のウィンドウで、**ビジュアルC#** または**Visual Basic**を展開し、 **[Windows デスクトップ]** を選択します。

3. 中央のペインで、 **[クラスライブラリ]** プロジェクトの種類を選択します。

4. プロジェクトに「**DataEntityTier**」という名前を付けます。

5. ソリューションに**NTierWalkthrough**という名前を指定し、[ **OK]** をクリックします。

     DataEntityTier プロジェクトを含む NTierWalkthrough ソリューションが作成され、**ソリューション エクスプローラー**に追加されます。

## <a name="create-the-class-library-to-hold-the-tableadapters-dataaccesstier"></a>Tableadapter を保持するクラスライブラリを作成する (Dataている)
DataEntityTier プロジェクトを作成したら、次に、クラス ライブラリ プロジェクトをもう 1 つ作成します。 このプロジェクトは生成された Tableadapter を保持し、アプリケーションの*データアクセス層*と呼ばれます。 データ アクセス層は、データベースへの接続に必要な情報を格納し、通常、中間層に置かれます。

### <a name="to-create-a-separate-class-library-for-the-tableadapters"></a>Tableadapter 用に個別のクラスライブラリを作成するには

1. **ソリューション エクスプローラー**でソリューションを右クリックし、 **[追加]**  >  **[新しいプロジェクト]** を選択します。

2. **[新しいプロジェクト]** ダイアログボックスの中央のペインで、 **[クラスライブラリ]** を選択します。

3. **プロジェクトに名前を指定**し、 **[OK]** を選択します。

     DataAccessTier プロジェクトが作成され、NTierWalkthrough ソリューションに追加されます。

## <a name="create-the-dataset"></a>データセットを作成する
次に、型指定されたデータセットを作成します。 型指定されたデータセットは、データセットクラス (`DataTables` クラスを含む) と `TableAdapter` クラスの両方で1つのプロジェクトに作成されます。 (すべてのクラスが1つのファイルに生成されます)。データセットと Tableadapter を別々のプロジェクトに分割すると、そのデータセットクラスは他のプロジェクトに移動され、`TableAdapter` クラスは元のプロジェクトに残ります。 そのため、最終的に Tableadapter を含むデータセットをプロジェクトに作成します (Dataているプロジェクト)。 データセットを作成するには、**データソース構成ウィザード**を使用します。

> [!NOTE]
> 接続を作成するには、Northwind サンプル データベースへのアクセス権を持っている必要があります。 Northwind サンプルデータベースを設定する方法については、「[方法: サンプルデータベースをインストール](../data-tools/installing-database-systems-tools-and-samples.md)する」を参照してください。

### <a name="to-create-the-dataset"></a>データセットを作成するには

1. **ソリューションエクスプローラー**で [ **data]** を選択します。

2. **[データ]** メニューの **[データソースの表示]** をクリックします。

   **[データ ソース]** ウィンドウが開きます。

3. **[データ ソース]** ウィンドウで、 **[新しいデータ ソースの追加]** をクリックして**データ ソース構成ウィザード**を起動します。

4. **[データソースの種類を選択]** ページで、 **[データベース]** を選択し、 **[次へ]** を選択します。

5. **[データ接続の選択]** ページで、次のいずれかの操作を行います。

     Northwind サンプル データベースへのデータ接続がドロップダウン リストに表示されている場合は選択します。

     -または-

     **[新しい接続]** を選択して **[接続の追加]** ダイアログボックスを開きます。

6. データベースにパスワードが必要な場合は、機密データを含めるオプションを選択し、 **[次へ]** をクリックします。

    > [!NOTE]
    > SQL Server に接続するのではなく、ローカル データベース ファイルを選択した場合は、ファイルをプロジェクトに追加するかどうかをたずねるメッセージが表示されます。 **[はい]** を選択して、データベースファイルをプロジェクトに追加します。

7. **[アプリケーション構成ファイルに接続文字列を保存]** ページで **[次へ]** を選択します。

8. **[データベース オブジェクトの選択]** ページの **[テーブル]** ノードを展開します。

9. **Customers**テーブルと**Orders**テーブルのチェックボックスをオンにし、 **[完了]** を選択します。

     NorthwindDataSet が DataAccessTier プロジェクトに追加され、 **[データ ソース]** ウィンドウに表示されます。

## <a name="separate-the-tableadapters-from-the-dataset"></a>データセットから Tableadapter を分離する
データセットを作成したら、生成されたデータセット クラスを TableAdapter から分離します。 これを行うには、 **[DataSet プロジェクト]** プロパティを、分離されたデータセット クラスを格納するプロジェクトの名前に設定します。

### <a name="to-separate-the-tableadapters-from-the-dataset"></a>データセットと TableAdapter を分離するには

1. **ソリューション エクスプローラー**で **NorthwindDataSet.xsd** をダブルクリックし、**データセット デザイナー**でデータセットを開きます。

2. デザイナーで空の領域を選択します。

3. **[プロパティ]** ウィンドウで **[DataSet プロジェクト]** ノードを見つけます。

4. **[データセットプロジェクト]** ボックスの一覧で **[dataentitytier]** を選択します。

5. **[ビルド]** メニューの **[ソリューションのビルド]** を選択します。

   データセットと TableAdapter が、2 つのクラス ライブラリ プロジェクトに分離されます。 データセット全体 (`DataAccessTier`) に最初に含まれていたプロジェクトには、Tableadapter だけが含まれるようになりました。 **Dataset プロジェクト**プロパティ (`DataEntityTier`) に指定されたプロジェクトには、型指定されたデータセット ( *NorthwindDataSet* (または*NorthwindDataSet.Dataset.Designer.cs*)) が含まれています。

> [!NOTE]
> **[DataSet プロジェクト]** プロパティを設定してデータセットと TableAdapter を分離する場合でも、プロジェクト内の既存のデータセット部分クラスは自動的には移動されません。 既存のデータセット部分クラスは、手動でデータセット プロジェクトに移動する必要があります。

## <a name="create-a-new-service-application"></a>新しいサービスアプリケーションの作成
このチュートリアルでは、WCF サービスを使用してデータアクセス層にアクセスする方法を説明します。そのため、新しい WCF サービスアプリケーションを作成しましょう。

### <a name="to-create-a-new-wcf-service-application"></a>新しい WCF サービス アプリケーションを作成するには

1. **ソリューション エクスプローラー**でソリューションを右クリックし、 **[追加]**  >  **[新しいプロジェクト]** を選択します。

2. **[新しいプロジェクト]** ダイアログボックスの左側のペインで、 **[WCF]** を選択します。 中央のペインで、 **[WCF サービスライブラリ]** を選択します。

3. プロジェクトに**DataService**という名前を指定し、[ **OK]** を選択します。

     DataService プロジェクトが作成されて NTierWalkthrough ソリューションに追加されます。

## <a name="create-methods-in-the-data-access-tier-to-return-the-customers-and-orders-data"></a>顧客と注文データを返すためのメソッドをデータアクセス層に作成する
データサービスは、`GetCustomers` と `GetOrders`の2つのメソッドをデータアクセス層で呼び出す必要があります。 これらのメソッドは、Northwind `Customers` テーブルと `Orders` テーブルを返します。 `DataAccessTier` プロジェクトで `GetCustomers` および `GetOrders` メソッドを作成します。

### <a name="to-create-a-method-in-the-data-access-tier-that-returns-the-customers-table"></a>Customers テーブルを返すメソッドをデータ アクセス層に作成するには

1. **ソリューションエクスプローラー**で、 **NorthwindDataset**をダブルクリックしてデータセットを開きます。

2. **CustomersTableAdapter**を右クリックし、 **[クエリの追加]** をクリックします。

3. **[コマンドの種類を選択します]** ページで、 **[SQL ステートメントを使用する]** の既定値を受け入れ、 **[次へ]** をクリックします。

4. **[クエリの種類の選択]** ページで、 **[複数行を返す SELECT]** の既定値を受け入れ、 **[次へ]** をクリックします。

5. **[SQL SELECT ステートメントの指定]** ページで、既定のクエリを受け入れ、 **[次へ]** をクリックします。

6. **[生成するメソッドの選択]** ページで、 **[DataTable を返す]** セクションの **[メソッド名]** に「**GetCustomers**」と入力します。

7. **[完了]** をクリックします。

### <a name="to-create-a-method-in-the-data-access-tier-that-returns-the-orders-table"></a>Orders テーブルを返すメソッドをデータ アクセス層に作成するには

1. **[OrdersTableAdapter]** を右クリックし、 **[クエリの追加]** をクリックします。

2. **[コマンドの種類を選択します]** ページで、 **[SQL ステートメントを使用する]** の既定値を受け入れ、 **[次へ]** をクリックします。

3. **[クエリの種類の選択]** ページで、 **[複数行を返す SELECT]** の既定値を受け入れ、 **[次へ]** をクリックします。

4. **[SQL SELECT ステートメントの指定]** ページで、既定のクエリを受け入れ、 **[次へ]** をクリックします。

5. **[生成するメソッドの選択]** ページで、 **[DataTable を返す]** セクションの **[メソッド名]** に「**GetOrders**」と入力します。

6. **[完了]** をクリックします。

7. **[ビルド]** メニューの **[ソリューションのビルド]** をクリックします。

## <a name="add-a-reference-to-the-data-entity-and-data-access-tiers-to-the-data-service"></a>データサービスにデータエンティティとデータアクセス層への参照を追加する
データ サービスはデータセットと TableAdapter の情報を必要とするため、**DataEntityTier** プロジェクトおよび **DataAccessTier** プロジェクトへの参照を追加します。

### <a name="to-add-references-to-the-data-service"></a>データ サービスに参照を追加するには

1. **ソリューション エクスプローラー**で、 **[DataService]** を右クリックし、 **[参照の追加]** をクリックします。

2. **[参照の追加]** ダイアログ ボックスの **[プロジェクト]** タブをクリックします。

3. **[DataAccessTier]** プロジェクトと **[DataEntityTier]** プロジェクトの両方を選択します。

4. **[OK]** をクリックします。

## <a name="add-functions-to-the-service-to-call-the-getcustomers-and-getorders-methods-in-the-data-access-tier"></a>サービスに関数を追加して、データアクセス層で GetCustomers メソッドおよび Getcustomers メソッドを呼び出します。
これで、データを返すメソッドをデータ アクセス層に含めることができました。次に、データ サービスにメソッドを作成して、データ アクセス層のメソッドを呼び出します。

> [!NOTE]
> C# プロジェクトの場合は、次のコードをコンパイルするために `System.Data.DataSetExtensions` アセンブリへの参照を追加する必要があります。

### <a name="to-create-the-getcustomers-and-getorders-functions-in-the-data-service"></a>データ サービスに GetCustomers 関数と GetOrders 関数を作成するには

1. **DataService** プロジェクトで、**IService1.vb** または **IService1.cs** をダブルクリックします。

2. **[Add your service operations here]** というコメントの下に、次のコードを追加します。

    ```vb
    <OperationContract()> _
    Function GetCustomers() As DataEntityTier.NorthwindDataSet.CustomersDataTable

    <OperationContract()> _
    Function GetOrders() As DataEntityTier.NorthwindDataSet.OrdersDataTable
    ```

    ```csharp
    [OperationContract]
    DataEntityTier.NorthwindDataSet.CustomersDataTable GetCustomers();

    [OperationContract]
    DataEntityTier.NorthwindDataSet.OrdersDataTable GetOrders();
    ```

3. DataService プロジェクトで、**Service1.vb** または **Service1.cs** をダブルクリックします。

4. **Service1** クラスに次のコードを追加します。

    ```vb
    Public Function GetCustomers() As DataEntityTier.NorthwindDataSet.CustomersDataTable Implements IService1.GetCustomers
        Dim CustomersTableAdapter1 As New DataAccessTier.NorthwindDataSetTableAdapters.CustomersTableAdapter
        Return CustomersTableAdapter1.GetCustomers()
    End Function

    Public Function GetOrders() As DataEntityTier.NorthwindDataSet.OrdersDataTable Implements IService1.GetOrders
        Dim OrdersTableAdapter1 As New DataAccessTier.NorthwindDataSetTableAdapters.OrdersTableAdapter
        Return OrdersTableAdapter1.GetOrders()
    End Function
    ```

    ```csharp
    public DataEntityTier.NorthwindDataSet.CustomersDataTable GetCustomers()
    {
        DataAccessTier.NorthwindDataSetTableAdapters.CustomersTableAdapter
             CustomersTableAdapter1
            = new DataAccessTier.NorthwindDataSetTableAdapters.CustomersTableAdapter();
        return CustomersTableAdapter1.GetCustomers();
    }
    public DataEntityTier.NorthwindDataSet.OrdersDataTable GetOrders()
    {
        DataAccessTier.NorthwindDataSetTableAdapters.OrdersTableAdapter
             OrdersTableAdapter1
            = new DataAccessTier.NorthwindDataSetTableAdapters.OrdersTableAdapter();
        return OrdersTableAdapter1.GetOrders();
    }
    ```

5. **[ビルド]** メニューの **[ソリューションのビルド]** をクリックします。

## <a name="create-a-presentation-tier-to-display-data-from-the-data-service"></a>データサービスからのデータを表示するプレゼンテーション層を作成する
このソリューションには、データアクセス層を呼び出すメソッドを持つデータサービスが含まれているので、データサービスを呼び出してデータをユーザーに提示する別のプロジェクトを作成します。 このチュートリアルでは、Windows フォーム アプリケーションを作成します。これは n 層アプリケーションのプレゼンテーション層です。

### <a name="to-create-the-presentation-tier-project"></a>プレゼンテーション層プロジェクトを作成するには

1. **ソリューション エクスプローラー**でソリューションを右クリックし、 **[追加]**  >  **[新しいプロジェクト]** を選択します。

2. **[新しいプロジェクト]** ダイアログボックスの左側のウィンドウで、 **[Windows デスクトップ]** を選択します。 中央のウィンドウで、 **[Windows フォームアプリ]** を選択します。

3. プロジェクトに「**PresentationTier**」という名前を付け、 **[OK]** をクリックします。

    PresentationTier プロジェクトが作成され、NTierWalkthrough ソリューションに追加されます。

## <a name="set-the-presentationtier-project-as-the-startup-project"></a>プレゼンテーション層プロジェクトをスタートアッププロジェクトとして設定する
**プレゼンテーション層**プロジェクトをソリューションのスタートアッププロジェクトとして設定します。これは、データを表示して操作する実際のクライアントアプリケーションであるためです。

### <a name="to-set-the-new-presentation-tier-project-as-the-startup-project"></a>新しいプレゼンテーション層プロジェクトをスタートアップ プロジェクトとして設定するには

- **ソリューション エクスプローラー**で、 **[PresentationTier]** を右クリックし、 **[スタートアップ プロジェクトに設定]** をクリックします。

## <a name="add-references-to-the-presentation-tier"></a>プレゼンテーション層への参照の追加
クライアント アプリケーションである PresentationTier には、サービスのメソッドにアクセスできるように、データ サービスへのサービス参照が必要です。 また、WCF サービスによる型の共有を有効にするために、データセットへの参照も必要です。 データサービスを介した型の共有を有効にするまで、部分的なデータセットクラスに追加されたコードはプレゼンテーション層で使用できません。 通常は、データテーブルの行や列の変化するイベントに検証コードなどのコードを追加するので、クライアントからこのコードにアクセスすることが必要になる可能性があります。

### <a name="to-add-a-reference-to-the-presentation-tier"></a>プレゼンテーション層に参照を追加するには

1. **ソリューションエクスプローラー**で、 **[プレゼンテーション層]** を右クリックし、 **[参照の追加]** を選択します。

2. **[参照の追加]** ダイアログボックスで、 **[プロジェクト]** タブを選択します。

3. **[Dataentitytier]** を選択し、[ **OK]** を選択します。

### <a name="to-add-a-service-reference-to-the-presentation-tier"></a>プレゼンテーション層にサービス参照を追加するには

1. **ソリューションエクスプローラー**で、 **[プレゼンテーション層]** を右クリックし、 **[サービス参照の追加]** を選択します。

2. **[サービス参照の追加]** ダイアログボックスで、 **[探索]** を選択します。

3. **[Service1]** を選択し、[ **OK]** を選択します。

    > [!NOTE]
    > 現在のコンピューターに複数のサービスがある場合は、このチュートリアルで以前に作成したサービス (`GetCustomers` および `GetOrders` メソッドを含むサービス) を選択します。

## <a name="add-datagridviews-to-the-form-to-display-the-data-returned-by-the-data-service"></a>データサービスによって返されたデータを表示するには、Datagridview をフォームに追加します。
データ サービスへのサービス参照を追加すると、サービスによって返されたデータが **[データ ソース]** ウィンドウに自動的に読み込まれます。

### <a name="to-add-two-data-bound-datagridviews-to-the-form"></a>フォームに 2 つのデータ バインド DataGridView を追加するには

1. **ソリューション エクスプローラー**で、**PresentationTier** プロジェクトを選択します。

2. **[データ ソース]** ウィンドウの **[NorthwindDataSet]** を展開し、 **[Customers]** ノードを見つけます。

3. **[Customers]** ノードを Form1 にドラッグします。

4. **[データ ソース]** ウィンドウの **[Customers]** ノードを展開し、関連する **[Orders]** ノード ( **[Customers]** ノードに入れ子になっている **[Orders]** ノード) を見つけます。

5. 関連する **[Orders]** ノードを Form1 にドラッグします。

6. フォームの空の領域をダブルクリックして、`Form1_Load` イベント ハンドラーを作成します。

7. `Form1_Load` イベント ハンドラーに次のコードを追加します。

    ```vb
    Dim DataSvc As New ServiceReference1.Service1Client
    NorthwindDataSet.Customers.Merge(DataSvc.GetCustomers)
    NorthwindDataSet.Orders.Merge(DataSvc.GetOrders)
    ```

    ```csharp
    ServiceReference1.Service1Client DataSvc =
        new ServiceReference1.Service1Client();
    northwindDataSet.Customers.Merge(DataSvc.GetCustomers());
    northwindDataSet.Orders.Merge(DataSvc.GetOrders());
    ```

## <a name="increase-the-maximum-message-size-allowed-by-the-service"></a>サービスで許容される最大メッセージサイズを増やす
`maxReceivedMessageSize` の既定値は、`Customers` テーブルと `Orders` テーブルから取得したデータを保持するのに十分な大きさではありません。 次の手順では、値を6553600に増やします。 クライアントの値を変更すると、サービス参照が自動的に更新されます。

> [!NOTE]
> 既定のサイズが低く設定されているのは、サービス拒否 (DoS) 攻撃を受けるリスクを低減するためです。 詳細については、「<xref:System.ServiceModel.WSHttpBindingBase.MaxReceivedMessageSize%2A>」を参照してください。

### <a name="to-increase-the-maxreceivedmessagesize-value"></a>maxReceivedMessageSize 値を増やすには

1. **ソリューション エクスプローラー**で、**PresentationTier** プロジェクトの **app.config** ファイルをダブルクリックします。

2. **maxReceivedMessage** サイズ属性を見つけ、値を「`6553600`」に変更します。

## <a name="test-the-application"></a>アプリのテスト
**F5** キーを押してアプリケーションを実行します。 `Customers` テーブルと `Orders` テーブルのデータがデータサービスから取得され、フォームに表示されます。

## <a name="next-steps"></a>次のステップ:
Windows ベース アプリケーションに関連データを保存した後で、アプリケーションの要件によってはさらに操作を追加する必要があります。 たとえば、このアプリケーションに対して次のような拡張を行うことができます。

- データセットへの検証の追加。

- サービスへの、データを更新してデータベースに戻す追加メソッドの追加。

## <a name="see-also"></a>関連項目

- [n 層アプリケーションでのデータセットの操作](../data-tools/work-with-datasets-in-n-tier-applications.md)
- [階層更新](../data-tools/hierarchical-update.md)
- [Visual Studio でのデータへのアクセス](../data-tools/accessing-data-in-visual-studio.md)
