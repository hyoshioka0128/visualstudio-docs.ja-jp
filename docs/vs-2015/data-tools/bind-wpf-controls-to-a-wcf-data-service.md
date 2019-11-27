---
title: Bind WPF controls to a WCF data service | Microsoft Docs
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
- WPF, data binding in Visual Studio
- WPF data binding [Visual Studio], walkthroughs
- WPF Designer, data binding
ms.assetid: 8823537c-82f0-41f7-bf30-705f0e5e59fd
caps.latest.revision: 44
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: a3d1aab68e3dc9f33e0b3e9f9a5665d59f6f2ddc
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74299405"
---
# <a name="bind-wpf-controls-to-a-wcf-data-service"></a>WCF Data Service への WPF コントロールのバインド
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このチュートリアルでは、データ バインド コントロールが含まれた WPF アプリケーションを作成します。 コントロールは、[!INCLUDE[ss_data_service](../includes/ss-data-service-md.md)] でカプセル化された顧客レコードにバインドされます。 また、顧客がレコードを表示および更新するために使用できるボタンも追加します。

 このチュートリアルでは、次の作業について説明します。

- AdventureWorksLT サンプル データベースのデータから生成される Entity Data Model を作成する。

- Creating a [!INCLUDE[ss_data_service](../includes/ss-data-service-md.md)] that exposes the data in the Entity Data Model to a WPF application.

- **[データ ソース]** ウィンドウから WPF デザイナーに項目をドラッグして、一連のデータ バインド コントロールを作成する。

- 顧客レコード間を前後に移動するためのボタンを作成する。

- Creating a button that saves changes to data in the controls to the [!INCLUDE[ss_data_service](../includes/ss-data-service-md.md)] and the underlying data source.

   [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>必要条件
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]

