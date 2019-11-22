---
title: 'Walkthrough: Creating a WCF Data Service with WPF and Entity Framework | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
helpviewer_keywords:
- data services in Visual Studio
- WCF Data Services, Visual Studio
- ADO.NET Data Services, Visual Studio
- WCF data services in Visual Studio
ms.assetid: da66ad1b-a25d-485c-af13-2d18f0422e3d
caps.latest.revision: 28
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 5abbb647f93c991d2de626a84e82f47e03f6f71e
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74299614"
---
# <a name="walkthrough-creating-a-wcf-data-service-with-wpf-and-entity-framework"></a>チュートリアル: WPF と Entity Framework を使用した WCF データ サービスの作成
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

This walkthrough demonstrates how to create a simple [!INCLUDE[ss_data_service](../includes/ss-data-service-md.md)] that is hosted in an [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] Web application and then access it from a Windows Forms application.

 このチュートリアルでは、次の作業を行います。

- [!INCLUDE[ss_data_service](../includes/ss-data-service-md.md)] をホストする Web アプリケーションを作成します。

- Northwind データベースの Customers テーブルを表す[!INCLUDE[adonet_edm](../includes/adonet-edm-md.md)]を作成します。

- [!INCLUDE[ss_data_service](../includes/ss-data-service-md.md)] を作成します。

- クライアント アプリケーションを作成し、[!INCLUDE[ss_data_service](../includes/ss-data-service-md.md)] への参照を追加します。

- サービスへのデータ バインディングを有効にし、ユーザー インターフェイスを生成します。

- 必要に応じて、アプリケーションにフィルター処理機能を追加します。

