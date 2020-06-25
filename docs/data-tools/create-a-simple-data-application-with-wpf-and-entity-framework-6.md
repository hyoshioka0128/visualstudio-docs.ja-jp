---
title: WPF と Entity Framework 6 を使用した単純なデータアプリケーション
ms.date: 08/22/2017
ms.topic: conceptual
dev_langs:
- CSharp
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 4aa978098c459d9e55ef0dc1423080357e067a5b
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85282762"
---
# <a name="create-a-simple-data-application-with-wpf-and-entity-framework-6"></a>WPF と Entity Framework 6 を使用して単純なデータ アプリケーションを作成する

このチュートリアルでは、Visual Studio で基本的な "フォームオーバーデータ" アプリケーションを作成する方法について説明します。 アプリは SQL Server LocalDB、Northwind データベース、Entity Framework 6 (Entity Framework Core ではありません)、Windows Presentation Foundation および (.NET Core ではなく) .NET Framework を使用します。 ここでは、マスター/詳細ビューで基本的なデータバインドを実行する方法について説明します。また、 **[次**に移動]、[**前**に移動]、[**先頭に**移動]、[**最後に移動**]、[**更新**]、および [**削除**] のボタンがあるカスタムバインドナビゲーターもあります。

この記事では、Visual Studio でのデータツールの使用に焦点を当てていますが、基になるテクノロジの詳細については説明しません。 XAML、Entity Framework、および SQL に関する基本的な知識があることを前提としています。 また、この例では、WPF アプリケーションの標準であるモデルビュービューモデル (MVVM) アーキテクチャについても説明しません。 ただし、いくつかの変更を加えて、このコードを独自の MVVM アプリケーションにコピーできます。

## <a name="install-and-connect-to-northwind"></a>Northwind にインストールして接続する

この例では SQL Server Express LocalDB と Northwind サンプルデータベースを使用します。 その製品の ADO.NET data provider が Entity Framework をサポートしている場合は、他の SQL database 製品とも同様に機能します。

