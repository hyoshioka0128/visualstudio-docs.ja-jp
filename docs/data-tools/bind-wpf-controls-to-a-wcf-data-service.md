---
title: WCF Data Service への WPF コントロールのバインド
description: Visual Studio で WCF データサービスに WPF コントロールをバインドします。 コントロールは、WCF データサービスにカプセル化された顧客レコードにバインドされます。
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- WPF, data binding in Visual Studio
- WPF data binding [Visual Studio], walkthroughs
- WPF Designer, data binding
ms.assetid: 8823537c-82f0-41f7-bf30-705f0e5e59fd
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: c627a9f09d5400e321bcc8a141c36ec46cad7958
ms.sourcegitcommit: 0893244403aae9187c9375ecf0e5c221c32c225b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/09/2020
ms.locfileid: "94382209"
---
# <a name="bind-wpf-controls-to-a-wcf-data-service"></a>WCF Data Service への WPF コントロールのバインド

このチュートリアルでは、データ バインド コントロールが含まれた WPF アプリケーションを作成します。 コントロールは、WCF データサービスにカプセル化された顧客レコードにバインドされます。 また、顧客がレコードを表示および更新するために使用できるボタンも追加します。

このチュートリアルでは、次の作業について説明します。

- AdventureWorksLT サンプル データベースのデータから生成される Entity Data Model を作成する。

- WPF アプリケーションに Entity Data Model 内のデータを公開する WCF データサービスを作成する。

- **[データ ソース]** ウィンドウから WPF デザイナーに項目をドラッグして、一連のデータ バインド コントロールを作成する。

- 顧客レコード間を前後に移動するためのボタンを作成する。

- コントロール内のデータに対する変更を WCF Data Service および基になるデータソースに保存するボタンを作成します。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

## <a name="prerequisites"></a>必須コンポーネント

このチュートリアルを実行するには、次のコンポーネントが必要です。

- Visual Studio

