---
title: WPF と Entity Framework 6 | を使用した単純なデータアプリケーションの作成Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
ms.assetid: 65929fab-5d78-4e04-af1e-cf4957f230f6
caps.latest.revision: 25
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 403415eaf8a882efdd63fdb9a73b5489b91f2529
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72651087"
---
# <a name="create-a-simple-data-application-with-wpf-and-entity-framework-6"></a>WPF と Entity Framework 6 を使用して単純なデータ アプリケーションを作成する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このチュートリアルでは、SQL Server LocalDB、Northwind データベース、Entity Framework 6、および Windows Presentation Foundation を使用して、Visual Studio で基本的な "フォームオーバーデータ" アプリケーションを作成する方法について説明します。 ここでは、マスター/詳細ビューで基本的なデータバインドを実行する方法について説明します。また、[次に移動]、[前に移動]、[先頭に移動]、[移動]、[更新]、および [削除] のボタンがあるカスタムの "バインドナビゲーター" もあります。

 この記事では、Visual Studio でのデータツールの使用に焦点を当てていますが、基になるテクノロジの詳細については説明しません。 XAML、Entity Framework、および SQL に関する基本的な知識があることを前提としています。 また、この例では、WPF アプリケーションの標準である MVVM アーキテクチャについては説明しません。 ただし、このコードは、わずかな変更で独自の MVVM アプリケーションにコピーできます。

## <a name="install-and-connect-to-northwind"></a>Northwind にインストールして接続する
 この例では SQL Server Express LocalDB と Northwind サンプルデータベースを使用します。 その製品の ADO.NET データプロバイダーが Entity Framework をサポートしている場合は、他の SQL database 製品とも同様に機能します。