1. LocalDB SQL Server Express ない場合は、 [SQL Server Express ダウンロードページ](https://www.microsoft.com/sql-server/sql-server-editions-express)からインストールするか、 **Visual Studio インストーラー**を使用してインストールします。 **Visual Studio インストーラー**で、**.NET デスクトップ開発** ワークロードの一部として、または個別のコンポーネントとして、SQL Server Express LocalDB をインストールできます。

2. 次の手順に従って、Northwind サンプルデータベースをインストールします。

    1. Visual Studio で、[ **SQL Server オブジェクトエクスプローラー** ] ウィンドウを開きます。 (**SQL Server オブジェクトエクスプローラー**は、 **Visual Studio インストーラー**の**データストレージと処理**ワークロードの一部としてインストールされます)。[ **SQL Server** ] ノードを展開します。 LocalDB インスタンスを右クリックし、[**新しいクエリ**] をクリックします。

       クエリエディターウィンドウが開きます。

    2. [Northwind transact-sql スクリプト](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true)をクリップボードにコピーします。 この T-sql スクリプトでは、Northwind データベースを最初から作成し、データを設定します。

    3. T-sql スクリプトをクエリエディターに貼り付け、[**実行**] ボタンをクリックします。

       しばらくすると、クエリの実行が完了し、Northwind データベースが作成されます。

3. Northwind の[新しい接続を追加](../data-tools/add-new-connections.md)します。

## <a name="configure-the-project"></a>プロジェクトを構成する

1. Visual Studio で、新しい C# **WPF アプリ**プロジェクトを作成します。

2. Entity Framework 6 の NuGet パッケージを追加します。 **ソリューションエクスプローラー**で、プロジェクトノードを選択します。 メインメニューで、[**プロジェクト**] [  >  **NuGet パッケージの管理**] の順に選択します。

     ![[NuGet パッケージの管理] メニュー項目](../data-tools/media/raddata_vs2015_manage_nuget_packages.png)

3. **NuGet パッケージマネージャー**で、[**参照**] リンクをクリックします。 Entity Framework は、一覧の最上位のパッケージであると思います。 右側のウィンドウで [**インストール**] をクリックし、画面の指示に従います。 インストールが完了すると、[出力] ウィンドウに通知されます。

     ![NuGet パッケージの Entity Framework](../data-tools/media/raddata_vs2015_nuget_ef.png)

4. これで、Visual Studio を使用して、Northwind データベースに基づくモデルを作成できるようになりました。

## <a name="create-the-model"></a>モデルを作成する

1. **ソリューションエクスプローラー**のプロジェクトノードを右クリックし、[新しい項目の**追加**] を選択し  >  **New Item**ます。 左側のウィンドウの [C#] ノードで、[**データ**] を選択し、中央のペインで [ **ADO.NET Entity Data Model**] を選択します。

   ![Entity Framework モデルの新しい項目](../data-tools/media/raddata-ef-new-project-item.png)

2. モデルを呼び出し `Northwind_model` 、 **[OK]** を選択します。 **Entity Data Model ウィザード**が開きます。 [**データベースから EF Designer** ] を選択し、[**次へ**] をクリックします。

   ![データベースからの EF モデル](../data-tools/media/raddata-ef-model-from-database.png)

3. 次の画面で、LocalDB Northwind 接続 (たとえば、(localdb) \MSSQLLocalDB) を入力または選択し、Northwind データベースを指定して、[**次へ**] をクリックします。

4. ウィザードの次のページで、Entity Framework モデルに含めるテーブル、ストアドプロシージャ、およびその他のデータベースオブジェクトを選択します。 ツリービューで [dbo] ノードを展開し、[ **Customers**]、[ **Orders**]、[ **Order Details**] を選択します。 既定値をオンのままにして、[**完了**] をクリックします。

    ![モデルのデータベースオブジェクトを選択する](../data-tools/media/raddata-choose-ef-objects.png)

5. このウィザードでは、Entity Framework モデルを表す C# クラスが生成されます。 クラスは、単純な旧 C# クラスであり、WPF ユーザーインターフェイスにデータをバインドします。 .Edmx ファイルには、クラスをデータベース内のオブジェクトに関連付けるリレーションシップとその他のメタデータが記述されて*い*ます。 *.Tt*ファイルは、モデルで動作するコードを生成し、変更をデータベースに保存する T4 テンプレートです。 これらのファイルはすべて、[Northwind_model] ノードの下の**ソリューションエクスプローラー**に表示されます。

      ![EF モデルファイルのソリューションエクスプローラー](../data-tools/media/raddata-solution-explorer-ef-model-files.png)

    *.Edmx*ファイルのデザイナー画面を使用すると、モデル内のいくつかのプロパティとリレーションシップを変更できます。 このチュートリアルでは、デザイナーを使用しません。

6. この *.tt*ファイルは汎用的なものであるため、ObservableCollections を必要とする WPF データバインドを使用するには、そのうちの1つを調整する必要があります。 **ソリューションエクスプローラー**で、Northwind_model が見つかるまで [Northwind_model] ノードを展開し*ます。* (に含まれていないことを確認してください *。Context.tt*ファイル。 *.edmx*ファイルの直下にあります)。

   - の2つのオカレンスを <xref:System.Collections.ICollection> に置き換え <xref:System.Collections.ObjectModel.ObservableCollection%601> ます。

   - の最初の出現箇所を、 <xref:System.Collections.Generic.HashSet%601> 51 行目で置き換え <xref:System.Collections.ObjectModel.ObservableCollection%601> ます。 HashSet の2回目の出現を置き換えないでください。

   - の出現箇所 <xref:System.Collections.Generic> (431 行目を囲む) のみをに置き換え <xref:System.Collections.ObjectModel> ます。

7. **Ctrl** + **Shift** + **B**キーを押して、プロジェクトをビルドします。 ビルドが完了すると、モデルクラスがデータソースウィザードに表示されます。

これで、データを表示、移動、および変更できるように、このモデルを XAML ページにフックする準備ができました。

## <a name="databind-the-model-to-the-xaml-page"></a>モデルを XAML ページにバインドする

独自のデータバインドコードを記述することもできますが、Visual Studio により簡単に実行できます。

1. メインメニューから、[**プロジェクト**] [新しいデータソースの追加] の順に選択し、  >  **Add new data source** **データソース構成ウィザード**を起動します。 データベースではなくモデルクラスにバインドするので、[**オブジェクト**] を選択します。

     ![オブジェクトソースを含むデータソース構成ウィザード](../data-tools/media/raddata-data-source-configuration-wizard-with-object-source.png)

2. プロジェクトのノードを展開し、[ **Customer**] を選択します。 (注文のソースは、Customer の Orders ナビゲーションプロパティから自動的に生成されます)。

     ![エンティティクラスをデータソースとして追加する](../data-tools/media/raddata-add-entity-classes-as-data-sources.png)

3. **[完了]** をクリックします。

4. コードビューで*mainwindow.xaml*に移動します。 この例では、XAML を単純なものにしています。 Mainwindow.xaml のタイトルをわかりやすいものに変更し、高さと幅を 600 x 800 に増やします。 後でいつでも変更できます。 ここで、次の3つの行定義をメイングリッドに追加します。1行はナビゲーションボタン用、もう1つは顧客の詳細用、もう1つは注文を表示するグリッド用です。

    ```xaml
        <Grid.RowDefinitions>
            <RowDefinition Height="auto"/>
            <RowDefinition Height="auto"/>
            <RowDefinition Height="*"/>
        </Grid.RowDefinitions>
    ```

5. ここで、デザイナーで表示するように*mainwindow.xaml*を開きます。 これにより、[**データソース**] ウィンドウが、**ツールボックス**の横にある Visual Studio ウィンドウの余白にオプションとして表示されます。 タブをクリックしてウィンドウを開くか、 **Shift** + **Alt** + **D**キーを押すか**View**、[  >  **他の Windows**  >  **データソース**を表示] を選択します。 個々のテキストボックスに Customers クラスの各プロパティを表示します。 まず、[ **Customers** ] コンボボックスの矢印をクリックし、[**詳細**] を選択します。 次に、デザインサーフェイスの中央部分にノードをドラッグして、デザイナーが中央の行に移動することを認識できるようにします。 置き忘れしている場合は、後で XAML で行を手動で指定できます。 既定では、コントロールはグリッド要素に垂直方向に配置されますが、この時点では、フォーム上に配置することができます。 たとえば、アドレスの上に [**名前**] テキストボックスを配置した方がよい場合があります。 この記事のサンプルアプリケーションでは、フィールドを並べ替え、2つの列に並べ替えます。

     ![個々のコントロールに対するデータソースのバインド](../data-tools/media/raddata-customers-data-source-binding-to-individual-controls.png)

     コードビューで、 `Grid` 親グリッドの行 1 (中央の行) に新しい要素が表示されるようになりました。 親グリッドには、 `DataContext` 要素に追加された CollectionViewSource を参照する属性があり `Windows.Resources` ます。 そのデータコンテキストでは、最初のテキストボックスが**アドレス**にバインドされると、その名前は `Address` collectionviewsource 内の現在のオブジェクトのプロパティにマップされ `Customer` ます。

    ```xaml
    <Grid DataContext="{StaticResource customerViewSource}">
    ```

6. ウィンドウの上半分に顧客が表示されている場合は、下半分に注文を表示します。 1つのグリッドビューコントロールに注文を表示します。 マスター/詳細データバインドが想定どおりに動作するには、[個別の注文] ノードではなく、Customers クラスの Orders プロパティにバインドすることが重要です。 Customers クラスの Orders プロパティをフォームの下半分にドラッグして、デザイナーによって行2に配置されるようにします。

     ![Orders クラスをグリッドとしてドラッグ](../data-tools/media/raddata-drag-orders-classes-as-grid.png)

7. Visual Studio は、UI コントロールをモデル内のイベントに接続するすべてのバインドコードを生成しました。 いくつかのデータを表示するために必要なのは、モデルを作成するためのコードを記述することだけです。 まず、 *MainWindow.xaml.cs*に移動し、データコンテキストの mainwindow.xaml クラスにデータメンバーを追加します。 生成されたこのオブジェクトは、モデル内の変更とイベントを追跡するコントロールのように機能します。 また、顧客と注文の CollectionViewSource データメンバーと、関連するコンストラクター初期化ロジックも追加します。 クラスの先頭は次のようになります。

     [!code-csharp[MainWindow#1](../data-tools/codesnippet/CSharp/CreateWPFDataApp/MainWindow.xaml.cs#1)]

     Add `using` 拡張メソッドをスコープに取り込むために、system.string のディレクティブを追加します。

     ```csharp
     using System.Data.Entity;
     ```

     次に、下にスクロールして、 `Window_Loaded` イベントハンドラーを見つけます。 Visual Studio によって CollectionViewSource オブジェクトが追加されていることに注意してください。 これは、モデルの作成時に選択した NorthwindEntities オブジェクトを表します。 これは既に追加されているので、ここでは必要ありません。 ここでは、メソッドが次のようになるように、のコードを置き換え `Window_Loaded` ます。

     [!code-csharp[Window_Loaded#2](../data-tools/codesnippet/CSharp/CreateWPFDataApp/MainWindow.xaml.cs#2)]

8. **F5**キーを押します。 CollectionViewSource に最初に取得された顧客の詳細が表示されます。 また、データグリッドにも注文が表示されます。 書式設定はそれほど優れていないので、修正しましょう。 また、他のレコードを表示し、基本的な CRUD 操作を実行する方法を作成することもできます。

## <a name="adjust-the-page-design-and-add-grids-for-new-customers-and-orders"></a>新しい顧客と注文のページデザインを調整し、グリッドを追加する

Visual Studio によって生成される既定の配置は、アプリケーションには適していないため、ここではコードにコピーするための最後の XAML を提供します。 また、ユーザーが新しい顧客または注文を追加できるようにするために、"フォーム" (実際にはグリッド) が必要です。 新しい顧客と注文を追加できるようにするには、にデータバインドされていない別のテキストボックスセットが必要です `CollectionViewSource` 。 任意の時点でユーザーに表示されるグリッドを制御するには、ハンドラーメソッドで Visible プロパティを設定します。 最後に、[Orders] グリッドの各行に [Delete] ボタンを追加して、ユーザーが個々の注文を削除できるようにします。

まず、次のスタイルを `Windows.Resources` *mainwindow.xaml*の要素に追加します。

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
<Grid>
     <Grid.RowDefinitions>
         <RowDefinition Height="auto"/>
         <RowDefinition Height="auto"/>
         <RowDefinition Height="*"/>
     </Grid.RowDefinitions>
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
         <TextBox x:Name="customerIDTextBox" Grid.Row="0" Style="{StaticResource CustTextBox}"
                  Text="{Binding CustomerID, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Company Name:" Grid.Row="1" Style="{StaticResource Label}"/>
         <TextBox x:Name="companyNameTextBox" Grid.Row="1" Style="{StaticResource CustTextBox}"
                  Text="{Binding CompanyName, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Contact Name:" Grid.Row="2" Style="{StaticResource Label}"/>
         <TextBox x:Name="contactNameTextBox" Grid.Row="2" Style="{StaticResource CustTextBox}"
                  Text="{Binding ContactName, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Contact title:" Grid.Row="3" Style="{StaticResource Label}"/>
         <TextBox x:Name="contactTitleTextBox" Grid.Row="3" Style="{StaticResource CustTextBox}"
                  Text="{Binding ContactTitle, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Address:" Grid.Row="4" Style="{StaticResource Label}"/>
         <TextBox x:Name="addressTextBox" Grid.Row="4" Style="{StaticResource CustTextBox}"
                  Text="{Binding Address, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="City:" Grid.Column="1" Grid.Row="0" Style="{StaticResource Label}"/>
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
         <TextBox x:Name="add_customerIDTextBox" Grid.Row="0" Style="{StaticResource CustTextBox}"
                  Text="{Binding CustomerID, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Company Name:" Grid.Row="1" Style="{StaticResource Label}"/>
         <TextBox x:Name="add_companyNameTextBox" Grid.Row="1" Style="{StaticResource CustTextBox}"
                  Text="{Binding CompanyName, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true }"/>
         <Label Content="Contact Name:" Grid.Row="2" Style="{StaticResource Label}"/>
         <TextBox x:Name="add_contactNameTextBox" Grid.Row="2" Style="{StaticResource CustTextBox}"
                  Text="{Binding ContactName, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Contact title:" Grid.Row="3" Style="{StaticResource Label}"/>
         <TextBox x:Name="add_contactTitleTextBox" Grid.Row="3" Style="{StaticResource CustTextBox}"
                  Text="{Binding ContactTitle, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Address:" Grid.Row="4" Style="{StaticResource Label}"/>
         <TextBox x:Name="add_addressTextBox" Grid.Row="4" Style="{StaticResource CustTextBox}"
                  Text="{Binding Address, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="City:" Grid.Column="1" Grid.Row="0" Style="{StaticResource Label}"/>
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
                         <Button Content="Delete" Command="{StaticResource DeleteOrderCommand}" CommandParameter="{Binding}"/>
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

Windows フォームアプリケーションでは、データベース内の行を移動して基本的な CRUD 操作を実行するためのボタンを持つ BindingNavigator オブジェクトを取得します。 WPF には BindingNavigator が用意されていませんが、簡単に作成できます。 この操作は、水平方向の StackPanel 内のボタンを使用して行い、分離コード内のメソッドにバインドされているコマンドにボタンを関連付けます。

コマンドロジックには、(1) コマンド、(2) バインド、(3) ボタン、および (4) 分離コード内のコマンドハンドラーの4つの部分があります。

### <a name="add-commands-bindings-and-buttons-in-xaml"></a>XAML にコマンド、バインド、およびボタンを追加する

1. 最初に、要素内に*mainwindow.xaml*ファイル内のコマンドを追加し `Windows.Resources` ます。

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

2. CommandBinding は、 `RoutedUICommand` イベントを分離コード内のメソッドにマップします。 `CommandBindings`終了タグの後に次の要素を追加し `Windows.Resources` ます。

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

3. 次に、[ `StackPanel` ナビゲーション]、[追加]、[削除]、および [更新] の各ボタンを使用して、を追加します。 まず、次のスタイルをに追加し `Windows.Resources` ます。

    ```xaml
    <Style x:Key="NavButton" TargetType="{x:Type Button}" BasedOn="{x:Null}">
        <Setter Property="FontSize" Value="24"/>
        <Setter Property="FontFamily" Value="Segoe UI Symbol"/>
        <Setter Property="Margin" Value="2,2,2,0"/>
        <Setter Property="Width" Value="40"/>
        <Setter Property="Height" Value="auto"/>
    </Style>
    ```

     次に、 `RowDefinitions` XAML ページの上部に向かって、外側の要素のの直後に次のコードを貼り付け `Grid` ます。

    ```xaml
    <StackPanel Orientation="Horizontal" Margin="2,2,2,0" Height="36" VerticalAlignment="Top" Background="Gainsboro" DataContext="{StaticResource customerViewSource}" d:LayoutOverrides="LeftMargin, RightMargin, TopMargin, BottomMargin">
        <Button Name="btnFirst" Content="|◄" Command="{StaticResource FirstCommand}" Style="{StaticResource NavButton}"/>
        <Button Name="btnPrev" Content="◄" Command="{StaticResource PreviousCommand}" Style="{StaticResource NavButton}"/>
        <Button Name="btnNext" Content="►" Command="{StaticResource NextCommand}" Style="{StaticResource NavButton}"/>
        <Button Name="btnLast" Content="►|" Command="{StaticResource LastCommand}" Style="{StaticResource NavButton}"/>
        <Button Name="btnDelete" Content="Delete Customer" Command="{StaticResource DeleteCustomerCommand}" FontSize="11" Width="120" Style="{StaticResource NavButton}"/>
        <Button Name="btnAdd" Content="New Customer" Command="{StaticResource AddCommand}" FontSize="11" Width="80" Style="{StaticResource NavButton}"/>
        <Button Content="New Order" Name="btnNewOrder" FontSize="11" Width="80" Style="{StaticResource NavButton}" Click="NewOrder_click"/>
        <Button Name="btnUpdate" Content="Commit" Command="{StaticResource UpdateCommand}" FontSize="11" Width="80" Style="{StaticResource NavButton}"/>
        <Button Content="Cancel" Name="btnCancel" Command="{StaticResource CancelCommand}" FontSize="11" Width="80" Style="{StaticResource NavButton}"/>
    </StackPanel>
    ```

### <a name="add-command-handlers-to-the-mainwindow-class"></a>Mainwindow.xaml クラスにコマンドハンドラーを追加する

コードビハインドは、add メソッドと delete メソッドを除き、最小限ではありません。 ナビゲーションは、CollectionViewSource の View プロパティでメソッドを呼び出すことによって実行されます。 は、 `DeleteOrderCommandHandler` 注文に対して連鎖削除を実行する方法を示しています。 最初に、関連付けられている Order_Details を削除する必要があります。 は `UpdateCommandHandler` 新しい顧客または注文をコレクションに追加します。それ以外の場合は、ユーザーがテキストボックスで行った変更を使用して、既存の顧客または注文を更新します。

これらのハンドラーメソッドを*MainWindow.xaml.cs*の mainwindow.xaml クラスに追加します。 Customers テーブルの CollectionViewSource に別の名前が付いている場合は、次の各メソッドで名前を調整する必要があります。

[!code-csharp[CommandHandlers#3](../data-tools/codesnippet/CSharp/CreateWPFDataApp/MainWindow.xaml.cs#3)]

## <a name="run-the-application"></a>アプリケーションの実行

デバッグを開始するには、**F5** キーを押します。 顧客データと注文データがグリッドに表示され、ナビゲーションボタンが期待どおりに動作するはずです。 [**コミット**] をクリックして、データの入力後に新しい顧客または注文をモデルに追加します。 [**キャンセル**] をクリックすると、データを保存せずに、新しい顧客または新しい注文フォームから戻ることができます。 既存の顧客や注文をテキストボックスに直接編集することができ、それらの変更は自動的にモデルに書き込まれます。

## <a name="see-also"></a>関連項目

- [.NET 用の Visual Studio データ ツール](../data-tools/visual-studio-data-tools-for-dotnet.md)
- [Entity Framework ドキュメント](/ef/)
