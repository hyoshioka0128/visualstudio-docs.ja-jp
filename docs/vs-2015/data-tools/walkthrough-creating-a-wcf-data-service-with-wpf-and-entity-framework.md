---
title: 'チュートリアル: WPF と Entity Framework を使用した WCF データサービスの作成 |Microsoft Docs'
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
ms.openlocfilehash: 4d825e625313febfa67cfb85f6a9c6bccb7f3608
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "75844270"
---
# <a name="walkthrough-creating-a-wcf-data-service-with-wpf-and-entity-framework"></a>チュートリアル: WPF と Entity Framework を使用した WCF データ サービスの作成
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このチュートリアル [!INCLUDE[ss_data_service](../includes/ss-data-service-md.md)] では、Web アプリケーションでホストされる単純なを作成 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] し、Windows フォームアプリケーションからアクセスする方法を示します。

 このチュートリアルでは、次の作業を行います。

- [!INCLUDE[ss_data_service](../includes/ss-data-service-md.md)] をホストする Web アプリケーションを作成します。

- Northwind データベースの Customers テーブルを表す[!INCLUDE[adonet_edm](../includes/adonet-edm-md.md)]を作成します。

- [!INCLUDE[ss_data_service](../includes/ss-data-service-md.md)] を作成します。

- クライアント アプリケーションを作成し、[!INCLUDE[ss_data_service](../includes/ss-data-service-md.md)] への参照を追加します。

- サービスへのデータ バインディングを有効にし、ユーザー インターフェイスを生成します。