1. SQL Server 2014 LocalDB Express 32 ビットをまだインストールしていない場合は、 [SQL Server エディションのダウンロードページ](https://www.microsoft.com/sql-server/sql-server-editions-express)からインストールします。

2. 「 [Install SQL Server sample databases](../data-tools/install-sql-server-sample-databases.md)」の手順に従って、Northwind サンプルデータベースをインストールします。

3. Northwind の[新しい接続を追加](../data-tools/add-new-connections.md)します。

## <a name="configure-the-project"></a>プロジェクトを構成する

1. Visual Studio で、[ **&#124; ファイル** ]、[新しいプロジェクト] の順に選択し、新しい C# WPF アプリケーションを作成します。

2. 次に、Entity Framework 6 の NuGet パッケージを追加します。 ソリューションエクスプローラーで、プロジェクトノードを選択します。 メインメニューで、[**プロジェクト] &#124; [NuGet パッケージの管理**] の順に選択します。

     ![[NuGet パッケージの管理] メニュー項目](../data-tools/media/raddata-vs2015-manage-nuget-packages.png "raddata_vs2015_manage_nuget_packages")

3. NuGet パッケージマネージャーで、[ **参照** ] リンクをクリックします。 Entity Framework は、一覧の最上位のパッケージであると思います。 右側のウィンドウで [ **インストール** ] をクリックし、画面の指示に従います。 インストールが完了すると、[出力] ウィンドウに通知されます。

     ![NuGet パッケージの Entity Framework](../data-tools/media/raddata-vs2015-nuget-ef.png "raddata_vs2015_Nuget_EF")

4. これで、Visual Studio を使用して、Northwind データベースに基づくモデルを作成できるようになりました。

## <a name="create-the-model"></a>モデルを作成する

1. ソリューションエクスプローラーでプロジェクトノードを右クリックし、[ **&#124; 新しい項目の追加**] を選択します。 左側のウィンドウの [C#] ノードで [ **Data** ] を選択し、中央のペインで [ **ADO.NET Entity Data Model**] を選択します。

    ![新しいプロジェクト項目の Entity Framework モデル](../data-tools/media/raddata-ef-new-project-item.png "レーダーデータ EF の新しいプロジェクト項目")

2. モデルを呼び出し `Northwind_model` 、[OK] を選択します。 これにより、 **Entity Data Model ウィザード**が起動します。 [ **データベースから EF Designer** ] を選択し、[ **次へ**] をクリックします。

    ![データベースからの EF モデル](../data-tools/media/raddata-ef-model-from-database.png "データベースからのレーダーデータ EF モデル")

3. 次の画面で、LocalDB Northwind 接続を選択し、[ **次へ**] をクリックします。

4. ウィザードの次のページでは、Entity Framework モデルに含めるテーブル、ストアドプロシージャ、およびその他のデータベースオブジェクトを選択します。 ツリービューで dbo ノードを展開し、Customers、Orders、Order Details を選択します。 既定値のままにして、[ **完了**] をクリックします。

    ![モデルのデータベースオブジェクトを選択する](../data-tools/media/raddata-choose-ef-objects.png "[レーダーデータ] 選択 EF オブジェクト")

5. このウィザードでは、Entity Framework モデルを表す C# クラスが生成されます。 これらは、従来の C# クラスであり、WPF ユーザーインターフェイスにデータをバインドします。 .Edmx ファイルには、クラスをデータベース内のオブジェクトに関連付けるリレーションシップとその他のメタデータが記述されています。  .Tt ファイルは、モデルに対して動作するコードを生成し、変更をデータベースに保存する T4 テンプレートです。 これらのファイルはすべて、[Northwind_model] ノードの下のソリューションエクスプローラーに表示されます。

    ![EF モデルファイルのソリューションエクスプローラー](../data-tools/media/raddata-solution-explorer-ef-model-files.png "ソリューションエクスプローラー EF モデルファイルのレーダーデータ")

    .Edmx ファイルのデザイナー画面を使用すると、モデル内のいくつかのプロパティとリレーションシップを変更できます。 このチュートリアルでは、デザイナーを使用しません。

6. この .tt ファイルは汎用的なものであるため、ObservableCollections を必要とする WPF データバインドを使用するように調整する必要があります。  ソリューションエクスプローラーで、Northwind_model が見つかるまで [Northwind_model] ノードを展開します。 (* に含まれて **いない** ことを確認してください。.Edmx ファイルの直下にあるコンテキストの .tt ファイル)。

   - の2つのオカレンスを <xref:System.Collections.ICollection> に置き換え <xref:System.Collections.ObjectModel.ObservableCollection%601> ます。

   - の最初の出現箇所を、 <xref:System.Collections.Generic.HashSet%601> 51 行目で置き換え <xref:System.Collections.ObjectModel.ObservableCollection%601> ます。 HashSet の2回目の出現を置換しないでください。

   - の出現箇所 <xref:System.Collections.Generic> (334 行目を囲む) のみをに置き換え <xref:System.Collections.ObjectModel> ます。

7. **Ctrl + Shift + B**キーを押して、プロジェクトをビルドします。 ビルドが完了すると、モデルクラスがデータソースウィザードに表示されます。

   これで、データを表示、移動、および変更できるように、このモデルを XAML ページにフックする準備ができました。

## <a name="databind-the-model-to-the-xaml-page"></a>モデルを XAML ページにバインドする
 独自のデータバインドコードを記述することもできますが、Visual Studio により簡単に実行できます。

1. メインメニューから、[&#124; プロジェクト]、[ **新しいデータソースの追加** ] の順に選択し、 **データソース構成ウィザード**を起動します。 データベースではなくモデルクラスにバインドするので、[ **オブジェクト** ] を選択します。

     ![オブジェクトソースを含むデータソース構成ウィザード](../data-tools/media/raddata-data-source-configuration-wizard-with-object-source.png "オブジェクトソースを使用したレーダーデータデータソース構成ウィザード")

2. [顧客] を選びます。  (注文のソースは、Customer の Orders ナビゲーションプロパティから自動的に生成されます)。

     ![エンティティクラスをデータソースとして追加する](../data-tools/media/raddata-add-entity-classes-as-data-sources.png "レーダーデータデータソースとしてエンティティクラスを追加する")

3. **[完了]** をクリックします。

4. コードビューで Mainwindow.xaml に移動します。 この例では、XAML を非常に単純なものにしておきます。 Mainwindow.xaml のタイトルをわかりやすいものに変更し、高さと幅を 600 x 800 に増やします。 後でいつでも変更できます。 ここで、次の3つの行定義をメイングリッドに追加します。1行は顧客の詳細用で、もう1つは注文を表示するグリッド用です。

    ```xaml
    <Grid.RowDefinitions>
               <RowDefinition Height="auto"/>
               <RowDefinition Height="auto"/>
               <RowDefinition Height="*"/>
           </Grid.RowDefinitions>
    ```

5. ここで、デザイナーで表示するように Mainwindow.xaml を開きます。 これにより、[ツールボックス] の横にある Visual Studio のウィンドウマージンに [データソース] ウィンドウがオプションとして表示されます。 タブをクリックしてウィンドウを開くか、 **Shift + Alt + D** キーを押すか、[ **&#124; その他の Windows &#124; データソース**] を選択します。 個々のテキストボックスに Customers クラスの各プロパティを表示します。 まず、[Customers] コンボボックスの矢印をクリックし、[ **Details**] を選択します。 次に、ノードをデザイン画面の中央部分にドラッグして、デザイナーが中央の行に移動することを認識できるようにします。  置き忘れしている場合は、後で XAML で行を手動で指定できます。 既定では、コントロールはグリッド要素に垂直方向に配置されますが、この時点ではフォーム上に配置できます。  たとえば、アドレスの上に [名前] テキストボックスを配置した方がよい場合があります。 この記事のサンプルアプリケーションでは、フィールドを並べ替え、2つの列に並べ替えます。

     ![個々のコントロールに対するデータソースのバインド](../data-tools/media/raddata-customers-data-source-binding-to-individual-controls.png "レーダーデータ顧客データソースと個々のコントロールのバインド")

     コードビューで、 `Grid` 親グリッドの行 1 (中央の行) に新しい要素が表示されるようになりました。 親グリッドには、 `DataContext` 要素に追加された CollectionViewSource を参照する属性があり `Windows.Resources` ます。 そのデータコンテキストを指定すると、たとえば、最初のテキストボックスが、 `Address` CollectionViewSource 内の現在のオブジェクトのプロパティにマップされた名前の "Address" にバインドされ `Customer` ます。

    ```xaml
    <Grid DataContext="{StaticResource customerViewSource}">
    ```

6. ウィンドウの上半分に顧客が表示されている場合は、下半分に注文を表示します。 1つのグリッドビューコントロールに注文を表示します。 マスター/詳細データバインドが想定どおりに動作するには、[個別の注文] ノードではなく、Customers クラスの Orders プロパティにバインドすることが重要です。 次の図に注意してください。 Customers クラスの Orders プロパティをフォームの下半分にドラッグして、デザイナーによって行2に配置されるようにします。

     ![Orders クラスをグリッドとしてドラッグ](../data-tools/media/raddata-drag-orders-classes-as-grid.png "レーダーデータドラッグ順序クラスをグリッドとして")

7. Visual Studio は、UI コントロールをモデル内のイベントに接続するすべてのバインドコードを生成しました。 いくつかのデータを表示するために必要なのは、モデルを作成するためのコードを記述することだけです。 まず、MainWindow.xaml.cs に移動し、データコンテキストの Mainwindow.xaml クラスにデータメンバーを追加します。 このオブジェクトは、生成されたもので、モデル内の変更やイベントを追跡するコントロールのように機能します。 ここでは、後で新しい顧客または新しい注文を追加するために使用する2つのメンバーを追加します。 また、コンストラクターの初期化ロジックも追加します。 クラスの先頭は次のようになります。

    ```csharp
    public partial class MainWindow : Window
       {
           public Customer newCustomer { get; set; }
           public Order newOrder { get; set; }

           NorthwindEntities context = new NorthwindEntities();
           CollectionViewSource custViewSource;
           CollectionViewSource ordViewSource;

           public MainWindow()
           {
               InitializeComponent();
               newCustomer = new Customer();
               newOrder = new Order();
               custViewSource = ((CollectionViewSource)
                   (FindResource("customerViewSource")));
               ordViewSource = ((CollectionViewSource)
                   (FindResource("customerOrdersViewSource")));
               DataContext = this;
           }
    ```

     Add `using` 拡張メソッドをスコープに取り込むために、system.string のディレクティブを追加します。

    ```csharp
    using System.Data.Entity;
    ```

     下にスクロールして、Window_Loaded イベントハンドラーを見つけます。 Visual Studio によって、CollectionViewSource オブジェクトが追加されていることに注意してください。 これは、モデルの作成時に選択した NorthwindEntities オブジェクトを表します。 Window_loaded にコードを追加して、メソッド全体が次のようになるようにしましょう。

    ```csharp
    private void Window_Loaded(object sender, RoutedEventArgs e)
        {
            // Load is an extension method on IQueryable,
            // defined in the System.Data.Entity namespace.
            // This method enumerates the results of the query,
            // similar to ToList but without creating a list.
            // When used with Linq to Entities this method
            // creates entity objects and adds them to the context.
            context.Customers.Load();

            // After the data is loaded call the DbSet<T>.Local property
            // to use the DbSet<T> as a binding source.
            custViewSource.Source = context.Customers.Local;
        }
    ```

8. **F5**キーを押します。 CollectionViewSource に最初に取得された顧客の詳細と、データグリッド内の注文が表示されます。 書式設定はそれほど優れていないので、修正しましょう。 とは、他のレコードを表示し、基本的な CRUD 操作を実行する方法を備えています。

## <a name="adjust-the-page-design-and-add-grids-for-new-customers-and-orders"></a>新しい顧客と注文のページデザインを調整し、グリッドを追加する
 Visual Studio によって生成される既定の配置は、アプリケーションには適していないため、XAML でいくつかの変更を手動で行います。 また、ユーザーが新しい顧客または新しい注文を追加できるようにするために、"フォーム" (実際にはグリッド) も必要になります。    新しい顧客と注文を追加できるようにするには、にデータバインドされていない別のテキストボックスセットが必要です `CollectionViewSource` 。 ここでは、ハンドラーメソッドで Visible プロパティを設定することによって、任意の時点でユーザーに表示されるグリッドを制御します。

 最後に、[Orders] グリッドの各行に [Delete] ボタンを追加して、ユーザーが個々の注文を削除できるようにします。

 まず、これらのスタイルを Windows に追加します。

```xaml
<Style x:Key="Label" TargetType="{x:Type Label}" BasedOn="{x:Null}">
    <Setter Property="HorizontalAlignment" Value="Left"/>
    <Setter Property="VerticalAlignment" Value="Center"/>
    <Setter Property="Margin" Value="3"/>
    <Setter Property="Height" Value="23"/>
</Style>
<Style x:Key="CustTextBox" TargetType="{x:Type TextBox}" BasedOn="{x:Null}">
    <Setter Property="HorizontalAlignment" Value="Right"/>
    <Setter Property="VerticalAlignment" Value="Center"/>
    <Setter Property="Margin" Value="3"/>
    <Setter Property="Height" Value="26"/>
    <Setter Property="Width" Value="120"/>
</Style>
```

 次に、外側のグリッド全体をこのマークアップに置き換えます。

```xaml
<Grid >
     <Grid.RowDefinitions>
         <RowDefinition Height="auto"/>
         <RowDefinition Height="auto"/>
         <RowDefinition Height="*"/>
     </Grid.RowDefinitions>
     <StackPanel  Orientation="Horizontal" Margin="2,2,2,0" Height="36" VerticalAlignment="Top" Background="Gainsboro" DataContext="{StaticResource customerViewSource}" d:LayoutOverrides="LeftMargin, RightMargin, TopMargin, BottomMargin">
         <Button Name="btnFirst" Content="|◄" Command="{StaticResource FirstCommand}" Style="{StaticResource NavButton}"  />
         <Button Name="btnPrev"  Content="◄" Command="{StaticResource PreviousCommand}" Style="{StaticResource NavButton}"/>
         <Button Name="btnNext"  Content="►" Command="{StaticResource NextCommand}"     Style="{StaticResource NavButton}"/>
         <Button Name="btnLast"  Content="►|" Command="{StaticResource LastCommand}" Style="{StaticResource NavButton}"/>
         <Button Name="btnDelete" Content="Delete Customer" Command="{StaticResource DeleteCustomerCommand}" FontSize="11" Width="120" Style="{StaticResource NavButton}"/>
         <Button  Name="btnAdd"   Content="New Customer"  Command="{StaticResource AddCommand}" FontSize="11" Width="80" Style="{StaticResource NavButton}"/>
         <Button Content="New Order" Name="btnNewOrder" FontSize="11" Width="80" Style="{StaticResource NavButton}" Click="NewOrder_click"/>
         <Button Name="btnUpdate" Content="Commit" Command="{StaticResource UpdateCommand}" FontSize="11" Width="80" Style="{StaticResource NavButton}"/>
         <Button Content="Cancel" Name="btnCancel"  Command="{StaticResource CancelCommand}" FontSize="11" Width="80" Style="{StaticResource NavButton}"/>
     </StackPanel>
     <Grid x:Name="existingCustomerGrid" Grid.Row="1" HorizontalAlignment="Left" Margin="5" Visibility="Visible" VerticalAlignment="Top" Background="AntiqueWhite" DataContext="{StaticResource customerViewSource}">
         <Grid.ColumnDefinitions>
             <ColumnDefinition Width="Auto" MinWidth="233"/>
             <ColumnDefinition Width="Auto" MinWidth="397"/>
         </Grid.ColumnDefinitions>
         <Grid.RowDefinitions>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
         </Grid.RowDefinitions>
         <Label Content="Customer ID:" Grid.Row="0" Style="{StaticResource Label}"/>
         <TextBox x:Name="customerIDTextBox"  Grid.Row="0" Style="{StaticResource CustTextBox}"
                  Text="{Binding CustomerID, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Company Name:"  Grid.Row="1" Style="{StaticResource Label}"/>
         <TextBox x:Name="companyNameTextBox"  Grid.Row="1" Style="{StaticResource CustTextBox}"
                  Text="{Binding CompanyName, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Contact Name:"  Grid.Row="2" Style="{StaticResource Label}"/>
         <TextBox x:Name="contactNameTextBox" Grid.Row="2" Style="{StaticResource CustTextBox}"
                  Text="{Binding ContactName, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Contact Title:"  Grid.Row="3" Style="{StaticResource Label}"/>
         <TextBox x:Name="contactTitleTextBox" Grid.Row="3" Style="{StaticResource CustTextBox}"
                  Text="{Binding ContactTitle, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Address:" Grid.Row="4" Style="{StaticResource Label}"/>
         <TextBox x:Name="addressTextBox" Grid.Row="4" Style="{StaticResource CustTextBox}"
                  Text="{Binding Address, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="City:" Grid.Column="1" Grid.Row="0"  Style="{StaticResource Label}"/>
         <TextBox x:Name="cityTextBox" Grid.Column="1" Grid.Row="0" Style="{StaticResource CustTextBox}"
                  Text="{Binding City, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Country:" Grid.Column="1" Grid.Row="1" Style="{StaticResource Label}"/>
         <TextBox x:Name="countryTextBox" Grid.Column="1" Grid.Row="1" Style="{StaticResource CustTextBox}"
                  Text="{Binding Country, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Fax:" Grid.Column="1" Grid.Row="2" Style="{StaticResource Label}"/>
         <TextBox x:Name="faxTextBox" Grid.Column="1" Grid.Row="2" Style="{StaticResource CustTextBox}"
                  Text="{Binding Fax, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Phone:" Grid.Column="1" Grid.Row="3" Style="{StaticResource Label}"/>
         <TextBox x:Name="phoneTextBox" Grid.Column="1" Grid.Row="3" Style="{StaticResource CustTextBox}"
                  Text="{Binding Phone, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Postal Code:" Grid.Column="1" Grid.Row="4" VerticalAlignment="Center" Style="{StaticResource Label}"/>
         <TextBox x:Name="postalCodeTextBox" Grid.Column="1" Grid.Row="4" Style="{StaticResource CustTextBox}"
                  Text="{Binding PostalCode, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Region:" Grid.Column="1" Grid.Row="5" Style="{StaticResource Label}"/>
         <TextBox x:Name="regionTextBox" Grid.Column="1" Grid.Row="5" Style="{StaticResource CustTextBox}"
                  Text="{Binding Region, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
     </Grid>
     <Grid x:Name="newCustomerGrid" Grid.Row="1" HorizontalAlignment="Left" VerticalAlignment="Top" Margin="5" DataContext="{Binding RelativeSource={RelativeSource FindAncestor, AncestorType={x:Type Window}}, Path=newCustomer, UpdateSourceTrigger=Explicit}" Visibility="Collapsed" Background="CornflowerBlue">
         <Grid.ColumnDefinitions>
             <ColumnDefinition Width="Auto" MinWidth="233"/>
             <ColumnDefinition Width="Auto" MinWidth="397"/>
         </Grid.ColumnDefinitions>
         <Grid.RowDefinitions>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
         </Grid.RowDefinitions>
         <Label Content="Customer ID:" Grid.Row="0" Style="{StaticResource Label}"/>
         <TextBox x:Name="add_customerIDTextBox"  Grid.Row="0"  Style="{StaticResource CustTextBox}"
                  Text="{Binding CustomerID, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Company Name:"  Grid.Row="1" Style="{StaticResource Label}"/>
         <TextBox x:Name="add_companyNameTextBox"  Grid.Row="1" Style="{StaticResource CustTextBox}"
                  Text="{Binding CompanyName, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true }"/>
         <Label Content="Contact Name:"  Grid.Row="2" Style="{StaticResource Label}"/>
         <TextBox x:Name="add_contactNameTextBox" Grid.Row="2" Style="{StaticResource CustTextBox}"
                  Text="{Binding ContactName, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Contact Title:"  Grid.Row="3" Style="{StaticResource Label}"/>
         <TextBox x:Name="add_contactTitleTextBox" Grid.Row="3" Style="{StaticResource CustTextBox}"
                  Text="{Binding ContactTitle, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Address:" Grid.Row="4" Style="{StaticResource Label}"/>
         <TextBox x:Name="add_addressTextBox" Grid.Row="4" Style="{StaticResource CustTextBox}"
                  Text="{Binding Address, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="City:" Grid.Column="1" Grid.Row="0"  Style="{StaticResource Label}"/>
         <TextBox x:Name="add_cityTextBox" Grid.Column="1" Grid.Row="0" Style="{StaticResource CustTextBox}"
                  Text="{Binding City, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Country:" Grid.Column="1" Grid.Row="1" Style="{StaticResource Label}"/>
         <TextBox x:Name="add_countryTextBox" Grid.Column="1" Grid.Row="1" Style="{StaticResource CustTextBox}"
                  Text="{Binding Country, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Fax:" Grid.Column="1" Grid.Row="2" Style="{StaticResource Label}"/>
         <TextBox x:Name="add_faxTextBox" Grid.Column="1" Grid.Row="2" Style="{StaticResource CustTextBox}"
                  Text="{Binding Fax, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Phone:" Grid.Column="1" Grid.Row="3" Style="{StaticResource Label}"/>
         <TextBox x:Name="add_phoneTextBox" Grid.Column="1" Grid.Row="3" Style="{StaticResource CustTextBox}"
                  Text="{Binding Phone, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Postal Code:" Grid.Column="1" Grid.Row="4" VerticalAlignment="Center" Style="{StaticResource Label}"/>
         <TextBox x:Name="add_postalCodeTextBox" Grid.Column="1" Grid.Row="4" Style="{StaticResource CustTextBox}"
                  Text="{Binding PostalCode, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Region:" Grid.Column="1" Grid.Row="5" Style="{StaticResource Label}"/>
         <TextBox x:Name="add_regionTextBox" Grid.Column="1" Grid.Row="5" Style="{StaticResource CustTextBox}"
                  Text="{Binding Region, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
     </Grid>
     <Grid x:Name="newOrderGrid" Grid.Row="1" HorizontalAlignment="Left" VerticalAlignment="Top" Margin="5" DataContext="{Binding Path=newOrder, Mode=TwoWay}" Visibility="Collapsed" Background="LightGreen">
         <Grid.ColumnDefinitions>
             <ColumnDefinition Width="Auto" MinWidth="233"/>
             <ColumnDefinition Width="Auto" MinWidth="397"/>
         </Grid.ColumnDefinitions>
         <Grid.RowDefinitions>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
         </Grid.RowDefinitions>
         <Label Content="New Order Form" FontWeight="Bold"/>
         <Label Content="Employee ID:"  Grid.Row="1" Style="{StaticResource Label}"/>
         <TextBox x:Name="add_employeeIDTextBox" Grid.Row="1" Style="{StaticResource CustTextBox}"
                  Text="{Binding EmployeeID, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Order Date:"  Grid.Row="2" Style="{StaticResource Label}"/>
         <DatePicker x:Name="add_orderDatePicker" Grid.Row="2"  HorizontalAlignment="Right" Width="120"
                 SelectedDate="{Binding OrderDate, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true, UpdateSourceTrigger=PropertyChanged}"/>
         <Label Content="Required Date:" Grid.Row="3" Style="{StaticResource Label}"/>
         <DatePicker x:Name="add_requiredDatePicker" Grid.Row="3" HorizontalAlignment="Right" Width="120"
                  SelectedDate="{Binding RequiredDate, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true, UpdateSourceTrigger=PropertyChanged}"/>
         <Label Content="Shipped Date:"  Grid.Row="4"  Style="{StaticResource Label}"/>
         <DatePicker x:Name="add_shippedDatePicker"  Grid.Row="4"  HorizontalAlignment="Right" Width="120"
                 SelectedDate="{Binding ShippedDate, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true, UpdateSourceTrigger=PropertyChanged}"/>
         <Label Content="Ship Via:"  Grid.Row="5" Style="{StaticResource Label}"/>
         <TextBox x:Name="add_ShipViaTextBox"  Grid.Row="5" Style="{StaticResource CustTextBox}"
                  Text="{Binding ShipVia, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Freight"  Grid.Row="6" Style="{StaticResource Label}"/>
         <TextBox x:Name="add_freightTextBox" Grid.Row="6" Style="{StaticResource CustTextBox}"
                  Text="{Binding Freight, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
     </Grid>
     <DataGrid x:Name="ordersDataGrid" SelectionUnit="Cell" SelectionMode="Single" AutoGenerateColumns="False" CanUserAddRows="false" IsEnabled="True" EnableRowVirtualization="True" Width="auto" ItemsSource="{Binding Source={StaticResource customerOrdersViewSource}}" Margin="10,10,10,10" Grid.Row="2" RowDetailsVisibilityMode="VisibleWhenSelected">
         <DataGrid.Columns>
             <DataGridTemplateColumn>
                 <DataGridTemplateColumn.CellTemplate>
                     <DataTemplate>
                         <Button Content="Delete"  Command="{StaticResource DeleteOrderCommand}" CommandParameter="{Binding}"/>
                     </DataTemplate>
                 </DataGridTemplateColumn.CellTemplate>
             </DataGridTemplateColumn>
             <DataGridTextColumn x:Name="customerIDColumn" Binding="{Binding CustomerID}" Header="Customer ID" Width="SizeToHeader"/>
             <DataGridTextColumn x:Name="employeeIDColumn" Binding="{Binding EmployeeID}" Header="Employee ID" Width="SizeToHeader"/>
             <DataGridTextColumn x:Name="freightColumn" Binding="{Binding Freight}" Header="Freight" Width="SizeToHeader"/>
             <DataGridTemplateColumn x:Name="orderDateColumn" Header="Order Date" Width="SizeToHeader">
                 <DataGridTemplateColumn.CellTemplate>
                     <DataTemplate>
                         <DatePicker SelectedDate="{Binding OrderDate, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true, UpdateSourceTrigger=PropertyChanged}"/>
                     </DataTemplate>
                 </DataGridTemplateColumn.CellTemplate>
             </DataGridTemplateColumn>
             <DataGridTextColumn x:Name="orderIDColumn" Binding="{Binding OrderID}" Header="Order ID" Width="SizeToHeader"/>
             <DataGridTemplateColumn x:Name="requiredDateColumn" Header="Required Date" Width="SizeToHeader">
                 <DataGridTemplateColumn.CellTemplate>
                     <DataTemplate>
                         <DatePicker SelectedDate="{Binding RequiredDate, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true, UpdateSourceTrigger=PropertyChanged}"/>
                     </DataTemplate>
                 </DataGridTemplateColumn.CellTemplate>
             </DataGridTemplateColumn>
             <DataGridTextColumn x:Name="shipAddressColumn" Binding="{Binding ShipAddress}" Header="Ship Address" Width="SizeToHeader"/>
             <DataGridTextColumn x:Name="shipCityColumn" Binding="{Binding ShipCity}" Header="Ship City" Width="SizeToHeader"/>
             <DataGridTextColumn x:Name="shipCountryColumn" Binding="{Binding ShipCountry}" Header="Ship Country" Width="SizeToHeader"/>
             <DataGridTextColumn x:Name="shipNameColumn" Binding="{Binding ShipName}" Header="Ship Name" Width="SizeToHeader"/>
             <DataGridTemplateColumn x:Name="shippedDateColumn" Header="Shipped Date" Width="SizeToHeader">
                 <DataGridTemplateColumn.CellTemplate>
                     <DataTemplate>
                         <DatePicker SelectedDate="{Binding ShippedDate, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true, UpdateSourceTrigger=PropertyChanged}"/>
                     </DataTemplate>
                 </DataGridTemplateColumn.CellTemplate>
             </DataGridTemplateColumn>
             <DataGridTextColumn x:Name="shipPostalCodeColumn" Binding="{Binding ShipPostalCode}" Header="Ship Postal Code" Width="SizeToHeader"/>
             <DataGridTextColumn x:Name="shipRegionColumn" Binding="{Binding ShipRegion}" Header="Ship Region" Width="SizeToHeader"/>
             <DataGridTextColumn x:Name="shipViaColumn" Binding="{Binding ShipVia}" Header="Ship Via" Width="SizeToHeader"/>
         </DataGrid.Columns>
     </DataGrid>
 </Grid>
```

## <a name="add-buttons-to-navigate-add-update-and-delete"></a>移動、追加、更新、削除するためのボタンを追加する
 Windows フォームアプリケーションでは、データベース内の行を移動して基本的な CRUD 操作を実行するためのボタンを持つ BindingNavigator オブジェクトを取得します。 WPF には BindingNavigator が用意されていませんが、簡単に作成できます。 この操作は、ページグリッドの一番下の行にある水平方向の StackPanel 内のボタンを使用して行います。また、コードビハインドのメソッドにバインドされているコマンドにボタンを関連付けます。

 コマンドロジックには4つの部分があります。 (1) コマンド、(2) バインド、(3) ボタン、(4) 分離コード内のコマンドハンドラー。

#### <a name="add-commands-bindings-and-buttons-in-xaml"></a>XAML にコマンド、バインド、およびボタンを追加する

1. まず、Mainwindow.xaml ファイルのコマンドを、次のように追加します。

    ```xaml

     <RoutedUICommand x:Key="FirstCommand" Text="First"/>
    <RoutedUICommand x:Key="LastCommand" Text="Last"/>
    <RoutedUICommand x:Key="NextCommand" Text="Next"/>
    <RoutedUICommand x:Key="PreviousCommand" Text="Previous"/>
    <RoutedUICommand x:Key="DeleteCustomerCommand" Text="Delete Customer"/>
    <RoutedUICommand x:Key="DeleteOrderCommand" Text="Delete Order"/>
    <RoutedUICommand x:Key="UpdateCommand" Text="Update"/>
    <RoutedUICommand x:Key="AddCommand" Text="Add"/>
    <RoutedUICommand x:Key="CancelCommand" Text="Cancel"/>
    ```

2. CommandBinding は、コードビハインド内のメソッドに RoutedUICommand イベントをマップします。 次の CommandBindings 要素を、Windows .Resources の終了タグの後に追加します。

    ```xaml

        <Window.CommandBindings>
        <CommandBinding Command="{StaticResource FirstCommand}" Executed="FirstCommandHandler"/>
        <CommandBinding Command="{StaticResource LastCommand}" Executed="LastCommandHandler"/>
        <CommandBinding Command="{StaticResource NextCommand}" Executed="NextCommandHandler"/>
        <CommandBinding Command="{StaticResource PreviousCommand}" Executed="PreviousCommandHandler"/>
        <CommandBinding Command="{StaticResource DeleteCustomerCommand}" Executed="DeleteCustomerCommandHandler"/>
        <CommandBinding Command="{StaticResource DeleteOrderCommand}" Executed="DeleteOrderCommandHandler"/>
        <CommandBinding Command="{StaticResource UpdateCommand}" Executed="UpdateCommandHandler"/>
        <CommandBinding Command="{StaticResource AddCommand}" Executed="AddCommandHandler"/>
        <CommandBinding Command="{StaticResource CancelCommand}" Executed="CancelCommandHandler"/>
    </Window.CommandBindings>
    ```

3. 次に、[ナビゲーション]、[追加]、[削除]、[更新] の各ボタンを使用して StackPanel を追加します。 まず、次のスタイルを Windows .Resources に追加します。

    ```xaml
    <Style x:Key="NavButton" TargetType="{x:Type Button}" BasedOn="{x:Null}">
        <Setter Property="FontSize" Value="24"/>
        <Setter Property="FontFamily" Value="Segoe UI Symbol"/>
        <Setter Property="Margin" Value="2,2,2,0"/>
        <Setter Property="Width" Value="40"/>
        <Setter Property="Height" Value="auto"/>
    </Style>
    ```

     ここで、外側の Grid 要素の RowDefinitions の直後に、XAML ページの上部にこのコードを貼り付けます。

    ```xaml
    <StackPanel  Orientation="Horizontal" Margin="2,2,2,0" Height="36" VerticalAlignment="Top" Background="Gainsboro" DataContext="{StaticResource customerViewSource}" d:LayoutOverrides="LeftMargin, RightMargin, TopMargin, BottomMargin">
        <Button Name="btnFirst" Content="|◄" Command="{StaticResource FirstCommand}" Style="{StaticResource NavButton}"  />
        <Button Name="btnPrev"  Content="◄" Command="{StaticResource PreviousCommand}" Style="{StaticResource NavButton}"/>
        <Button Name="btnNext"  Content="►" Command="{StaticResource NextCommand}"     Style="{StaticResource NavButton}"/>
        <Button Name="btnLast"  Content="►|" Command="{StaticResource LastCommand}" Style="{StaticResource NavButton}"/>
        <Button Name="btnDelete" Content="Delete Customer" Command="{StaticResource DeleteCustomerCommand}" FontSize="11" Width="120" Style="{StaticResource NavButton}"/>
        <Button  Name="btnAdd"   Content="New Customer"  Command="{StaticResource AddCommand}" FontSize="11" Width="80" Style="{StaticResource NavButton}"/>
        <Button Content="New Order" Name="btnNewOrder" FontSize="11" Width="80" Style="{StaticResource NavButton}" Click="NewOrder_click"/>
        <Button Name="btnUpdate" Content="Commit" Command="{StaticResource UpdateCommand}" FontSize="11" Width="80" Style="{StaticResource NavButton}"/>
        <Button Content="Cancel" Name="btnCancel"  Command="{StaticResource CancelCommand}" FontSize="11" Width="80" Style="{StaticResource NavButton}"/>
    </StackPanel>
    ```

#### <a name="add-command-handlers-to-the-mainwindow-class"></a>Mainwindow.xaml クラスにコマンドハンドラーを追加する

1. コードビハインドは、add メソッドと delete メソッドを除き、最小限ではありません。 ナビゲーションは、CollectionViewSource の View プロパティでメソッドを呼び出すことによって実行されることに注意してください。 DeleteOrderCommandHandler は、注文に対して連鎖削除を実行する方法を示しています。 最初に、関連付けられている Order_Details を削除する必要があります。 UpdateCommandHandler は新しい顧客をコレクションに追加します。それ以外の場合は、テキストボックスでユーザーが行った変更をすべて使用して、既存のオブジェクトを更新します。

2. これらのハンドラーメソッドを MainWindow.xaml.cs の Mainwindow.xaml クラスに追加します。この場合、Customers テーブルの CollectionViewSource に別の名前がある場合は、次の各メソッドで名前を調整する必要があります。

    ```csharp
       private void LastCommandHandler(object sender, ExecutedRoutedEventArgs e)
    {
        custViewSource.View.MoveCurrentToLast();
    }

    private void PreviousCommandHandler(object sender, ExecutedRoutedEventArgs e)
    {
        custViewSource.View.MoveCurrentToPrevious();
    }

    private void NextCommandHandler(object sender, ExecutedRoutedEventArgs e)
    {
        custViewSource.View.MoveCurrentToNext();
    }

    private void FirstCommandHandler(object sender, ExecutedRoutedEventArgs e)
    {
        custViewSource.View.MoveCurrentToFirst();
    }

    private void DeleteCustomerCommandHandler(object sender, ExecutedRoutedEventArgs e)
    {
        // If existing window is visible, then delete the customer and all their orders.
        // In a real application, you should add warnings and allow a user to cancel the operation.
        var cur = custViewSource.View.CurrentItem as Customer;

        var cust = (from c in context.Customers
                    where c.CustomerID == cur.CustomerID
                    select c).FirstOrDefault();

        if (cust != null)
        {
            foreach (var ord in cust.Orders.ToList())
            {
                Delete_Order(ord);
            }
            context.Customers.Remove(cust);
        }
        context.SaveChanges();
        custViewSource.View.Refresh();
    }

    // Commit changes from the new customer form, the new order form,
    // or edits made to the existing customer form.
    private void UpdateCommandHandler(object sender, ExecutedRoutedEventArgs e)
    {
        if (newCustomerGrid.IsVisible)
        {
            // Create a new object because the old one
            // is being tracked by EF now.
            newCustomer = new Customer();
            newCustomer.Address = add_addressTextBox.Text;
            newCustomer.City = add_cityTextBox.Text;
            newCustomer.CompanyName = add_companyNameTextBox.Text;
            newCustomer.ContactName = add_contactNameTextBox.Text;
            newCustomer.ContactTitle = add_contactTitleTextBox.Text;
            newCustomer.Country = add_countryTextBox.Text;
            newCustomer.CustomerID = add_customerIDTextBox.Text;
            newCustomer.Fax = add_faxTextBox.Text;
            newCustomer.Phone = add_phoneTextBox.Text;
            newCustomer.PostalCode = add_postalCodeTextBox.Text;
            newCustomer.Region = add_regionTextBox.Text;

            // Perform very basic validation
            if (newCustomer.CustomerID.Length == 5)
            {
                // Insert the new customer at correct position:
                int len = context.Customers.Local.Count();
                int pos = len;
                for (int i = 0; i < len; ++i)
                {
                    if (String.CompareOrdinal(newCustomer.CustomerID, context.Customers.Local[i].CustomerID) < 0)
                    {
                        pos = i;
                        break;
                    }
                }
                context.Customers.Local.Insert(pos, newCustomer);
                custViewSource.View.Refresh();
                custViewSource.View.MoveCurrentTo(newCustomer);
            }
            else
            {
                MessageBox.Show("CustomerID must have 5 characters.");
            }

            newCustomerGrid.Visibility = Visibility.Collapsed;
            existingCustomerGrid.Visibility = Visibility.Visible;
        }
        else if (newOrderGrid.IsVisible)
        {
            // Order ID is auto-generated so we don't set it here.
            // For CustomerID, address, etc we use the values from current customer.
            // User can modify these in the datagrid after the order is entered.

            newOrder.OrderDate = add_orderDatePicker.SelectedDate;
            newOrder.RequiredDate = add_requiredDatePicker.SelectedDate;
            newOrder.ShippedDate = add_shippedDatePicker.SelectedDate;
            try
            {
                // Exercise for the reader if you are using Northwind:
                // Add the Northwind Shippers table to the model.
                // Acceptable ShipperID values are 1, 2, or 3.
                if (add_ShipViaTextBox.Text == "1" || add_ShipViaTextBox.Text == "2"
                    || add_ShipViaTextBox.Text == "3")
                {
                    newOrder.ShipVia = Convert.ToInt32(add_ShipViaTextBox.Text);
                }
                else
                {
                    MessageBox.Show("Shipper ID must be 1, 2, or 3 in Northwind.");
                    return;
                }
            }
            catch
            {
                MessageBox.Show("Ship Via must be convertible to int");
                return;
            }
            try
            {
                newOrder.Freight = Convert.ToDecimal(add_freightTextBox.Text);
            }
            catch
            {
                MessageBox.Show("Freight must be convertible to decimal.");
                return;
            }

            // Add the order into the EF model
            context.Orders.Add(newOrder);
            ordViewSource.View.Refresh();
        }

        // Save the changes, either for a new customer, a new order
        // or an edit in an existing customer or order
        context.SaveChanges();
    }

    // Sets up the form so that user can enter data. Data is later
    // saved when user clicks Commit.
    private void AddCommandHandler(object sender, ExecutedRoutedEventArgs e)
    {
        existingCustomerGrid.Visibility = Visibility.Collapsed;
        newOrderGrid.Visibility = Visibility.Collapsed;
        newCustomerGrid.Visibility = Visibility.Visible;

        // Clear all the text boxes before adding a new customer.
        foreach (var child in newCustomerGrid.Children)
        {
            var tb = child as TextBox;
            if (tb != null)
            {
                tb.Text = "";
            }
        }
    }

    private void NewOrder_click(object sender, RoutedEventArgs e)
    {
        var cust = custViewSource.View.CurrentItem as Customer;
        if (cust == null)
        {
            MessageBox.Show("No customer selected.");
            return;
        }

        newOrder.CustomerID = cust.CustomerID;

        // Get address and other mostly constant fields from
        // an existing order, if one exists
        var coll = custViewSource.Source as IEnumerable<Customer>;
        var lastOrder = (from c in coll
                         from ord in c.Orders
                         select ord).LastOrDefault();
        if (lastOrder != null)
        {
            newOrder.ShipAddress = lastOrder.ShipAddress;
            newOrder.ShipCity = lastOrder.ShipCity;
            newOrder.ShipCountry = lastOrder.ShipCountry;
            newOrder.ShipName = lastOrder.ShipName;
            newOrder.ShipPostalCode = lastOrder.ShipPostalCode;
            newOrder.ShipRegion = lastOrder.ShipRegion;
        }

        existingCustomerGrid.Visibility = Visibility.Collapsed;
        newCustomerGrid.Visibility = Visibility.Collapsed;
        newOrderGrid.UpdateLayout();
        newOrderGrid.Visibility = Visibility.Visible;
    }

    // Cancels any input into the new customer form
    private void CancelCommandHandler(object sender, ExecutedRoutedEventArgs e)
    {
        add_addressTextBox.Text = "";
        add_cityTextBox.Text = "";
        add_companyNameTextBox.Text = "";
        add_contactNameTextBox.Text = "";
        add_contactTitleTextBox.Text = "";
        add_countryTextBox.Text = "";
        add_customerIDTextBox.Text = "";
        add_faxTextBox.Text = "";
        add_phoneTextBox.Text = "";
        add_postalCodeTextBox.Text = "";
        add_regionTextBox.Text = "";

        existingCustomerGrid.Visibility = Visibility.Visible;
        newCustomerGrid.Visibility = Visibility.Collapsed;
        newOrderGrid.Visibility = Visibility.Collapsed;
    }

    private void Delete_Order(Order order)
    {
        // Find the order in the EF model.
        var ord = (from o in context.Orders.Local
                   where o.OrderID == order.OrderID
                   select o).FirstOrDefault();

        // Delete all the order_details that have
        // this Order as a foreign key
        foreach (var detail in ord.Order_Details.ToList())
        {
            context.Order_Details.Remove(detail);
        }

        // Now it's safe to delete the order.
        context.Orders.Remove(ord);
        context.SaveChanges();

        // Update the data grid.
        ordViewSource.View.Refresh();
    }

    private void DeleteOrderCommandHandler(object sender, ExecutedRoutedEventArgs e)
    {
        // Get the Order in the row in which the Delete button was clicked.
        Order obj = e.Parameter as Order;
        Delete_Order(obj);
    }
    ```

3. **F5**キーを押します。 データが表示され、ナビゲーションボタンが期待どおりに動作するはずです。 データの入力後に新しい顧客または注文をモデルに追加するには、[コミット] をクリックします。  [キャンセル] をクリックすると、新しい顧客または新しい注文フォームを保存せずに元に戻すことができます。 既存の顧客や注文をテキストボックスに直接編集することができ、それらの変更は自動的にモデルに書き込まれます。

## <a name="see-also"></a>参照
 [Visual Studio data tools for .net](../data-tools/visual-studio-data-tools-for-dotnet.md) [Entity Framework のドキュメント](https://msdn.microsoft.com/data/ee712907.aspx)