## <a name="prerequisites"></a>必要条件
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- Northwind サンプル データベース。

     開発用コンピューターにこのデータベースがない場合は、 [Microsoft ダウンロード センター](https://go.microsoft.com/fwlink/?LinkID=98088)からダウンロードできます。 For instructions, see [Downloading Sample Databases](https://msdn.microsoft.com/library/ef9d69a1-9461-43fe-94bb-7c836754bcb5).

## <a name="creating-the-service"></a>サービスの作成
 [!INCLUDE[ss_data_service](../includes/ss-data-service-md.md)] を作成するには、Web プロジェクトを追加し、[!INCLUDE[adonet_edm](../includes/adonet-edm-md.md)]を作成した後、そのモデルからサービスを作成します。

 最初に、サービスをホストする Web プロジェクトを追加します。

 [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]

#### <a name="to-create-the-web-project"></a>Web プロジェクトを作成するには

1. On the menu bar, choose **File**, **New**,  **Project**.

2. **[新しいプロジェクト]** ダイアログ ボックスの **[Visual Basic]** または **[Visual C#]** ノードを展開して、 **[Web]** ノードをクリックし、 **[ASP.NET Web アプリケーション]** テンプレートをクリックします。

3. **[名前]** ボックスに「**NorthwindWeb**」と入力し、 **[OK]** をクリックします。

4. **[新しい ASP.NET プロジェクト]** ダイアログ ボックスの **[テンプレートの選択]** リストで **[なし]** を選択し、 **[OK]** ボタンをクリックします。

   この手順では、Northwind データベースにある Customers テーブルを表す[!INCLUDE[adonet_edm](../includes/adonet-edm-md.md)]を作成します。

#### <a name="to-create-the-entity-data-model"></a>Entity Data Model を作成するには

1. On the menu bar, choose **Project**, **Add New Item**.

2. **[新しい項目の追加]** ダイアログ ボックスで **[データ]** ノードを選択し、 **[ADO.NET エンティティ データ モデル]** 項目を選択します。

3. In the **Name** text box, enter `NorthwindModel`, and then choose the **Add** button.

    Entity Data Model ウィザードが表示されます。

4. エンティティ データ モデル ウィザードの **[モデルのコンテンツの選択]** ページで、 **[データベースから EF デザイナー]** 項目を選択してから **[次へ]** ボタンを選択します。

5. **[データ接続の選択]** ページで、次のいずれかの操作を行います。

   - Northwind サンプル データベースへのデータ接続がドロップダウン リストに表示されている場合は選択します。

        -または-

   - **[新しい接続]** を選択して、新しいデータ接続を構成します。 For more information, see [Add new connections](../data-tools/add-new-connections.md).

6. データベースにパスワードが必要な場合は、 **[はい、重要情報を接続文字列に含めます。]** を選択し、 **[次へ]** をクリックします。

   > [!NOTE]
   > ダイアログ ボックスが表示された場合は、 **[はい]** をクリックしてファイルをプロジェクトに保存します。

7. **[バージョンの選択]** ページで **[Entity Framework 5.0]** オプション ボタンを選択し、 **[次へ]** をクリックします。

   > [!NOTE]
   > WCF サービス で Entity Framework 6 の最新バージョンを使用するには、WCF Data Services Entity Framework Provider NuGet パッケージのインストールが必要になります。 See [Using WCF Data Services 5.6.0 with Entity Framework 6+](https://devblogs.microsoft.com/odata/using-wcf-data-services-5-6-0-with-entity-framework-6/).

8. **[データベース オブジェクトの選択]** ページで、 **[テーブル]** ノードを展開し、 **[Customers]** チェック ボックスをオンにして **[完了]** をクリックします。

    エンティティ モデル ダイアグラムが表示され、プロジェクトに NorthwindModel.edmx ファイルが追加されます。

   この手順では、データ サービスを作成してテストします。

#### <a name="to-create-the-data-service"></a>データ サービスを作成するには

1. On the menu bar, choose **Project**, **Add New Item**.

2. **[新しい項目の追加]** ダイアログ ボックスで **[Web]** ノードを選択し、 **[WCF Data Service 5.6]** 項目を選択します。

3. In the **Name** text box, enter `NorthwindCustomers`, and then choose the **Add** button.

    The NorthwindCustomers.svc file appears in the **Code Editor**.

4. **コード エディター**で、最初の `TODO:` コメントを探して、コードを次のコードに置き換えます。

    [!code-csharp[WCFDataServiceWalkthrough#1](../snippets/csharp/VS_Snippets_VBCSharp/wcfdataservicewalkthrough/cs/northwindcustomers.svc.cs#1)]
    [!code-vb[WCFDataServiceWalkthrough#1](../snippets/visualbasic/VS_Snippets_VBCSharp/wcfdataservicewalkthrough/vb/northwindcustomers.svc.vb#1)]

5. `InitializeService` イベント ハンドラーのコメントを次のコードに置き換えます。

    [!code-csharp[WCFDataServiceWalkthrough#2](../snippets/csharp/VS_Snippets_VBCSharp/wcfdataservicewalkthrough/cs/northwindcustomers.svc.cs#2)]
    [!code-vb[WCFDataServiceWalkthrough#2](../snippets/visualbasic/VS_Snippets_VBCSharp/wcfdataservicewalkthrough/vb/northwindcustomers.svc.vb#2)]

6. On the menu bar, choose **Debug**, **Start Without Debugging** to run the service. ブラウザー ウィンドウが開き、そのサービスの XML スキーマが表示されます。

7. In the **Address** bar, enter `Customers` at the end of the URL for NorthwindCustomers.svc, and then choose the **ENTER** key.

    Customers テーブル内のデータの XML 表現が表示されます。

   > [!NOTE]
   > Internet Explorer がデータを誤って RSS フィードとして解釈する場合があります。 RSS フィードを表示するオプションが無効になっていることを確認してください。 For more information, see [Troubleshooting Service References](../data-tools/troubleshooting-service-references.md).

8. ブラウザー ウィンドウを閉じます。

   次の手順では、サービスを使用する Windows フォーム クライアント アプリケーションを作成します。

## <a name="creating-the-client-application"></a>クライアント アプリケーションの作成
 クライアント アプリケーションを作成するには、2 つ目のプロジェクトを追加し、そのプロジェクトにサービス参照を追加します。そして、データ ソースを構成し、サービスから取得したデータを表示するユーザー インターフェイスを作成します。

 最初に、Windows フォーム プロジェクトをソリューションに追加し、スタートアップ プロジェクトに設定します。

#### <a name="to-create-the-client-application"></a>クライアント アプリケーションを作成するには

1. On the menu bar, choose File, **Add**, **New Project**.

2. In the **New Project** dialog box, expand the **Visual Basic** or **Visual C#** node and choose the **Windows** node, and then choose **Windows Forms Application**.

3. **[名前]** ボックスに「`NorthwindClient`」と入力して、 **[OK]** を選択します。

4. **ソリューション エクスプローラー**で、 **[NorthwindClient]** プロジェクト ノードをクリックします。

5. メニュー バーで、 **[プロジェクト]** 、 **[スタートアップ プロジェクトに設定]** の順に選択します。

   この手順では、Web プロジェクト内の [!INCLUDE[ss_data_service](../includes/ss-data-service-md.md)] へのサービス参照を追加します。

#### <a name="to-add-a-service-reference"></a>サービス参照を追加するには

1. On the menu bar, choose **Project**, **Add Service Reference**.

2. **[サービス参照の追加]** ダイアログ ボックスで、 **[探索]** をクリックします。

    NorthwindCustomers サービスの URL が **[アドレス]** フィールドに表示されます。

3. **[OK]** をクリックして、サービス参照を追加します。

   この手順では、データ ソースを構成して、サービスへのデータ バインディングを有効にします。

#### <a name="to-enable-data-binding-to-the-service"></a>サービスへのデータ バインディングを有効にするには

1. On the menu bar, choose **View**, **Other Windows**, **Data Sources**.

2. **[データ ソース]** ウィンドウで、 **[新しいデータ ソースの追加]** をクリックします。

3. **データ ソースの構成ウィザード**の **[データ ソースの種類を選択]** ページで、 **[オブジェクト]** をクリックし、 **[次へ]** をクリックします。

4. **[データ オブジェクトの選択]** ページで、**NorthwindClient** ノードを展開し、さらに **NorthwindClient.ServiceReference1** ノードを展開します。

5. **[Customer]** チェック ボックスをオンにし、 **[完了]** をクリックします。

   この手順では、サービスから取得したデータを表示するユーザー インターフェイスを作成します。

#### <a name="to-create-the-user-interface"></a>ユーザー インターフェイスを作成するには

1. **[データ ソース]** ウィンドウで、 **[Customers]** ノードのショートカット メニューを開き、 **[コピー]** をクリックします。

2. **[Form1.vb]** または **[Form1.cs]** フォーム デザイナーで、ショートカット メニューを開き、 **[貼り付け]** をクリックします。

    <xref:System.Windows.Forms.DataGridView> コントロール、<xref:System.Windows.Forms.BindingSource> コンポーネント、および <xref:System.Windows.Forms.BindingNavigator> コンポーネントがフォームに追加されます。

3. **[CustomersDataGridView]** コントロールを選択してから、 **[プロパティ]** ウィンドウで **[Dock]** プロパティを **[Fill]** に設定します。

4. In **Solution Explorer**, open the shortcut menu for the **Form1** node and choose **View Code** to open the Code Editor, and add the following Imports or Using statement at the top of the file:

   ```vb
   Imports NorthwindClient.ServiceReference1
   ```

   ```csharp
   using NorthwindClient.ServiceReference1;
   ```

5. `Form1_Load` イベント ハンドラーに次のコードを追加します。

   ```vb
   Private Sub Form1_Load(sender As Object, e As EventArgs) Handles MyBase.Load
           Dim proxy As New NorthwindEntities _
   (New Uri("http://localhost:53161/NorthwindCustomers.svc/"))
           Me.CustomersBindingSource.DataSource = proxy.Customers
       End Sub
   ```

   ```csharp
   private void Form1_Load(object sender, EventArgs e)
   {
   NorthwindEntities proxy = new NorthwindEntities(new Uri("http://localhost:53161/NorthwindCustomers.svc/"));
   this.CustomersBindingSource.DataSource = proxy.Customers;
   }

   ```

6. In **Solution Explorer**, open the shortcut menu for the NorthwindCustomers.svc file and choose **View in Browser**. Internet Explorer が開き、そのサービスの XML スキーマが表示されます。

7. Internet Explorer のアドレス バーから URL をコピーします。

8. 手順 4. で追加したコードの「`http://localhost:53161/NorthwindCustomers.svc/`」を選択し、コピーした URL に置き換えます。

9. On the menu bar, choose **Debug**, **Start Debugging** to run the application. 顧客情報が表示されます。

   この時点で、NorthwindCustomers サービスから取得した顧客の一覧を表示するアプリケーションが作成されました。 このサービスを使用して他のデータも公開する場合は、[!INCLUDE[adonet_edm](../includes/adonet-edm-md.md)]を変更して、Northwind データベースの他のテーブルを含めます。

   次の省略可能な手順では、サービスによって返されたデータをフィルター処理する方法について説明します。

## <a name="adding-filtering-capabilities"></a>フィルター処理機能の追加
 この手順では、アプリケーションをカスタマイズして、都市で顧客データをフィルター処理します。

#### <a name="to-add-filtering-by-city"></a>都市によるフィルター処理を追加するには

1. **ソリューション エクスプローラー**で、 **[Form1.vb]** または **[Form1.cs]** ノードのショートカット メニューを開き、 **[開く]** をクリックします。

2. **[ツールボックス]** から、<xref:System.Windows.Forms.TextBox> コントロールと <xref:System.Windows.Forms.Button> コントロールをフォームに追加します。

3. Open the shortcut menu for the <xref:System.Windows.Forms.Button> control, and choose **View Code**, and then add the following code in the `Button1_Click` event handler:

    ```vb
    Private Sub Button1_Click(sender As Object, e As EventArgs) Handles Button1.Click
            Dim proxy As New northwindEntities _
    (New Uri("http://localhost:53161/NorthwindCustomers.svc"))
            Dim city As String = TextBox1.Text

            If city <> "" Then
                Me.CustomersBindingSource.DataSource = From c In _
             proxy.Customers Where c.City = city
            End If

        End Sub
    ```

    ```csharp
    private void Button1_Click(object sender, EventArgs e)
    {
    ServiceReference1.northwindModel.northwindEntities proxy = new northwindEntities(new Uri("http://localhost:53161/NorthwindCustomers.svc"));
    string city = TextBox1.Text;

    if (!string.IsNullOrEmpty(city)) {
    this.CustomersBindingSource.DataSource = from c in proxy.Customers where c.City == city;
    }

    }
    ```

4. このコードの `http://localhost:53161/NorthwindCustomers.svc` を `Form1_Load` イベント ハンドラーの URL に置き換えます。

5. On the menu bar, choose **Debug**, **Start Debugging** to run the application.

6. テキスト ボックスに「**London**」と入力し、ボタンをクリックします。 ロンドンの顧客だけが表示されます。

## <a name="see-also"></a>参照
 [Windows Communication Foundation Services and WCF Data Services in Visual Studio](../data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio.md) [How to: Add, Update, or Remove a WCF Data Service Reference](../data-tools/how-to-add-update-or-remove-a-wcf-data-service-reference.md)
