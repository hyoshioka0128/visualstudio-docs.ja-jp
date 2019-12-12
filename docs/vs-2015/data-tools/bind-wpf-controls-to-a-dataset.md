---
title: WPF コントロールを dataset にバインドする |Microsoft Docs
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
ms.assetid: 177420b9-568b-4dad-9d16-1b0e98a24d71
caps.latest.revision: 35
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: f0ad4ea108cb0ec3b874c7f360be2e1f0e25ef45
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74299418"
---
# <a name="bind-wpf-controls-to-a-dataset"></a>データセットへの WPF コントロールのバインド
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このチュートリアルでは、データ バインド コントロールが含まれた WPF アプリケーションを作成します。 コントロールは、データセットでカプセル化された製品レコードにバインドされます。 また、製品を参照するためのボタンの追加と、製品レコードへの変更の保存も行います。

 このチュートリアルでは、次の作業について説明します。

- WPF アプリケーションと、AdventureWorksLT サンプル データベースのデータから生成されるデータセットを作成する。

- **[データ ソース]** ウィンドウから WPF デザイナーのウィンドウにデータ テーブルをドラッグして、一連のデータ バインド コントロールを作成する。

- 製品レコード間を前後に移動するためのボタンを作成する。

- ユーザーが製品レコードに加えた変更を、データ テーブルおよび基になるデータ ソースに保存するボタンを作成する。

   [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]

