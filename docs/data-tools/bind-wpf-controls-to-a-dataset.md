---
title: データセットへの WPF コントロールのバインド
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- WPF, data binding in Visual Studio
- WPF data binding [Visual Studio], walkthroughs
- WPF Designer, data binding
ms.assetid: 177420b9-568b-4dad-9d16-1b0e98a24d71
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 3ad960054e0c2dfe6470c51adbd9f3675fc87952
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85282918"
---
# <a name="bind-wpf-controls-to-a-dataset"></a>データセットへの WPF コントロールのバインド

このチュートリアルでは、データバインドコントロールを含む WPF アプリケーションを作成します。 コントロールは、データセットでカプセル化された製品レコードにバインドされます。 また、製品を参照して製品レコードへの変更を保存するためのボタンを追加します。

このチュートリアルでは、次の作業について説明します。

- WPF アプリケーションと、AdventureWorksLT サンプル データベースのデータから生成されるデータセットを作成する。

- **[データ ソース]** ウィンドウから WPF デザイナーのウィンドウにデータ テーブルをドラッグして、一連のデータ バインド コントロールを作成する。

- 製品レコード間を前後に移動するためのボタンを作成する。

- ユーザーが製品レコードに加えた変更を、データ テーブルおよび基になるデータ ソースに保存するボタンを作成する。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

## <a name="prerequisites"></a>必須コンポーネント

このチュートリアルを実行するには、次のコンポーネントが必要です。

- Visual Studio