- 必要に応じて、アプリケーションにフィルター処理機能を追加します。

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- Northwind サンプル データベース。

     開発用コンピューターにこのデータベースがない場合は、 [Microsoft ダウンロードセンター](https://www.microsoft.com/downloads)からダウンロードできます。 手順については、「[サンプル データベースのダウンロード](https://msdn.microsoft.com/library/ef9d69a1-9461-43fe-94bb-7c836754bcb5)」を参照してください。

## <a name="creating-the-service"></a>サービスの作成
 [!INCLUDE[ss_data_service](../includes/ss-data-service-md.md)] を作成するには、Web プロジェクトを追加し、[!INCLUDE[adonet_edm](../includes/adonet-edm-md.md)]を作成した後、そのモデルからサービスを作成します。

 最初に、サービスをホストする Web プロジェクトを追加します。

 [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]

#### <a name="to-create-the-web-project"></a>Web プロジェクトを作成するには

1. メニューバーで、[ **ファイル**]、[ **新規作成**]、[  **プロジェクト**] の順に選択します。

2. **[新しいプロジェクト]** ダイアログ ボックスの **[Visual Basic]** または **[Visual C#]** ノードを展開して、**[Web]** ノードをクリックし、**[ASP.NET Web アプリケーション]** テンプレートをクリックします。

3. **[名前]** ボックスに「**NorthwindWeb**」と入力し、**[OK]** をクリックします。

4. **[新しい ASP.NET プロジェクト]** ダイアログ ボックスの **[テンプレートの選択]** リストで **[なし]** を選択し、**[OK]** ボタンをクリックします。

   この手順では、Northwind データベースにある Customers テーブルを表す[!INCLUDE[adonet_edm](../includes/adonet-edm-md.md)]を作成します。

#### <a name="to-create-the-entity-data-model"></a>Entity Data Model を作成するには

1. メニューバーで、[ **プロジェクト**]、[ **新しい項目の追加**] の順に選択します。

2. **[新しい項目の追加]** ダイアログ ボックスで **[データ]** ノードを選択し、**[ADO.NET エンティティ データ モデル]** 項目を選択します。

3. [ **名前** ] テキストボックスに `NorthwindModel` 「」と入力し、[ **追加** ] ボタンをクリックします。

    Entity Data Model ウィザードが表示されます。

4. エンティティ データ モデル ウィザードの **[モデルのコンテンツの選択]** ページで、**[データベースから EF デザイナー]** 項目を選択してから **[次へ]** ボタンを選択します。

5. **[データ接続の選択]** ページで、次のいずれかの操作を行います。

   - Northwind サンプル データベースへのデータ接続がドロップダウン リストに表示されている場合は選択します。

        - または -

   - **[新しい接続]** を選択して、新しいデータ接続を構成します。 詳細については、「 [新しい接続の追加](../data-tools/add-new-connections.md)」を参照してください。

6. データベースにパスワードが必要な場合は、**[はい、重要情報を接続文字列に含めます。]** を選択し、**[次へ]** をクリックします。

   > [!NOTE]
   > ダイアログ ボックスが表示された場合は、**[はい]** をクリックしてファイルをプロジェクトに保存します。

7. **[バージョンの選択]** ページで **[Entity Framework 5.0]** オプション ボタンを選択し、**[次へ]** をクリックします。

   > [!NOTE]
   > WCF サービス で Entity Framework 6 の最新バージョンを使用するには、WCF Data Services Entity Framework Provider NuGet パッケージのインストールが必要になります。 「 [Using WCF Data Services 5.6.0 with Entity Framework 6 +」を](https://devblogs.microsoft.com/odata/using-wcf-data-services-5-6-0-with-entity-framework-6/)参照してください。

8. **[データベース オブジェクトの選択]** ページで、**[テーブル]** ノードを展開し、**[Customers]** チェック ボックスをオンにして **[完了]** をクリックします。

    エンティティ モデル ダイアグラムが表示され、プロジェクトに NorthwindModel.edmx ファイルが追加されます。

   この手順では、データ サービスを作成してテストします。

#### <a name="to-create-the-data-service"></a>データ サービスを作成するには

1. メニューバーで、[ **プロジェクト**]、[ **新しい項目の追加**] の順に選択します。

2. **[新しい項目の追加]** ダイアログ ボックスで **[Web]** ノードを選択し、**[WCF Data Service 5.6]** 項目を選択します。

3. [ **名前** ] テキストボックスに `NorthwindCustomers` 「」と入力し、[ **追加** ] ボタンをクリックします。

    NorthwindCustomers.svc ファイルが**コード エディター**に表示されます。

4. **コード エディター**で、最初の `TODO:` コメントを探して、コードを次のコードに置き換えます。

    [!code-csharp[WCFDataServiceWalkthrough#1](../snippets/csharp/VS_Snippets_VBCSharp/wcfdataservicewalkthrough/cs/northwindcustomers.svc.cs#1)]
    [!code-vb[WCFDataServiceWalkthrough#1](../snippets/visualbasic/VS_Snippets_VBCSharp/wcfdataservicewalkthrough/vb/northwindcustomers.svc.vb#1)]

5. `InitializeService` イベント ハンドラーのコメントを次のコードに置き換えます。

    [!code-csharp[WCFDataServiceWalkthrough#2](../snippets/csharp/VS_Snippets_VBCSharp/wcfdataservicewalkthrough/cs/northwindcustomers.svc.cs#2)]
    [!code-vb[WCFDataServiceWalkthrough#2](../snippets/visualbasic/VS_Snippets_VBCSharp/wcfdataservicewalkthrough/vb/northwindcustomers.svc.vb#2)]

6. メニューバーで、[ **デバッグ**]、[ **デバッグなしで開始** ] の順に選択してサービスを実行します。 ブラウザー ウィンドウが開き、そのサービスの XML スキーマが表示されます。

7. **アドレス**バーで、 `Customers` northwindcustomers.svc の URL の末尾に「」と入力し、 **enter**キーを押します。

    Customers テーブル内のデータの XML 表現が表示されます。

   > [!NOTE]
   > Internet Explorer がデータを誤って RSS フィードとして解釈する場合があります。 RSS フィードを表示するオプションが無効になっていることを確認してください。 詳細については、「 [サービス参照のトラブルシューティング](../data-tools/troubleshooting-service-references.md)」を参照してください。

8. ブラウザー ウィンドウを閉じます。

   次の手順では、サービスを使用する Windows フォーム クライアント アプリケーションを作成します。

## <a name="creating-the-client-application"></a>クライアント アプリケーションの作成
 クライアント アプリケーションを作成するには、2 つ目のプロジェクトを追加し、そのプロジェクトにサービス参照を追加します。そして、データ ソースを構成し、サービスから取得したデータを表示するユーザー インターフェイスを作成します。

 最初に、Windows フォーム プロジェクトをソリューションに追加し、スタートアップ プロジェクトに設定します。

#### <a name="to-create-the-client-application"></a>クライアント アプリケーションを作成するには

1. メニューバーで、[ファイル]、[ **追加**]、[ **新しいプロジェクト**] の順に選択します。

2. [ **新しいプロジェクト** ] ダイアログボックスで、[ **Visual Basic** ] または [ **Visual C#** ] ノードを展開し、[ **Windows** ] ノードを選択し、[ **Windows フォームアプリケーション**] を選択します。

3. **[名前]** ボックスに「`NorthwindClient`」と入力して、 **[OK]** を選択します。

4. **ソリューション エクスプローラー**で、**[NorthwindClient]** プロジェクト ノードをクリックします。

5. メニュー バーで、**[プロジェクト]**、**[スタートアップ プロジェクトに設定]** の順に選択します。

   この手順では、Web プロジェクト内の [!INCLUDE[ss_data_service](../includes/ss-data-service-md.md)] へのサービス参照を追加します。

#### <a name="to-add-a-service-reference"></a>サービス参照を追加するには

1. メニューバーで、[ **プロジェクト**]、[ **サービス参照の追加**] の順に選択します。

2. **[サービス参照の追加]** ダイアログ ボックスで、**[探索]** をクリックします。

    NorthwindCustomers サービスの URL が **[アドレス]** フィールドに表示されます。

3. **[OK]** をクリックして、サービス参照を追加します。

   この手順では、データ ソースを構成して、サービスへのデータ バインディングを有効にします。

#### <a name="to-enable-data-binding-to-the-service"></a>サービスへのデータ バインディングを有効にするには

1. メニューバーで、[ **表示**]、[ **その他のウィンドウ**]、[ **データソース**] の順に選択します。

2. **[データ ソース]** ウィンドウで、**[新しいデータ ソースの追加]** をクリックします。

3. **データ ソースの構成ウィザード**の **[データ ソースの種類を選択]** ページで、**[オブジェクト]** をクリックし、**[次へ]** をクリックします。

4. **[データ オブジェクトの選択]** ページで、**NorthwindClient** ノードを展開し、さらに **NorthwindClient.ServiceReference1** ノードを展開します。

5. **[Customer]** チェック ボックスをオンにし、**[完了]** をクリックします。

   この手順では、サービスから取得したデータを表示するユーザー インターフェイスを作成します。

#### <a name="to-create-the-user-interface"></a>ユーザー インターフェイスを作成するには

1. **[データ ソース]** ウィンドウで、**[Customers]** ノードのショートカット メニューを開き、**[コピー]** をクリックします。

2. **[Form1.vb]** または **[Form1.cs]** フォーム デザイナーで、ショートカット メニューを開き、**[貼り付け]** をクリックします。

    <xref:System.Windows.Forms.DataGridView> コントロール、<xref:System.Windows.Forms.BindingSource> コンポーネント、および <xref:System.Windows.Forms.BindingNavigator> コンポーネントがフォームに追加されます。

3. **[CustomersDataGridView]** コントロールを選択してから、**[プロパティ]** ウィンドウで **[Dock]** プロパティを **[Fill]** に設定します。

4. **ソリューションエクスプローラー**で、 **Form1**ノードのショートカットメニューを開き、[**コードの表示**] をクリックしてコードエディターを開き、ファイルの先頭に次の Imports または using ステートメントを追加します。

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

6. **ソリューション エクスプローラー**で、NorthwindCustomers.svc ファイルのショートカット メニューを開き、**[ブラウザーで表示]** をクリックします。 Internet Explorer が開き、そのサービスの XML スキーマが表示されます。

7. Internet Explorer のアドレス バーから URL をコピーします。

8. 手順 4. で追加したコードの「`http://localhost:53161/NorthwindCustomers.svc/`」を選択し、コピーした URL に置き換えます。

9. メニューバーで、[ **デバッグ**]、[ **デバッグ開始** ] の順に選択してアプリケーションを実行します。 顧客情報が表示されます。

   この時点で、NorthwindCustomers サービスから取得した顧客の一覧を表示するアプリケーションが作成されました。 このサービスを使用して他のデータも公開する場合は、[!INCLUDE[adonet_edm](../includes/adonet-edm-md.md)]を変更して、Northwind データベースの他のテーブルを含めます。

   次の省略可能な手順では、サービスによって返されたデータをフィルター処理する方法について説明します。

## <a name="adding-filtering-capabilities"></a>フィルター処理機能の追加
 この手順では、アプリケーションをカスタマイズして、都市で顧客データをフィルター処理します。

#### <a name="to-add-filtering-by-city"></a>都市によるフィルター処理を追加するには

1. **ソリューション エクスプローラー**で、**[Form1.vb]** または **[Form1.cs]** ノードのショートカット メニューを開き、**[開く]** をクリックします。

2. **[ツールボックス]** から、<xref:System.Windows.Forms.TextBox> コントロールと <xref:System.Windows.Forms.Button> コントロールをフォームに追加します。

3. コントロールのショートカットメニューを開き、[コードの表示] をクリックして、 <xref:System.Windows.Forms.Button> イベントハンドラーに次のコードを追加し**View Code** `Button1_Click` ます。

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

5. メニューバーで、[ **デバッグ**]、[ **デバッグ開始** ] の順に選択してアプリケーションを実行します。

6. テキスト ボックスに「**London**」と入力し、ボタンをクリックします。 ロンドンの顧客だけが表示されます。

## <a name="see-also"></a>参照
 [Visual Studio でのサービスと WCF Data Services の Windows Communication Foundation](../data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio.md) [方法: WCF データサービス参照を追加、更新、または削除する](../data-tools/how-to-add-update-or-remove-a-wcf-data-service-reference.md)