- AdventureWorksLT サンプル データベースが添付された、SQL Server または SQL Server Express の実行中のインスタンスへのアクセス権。 You can download the AdventureWorksLT database from the [CodePlex Web site](https://go.microsoft.com/fwlink/?linkid=87843).

  次の概念に関する知識があると役立ちますが、チュートリアルを実行するうえで必須というわけではありません。

- WCF Data Services。 For more information, see [Overview](https://msdn.microsoft.com/library/7924cf94-c9a6-4015-afc9-f5d22b1743bb).

- [!INCLUDE[ssAstoria](../includes/ssastoria-md.md)] のデータ モデル。

- Entity Data Model および ADO.NET Entity Framework。 For more information, see [Entity Framework Overview](https://msdn.microsoft.com/library/a2166b3d-d8ba-4a0a-8552-6ba1e3eaaee0).

- WPF デザイナーの操作。 For more information, see [WPF and Silverlight Designer Overview](https://msdn.microsoft.com/570b7a5c-0c86-4326-a371-c9b63378fc62).

- WPF データ バインディング。 詳しくは、「[データ バインディングの概要](https://msdn.microsoft.com/library/c707c95f-7811-401d-956e-2fffd019a211)」をご覧ください。

## <a name="create-the-service-project"></a>Create the service project
 このチュートリアルでは、まず [!INCLUDE[ss_data_service](../includes/ss-data-service-md.md)] のプロジェクトを作成します。

#### <a name="to-create-the-service-project"></a>サービス プロジェクトを作成するには

1. Visual Studio を起動します。

2. **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。

3. **[Visual C#]** または **[Visual Basic]** を展開し、 **[Web]** を選択します。

4. **[ASP.NET Web アプリケーション]** プロジェクト テンプレートを選択します。

5. In the **Name** box, type `AdventureWorksService` and click **OK**.

     Visual Studio creates the `AdventureWorksService` project.

6. **ソリューション エクスプローラー**で、**Default.aspx** を右クリックし、 **[削除]** を選択します。 このファイルは、このチュートリアルでは必要ありません。

## <a name="create-an-entity-data-model-for-the-service"></a>Create an Entity Data Model for the service
 [!INCLUDE[ss_data_service](../includes/ss-data-service-md.md)] を使用してアプリケーションにデータを公開するには、サービスのデータ モデルを定義する必要があります。 The [!INCLUDE[ss_data_service](../includes/ss-data-service-md.md)] supports two types of data models: Entity Data Models, and custom data models that are defined by using common language runtime (CLR) objects that implement the <xref:System.Linq.IQueryable%601> interface. このチュートリアルでは、データ モデルとして Entity Data Model を作成します。

#### <a name="to-create-an-entity-data-model"></a>Entity Data Model を作成するには

1. **[プロジェクト]** メニューの **[新しい項目の追加]** をクリックします。

2. [インストールされたテンプレート] ボックスの一覧で、 **[データ]** をクリックし、 **[ADO.NET エンティティ データ モデル]** プロジェクト項目を選択します。

3. Change the name to `AdventureWorksModel.edmx`, and click **Add**.

     **Entity Data Model** ウィザードが開きます。

4. **[モデルのコンテンツの選択]** ページで、 **[データベースから生成]** をクリックし、 **[次へ]** をクリックします。

5. **[データ接続の選択]** ページで、次のいずれかのオプションを選択します。

    - AdventureWorksLT サンプル データベースへのデータ接続がドロップダウン リストに表示されている場合は、これを選択します。

    - **[新しい接続]** をクリックして、AdventureWorksLT データベースへの接続を作成します。

6. **[データ接続の選択]** ページで、 **[エンティティ接続設定に名前を付けて App.Config に保存]** オプションが選択されていることを確認し、 **[次へ]** をクリックします。

7. **[データベース オブジェクトの選択]** ページで、 **[テーブル]** を展開し、**SalesOrderHeader** テーブルを選択します。

8. **[完了]** をクリックします。

## <a name="create-the-service"></a>サービスを作成する
 Create a [!INCLUDE[ss_data_service](../includes/ss-data-service-md.md)] to expose the data in the Entity Data Model to a WPF application.

#### <a name="to-create-the-service"></a>サービスを作成するには

1. **[プロジェクト]** メニューで **[新しい項目の追加]** を選択します。

2. In the Installed Templates list, click **Web**, and then select the **WCF Data Service** project item.

3. In the **Name** box, type `AdventureWorksService.svc`, and click **Add**.

     Visual Studio adds the `AdventureWorksService.svc` to the project.

## <a name="configure-the-service"></a>サービスの構成
 作成した Entity Data Model を操作するには、サービスを構成する必要があります。

#### <a name="to-configure-the-service"></a>サービスを構成するには

1. In the `AdventureWorks.svc` code file, replace the `AdventureWorksService` class declaration with the following code.

     [!code-csharp[Data_WPFWCF#1](../snippets/csharp/VS_Snippets_ProTools/data_wpfwcf/cs/adventureworksservice.svc.cs#1)]
     [!code-vb[Data_WPFWCF#1](../snippets/visualbasic/VS_Snippets_ProTools/data_wpfwcf/vb/adventureworksservice.svc.vb#1)]

     This code updates the `AdventureWorksService` class, so that it derives from a <xref:System.Data.Services.DataService%601> that operates on the `AdventureWorksLTEntities` object context class in your Entity Data Model. また、`InitializeService` メソッドも更新され、`SalesOrderHeader` エンティティへの完全な読み取り/書き込みアクセスがサービスのクライアントに許可されます。

2. プロジェクトをビルドし、エラーが発生しないことを確認します。

## <a name="create-the-wpf-client-application"></a>Create the WPF client application
 [!INCLUDE[ss_data_service](../includes/ss-data-service-md.md)] のデータを表示するには、サービスに基づくデータ ソースを使用して、新しい WPF アプリケーションを作成します。 このチュートリアルの後半で、データ バインド コントロールをアプリケーションに追加します。

#### <a name="to-create-the-wpf-client-application"></a>WPF クライアント アプリケーションを作成するには

1. **ソリューション エクスプローラー**で、ソリューション ノードを右クリックし、 **[追加]** をクリックして、 **[新しいプロジェクト]** を選択します。

2. **[新しいプロジェクト]** ダイアログで、 **[Visual C#]** または **[Visual Basic]** を展開し、 **[Windows]** を選択します。

3. **[WPF アプリケーション]** プロジェクト テンプレートを選択します。

4. **[名前]** ボックスに `AdventureWorksSalesEditor` と入力して、 **[OK]** をクリックします。

     Visual Studio adds the `AdventureWorksSalesEditor` project to the solution.

5. **[データ]** メニューの **[データ ソースの表示]** をクリックします。

     **[データ ソース]** ウィンドウが開きます。

6. **[データ ソース]** ウィンドウで、 **[新しいデータ ソースの追加]** をクリックします。

     **データ ソース構成**ウィザードが開きます。

7. ウィザードの **[データ ソースの種類を選択]** ページで、 **[サービス]** を選択し、 **[次へ]** をクリックします。

8. **[サービス参照の追加]** ダイアログ ボックスで **[探索]** をクリックします。

     Visual Studio searches the current solution for available services, and adds `AdventureWorksService.svc` to the list of available services in the **Services** box.

9. In the **Namespace** box, type `AdventureWorksService`.

10. **[サービス]** ボックスで **[AdventureWorksService.svc]** をクリックし、 **[OK]** をクリックします。

     Visual Studio downloads the service information, and then returns to the **Data Source Configuration** wizard.

11. **[サービス参照の追加]** ページで、 **[完了]** をクリックします。

     Visual Studio によって、サービスから返されたデータを表すノードが **[データ ソース]** ウィンドウに追加されます。

## <a name="define-the-user-interface-of-the-window"></a>Define the user interface of the window
 WPF デザイナーで XAML を変更して、いくつかのボタンをウィンドウに追加します。 これらのボタンを使用して販売レコードを表示および更新できるようにするコードは、このチュートリアルで後で追加します。

#### <a name="to-create-the-window-layout"></a>ウィンドウ レイアウトを作成するには

1. In **Solution Explorer**, double-click MainWindow.xaml.

     WPF デザイナーでウィンドウが開きます。

2. デザイナーの [!INCLUDE[TLA#tla_titlexaml](../includes/tlasharptla-titlexaml-md.md)] ビューで、`<Grid>` タグの間に次のコードを追加します。

    ```
    <Grid.RowDefinitions>
        <RowDefinition Height="75" />
        <RowDefinition Height="525" />
    </Grid.RowDefinitions>
    <Button HorizontalAlignment="Left" Margin="22,20,0,24" Name="backButton" Width="75"><</Button>
    <Button HorizontalAlignment="Left" Margin="116,20,0,24" Name="nextButton" Width="75">></Button>
    <Button HorizontalAlignment="Right" Margin="0,21,46,24" Name="saveButton" Width="110">Save changes</Button>
    ```

3. プロジェクトをビルドします。

## <a name="create-the-data-bound-controls"></a>Create the data-bound controls
 Create controls that display customer records by dragging the `SalesOrderHeaders` node from the **Data Sources** window to the designer.

#### <a name="to-create-the-data-bound-controls"></a>データ バインディング コントロールを作成するには

1. **[データ ソース]** ウィンドウで、 **[SalesOrderHeaders]** ノードのドロップダウン メニューをクリックし、 **[詳細]** を選択します。

2. **[SalesOrderHeaders]** ノードを展開します。

3. この例ではいくつかのフィールドを非表示にするために、次のノードの横のドロップダウン メニューをクリックして **[なし]** を選択します。

   - **CreditCardApprovalCode**

   - **ModifiedDate**

   - **OnlineOrderFlag**

   - **RevisionNumber**

   - **rowguid**

     この操作は、次の手順において、これらのノードに対応するデータ バインド コントロールが Visual Studio で作成されるのを防ぎます。 For this walkthrough, assume that the end user does not need to see this data.

4. **[データ ソース]** ウィンドウから、ボタンのある行の下のグリッド行に **[SalesOrderHeaders]** ノードをドラッグします。

    Visual Studio によって、**Product** テーブルのデータにバインドされるコントロール セットを作成する XAML とコードが生成されます。 For more information about the generated XAML and code, see [Bind WPF controls to data in Visual Studio](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md).

5. デザイナーで、 **[Customer ID]** ラベルの横のテキスト ボックスをクリックします。

6. **[プロパティ]** ウィンドウで、**IsReadOnly** プロパティの横のチェック ボックスをオンにします。

7. 次の各テキスト ボックスに **IsReadOnly** プロパティを設定します。

   - **[Purchase Order Number]**

   - **[Sales Order ID]**

   - **[Sales Order Number]**

## <a name="load-the-data-from-the-service"></a>サービスからのデータの読み込み
 Use the service proxy object to load sales data from the service. Then assign the returned data to the data source for the <xref:System.Windows.Data.CollectionViewSource> in the WPF window.

#### <a name="to-load-the-data-from-the-service"></a>サービスからデータを読み込むには

1. 作成するため、デザイナーで、`Window_Loaded`イベント ハンドラーを読み取るテキストをダブルクリックします**MainWindow**。

2. イベント ハンドラーを次のコードで置き換えます。 このコードの *localhost* アドレスは、使用している開発コンピューターのローカル ホスト アドレスで置き換えてください。

     [!code-csharp[Data_WPFWCF#2](../snippets/csharp/VS_Snippets_ProTools/data_wpfwcf/cs/adventureworkssaleseditor/mainwindow.xaml.cs#2)]
     [!code-vb[Data_WPFWCF#2](../snippets/visualbasic/VS_Snippets_ProTools/data_wpfwcf/vb/adventureworkssaleseditor/mainwindow.xaml.vb#2)]

## <a name="navigatesales-records"></a>Navigatesales records
 ユーザーが **[\<]** ボタンと **[>]** ボタンを使用して販売レコード間をスクロールできるようにするコードを追加します。

#### <a name="to-enable-users-to-navigate-sales-records"></a>ユーザーが販売レコード間を移動できるようにするには

1. デザイナーで、ウィンドウ サーフェイスの **[<]** をダブルクリックします。

     Visual Studio によって分離コード ファイルが開かれ、`backButton_Click` イベントのために新しい <xref:System.Windows.Controls.Primitives.ButtonBase.Click> イベント ハンドラーが作成されます。

2. 生成された `backButton_Click` イベント ハンドラーに次のコードを追加します。

     [!code-csharp[Data_WPFWCF#3](../snippets/csharp/VS_Snippets_ProTools/data_wpfwcf/cs/adventureworkssaleseditor/mainwindow.xaml.cs#3)]
     [!code-vb[Data_WPFWCF#3](../snippets/visualbasic/VS_Snippets_ProTools/data_wpfwcf/vb/adventureworkssaleseditor/mainwindow.xaml.vb#3)]

3. デザイナーに戻り、 **[>]** をダブルクリックします。

     Visual Studio によって分離コード ファイルが開かれ、`nextButton_Click` イベントのために新しい <xref:System.Windows.Controls.Primitives.ButtonBase.Click> イベント ハンドラーが作成されます。

4. 生成された `nextButton_Click` イベント ハンドラーに次のコードを追加します。

     [!code-csharp[Data_WPFWCF#4](../snippets/csharp/VS_Snippets_ProTools/data_wpfwcf/cs/adventureworkssaleseditor/mainwindow.xaml.cs#4)]
     [!code-vb[Data_WPFWCF#4](../snippets/visualbasic/VS_Snippets_ProTools/data_wpfwcf/vb/adventureworkssaleseditor/mainwindow.xaml.vb#4)]

## <a name="saving-changes-to-sales-records"></a>Saving changes to sales records
 Add code that enables users to both view and save changes to sales records by using the **Save changes** button.

#### <a name="to-add-the-ability-to-save-changes-to-sales-records"></a>販売レコードへの変更を保存する機能を追加するには

1. デザイナーで、 **[変更の保存]** をダブルクリックします。

     Visual Studio によって分離コード ファイルが開かれ、`saveButton_Click` イベントのために新しい <xref:System.Windows.Controls.Primitives.ButtonBase.Click> イベント ハンドラーが作成されます。

2. `saveButton_Click` イベント ハンドラーに次のコードを追加します。

     [!code-csharp[Data_WPFWCF#5](../snippets/csharp/VS_Snippets_ProTools/data_wpfwcf/cs/adventureworkssaleseditor/mainwindow.xaml.cs#5)]
     [!code-vb[Data_WPFWCF#5](../snippets/visualbasic/VS_Snippets_ProTools/data_wpfwcf/vb/adventureworkssaleseditor/mainwindow.xaml.vb#5)]

## <a name="testing-the-application"></a>アプリケーションのテスト
 アプリケーションをビルドして実行し、顧客レコードを表示および更新できることを確認します。

#### <a name="to-test-the-application"></a>アプリケーションをテストするには

1. On **Build** menu, click **Build Solution**. ソリューションがエラーなしでビルドされることを確認します。

2. Press **Ctrl+F5**.

     Visual Studio によって、**AdventureWorksService** プロジェクトがデバッグなしで開始されます。

3. **ソリューション エクスプローラー**で、**AdventureWorksSalesEditor** プロジェクトを右クリックします。

4. コンテキスト メニューの **[デバッグ]** で、 **[新しいインスタンスを開始]** をクリックします。

     アプリケーションが実行されます。 次のことを検証します。

    - テキスト ボックスに、先頭の販売レコードの各種データ フィールドが表示されること。このレコードの販売注文 ID は **71774** です。

    - **[>]** または **[<]** をクリックして、他の販売レコードに移動できること。

5. いずれかの販売レコードの **[コメント]** ボックスに任意のテキストを入力し、 **[変更の保存]** をクリックします。

6. アプリケーションを終了し、Visual Studio からもう一度アプリケーションを起動します。

7. 変更した販売レコードに移動し、アプリケーションを終了して再起動した後でも変更が保持されていることを確認します。

8. アプリケーションを終了します。

## <a name="next-steps"></a>次のステップ
 このチュートリアルを完了した後、関連する次のタスクを実行できます。

- Visual Studio の **[データ ソース]** ウィンドウを使用して、WPF コントロールをその他の種類のデータ ソースにバインドする方法について学習します。 For more information, see [Bind WPF controls to a dataset](../data-tools/bind-wpf-controls-to-a-dataset.md).

- Visual Studio の **[データ ソース]** ウィンドウを使用して、WPF コントロールでの関連するデータ (つまり、親子関係にあるデータ) を表示する方法について学習します。 For more information, see [Walkthrough: Displaying Related Data in a WPF Application](../data-tools/walkthrough-displaying-related-data-in-a-wpf-application.md).

## <a name="see-also"></a>参照
 [Bind WPF controls to data in Visual Studio](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md) [Bind WPF controls to data in Visual Studio](../data-tools/bind-wpf-controls-to-data-in-visual-studio2.md) [Bind WPF controls to a dataset](../data-tools/bind-wpf-controls-to-a-dataset.md) [Overview](https://msdn.microsoft.com/library/7924cf94-c9a6-4015-afc9-f5d22b1743bb) [Entity Framework Overview](https://msdn.microsoft.com/library/a2166b3d-d8ba-4a0a-8552-6ba1e3eaaee0) [WPF and Silverlight Designer Overview](https://msdn.microsoft.com/570b7a5c-0c86-4326-a371-c9b63378fc62) [Data Binding Overview](https://msdn.microsoft.com/library/c707c95f-7811-401d-956e-2fffd019a211)