- AdventureWorksLT サンプル データベースが添付された、SQL Server または SQL Server Express の実行中のインスタンスへのアクセス権。 AdventureWorksLT データベースは、 [CodePlex の web サイト](https://archive.codeplex.com/?p=SqlServerSamples)からダウンロードできます。

次の概念に関する知識があると役立ちますが、チュートリアルを実行するうえで必須というわけではありません。

- [WCF Data Services](/dotnet/framework/data/wcf/wcf-data-services-overview)。

- [!INCLUDE[ssAstoria](../data-tools/includes/ssastoria_md.md)] のデータ モデル。

- Entity Data Model および ADO.NET Entity Framework。 詳細については、「 [Entity Framework の概要](/dotnet/framework/data/adonet/ef/overview)」を参照してください。

- WPF データ バインディング。 詳細については、「 [データバインディングの概要](/dotnet/desktop-wpf/data/data-binding-overview)」を参照してください。

## <a name="create-the-service-project"></a>サービスプロジェクトを作成する

1. このチュートリアルを開始するには、C# または Visual Basic **ASP.NET Web アプリケーション** プロジェクトを作成します。 プロジェクトに **adventureworksservice.svc** という名前を指定します。

2. **ソリューション エクスプローラー** で、 **Default.aspx** を右クリックし、 **[削除]** を選択します。 このチュートリアルでは、このファイルは必要ありません。

## <a name="create-an-entity-data-model-for-the-service"></a>サービスの Entity Data Model を作成する

WCF Data Service を使用してアプリケーションにデータを公開するには、サービスのデータモデルを定義する必要があります。 WCF Data Service では、エンティティデータモデルと、インターフェイスを実装する共通言語ランタイム (CLR) オブジェクトを使用して定義されたカスタムデータモデルの2種類のデータモデルがサポートされています。 <xref:System.Linq.IQueryable%601> このチュートリアルでは、データ モデルとして Entity Data Model を作成します。

1. **[プロジェクト]** メニューの **[新しい項目の追加]** をクリックします。

2. [インストールされたテンプレート] ボックスの一覧で、 **[データ]** をクリックし、 **[ADO.NET エンティティ データ モデル]** プロジェクト項目を選択します。

3. 名前をに変更し、 `AdventureWorksModel.edmx` [ **追加** ] をクリックします。

     **Entity Data Model** ウィザードが開きます。

4. **[モデルのコンテンツの選択]** ページで、 **[データベースから生成]** をクリックし、 **[次へ]** をクリックします。

5. **[データ接続の選択]** ページで、次のいずれかのオプションを選択します。

    - AdventureWorksLT サンプル データベースへのデータ接続がドロップダウン リストに表示されている場合は、これを選択します。

    - **[新しい接続]** をクリックして、AdventureWorksLT データベースへの接続を作成します。

6. **[データ接続の選択]** ページで、 **[エンティティ接続設定に名前を付けて App.Config に保存]** オプションが選択されていることを確認し、 **[次へ]** をクリックします。

7. **[データベース オブジェクトの選択]** ページで、 **[テーブル]** を展開し、 **SalesOrderHeader** テーブルを選択します。

8. **[完了]** をクリックします。

## <a name="create-the-service"></a>サービスの作成

WCF データサービスを作成し、Entity Data Model のデータを WPF アプリケーションに公開します。

1. **[プロジェクト]** メニューで、 **[新しい項目の追加]** を選択します。

2. **[インストールされたテンプレート]** ボックスの一覧で、で、 **[Web]** をクリックし、 **[WCF Data Service]** プロジェクト項目を選択します。

3. [ **名前** ] ボックスに「 `AdventureWorksService.svc` 」と入力し、[ **追加** ] をクリックします。

     Visual Studio によってがプロジェクトに追加され `AdventureWorksService.svc` ます。

## <a name="configure-the-service"></a>サービスの構成

作成した Entity Data Model を操作するには、サービスを構成する必要があります。

1. `AdventureWorks.svc`コードファイルで、 **adventureworksservice.svc** クラスの宣言を次のコードに置き換えます。

     [!code-csharp[Data_WPFWCF#1](../data-tools/codesnippet/CSharp/bind-wpf-controls-to-a-wcf-data-service_1.cs)]
     [!code-vb[Data_WPFWCF#1](../data-tools/codesnippet/VisualBasic/bind-wpf-controls-to-a-wcf-data-service_1.vb)]

     このコードは、 **AdventureWorksService** <xref:System.Data.Services.DataService%601> `AdventureWorksLTEntities` Entity Data Model のオブジェクトコンテキストクラスで動作するから派生するように、adventureworksservice.svc クラスを更新します。 また、`InitializeService` メソッドも更新され、`SalesOrderHeader` エンティティへの完全な読み取り/書き込みアクセスがサービスのクライアントに許可されます。

2. プロジェクトをビルドし、エラーが発生しないことを確認します。

## <a name="create-the-wpf-client-application"></a>WPF クライアントアプリケーションを作成する

WCF Data Service のデータを表示するには、サービスに基づくデータソースを含む新しい WPF アプリケーションを作成します。 このチュートリアルの後半で、データ バインド コントロールをアプリケーションに追加します。

1. **ソリューション エクスプローラー** で、ソリューション ノードを右クリックし、 **[追加]** をクリックして、 **[新しいプロジェクト]** を選択します。

2. **[新しいプロジェクト]** ダイアログで、 **[Visual C#]** または **[Visual Basic]** を展開し、 **[Windows]** を選択します。

3. **[WPF アプリケーション]** プロジェクト テンプレートを選択します。

4. **[名前]** ボックスに `AdventureWorksSalesEditor` と入力して、 **[OK]** をクリックします。

   Visual Studio によってソリューションにプロジェクトが追加され `AdventureWorksSalesEditor` ます。

5. **[データ]** メニューの **[データ ソースの表示]** をクリックします。

   **[データ ソース]** ウィンドウが開きます。

6. **[データ ソース]** ウィンドウで、 **[新しいデータ ソースの追加]** をクリックします。

   **データソース構成** ウィザードが開きます。

7. ウィザードの **[データ ソースの種類を選択]** ページで、 **[サービス]** を選択し、 **[次へ]** をクリックします。

8. **[サービス参照の追加]** ダイアログ ボックスで、 **[探索]** をクリックします。

   Visual Studio は、現在のソリューションで利用可能なサービスを検索し、[ `AdventureWorksService.svc` **サービス** ] ボックスで利用可能なサービスの一覧に追加します。

9. **[名前空間]** ボックスに「 **AdventureWorksService** 」と入力します。

10. **[サービス]** ボックスで **[AdventureWorksService.svc]** をクリックし、 **[OK]** をクリックします。

    Visual Studio によってサービス情報がダウンロードされ、 **データ ソース構成** ウィザードに戻ります。

11. **[サービス参照の追加]** ページで、 **[完了]** をクリックします。

    Visual Studio によって、サービスから返されたデータを表すノードが **[データ ソース]** ウィンドウに追加されます。

## <a name="define-the-user-interface"></a>ユーザーインターフェイスを定義する

WPF デザイナーで XAML を変更して、いくつかのボタンをウィンドウに追加します。 これらのボタンを使用して販売レコードを表示および更新できるようにするコードは、このチュートリアルで後で追加します。

1. **ソリューション エクスプローラー** で、 **MainWindow.xaml** をダブルクリックします。

   WPF デザイナーでウィンドウが開きます。

2. デザイナーの [!INCLUDE[TLA#tla_titlexaml](../data-tools/includes/tlasharptla_titlexaml_md.md)] ビューで、`<Grid>` タグの間に次のコードを追加します。

   ```xaml
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

`SalesOrderHeaders`[ **データソース** ] ウィンドウからデザイナーにノードをドラッグして、顧客レコードを表示するコントロールを作成します。

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

     Visual Studio によって、 **Product** テーブルのデータにバインドされるコントロール セットを作成する XAML とコードが生成されます。 生成される XAML とコードの詳細については、「 [Visual Studio でのデータへの WPF コントロールのバインド](../data-tools/bind-wpf-controls-to-data-in-visual-studio.md)」を参照してください。

5. デザイナーで、 **[Customer ID]** ラベルの横のテキスト ボックスをクリックします。

6. **[プロパティ]** ウィンドウで、 **IsReadOnly** プロパティの横のチェック ボックスをオンにします。

7. 次の各テキスト ボックスに **IsReadOnly** プロパティを設定します。

    - **注文書番号**

    - **[Sales Order ID]**

    - **Sales Order Number**

## <a name="load-the-data-from-the-service"></a>サービスからのデータの読み込み

サービスから販売データを読み込むには、サービスプロキシオブジェクトを使用します。 次に、返されたデータを WPF ウィンドウののデータソースに割り当て <xref:System.Windows.Data.CollectionViewSource> ます。

1. 作成するため、デザイナーで、`Window_Loaded`イベント ハンドラーを読み取るテキストをダブルクリックします **MainWindow** 。

2. イベント ハンドラーを次のコードで置き換えます。 このコードの *localhost* アドレスは、使用している開発コンピューターのローカル ホスト アドレスで置き換えてください。

     [!code-csharp[Data_WPFWCF#2](../data-tools/codesnippet/CSharp/bind-wpf-controls-to-a-wcf-data-service_2.cs)]
     [!code-vb[Data_WPFWCF#2](../data-tools/codesnippet/VisualBasic/bind-wpf-controls-to-a-wcf-data-service_2.vb)]

## <a name="navigate-sales-records"></a>販売レコードの移動

ボタンを使用して、ユーザーが販売レコードをスクロールできるようにするコードを追加し **\<** and **>** ます。

1. デザイナーで、ウィンドウ画面のボタンをダブルクリックし **<** ます。

     Visual Studio によって分離コード ファイルが開かれ、`backButton_Click` イベントのために新しい <xref:System.Windows.Controls.Primitives.ButtonBase.Click> イベント ハンドラーが作成されます。

2. 生成された `backButton_Click` イベント ハンドラーに次のコードを追加します。

     [!code-csharp[Data_WPFWCF#3](../data-tools/codesnippet/CSharp/bind-wpf-controls-to-a-wcf-data-service_3.cs)]
     [!code-vb[Data_WPFWCF#3](../data-tools/codesnippet/VisualBasic/bind-wpf-controls-to-a-wcf-data-service_3.vb)]

3. デザイナーに戻り、ボタンをダブルクリックし **>** ます。

     Visual Studio によって分離コード ファイルが開かれ、`nextButton_Click` イベントのために新しい <xref:System.Windows.Controls.Primitives.ButtonBase.Click> イベント ハンドラーが作成されます。

4. 生成された `nextButton_Click` イベント ハンドラーに次のコードを追加します。

     [!code-csharp[Data_WPFWCF#4](../data-tools/codesnippet/CSharp/bind-wpf-controls-to-a-wcf-data-service_4.cs)]
     [!code-vb[Data_WPFWCF#4](../data-tools/codesnippet/VisualBasic/bind-wpf-controls-to-a-wcf-data-service_4.vb)]

## <a name="save-changes-to-sales-records"></a>販売レコードへの変更を保存する

ユーザーが販売レコードを表示し、 **[変更の保存]** ボタンを使用して変更を保存できるようにするコードを追加します。

1. デザイナーで、[ **変更の保存** ] ボタンをダブルクリックします。

     Visual Studio によって分離コード ファイルが開かれ、`saveButton_Click` イベントのために新しい <xref:System.Windows.Controls.Primitives.ButtonBase.Click> イベント ハンドラーが作成されます。

2. `saveButton_Click` イベント ハンドラーに次のコードを追加します。

     [!code-csharp[Data_WPFWCF#5](../data-tools/codesnippet/CSharp/bind-wpf-controls-to-a-wcf-data-service_5.cs)]
     [!code-vb[Data_WPFWCF#5](../data-tools/codesnippet/VisualBasic/bind-wpf-controls-to-a-wcf-data-service_5.vb)]

## <a name="test-the-application"></a>アプリケーションをテストする

アプリケーションをビルドして実行し、顧客レコードを表示および更新できることを確認します。

1. [ **ビルド** ] メニューの [ **ソリューションのビルド** ] をクリックします。 ソリューションがエラーなしでビルドされることを確認します。

2. **Ctrl** + **F5** キーを押します。

     Visual Studio によって、 **AdventureWorksService** プロジェクトがデバッグなしで開始されます。

3. **ソリューション エクスプローラー** で、 **AdventureWorksSalesEditor** プロジェクトを右クリックします。

4. 右クリックメニュー (コンテキストメニュー) で、[ **デバッグ** ] の下にある [ **新しいインスタンスを開始** ] をクリックします。

     アプリケーションが実行されます。 次の点を確認します。

    - テキスト ボックスに、先頭の販売レコードの各種データ フィールドが表示されること。このレコードの販売注文 ID は **71774** です。

    - **>** または **<** ボタンをクリックすると、他の販売レコード間を移動できます。

5. いずれかの販売レコードの **[コメント]** ボックスに任意のテキストを入力し、 **[変更の保存]** をクリックします。

6. アプリケーションを終了し、Visual Studio からもう一度アプリケーションを起動します。

7. 変更した販売レコードに移動し、アプリケーションを終了して再起動した後でも変更が保持されていることを確認します。

8. アプリケーションを終了します。

## <a name="next-steps"></a>次のステップ

このチュートリアルを完了した後、関連する次のタスクを実行できます。

- Visual Studio の **[データ ソース]** ウィンドウを使用して、WPF コントロールをその他の種類のデータ ソースにバインドする方法について学習します。 詳細については、「 [データセットへの WPF コントロールのバインド](../data-tools/bind-wpf-controls-to-a-dataset.md)」を参照してください。

- Visual Studio の **[データ ソース]** ウィンドウを使用して、WPF コントロールでの関連するデータ (つまり、親子関係にあるデータ) を表示する方法について学習します。 詳細については、「 [チュートリアル: WPF アプリケーションでの関連データの表示](../data-tools/display-related-data-in-wpf-applications.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [Visual Studio でデータに WPF コントロールをバインドする](../data-tools/bind-wpf-controls-to-data-in-visual-studio.md)
- [データセットへの WPF コントロールのバインド](../data-tools/bind-wpf-controls-to-a-dataset.md)
- [WCF の概要 (.NET Framework)](/dotnet/framework/data/wcf/wcf-data-services-overview)
- [Entity Framework の概要 (.NET Framework)](/dotnet/framework/data/adonet/ef/overview)
- [データバインディングの概要 (.NET Framework)](/dotnet/desktop-wpf/data/data-binding-overview)
