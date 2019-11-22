---
title: 'Walkthrough: Creating an N-Tier Data Application | Microsoft Docs'
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
- n-tier applications, creating
- n-tier applications, walkthroughs
ms.assetid: d15e4d31-2839-48d9-9e0e-2e73404d82a2
caps.latest.revision: 51
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: bd77006eda03b716e3c54c0b5b52ac633a383377
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74299591"
---
# <a name="walkthrough-creating-an-n-tier-data-application"></a>チュートリアル : n 層データ アプリケーションの作成
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

N-tier* data applications are applications that access data and are separated into multiple logical layers, or *tiers*. アプリケーション コンポーネントをこのように別個の層に分離すると、アプリケーションの保守容易性とスケーラビリティが向上します。 これは、ソリューション全体を再設計しなくても 1 つの層に適用できる、新しい技術を簡単に導入できるようにすることで実現されます。 n 層アーキテクチャには、プレゼンテーション層、中間層、およびデータ層が存在します。 通常、中間層には、データ アクセス層、ビジネス ロジック層、および認証や検証などの共有コンポーネントが含まれます。 データ層には、リレーショナル データベースが含まれます。 通常、n 層アプリケーションでは、機密情報が中間層のデータ アクセス層に格納され、プレゼンテーション層にアクセスするエンド ユーザーから分離されます。 For more information, see [N-Tier Data Applications Overview](../data-tools/n-tier-data-applications-overview.md).

 n 層アプリケーションで各層を分離する 1 つの方法は、アプリケーションに組み込む層ごとに別個のプロジェクトを作成することです。 型指定されたデータセットには、生成されたデータセットと `DataSet Project` コードの格納先となるプロジェクトを決定する、`TableAdapter` プロパティが含まれています。

 このチュートリアルでは、**データセット デザイナー**を使用して、別個のクラス ライブラリ プロジェクトにデータセットと `TableAdapter` コードを分離する方法を示します。 After you separate the dataset and TableAdapter code, you will create a [Windows Communication Foundation Services and WCF Data Services in Visual Studio](../data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio.md) service to call into the data access tier. 最後に、プレゼンテーション層として Windows フォーム アプリケーションを作成します。 この層は、データ サービスからデータにアクセスします。

 このチュートリアルでは、次の手順を実行します。

- 複数のプロジェクトを含む新しい n 層ソリューションを作成する。

- この n 層ソリューションに 2 つのクラス ライブラリ プロジェクトを追加する。

- **データ ソース構成ウィザード**を実行して、型指定されたデータセットを作成する。

