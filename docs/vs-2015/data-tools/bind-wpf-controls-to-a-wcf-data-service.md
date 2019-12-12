---
title: WCF データサービスに WPF コントロールをバインドする |Microsoft Docs
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

- Entity Data Model 内のデータを WPF アプリケーションに公開する [!INCLUDE[ss_data_service](../includes/ss-data-service-md.md)] を作成する。

- **[データ ソース]** ウィンドウから WPF デザイナーに項目をドラッグして、一連のデータ バインド コントロールを作成する。

- 顧客レコード間を前後に移動するためのボタンを作成する。

- コントロール内のデータに対する変更を [!INCLUDE[ss_data_service](../includes/ss-data-service-md.md)] および基になるデータソースに保存するボタンを作成します。

   [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]

- AdventureWorksLT サンプル データベースが添付された、SQL Server または SQL Server Express の実行中のインスタンスへのアクセス権。 AdventureWorksLT データベースは、 [CodePlex Web サイト](https://go.microsoft.com/fwlink/?linkid=87843)からダウンロードできます。

  次の概念に関する知識があると役立ちますが、チュートリアルを実行するうえで必須というわけではありません。

- WCF Data Services。 詳細については、「[概要](https://msdn.microsoft.com/library/7924cf94-c9a6-4015-afc9-f5d22b1743bb)」を参照してください。

- [!INCLUDE[ssAstoria](../includes/ssastoria-md.md)] のデータ モデル。

- Entity Data Model および ADO.NET Entity Framework。 詳細については、「 [Entity Framework の概要](https://msdn.microsoft.com/library/a2166b3d-d8ba-4a0a-8552-6ba1e3eaaee0)」を参照してください。

- WPF デザイナーの操作。 詳細については、「 [WPF と Silverlight デザイナーの概要](https://msdn.microsoft.com/570b7a5c-0c86-4326-a371-c9b63378fc62)」を参照してください。

- WPF データ バインディング。 詳しくは、「[データ バインディングの概要](https://msdn.microsoft.com/library/c707c95f-7811-401d-956e-2fffd019a211)」をご覧ください。

## <a name="create-the-service-project"></a>サービスプロジェクトを作成する
 このチュートリアルでは、まず [!INCLUDE[ss_data_service](../includes/ss-data-service-md.md)] のプロジェクトを作成します。

#### <a name="to-create-the-service-project"></a>サービス プロジェクトを作成するには

1. Visual Studio を起動します。

2. **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。

3. **[Visual C#]** または **[Visual Basic]** を展開し、 **[Web]** を選択します。

4. **[ASP.NET Web アプリケーション]** プロジェクト テンプレートを選択します。

5. **[名前]** ボックスに「`AdventureWorksService`」と入力し、[ **OK]** をクリックします。

     Visual Studio によって `AdventureWorksService` プロジェクトが作成されます。

6. **ソリューション エクスプローラー**で、**Default.aspx** を右クリックし、 **[削除]** を選択します。 このファイルは、このチュートリアルでは必要ありません。

## <a name="create-an-entity-data-model-for-the-service"></a>サービスの Entity Data Model を作成する
 [!INCLUDE[ss_data_service](../includes/ss-data-service-md.md)] を使用してアプリケーションにデータを公開するには、サービスのデータ モデルを定義する必要があります。 [!INCLUDE[ss_data_service](../includes/ss-data-service-md.md)] では、次の2種類のデータモデルがサポートされています。エンティティデータモデル、および <xref:System.Linq.IQueryable%601> インターフェイスを実装する共通言語ランタイム (CLR) オブジェクトを使用して定義されるカスタムデータモデル。 このチュートリアルでは、データ モデルとして Entity Data Model を作成します。

#### <a name="to-create-an-entity-data-model"></a>Entity Data Model を作成するには

1. **[プロジェクト]** メニューの **[新しい項目の追加]** をクリックします。

2. [インストールされたテンプレート] ボックスの一覧で、 **[データ]** をクリックし、 **[ADO.NET エンティティ データ モデル]** プロジェクト項目を選択します。

3. 名前を `AdventureWorksModel.edmx`に変更し、 **[追加]** をクリックします。

     **Entity Data Model** ウィザードが開きます。

4. **[モデルのコンテンツの選択]** ページで、 **[データベースから生成]** をクリックし、 **[次へ]** をクリックします。

5. **[データ接続の選択]** ページで、次のいずれかのオプションを選択します。

    - AdventureWorksLT サンプル データベースへのデータ接続がドロップダウン リストに表示されている場合は、これを選択します。

    - **[新しい接続]** をクリックして、AdventureWorksLT データベースへの接続を作成します。

6. **[データ接続の選択]** ページで、 **[エンティティ接続設定に名前を付けて App.Config に保存]** オプションが選択されていることを確認し、 **[次へ]** をクリックします。

7. **[データベース オブジェクトの選択]** ページで、 **[テーブル]** を展開し、**SalesOrderHeader** テーブルを選択します。

8. **[完了]** をクリックします。

## <a name="create-the-service"></a>サービスを作成する
 Entity Data Model 内のデータを WPF アプリケーションに公開するための [!INCLUDE[ss_data_service](../includes/ss-data-service-md.md)] を作成します。

#### <a name="to-create-the-service"></a>サービスを作成するには

1. **[プロジェクト]** メニューで **[新しい項目の追加]** を選択します。

2. インストールされたテンプレート の一覧で  **Web** をクリックし、**WCF Data Service** プロジェクト項目を選択します。

3. **[名前]** ボックスに「`AdventureWorksService.svc`」と入力し、 **[追加]** をクリックします。

     Visual Studio によって `AdventureWorksService.svc` がプロジェクトに追加されます。

## <a name="configure-the-service"></a>サービスの構成
 作成した Entity Data Model を操作するには、サービスを構成する必要があります。

#### <a name="to-configure-the-service"></a>サービスを構成するには

1. `AdventureWorks.svc` コードファイルで、`AdventureWorksService` クラスの宣言を次のコードに置き換えます。

     [!code-csharp[Data_WPFWCF#1](../snippets/csharp/VS_Snippets_ProTools/data_wpfwcf/cs/adventureworksservice.svc.cs#1)]
     [!code-vb[Data_WPFWCF#1](../snippets/visualbasic/VS_Snippets_ProTools/data_wpfwcf/vb/adventureworksservice.svc.vb#1)]

     このコードは、Entity Data Model 内の `AdventureWorksLTEntities` オブジェクトコンテキストクラスで動作する <xref:System.Data.Services.DataService%601> から派生するように `AdventureWorksService` クラスを更新します。 また、`InitializeService` メソッドも更新され、`SalesOrderHeader` エンティティへの完全な読み取り/書き込みアクセスがサービスのクライアントに許可されます。

2. プロジェクトをビルドし、エラーが発生しないことを確認します。

## <a name="create-the-wpf-client-application"></a>WPF クライアントアプリケーションを作成する
 [!INCLUDE[ss_data_service](../includes/ss-data-service-md.md)] のデータを表示するには、サービスに基づくデータ ソースを使用して、新しい WPF アプリケーションを作成します。 このチュートリアルの後半で、データ バインド コントロールをアプリケーションに追加します。

#### <a name="to-create-the-wpf-client-application"></a>WPF クライアント アプリケーションを作成するには

1. **ソリューション エクスプローラー**で、ソリューション ノードを右クリックし、 **[追加]** をクリックして、 **[新しいプロジェクト]** を選択します。

2. **[新しいプロジェクト]** ダイアログで、 **[Visual C#]** または **[Visual Basic]** を展開し、 **[Windows]** を選択します。

3. **[WPF アプリケーション]** プロジェクト テンプレートを選択します。

4. **[名前]** ボックスに `AdventureWorksSalesEditor` と入力して、 **[OK]** をクリックします。

     Visual Studio によって、`AdventureWorksSalesEditor` プロジェクトがソリューションに追加されます。

5. **[データ]** メニューの **[データ ソースの表示]** をクリックします。

     **[データ ソース]** ウィンドウが開きます。

6. **[データ ソース]** ウィンドウで、 **[新しいデータ ソースの追加]** をクリックします。

     **データ ソース構成**ウィザードが開きます。

7. ウィザードの **[データ ソースの種類を選択]** ページで、 **[サービス]** を選択し、 **[次へ]** をクリックします。

8. **[サービス参照の追加]** ダイアログ ボックスで **[探索]** をクリックします。

     Visual Studio は、現在のソリューションで利用可能なサービスを検索し、 **[サービス]** ボックスで利用可能なサービスの一覧に `AdventureWorksService.svc` を追加します。

9. **[名前空間]** ボックスに、「`AdventureWorksService`」と入力します。

10. **[サービス]** ボックスで **[AdventureWorksService.svc]** をクリックし、 **[OK]** をクリックします。

     Visual Studio によってサービス情報がダウンロードされ、**データソース構成**ウィザードに戻ります。

11. **[サービス参照の追加]** ページで、 **[完了]** をクリックします。

     Visual Studio によって、サービスから返されたデータを表すノードが **[データ ソース]** ウィンドウに追加されます。

## <a name="define-the-user-interface-of-the-window"></a>ウィンドウのユーザーインターフェイスを定義します。
 WPF デザイナーで XAML を変更して、いくつかのボタンをウィンドウに追加します。 これらのボタンを使用して販売レコードを表示および更新できるようにするコードは、このチュートリアルで後で追加します。

#### <a name="to-create-the-window-layout"></a>ウィンドウ レイアウトを作成するには

1. **ソリューションエクスプローラー**で、mainwindow.xaml をダブルクリックします。

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

## <a name="create-the-data-bound-controls"></a>データバインドコントロールの作成
 **[データソース]** ウィンドウからデザイナーに [`SalesOrderHeaders`] ノードをドラッグして、顧客レコードを表示するコントロールを作成します。

#### <a name="to-create-the-data-bound-controls"></a>データ バインディング コントロールを作成するには

1. **[データ ソース]** ウィンドウで、 **[SalesOrderHeaders]** ノードのドロップダウン メニューをクリックし、 **[詳細]** を選択します。

2. **[SalesOrderHeaders]** ノードを展開します。

3. この例ではいくつかのフィールドを非表示にするために、次のノードの横のドロップダウン メニューをクリックして **[なし]** を選択します。

   - **CreditCardApprovalCode**

   - **ModifiedDate**

   - **OnlineOrderFlag**

   - **RevisionNumber**

   - **rowguid**

     この操作は、次の手順において、これらのノードに対応するデータ バインド コントロールが Visual Studio で作成されるのを防ぎます。 このチュートリアルでは、エンドユーザーがこのデータを表示する必要がないことを想定しています。

4. **[データ ソース]** ウィンドウから、ボタンのある行の下のグリッド行に **[SalesOrderHeaders]** ノードをドラッグします。

    Visual Studio によって、**Product** テーブルのデータにバインドされるコントロール セットを作成する XAML とコードが生成されます。 生成される XAML とコードの詳細については、「 [Visual Studio でのデータへの WPF コントロールのバインド](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md)」を参照してください。

5. デザイナーで、 **[Customer ID]** ラベルの横のテキスト ボックスをクリックします。

6. **[プロパティ]** ウィンドウで、**IsReadOnly** プロパティの横のチェック ボックスをオンにします。

7. 次の各テキスト ボックスに **IsReadOnly** プロパティを設定します。

   - **[Purchase Order Number]**

   - **[Sales Order ID]**

   - **[Sales Order Number]**

## <a name="load-the-data-from-the-service"></a>サービスからのデータの読み込み
 サービスから販売データを読み込むには、サービスプロキシオブジェクトを使用します。 次に、返されたデータを WPF ウィンドウの <xref:System.Windows.Data.CollectionViewSource> のデータソースに割り当てます。

#### <a name="to-load-the-data-from-the-service"></a>サービスからデータを読み込むには

1. デザイナーで、`Window_Loaded` イベントハンドラーを作成するには、次のように表示されるテキストをダブルクリックします。**Mainwindow.xaml**。

2. イベント ハンドラーを次のコードで置き換えます。 このコードの *localhost* アドレスは、使用している開発コンピューターのローカル ホスト アドレスで置き換えてください。

     [!code-csharp[Data_WPFWCF#2](../snippets/csharp/VS_Snippets_ProTools/data_wpfwcf/cs/adventureworkssaleseditor/mainwindow.xaml.cs#2)]
     [!code-vb[Data_WPFWCF#2](../snippets/visualbasic/VS_Snippets_ProTools/data_wpfwcf/vb/adventureworkssaleseditor/mainwindow.xaml.vb#2)]

## <a name="navigatesales-records"></a>Navigatesales レコード
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

## <a name="saving-changes-to-sales-records"></a>販売レコードへの変更を保存しています
 **[変更の保存]** ボタンを使用して、ユーザーが販売レコードへの変更を表示して保存できるようにするコードを追加します。

#### <a name="to-add-the-ability-to-save-changes-to-sales-records"></a>販売レコードへの変更を保存する機能を追加するには

1. デザイナーで、 **[変更の保存]** をダブルクリックします。

     Visual Studio によって分離コード ファイルが開かれ、`saveButton_Click` イベントのために新しい <xref:System.Windows.Controls.Primitives.ButtonBase.Click> イベント ハンドラーが作成されます。

2. `saveButton_Click` イベント ハンドラーに次のコードを追加します。

     [!code-csharp[Data_WPFWCF#5](../snippets/csharp/VS_Snippets_ProTools/data_wpfwcf/cs/adventureworkssaleseditor/mainwindow.xaml.cs#5)]
     [!code-vb[Data_WPFWCF#5](../snippets/visualbasic/VS_Snippets_ProTools/data_wpfwcf/vb/adventureworkssaleseditor/mainwindow.xaml.vb#5)]

## <a name="testing-the-application"></a>アプリケーションのテスト
 アプリケーションをビルドして実行し、顧客レコードを表示および更新できることを確認します。

#### <a name="to-test-the-application"></a>アプリケーションをテストするには

1. **[ビルド]** メニューの **[ソリューションのビルド]** をクリックします。 ソリューションがエラーなしでビルドされることを確認します。

2. Ctrl キーを押し**ながら F5**キーを押します。

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

## <a name="next-steps"></a>次の手順
 このチュートリアルを完了した後、関連する次のタスクを実行できます。

- Visual Studio の **[データ ソース]** ウィンドウを使用して、WPF コントロールをその他の種類のデータ ソースにバインドする方法について学習します。 詳細については、「[データセットへの WPF コントロールのバインド](../data-tools/bind-wpf-controls-to-a-dataset.md)」を参照してください。

- Visual Studio の **[データ ソース]** ウィンドウを使用して、WPF コントロールでの関連するデータ (つまり、親子関係にあるデータ) を表示する方法について学習します。 詳細については、「[チュートリアル:WPF アプリケーションでの関連データの表示](../data-tools/walkthrough-displaying-related-data-in-a-wpf-application.md)。

## <a name="see-also"></a>関連項目
 [Visual studio でのデータへの wpf コントロールの](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md)[バインド visual studio で](../data-tools/bind-wpf-controls-to-data-in-visual-studio2.md)のデータへの wpf コントロールのバインド[dataset への Wpf](../data-tools/bind-wpf-controls-to-a-dataset.md) [概要](https://msdn.microsoft.com/library/7924cf94-c9a6-4015-afc9-f5d22b1743bb)コントロールのバインド[Entity Framework 概要](https://msdn.microsoft.com/library/a2166b3d-d8ba-4a0a-8552-6ba1e3eaaee0) [wpf と Silverlight デザイナーの概要](https://msdn.microsoft.com/570b7a5c-0c86-4326-a371-c9b63378fc62)[データバインディングの概要](https://msdn.microsoft.com/library/c707c95f-7811-401d-956e-2fffd019a211)