- AdventureWorks Light (AdventureWorksLT) サンプルデータベースがアタッチされている SQL Server または SQL Server Express の実行中のインスタンスへのアクセス。 AdventureWorksLT データベースは、 [CodePlex アーカイブ](https://archive.codeplex.com/?p=awlt2008dbscript)からダウンロードできます。

次の概念に関する知識があると役立ちますが、チュートリアルを実行するうえで必須というわけではありません。

- データセットおよび TableAdapter。 詳細については、「 [Visual Studio のデータセットツール](../data-tools/dataset-tools-in-visual-studio.md)」および「 [tableadapter](../data-tools/create-and-configure-tableadapters.md)」を参照してください。

- WPF データ バインディング。 詳しくは、「 [データ バインディングの概要](/dotnet/desktop-wpf/data/data-binding-overview)」をご覧ください。

## <a name="create-the-project"></a>プロジェクトを作成する

新しい WPF プロジェクトを作成して、製品レコードを表示します。

::: moniker range="vs-2017"

1. Visual Studio を開きます。

2. **[ファイル]** メニューの **[新規]** > **[プロジェクト]** を選択します。

3. **[Visual Basic]** または **[Visual C#]** を展開し、**[Windows]** を選択します。

4. [ **WPF アプリケーション**] プロジェクトテンプレートを選択します。

5. [**名前**] ボックスに「 **AdventureWorksProductsEditor** 」と入力し、[ **OK]** を選択します。

::: moniker-end

::: moniker range=">=vs-2019"

1. Visual Studio を開きます。

2. スタート ウィンドウで、 **[新しいプロジェクトの作成]** を選択します。

3. C# の**WPF アプリ**プロジェクトテンプレートを検索し、プロジェクトを作成する手順に従って、プロジェクトに**AdventureWorksProductsEditor**という名前を付けます。

::: moniker-end

   Visual Studio によって AdventureWorksProductsEditor プロジェクトが作成されます。

## <a name="create-a-dataset-for-the-application"></a>アプリケーションのデータセットを作成する

データ バインド コントロールを作成するには、まず、アプリケーション用のデータ モデルを定義し、**[データ ソース]** ウィンドウに追加する必要があります。 このチュートリアルでは、データ モデルとして使用するデータセットを作成します。

1. **[データ]** メニューの **[データ ソースの表示]** をクリックします。

   **[データ ソース]** ウィンドウが開きます。

2. **[データ ソース]** ウィンドウで、 **[新しいデータ ソースの追加]** をクリックします。

   **データソース構成**ウィザードが開きます。

3. **[データソースの種類を選択]** ページで、**[データベース]** を選択し、**[次へ]** をクリックします。

4. **[データベース モデルの選択]** ページで、**[データセット]** を選択し、**[次へ]** をクリックします。

5. **[データ接続の選択]** ページで、次のいずれかのオプションを選択します。

   - AdventureWorksLT サンプル データベースへのデータ接続がドロップダウン リストに表示されている場合は、これを選択し、**[次へ]** をクリックします。

   - **[新しい接続]** をクリックして、AdventureWorksLT データベースへの接続を作成します。

6. **[接続文字列をアプリケーション構成ファイルに保存する]** ページで、**[次の名前で接続を保存する]** チェック ボックスをオンにし、**[次へ]** をクリックします。

7. **[データベース オブジェクトの選択]** ページで、**[テーブル]** を展開し、**Product (SalesLT)** テーブルを選択します。

8. **[完了]** をクリックします。

   Visual Studio によって新しいファイルがプロジェクトに追加され、 `AdventureWorksLTDataSet.xsd` 対応する**adventureworksltdataset.xsd**アイテムが [**データソース**] ウィンドウに追加されます。 このファイルは、という名前の `AdventureWorksLTDataSet.xsd` 型指定されたデータセットと、という名前の TableAdapter を定義し `AdventureWorksLTDataSet` `ProductTableAdapter` ます。 このチュートリアルの後半で、`ProductTableAdapter` を使用してデータセットにデータを読み込み、変更をデータベースに保存します。

9. プロジェクトをビルドします。

## <a name="edit-the-default-fill-method-of-the-tableadapter"></a>TableAdapter の既定の fill メソッドを編集する

データセットにデータを読み込むには、`Fill` の `ProductTableAdapter` メソッドを使用します。 既定では、`Fill` メソッドによって、`ProductDataTable` の `AdventureWorksLTDataSet` に Product テーブルのすべてのデータ行が読み込まれます。 このメソッドは、行のサブセットのみを返すように変更できます。 このチュートリアルでは、写真付きの製品の行のみを返すように `Fill` メソッドを変更します。

1. **ソリューション エクスプローラー**で、*AdventureWorksLTDataSet.xsd* ファイルをダブルクリックします。

     データセット デザイナーが開きます。

2. デザイナーで、**[Fill**, **GetData()]** クエリを右クリックし、**[構成]** を選択します。

     **TableAdapter 構成**ウィザードが開きます。

3. **[SQL ステートメントの入力]** ページのテキスト ボックスで、`SELECT` ステートメントの後に次の WHERE 句を追加します。

    ```sql
    WHERE ThumbnailPhotoFileName <> 'no_image_available_small.gif'
    ```

4. **[完了]** をクリックします。

## <a name="define-the-user-interface"></a>ユーザーインターフェイスを定義する

WPF デザイナーで XAML を変更して、いくつかのボタンをウィンドウに追加します。 これらのボタンを使用して製品レコード間をスクロールしたり、製品レコードへの変更を保存したりできるようにするコードは、このチュートリアルで後で追加します。

1. **ソリューション エクスプローラー**で、*MainWindow.xaml* をダブルクリックします。

    **WPF デザイナー**でウィンドウが開きます。

2. デザイナーの [!INCLUDE[TLA#tla_titlexaml](../data-tools/includes/tlasharptla_titlexaml_md.md)] ビューで、`<Grid>` タグの間に次のコードを追加します。

   ```xaml
   <Grid.RowDefinitions>
       <RowDefinition Height="75" />
       <RowDefinition Height="625" />
   </Grid.RowDefinitions>
   <Button HorizontalAlignment="Left" Margin="22,20,0,24" Name="backButton" Width="75"><</Button>
   <Button HorizontalAlignment="Left" Margin="116,20,0,24" Name="nextButton" Width="75">></Button>
   <Button HorizontalAlignment="Right" Margin="0,21,46,24" Name="saveButton" Width="110">Save changes</Button>
   ```

3. プロジェクトをビルドします。

## <a name="create-data-bound-controls"></a>データ バインド コントロールを作成する

`Product`[**データソース**] ウィンドウから WPF デザイナーにテーブルをドラッグして、顧客レコードを表示するコントロールを作成します。

1. **[データ ソース]** ウィンドウで、**[Product]** ノードのドロップダウン メニューをクリックし、**[詳細]** を選択します。

2. **[Product]** ノードを展開します。

3. この例ではいくつかのフィールドを非表示にするために、次のノードの横のドロップダウン メニューをクリックして **[なし]** を選択します。

    - ProductCategoryID

    - ProductModelID

    - ThumbnailPhotoFileName

    - rowguid

    - ModifiedDate

4. **[ThumbNailPhoto]** ノードの横にあるドロップダウン メニューをクリックし、**[イメージ]** を選択します。

    > [!NOTE]
    > 既定では、画像を表す **[データ ソース]** ウィンドウ内の項目は、既定のコントロールが **[なし]** に設定されています。 これは、画像がデータベース内でバイト配列として格納されているためです。バイト配列には、単純なバイト配列から大規模なアプリケーションの実行可能ファイルまで、あらゆるデータを格納できます。

5. **[データ ソース]** ウィンドウから、ボタンがある行の下のグリッド行に **[Product]** ノードをドラッグします。

     Visual Studio によって、**Product** テーブルのデータにバインドされるコントロール セットを定義する XAML が生成されます。 また、データを読み込むコードも生成されます。 生成される XAML とコードの詳細については、「 [Visual Studio でのデータへの WPF コントロールのバインド](../data-tools/bind-wpf-controls-to-data-in-visual-studio.md)」を参照してください。

6. デザイナーで、**[Product ID]** ラベルの横のテキスト ボックスをクリックします。

7. **[プロパティ]** ウィンドウで、**IsReadOnly** プロパティの横のチェック ボックスをオンにします。

## <a name="navigate-product-records"></a>製品レコードの移動

ボタンを使用して、ユーザーが製品レコードをスクロールできるようにするコードを追加し **\<** and **>** ます。

1. デザイナーで、ウィンドウ画面のボタンをダブルクリックし **<** ます。

     Visual Studio によって分離コード ファイルが開かれ、`backButton_Click` イベントのために新しい <xref:System.Windows.Controls.Primitives.ButtonBase.Click> イベント ハンドラーが作成されます。

2. `Window_Loaded` イベント ハンドラーを変更して、`ProductViewSource`、`AdventureWorksLTDataSet`、`AdventureWorksLTDataSetProductTableAdapter` がメソッドの外部になり、フォーム全体からアクセスできるようにします。 これらのをフォームに対してグローバルに宣言し、 `Window_Loaded` 次のようなイベントハンドラー内でそれらを割り当てます。

     [!code-csharp[Data_WPFDATASET#1](../data-tools/codesnippet/CSharp/bind-wpf-controls-to-a-dataset_1.cs)]
     [!code-vb[Data_WPFDATASET#1](../data-tools/codesnippet/VisualBasic/bind-wpf-controls-to-a-dataset_1.vb)]

3. `backButton_Click` イベント ハンドラーに次のコードを追加します。

     [!code-csharp[Data_WPFDATASET#2](../data-tools/codesnippet/CSharp/bind-wpf-controls-to-a-dataset_2.cs)]
     [!code-vb[Data_WPFDATASET#2](../data-tools/codesnippet/VisualBasic/bind-wpf-controls-to-a-dataset_2.vb)]

4. デザイナーに戻り、ボタンをダブルクリックし **>** ます。

5. `nextButton_Click` イベント ハンドラーに次のコードを追加します。

     [!code-csharp[Data_WPFDATASET#3](../data-tools/codesnippet/CSharp/bind-wpf-controls-to-a-dataset_3.cs)]
     [!code-vb[Data_WPFDATASET#3](../data-tools/codesnippet/VisualBasic/bind-wpf-controls-to-a-dataset_3.vb)]

## <a name="save-changes-to-product-records"></a>製品レコードへの変更を保存する

ユーザーが **[変更の保存]** ボタンを使用して製品レコードへの変更を保存できるようにするコードを追加します。

1. デザイナーで、**[変更の保存]** をダブルクリックします。

     Visual Studio によって分離コード ファイルが開かれ、`saveButton_Click` イベントのために新しい <xref:System.Windows.Controls.Primitives.ButtonBase.Click> イベント ハンドラーが作成されます。

2. `saveButton_Click` イベント ハンドラーに次のコードを追加します。

     [!code-csharp[Data_WPFDATASET#4](../data-tools/codesnippet/CSharp/bind-wpf-controls-to-a-dataset_4.cs)]
     [!code-vb[Data_WPFDATASET#4](../data-tools/codesnippet/VisualBasic/bind-wpf-controls-to-a-dataset_4.vb)]

    > [!NOTE]
    > この例では、`Save` の `TableAdapter` メソッドを使用して変更を保存します。 このチュートリアルでは、データ テーブルが 1 つのみ変更されるため、この方法が適しています。 複数のデータ テーブルへの変更を保存する必要がある場合は、Visual Studio によってデータセットと共に生成される `UpdateAll` の `TableAdapterManager` メソッドを使用することもできます。 詳細については、「 [tableadapter](../data-tools/create-and-configure-tableadapters.md)」を参照してください。

## <a name="test-the-application"></a>アプリケーションをテストする

アプリケーションをビルドして実行します。 製品レコードを表示および更新できることを確認します。

1. **F5**キーを押します。

     アプリケーションがビルドされ、実行されます。 次の点を確認します。

    - テキスト ボックスに、写真付きの製品の先頭のレコードのデータが表示されること。 この製品の製品 ID は 713 で、製品名は **Long-Sleeve Logo Jersey, S** です。

    - **>** または **<** ボタンをクリックすると、他の製品レコード間を移動できます。

2. いずれかの製品レコードで **[サイズ]** の値を変更し、**[変更の保存]** をクリックします。

3. アプリケーションを終了し、Visual Studio で **F5** キーを押してアプリケーションを再起動します。

4. 変更した製品レコードに移動し、変更が保持されていることを確認します。

5. アプリケーションを終了します。

## <a name="next-steps"></a>次の手順

このチュートリアルを完了すると、次の関連タスクを試すことができます。

- Visual Studio の **[データ ソース]** ウィンドウを使用して、WPF コントロールをその他の種類のデータ ソースにバインドする方法について学習します。 詳細については、「 [WCF データサービスへの WPF コントロールのバインド](../data-tools/bind-wpf-controls-to-a-wcf-data-service.md)」を参照してください。

- Visual Studio の **[データ ソース]** ウィンドウを使用して、WPF コントロールでの関連するデータ (つまり、親子関係にあるデータ) を表示する方法について学習します。 詳細については、「[チュートリアル: WPF アプリで関連データを表示](../data-tools/display-related-data-in-wpf-applications.md)する」を参照してください。

## <a name="see-also"></a>関連項目

- [Visual Studio でデータに WPF コントロールをバインドする](../data-tools/bind-wpf-controls-to-data-in-visual-studio.md)
- [Visual Studio のデータセットツール](../data-tools/dataset-tools-in-visual-studio.md)
- [データ バインディングの概要](/dotnet/desktop-wpf/data/data-binding-overview)