- Separate the generated [TableAdapters](https://msdn.microsoft.com/library/09416de9-134c-4dc7-8262-6c8d81e3f364) and dataset code into discrete projects.

- データ アクセス層を呼び出す Windows Communication Foundation (WCF) サービスを作成する。

- このサービスに、データ アクセス層からデータを取得する関数を作成する。

- プレゼンテーション層として機能する Windows フォーム アプリケーションを作成する。

- Windows フォーム コントロールを作成し、データ ソースにバインドする。

- データ テーブルにデータを読み込むコードを記述する。

  ![link to video](../data-tools/media/playvideo.gif "PlayVideo") For a video version of this topic, see [Video How to: Creating an N-Tier Data Application](https://go.microsoft.com/fwlink/?LinkId=115188).

## <a name="prerequisites"></a>必要条件
 このチュートリアルを完了するには、次の条件が必要です。

- Northwind サンプル データベースにアクセスします。

## <a name="creating-the-n-tier-solution-and-class-library-to-hold-the-dataset-dataentitytier"></a>n 層ソリューションの作成とデータセットを保持するクラス ライブラリ (DataEntityTier) の作成
 このチュートリアルでは、まず、1 つのソリューションと 2 つのクラス ライブラリ プロジェクトを作成します。 最初のクラス ライブラリは、データセット (生成した型指定された DataSet クラスと、アプリケーションのデータを保持する DataTable) を保持します。 このプロジェクトは、アプリケーションのデータ エンティティ層として使用され、通常は中間層に配置されます。 The Dataset Designer is used to create the initial dataset and automatically separate the code into the two class libraries.

> [!NOTE]
> **[OK]** をクリックする前に、必ずプロジェクトとソリューションに適切な名前を付けてください。 これにより、チュートリアルの完了が容易になります。

#### <a name="to-create-the-n-tier-solution-and-dataentitytier-class-library"></a>n 層ソリューションと DataEntityTier クラス ライブラリを作成するには

1. From the **File** menu, create a new project.

    > [!NOTE]
    > The **Dataset Designer** is supported in [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] and C# projects. 新しいプロジェクトはこれらの言語のどちらかで作成してください。

2. In the **New Project** dialog box, in the **Project types** pane, click **Windows**.

3. Click the **Class Library** template.

4. プロジェクトに「**DataEntityTier**」という名前を付けます。

5. Name the solution **NTierWalkthrough**.

6. **[OK]** をクリックします。

     DataEntityTier プロジェクトを含む NTierWalkthrough ソリューションが作成され、**ソリューション エクスプローラー**に追加されます。

## <a name="creating-the-class-library-to-hold-the-tableadapters-dataaccesstier"></a>TableAdapter (DataAccessTier) を保持するクラス ライブラリの作成
 DataEntityTier プロジェクトを作成したら、次に、クラス ライブラリ プロジェクトをもう 1 つ作成します。 This project will hold the generated `TableAdapter`s and is called the *data access tier* of the application. データ アクセス層は、データベースへの接続に必要な情報を格納し、通常、中間層に置かれます。

#### <a name="to-create-the-new-class-library-for-the-tableadapters"></a>TableAdapter を保持する新しいクラス ライブラリを作成するには

1. From the **File** menu, add a new project to the NTierWalkthrough solution.

2. In the **New Project** dialog box, in the **Templates** pane, click **Class Library**.

3. Name the project **DataAccessTier** and click **OK**.

     DataAccessTier プロジェクトが作成され、NTierWalkthrough ソリューションに追加されます。

## <a name="creating-the-dataset"></a>データセットの作成
 次に、型指定されたデータセットを作成します。 型指定されたデータセットは、データセット クラス (DataTable クラスを含む) と `TableAdapter` クラスの両方を含む単一のプロジェクトとして作成されます (All classes are generated into a single file.) When you separate the dataset and `TableAdapter`s into different projects, it is the dataset class that is moved to the other project, leaving the `TableAdapter` classes in the original project. このため、最終的に `TableAdapter` が含まれるプロジェクト (DataAccessTier プロジェクト) にデータセットを作成します。 You will create the dataset by using the **Data Source Configuration Wizard**.

> [!NOTE]
> 接続を作成するには、Northwind サンプル データベースへのアクセス権を持っている必要があります。

#### <a name="to-create-the-dataset"></a>データセットを作成するには

1. Click DataAccessTier in **Solution Explorer**.

2. **[データ]** メニューの **[データ ソースの表示]** をクリックします。

3. In the **Data Sources** window, click **Add New Data Source** to start the **Data Source Configuration Wizard**.

4. On the **Choose a Data Source Type** page, click **Database** and then click **Next**.

5. **[データ接続の選択]** ページで、次のいずれかの操作を行います。

     Northwind サンプル データベースへのデータ接続がドロップダウン リストに表示されている場合は、これをクリックします。

     -または-

     Click **New Connection** to open the **Add Connection** dialog box.

6. データベースにパスワードが必要な場合は、該当するオプションを選択して重要情報を含め、 **[次へ]** をクリックします。

    > [!NOTE]
    > SQL Server に接続するのではなく、ローカル データベース ファイルを選択した場合は、ファイルをプロジェクトに追加するかどうかをたずねるメッセージが表示されます。 Click **Yes** to add the database file to the project.

7. Click **Next** on the **Save the Connection String to the Application Configuration File** page.

8. **[データベース オブジェクトの選択]** ページの **[テーブル]** ノードを展開します。

9. Click the check boxes for the **Customers** and **Orders** tables, and then click **Finish**.

     NorthwindDataSet が DataAccessTier プロジェクトに追加され、 **[データ ソース]** ウィンドウに表示されます。

## <a name="separating-the-tableadapters-from-the-dataset"></a>データセットと TableAdapter の分離
 データセットを作成したら、生成されたデータセット クラスを TableAdapter から分離します。 これを行うには、 **[DataSet プロジェクト]** プロパティを、分離されたデータセット クラスを格納するプロジェクトの名前に設定します。

#### <a name="to-separate-the-tableadapters-from-the-dataset"></a>データセットと TableAdapter を分離するには

1. **ソリューション エクスプローラー**で **NorthwindDataSet.xsd** をダブルクリックし、**データセット デザイナー**でデータセットを開きます。

2. デザイナーの空の領域をクリックします。

3. **[プロパティ]** ウィンドウで **[DataSet プロジェクト]** ノードを見つけます。

4. In the **DataSet Project** list, click **DataEntityTier**.

5. **[ビルド]** メニューの **[ソリューションのビルド]** をクリックします。

   データセットと TableAdapter が、2 つのクラス ライブラリ プロジェクトに分離されます。 最初にデータセット全体 (DataAccessTier) を含んでいたプロジェクトには、現在は TableAdapter しか含まれません。 The project designated in the **DataSet Project** property (DataEntityTier) contains the typed dataset: NorthwindDataSet.Dataset.Designer.vb (or NorthwindDataSet.Dataset.Designer.cs).

> [!NOTE]
> **[DataSet プロジェクト]** プロパティを設定してデータセットと TableAdapter を分離する場合でも、プロジェクト内の既存のデータセット部分クラスは自動的には移動されません。 既存のデータセット部分クラスは、手動でデータセット プロジェクトに移動する必要があります。

## <a name="creating-a-new-service-application"></a>新しいサービス アプリケーションの作成
 このチュートリアルでは WCF サービスを使用してデータ アクセス層にアクセスする方法を説明するので、新しい WCF サービス アプリケーションを作成します。

#### <a name="to-create-a-new-wcf-service-application"></a>新しい WCF サービス アプリケーションを作成するには

1. From the **File** menu, add a new project to the NTierWalkthrough solution.

2. In the **New Project** dialog box, in the **Project types** pane, click **WCF**. In the **Templates** pane, click **WCF Service Library**.

3. Name the project **DataService** and click **OK**.

     DataService プロジェクトが作成されて NTierWalkthrough ソリューションに追加されます。

## <a name="creating-methods-in-the-data-access-tier-to-return-the-customers-and-orders-data"></a>Customers および Orders のデータを返すデータ アクセス層のメソッドの作成
 データ サービスは、データ アクセス層の 2 つのメソッド (GetCustomers および GetOrders) を呼び出す必要があります。 これらのメソッドは、Northwind の Customers テーブルと Orders テーブルを返します。 GetCustomers メソッドと GetOrders メソッドは、DataAccessTier プロジェクトに作成します。

#### <a name="to-create-a-method-in-the-data-access-tier-that-returns-the-customers-table"></a>Customers テーブルを返すメソッドをデータ アクセス層に作成するには

1. In **Solution Explorer**, double-click NorthwindDataset.xsd to open the dataset in the Dataset Designer.

2. Right-click CustomersTableAdapter and click **Add Query** to edit the Tableadapter.

3. **[コマンドの種類を選択します]** ページで、 **[SQL ステートメントを使用する]** の既定値を受け入れ、 **[次へ]** をクリックします。

4. **[クエリの種類の選択]** ページで、 **[複数行を返す SELECT]** の既定値を受け入れ、 **[次へ]** をクリックします。

5. **[SQL SELECT ステートメントの指定]** ページで、既定のクエリを受け入れ、 **[次へ]** をクリックします。

6. **[生成するメソッドの選択]** ページで、 **[DataTable を返す]** セクションの **[メソッド名]** に「**GetCustomers**」と入力します。

7. **[完了]** をクリックします。

#### <a name="to-create-a-method-in-the-data-access-tier-that-returns-the-orders-table"></a>Orders テーブルを返すメソッドをデータ アクセス層に作成するには

1. Right-click OrdersTableAdapter and click **Add Query**.

2. **[コマンドの種類を選択します]** ページで、 **[SQL ステートメントを使用する]** の既定値を受け入れ、 **[次へ]** をクリックします。

3. **[クエリの種類の選択]** ページで、 **[複数行を返す SELECT]** の既定値を受け入れ、 **[次へ]** をクリックします。

4. **[SQL SELECT ステートメントの指定]** ページで、既定のクエリを受け入れ、 **[次へ]** をクリックします。

5. **[生成するメソッドの選択]** ページで、 **[DataTable を返す]** セクションの **[メソッド名]** に「**GetOrders**」と入力します。

6. **[完了]** をクリックします。

7. **[ビルド]** メニューの **[ソリューションのビルド]** をクリックします。

## <a name="adding-a-reference-to-the-data-entity-and-data-access-tiers-to-the-data-service"></a>データ サービスへの、データ エンティティ層およびデータ アクセス層への参照の追加
 データ サービスはデータセットと TableAdapter の情報を必要とするため、DataEntityTier プロジェクトおよび DataAccessTier プロジェクトへの参照を追加します。

#### <a name="to-add-references-to-the-data-service"></a>データ サービスに参照を追加するには

1. Right-click DataService in **Solution Explorer** and click **Add Reference**.

2. **[参照の追加]** ダイアログ ボックスの **[プロジェクト]** タブをクリックします。

3. **[DataAccessTier]** プロジェクトと **[DataEntityTier]** プロジェクトの両方を選択します。

4. **[OK]** をクリックします。

## <a name="adding-functions-to-the-service-to-call-the-getcustomers-and-getorders-methods-in-the-data-access-tier"></a>データ アクセス層の GetCustomers メソッドおよび GetOrders メソッドを呼び出す関数のサービスへの追加
 これで、データを返すメソッドをデータ アクセス層に含めることができました。次に、データ サービスにメソッドを作成して、データ アクセス層のメソッドを呼び出します。

> [!NOTE]
> C# プロジェクトの場合は、次のコードをコンパイルするために `System.Data.DataSetExtensions` アセンブリへの参照を追加する必要があります。

#### <a name="to-create-the-getcustomers-and-getorders-functions-in-the-data-service"></a>データ サービスに GetCustomers 関数と GetOrders 関数を作成するには

1. In the **DataService** project, double-click IService1.vb or IService1.cs.

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

3. DataService プロジェクトで、Service1.vb または Service1.cs をダブルクリックします。

4. Service1 クラスに次のコードを追加します。

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

## <a name="creating-a-presentation-tier-to-display-data-from-the-data-service"></a>データ サービスのデータを表示するプレゼンテーション層の作成
 これで、データ アクセス層を呼び出すメソッドを持つデータ サービスをソリューションに含めることができました。次に、データ サービスを呼び出してデータをユーザーに表示する別のプロジェクトを作成します。 このチュートリアルでは、Windows フォーム アプリケーションを作成します。これは n 層アプリケーションのプレゼンテーション層です。

#### <a name="to-create-the-presentation-tier-project"></a>プレゼンテーション層プロジェクトを作成するには

1. From the **File** menu, add a new project to the NTierWalkthrough solution.

2. In the **New Project** dialog box, in the **Project types** pane, click **Windows**. **[テンプレート]** ペインの **[Windows フォーム アプリケーション]** をクリックします。

3. プロジェクトに「**PresentationTier**」という名前を付け、 **[OK]** をクリックします。

4. PresentationTier プロジェクトが作成され、NTierWalkthrough ソリューションに追加されます。

## <a name="setting-the-presentationtier-project-as-the-startup-project"></a>スタートアップ プロジェクトとしての PresentationTier プロジェクトの設定
 プレゼンテーション層は、データを提示して対話するために使用する実際のクライアント アプリケーションです。このため、PresentationTier プロジェクトをスタートアップ プロジェクトとして設定する必要があります。

#### <a name="to-set-the-new-presentation-tier-project-as-the-startup-project"></a>新しいプレゼンテーション層プロジェクトをスタートアップ プロジェクトとして設定するには

- **ソリューション エクスプローラー**で、 **[PresentationTier]** を右クリックし、 **[スタートアップ プロジェクトに設定]** をクリックします。

## <a name="adding-references-to-the-presentation-tier"></a>プレゼンテーション層への参照の追加
 クライアント アプリケーションである PresentationTier には、サービスのメソッドにアクセスできるように、データ サービスへのサービス参照が必要です。 また、WCF サービスによる型の共有を有効にするために、データセットへの参照も必要です。 データセット部分クラスに追加したコードは、データ サービスを介した型の共有を有効にするまで、プレゼンテーション層で使用することはできません。 通常は、データ テーブルの行と列の変更イベントに検証などのコードを追加するため、クライアントからこのコードにアクセスすることが必要になります。

#### <a name="to-add-a-reference-to-the-presentation-tier"></a>プレゼンテーション層に参照を追加するには

1. In **Solution Explorer**, right-click PresentationTier and click **Add Reference**.

2. In the **Add Reference** dialog box, click the **Projects** tab.

3. Select **DataEntityTier** and click **OK**.

#### <a name="to-add-a-service-reference-to-the-presentation-tier"></a>プレゼンテーション層にサービス参照を追加するには

1. In **Solution Explorer**, right-click PresentationTier and click **Add Service Reference**.

2. **[サービス参照の追加]** ダイアログ ボックスで **[探索]** をクリックします。

3. Select **Service1** and click **OK**.

    > [!NOTE]
    > 現在のコンピューターに複数のサービスがある場合は、このチュートリアルで以前に作成したサービス (GetCustomers メソッドおよび GetOrders メソッドを含むサービス) を選択します。

## <a name="adding-datagridviews-to-the-form-to-display-the-data-returned-by-the-data-service"></a>フォームへの DataGridView の追加とデータ サービスから返されたデータの表示
 データ サービスへのサービス参照を追加すると、サービスによって返されたデータが **[データ ソース]** ウィンドウに自動的に読み込まれます。

#### <a name="to-add-two-data-bound-datagridviews-to-the-form"></a>フォームに 2 つのデータ バインド DataGridView を追加するには

1. In **Solution Explorer**, select the PresentationTier project.

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

## <a name="increasing-the-maximum-message-size-allowed-by-the-service"></a>サービスで許可されるメッセージの最大サイズの増加
 サービスは Customers テーブルと Orders テーブルからデータを返すため、maxReceivedMessageSize の既定値ではデータを保持するのに十分ではなく、この値を大きくする必要があります。 このチュートリアルでは、値を 6553600 に変更します。 クライアントで値を変更すると、サービス参照が自動的に更新されます。

> [!NOTE]
> 既定のサイズが低く設定されているのは、サービス拒否 (DoS) 攻撃を受けるリスクを低減するためです。 詳細については、「<xref:System.ServiceModel.WSHttpBindingBase.MaxReceivedMessageSize%2A>」を参照してください。

#### <a name="to-increase-the-maxreceivedmessagesize-value"></a>maxReceivedMessageSize 値を増やすには

1. In **Solution Explorer**, double-click the app.config file in the PresentationTier project.

2. **maxReceivedMessage** サイズ属性を見つけ、値を「`6553600`」に変更します。

## <a name="testing-the-application"></a>アプリケーションのテスト
 アプリケーションを実行します。 データがデータ サービスから取得され、フォームに表示されます。

#### <a name="to-test-the-application"></a>アプリケーションをテストするには

1. F5 キーを押します。

2. Customers テーブルと Orders テーブルのデータがデータ サービスから取得され、フォームに表示されます。

## <a name="next-steps"></a>次のステップ
 Windows ベース アプリケーションに関連データを保存した後で、アプリケーションの要件によってはさらに操作を追加する必要があります。 たとえば、このアプリケーションに対して次のような拡張を行うことができます。

- データセットへの検証の追加。 For information, see [Walkthrough: Adding Validation to an N-Tier Data Application](https://msdn.microsoft.com/library/b35d072c-31f0-49ba-a225-69177592c265).

- サービスへの、データを更新してデータベースに戻す追加メソッドの追加。

## <a name="see-also"></a>参照
 [Work with datasets in n-tier applications](../data-tools/work-with-datasets-in-n-tier-applications.md) [Hierarchical update](../data-tools/hierarchical-update.md) [Accessing data in Visual Studio](../data-tools/accessing-data-in-visual-studio.md)