- AdventureWorksLT サンプル データベースが添付された、SQL Server または SQL Server Express の実行中のインスタンスへのアクセス権。 AdventureWorksLT データベースは、 [CodePlex Web サイト](https://go.microsoft.com/fwlink/?linkid=87843)からダウンロードできます。

  次の概念に関する知識があると役立ちますが、チュートリアルを実行するうえで必須というわけではありません。

- データセットおよび TableAdapter。 詳細については、「 [Visual Studio のデータセットツール](../data-tools/dataset-tools-in-visual-studio.md)」を参照してください。

- WPF デザイナーの操作。 詳細については、「 [WPF と Silverlight デザイナーの概要](https://msdn.microsoft.com/570b7a5c-0c86-4326-a371-c9b63378fc62)」を参照してください。

- WPF データ バインディング。 詳しくは、「[データ バインディングの概要](https://msdn.microsoft.com/library/c707c95f-7811-401d-956e-2fffd019a211)」をご覧ください。

## <a name="create-the-project"></a>プロジェクトの作成
 新しい WPF プロジェクトを作成します。 このプロジェクトでは、製品レコードを表示します。

#### <a name="to-create-the-project"></a>プロジェクトを作成するには

1. Visual Studio を起動します。

2. **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。

3. **[Visual Basic]** または **[Visual C#]** を展開し、 **[Windows]** を選択します。

4. **[WPF アプリケーション]** プロジェクト テンプレートを選択します。

5. **[名前]** ボックスに「`AdventureWorksProductsEditor`」と入力し、[ **OK]** をクリックします。

     Visual Studio によって `AdventureWorksProductsEditor` プロジェクトが作成されます。

## <a name="create-a-dataset-for-the-application"></a>アプリケーションのデータセットを作成する
 データ バインド コントロールを作成するには、まず、アプリケーション用のデータ モデルを定義し、 **[データ ソース]** ウィンドウに追加する必要があります。 このチュートリアルでは、データ モデルとして使用するデータセットを作成します。

#### <a name="to-create-a-dataset"></a>データセットを作成するには

1. **[データ]** メニューの **[データ ソースの表示]** をクリックします。

     **[データ ソース]** ウィンドウが開きます。

2. **[データ ソース]** ウィンドウで、 **[新しいデータ ソースの追加]** をクリックします。

     **データ ソース構成**ウィザードが開きます。

3. **[データソースの種類を選択]** ページで、 **[データベース]** を選択し、 **[次へ]** をクリックします。

4. **[データベース モデルの選択]** ページで、 **[データセット]** を選択し、 **[次へ]** をクリックします。

5. **[データ接続の選択]** ページで、次のいずれかのオプションを選択します。

    - AdventureWorksLT サンプル データベースへのデータ接続がドロップダウン リストに表示されている場合は、これを選択し、 **[次へ]** をクリックします。

    - **[新しい接続]** をクリックして、AdventureWorksLT データベースへの接続を作成します。

6. **[接続文字列をアプリケーション構成ファイルに保存する]** ページで、 **[次の名前で接続を保存する]** チェック ボックスをオンにし、 **[次へ]** をクリックします。

7. **[データベース オブジェクトの選択]** ページで、 **[テーブル]** を展開し、**Product (SalesLT)** テーブルを選択します。

8. **[完了]** をクリックします。

     Visual Studio によって新しい Adventureworksltdataset.xsd ファイルがプロジェクトに追加され、対応する**adventureworksltdataset.xsd**項目が **[データソース]** ウィンドウに追加されます。 AdventureWorksLTDataSet.xsd ファイルには、`AdventureWorksLTDataSet` という名前の型指定されたデータセットと、`ProductTableAdapter` という名前の TableAdapter が定義されます。 このチュートリアルの後半で、`ProductTableAdapter` を使用してデータセットにデータを読み込み、変更をデータベースに保存します。

9. プロジェクトをビルドします。

## <a name="edit-the-default-fill-method-of-the-tableadapter"></a>TableAdapter の既定の fill メソッドを編集する
 データセットにデータを読み込むには、`Fill` の `ProductTableAdapter` メソッドを使用します。 既定では、`Fill` メソッドによって、`ProductDataTable` の `AdventureWorksLTDataSet` に Product テーブルのすべてのデータ行が読み込まれます。 このメソッドは、行のサブセットのみを返すように変更できます。 このチュートリアルでは、写真付きの製品の行のみを返すように `Fill` メソッドを変更します。

#### <a name="to-load-product-rows-that-have-photos"></a>写真付きの製品の行を読み込むには

1. **ソリューションエクスプローラー**で、adventureworksltdataset.xsd ファイルをダブルクリックします。

     データセット デザイナーが開きます。

2. デザイナーで、 **Fill、GetData ()** クエリを右クリックし、 **[構成]** を選択します。

     **TableAdapter 構成**ウィザードが開きます。

3. **[SQL ステートメントの入力]** ページのテキスト ボックスで、`SELECT` ステートメントの後に次の WHERE 句を追加します。

    ```
    WHERE ThumbnailPhotoFileName <> 'no_image_available_small.gif'
    ```

4. **[完了]** をクリックします。

## <a name="define-the-user-interface"></a>ユーザーインターフェイスを定義する
 WPF デザイナーで XAML を変更して、いくつかのボタンをウィンドウに追加します。 これらのボタンを使用して製品レコード間をスクロールしたり、製品レコードへの変更を保存したりできるようにするコードは、このチュートリアルで後で追加します。

#### <a name="to-define-the-user-interface-of-the-window"></a>ウィンドウのユーザー インターフェイスを定義するには

1. **ソリューションエクスプローラー**で、mainwindow.xaml をダブルクリックします。

     WPF デザイナーでウィンドウが開きます。

2. デザイナーの [!INCLUDE[TLA#tla_titlexaml](../includes/tlasharptla-titlexaml-md.md)] ビューで、`<Grid>` タグの間に次のコードを追加します。

    ```
    <Grid.RowDefinitions>
        <RowDefinition Height="75" />
        <RowDefinition Height="625" />
    </Grid.RowDefinitions>
    <Button HorizontalAlignment="Left" Margin="22,20,0,24" Name="backButton" Width="75"><</Button>
    <Button HorizontalAlignment="Left" Margin="116,20,0,24" Name="nextButton" Width="75">></Button>
    <Button HorizontalAlignment="Right" Margin="0,21,46,24" Name="saveButton" Width="110">Save changes</Button>
    ```

3. プロジェクトをビルドします。

## <a name="createdata-bound-controls"></a>Createdata バインドコントロール
 **[データソース]** ウィンドウから WPF デザイナーに `Product` テーブルをドラッグして、顧客レコードを表示するコントロールを作成します。

#### <a name="to-create-data-bound-controls"></a>データ バインド コントロールを作成するには

1. **[データ ソース]** ウィンドウで、 **[Product]** ノードのドロップダウン メニューをクリックし、 **[詳細]** を選択します。

2. **[Product]** ノードを展開します。

3. この例ではいくつかのフィールドを非表示にするために、次のノードの横のドロップダウン メニューをクリックして **[なし]** を選択します。

    - ProductCategoryID

    - ProductModelID

    - ThumbnailPhotoFileName

    - rowguid

    - ModifiedDate

4. **[ThumbNailPhoto]** ノードの横にあるドロップダウン メニューをクリックし、 **[イメージ]** を選択します。

    > [!NOTE]
    > 既定では、画像を表す **[データ ソース]** ウィンドウ内の項目は、既定のコントロールが **[なし]** に設定されています。 これは、画像がデータベース内でバイト配列として格納されているためです。バイト配列には、単純なバイト配列から大規模なアプリケーションの実行可能ファイルまで、あらゆるデータを格納できます。

5. **[データ ソース]** ウィンドウから、ボタンがある行の下のグリッド行に **[Product]** ノードをドラッグします。

     Visual Studio によって、**Product** テーブルのデータにバインドされるコントロール セットを定義する XAML が生成されます。 また、データを読み込むコードも生成されます。 生成される XAML とコードの詳細については、「 [Visual Studio でのデータへの WPF コントロールのバインド](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md)」を参照してください。

6. デザイナーで、 **[Product ID]** ラベルの横のテキスト ボックスをクリックします。

7. **[プロパティ]** ウィンドウで、**IsReadOnly** プロパティの横のチェック ボックスをオンにします。

## <a name="navigating-product-records"></a>製品レコードの移動
 ユーザーが **[\<]** ボタンと **[>]** ボタンを使用して製品レコード間をスクロールできるようにするコードを追加します。

#### <a name="to-enable-users-to-navigate-product-records"></a>ユーザーが製品レコード間を移動できるようにするには

1. デザイナーで、ウィンドウ サーフェイスの **[<]** をダブルクリックします。

     Visual Studio によって分離コード ファイルが開かれ、<xref:System.Windows.Controls.Primitives.ButtonBase.Click> イベントのために新しい `backButton_Click` イベント ハンドラーが作成されます。

2. `Window_Loaded` イベント ハンドラーを変更して、`ProductViewSource`、`AdventureWorksLTDataSet`、`AdventureWorksLTDataSetProductTableAdapter` がメソッドの外部になり、フォーム全体からアクセスできるようにします。 これらのをフォームに対してグローバルに宣言し、次のような `Window_Loaded` イベントハンドラー内でそれらを割り当てます。

     [!code-csharp[Data_WPFDATASET#1](../snippets/csharp/VS_Snippets_ProTools/data_wpfdataset/cs/mainwindow.xaml.cs#1)]
     [!code-vb[Data_WPFDATASET#1](../snippets/visualbasic/VS_Snippets_ProTools/data_wpfdataset/vb/mainwindow.xaml.vb#1)]

3. `backButton_Click` イベント ハンドラーに次のコードを追加します。

     [!code-csharp[Data_WPFDATASET#2](../snippets/csharp/VS_Snippets_ProTools/data_wpfdataset/cs/mainwindow.xaml.cs#2)]
     [!code-vb[Data_WPFDATASET#2](../snippets/visualbasic/VS_Snippets_ProTools/data_wpfdataset/vb/mainwindow.xaml.vb#2)]

4. デザイナーに戻り、 **[>]** をダブルクリックします。

5. `nextButton_Click` イベント ハンドラーに次のコードを追加します。

     [!code-csharp[Data_WPFDATASET#3](../snippets/csharp/VS_Snippets_ProTools/data_wpfdataset/cs/mainwindow.xaml.cs#3)]
     [!code-vb[Data_WPFDATASET#3](../snippets/visualbasic/VS_Snippets_ProTools/data_wpfdataset/vb/mainwindow.xaml.vb#3)]

## <a name="savechanges-to-product-records"></a>Savechanges から製品レコードへ
 ユーザーが **[変更の保存]** ボタンを使用して製品レコードへの変更を保存できるようにするコードを追加します。

#### <a name="to-add-the-ability-to-save-changes-to-product-records"></a>製品レコードへの変更を保存する機能を追加するには

1. デザイナーで、 **[変更の保存]** をダブルクリックします。

     Visual Studio によって分離コード ファイルが開かれ、`saveButton_Click` イベントのために新しい <xref:System.Windows.Controls.Primitives.ButtonBase.Click> イベント ハンドラーが作成されます。

2. `saveButton_Click` イベント ハンドラーに次のコードを追加します。

     [!code-csharp[Data_WPFDATASET#4](../snippets/csharp/VS_Snippets_ProTools/data_wpfdataset/cs/mainwindow.xaml.cs#4)]
     [!code-vb[Data_WPFDATASET#4](../snippets/visualbasic/VS_Snippets_ProTools/data_wpfdataset/vb/mainwindow.xaml.vb#4)]

    > [!NOTE]
    > この例では、`Save` の `TableAdapter` メソッドを使用して変更を保存します。 このチュートリアルでは、データ テーブルが 1 つのみ変更されるため、この方法が適しています。 複数のデータ テーブルへの変更を保存する必要がある場合は、Visual Studio によってデータセットと共に生成される `UpdateAll` の `TableAdapterManager` メソッドを使用することもできます。 詳細については、「 [TableAdapterManager の概要](https://msdn.microsoft.com/library/33076d42-6b41-491a-ac11-6c6339aea650)」を参照してください。

## <a name="test-the-application"></a>アプリケーションをテストする
 アプリケーションをビルドして実行します。 製品レコードを表示および更新できることを確認します。

#### <a name="to-test-the-application"></a>アプリケーションをテストするには

1. **F5**キーを押します。

     アプリケーションがビルドされ、実行されます。 次のことを検証します。

    - テキスト ボックスに、写真付きの製品の先頭のレコードのデータが表示されること。 この製品の製品 ID は 713 で、製品名は **Long-Sleeve Logo Jersey, S** です。

    - **[>]** または **[<]** をクリックして、他の製品レコードに移動できること。

2. いずれかの製品レコードで **[サイズ]** の値を変更し、 **[変更の保存]** をクリックします。

3. アプリケーションを終了し、Visual Studio で **F5** キーを押してアプリケーションを再起動します。

4. 変更した製品レコードに移動し、変更が保持されていることを確認します。

5. アプリケーションを終了します。

## <a name="next-steps"></a>次の手順
 このチュートリアルを完了した後、関連する次のタスクを実行できます。

- Visual Studio の **[データ ソース]** ウィンドウを使用して、WPF コントロールをその他の種類のデータ ソースにバインドする方法について学習します。 詳細については、「 [WCF データサービスへの WPF コントロールのバインド](../data-tools/bind-wpf-controls-to-a-wcf-data-service.md)」を参照してください。

- Visual Studio の **[データ ソース]** ウィンドウを使用して、WPF コントロールでの関連するデータ (つまり、親子関係にあるデータ) を表示する方法について学習します。 詳細については、「[チュートリアル:WPF アプリケーションでの関連データの表示](../data-tools/walkthrough-displaying-related-data-in-a-wpf-application.md)。

## <a name="see-also"></a>関連項目
 Visual studio[でのデータへの wpf コントロール](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md)のバインド visual studio でのデータ[への wpf コントロールのバインド](../data-tools/bind-wpf-controls-to-data-in-visual-studio2.md) [Dataset tools in Visual Studio](../data-tools/dataset-tools-in-visual-studio.md) [Wpf と Silverlight デザイナーの概要](https://msdn.microsoft.com/570b7a5c-0c86-4326-a371-c9b63378fc62)[データバインディング](https://msdn.microsoft.com/library/c707c95f-7811-401d-956e-2fffd019a211)の概要
